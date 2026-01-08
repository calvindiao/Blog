---
title: Structured DNS Errors in Chromium, GSoC 2025
date: 2025-08-30
updated: 2025-08-30
tags: [GSoC, Chromium, DNS, Networking, C++, IETF]
---

During Google Summer of Code (GSoC) 2025, I worked on bringing **Public Resolver Errors ([PRE](https://datatracker.ietf.org/doc/draft-nottingham-public-resolver-errors/01/?utm_source=chatgpt.com))** support into **Chromium’s DNS stack**, extending the existing **Extended DNS Error ([EDE, RFC 8914](https://www.rfc-editor.org/rfc/rfc8914))** mechanism. The goal is to help Chromium understand **why** a DNS query failed when a public resolver blocks a domain for policy, legal or other reasons. So the browser can eventually surface a meaningful explanation instead of a generic “DNS error”.

**Mentors:** Andrew Williams, David Adrian  

<!-- more -->

## 🤔 Why PRE matters

Modern public DNS resolvers may be required to block certain domains. Without a structured signal, clients often treat these failures as network instability. PRE provides a standards-driven way to attach **machine-readable metadata** (and resolver-provided links) so browser can distinguish “blocked” from “broken”.

## 🎯 Project goals

- Parse PRE’s structured JSON object from the **EDE “extra text”** field
- Extract key fields defined by [`draft-nottingham-public-resolver-errors-01`](https://datatracker.ietf.org/doc/draft-nottingham-public-resolver-errors/01/?utm_source=chatgpt.com):
  - `ro` (resolver operator ID)
  - `inc` (filtering incident ID)
- Expand `{inc}` into dereferenceable URLs using **URI templates**
- Add robust unit tests (correctness + edge cases)
- Integrate behind a feature flag

## 🙋 What I implemented

### 1) PRE parsing in `OptRecordRdata::EdeOpt`

I extended Chromium’s EDE parsing to support JSON-based “Filtering Details”.  

- Added `EdeOpt::FilteringDetails` struct to hold parsed metadata (`ro`, `inc`)
- Implemented `ParseFilteringDetails()` with strong validation:
  - **UTF-8 only** (reject UTF-16/UTF-32 encoded text)
  - Reject **unpaired surrogate** code points
  - Reject Unicode **non-characters** (e.g., U+FDD0, U+FFFE)
  - Accept emoji, surrogate-pair characters, and key-order variations

Result: PRE metadata is parsed into `EdeOpt::FilteringDetails` and ready to be consumed by higher layers.

### 2) `FilteringDetailsUrlGenerator` utility

I added a new helper in `net/dns/` that turns PRE metadata into a user-actionable link:
- Maintains a registry mapping `ro` → URI template
- Expands `{inc}` into a full URL using Chromium’s `url_template` library
- Supports injecting a custom registry for tests + a built-in registry path for production

This keeps responsibilities clean:
- `OptRecordRdata` parses protocol data
- `FilteringDetailsUrlGenerator` handles policy/config and URL generation

### 3) Feature flag: `kDnsFilteringDetails`

Everything is guarded behind `kDnsFilteringDetails`:
- When disabled (default), parsing is skipped and behavior remains unchanged
- This allows safe incremental rollout and review

### 4) Unit tests (net_unittests)

I added comprehensive tests covering:
- Positive: valid JSON, emoji, surrogate pairs, key order variations
- Negative: missing fields, wrong types, invalid encodings, invalid surrogates, non-characters
- Feature flag disabled behavior
- URL generator expansion correctness + missing registry entries

### 5) Requesting EDE and NetLog exploration

Separately, I prepared work to request **EDE on all DNS request types** and validated behavior using a resolver that supports EDE (AdGuard DNS).  
I also reviewed where EDE fields surface in NetLog to understand current observability and what remains to wire end-to-end.

## 🔗 Links

**Main Gerrit CLs (PRE parsing + generator):**

- https://chromium-review.googlesource.com/c/chromium/src/+/6707102
- https://chromium-review.googlesource.com/c/chromium/src/+/6645800

**Follow-up (request EDE broadly):**

- https://chromium-review.googlesource.com/c/chromium/src/+/6897435

**Relevant bugs:**

- [crbug.com/396483553](https://issues.chromium.org/issues/396483553?utm_source=chatgpt.com) Structured DNS Extensions for Public Resolvers
- [crbug.com/40912798](https://issues.chromium.org/40912798?utm_source=chatgpt.com) Extended DNS Error

## Challenges & learnings

- Learned Chromium’s end-to-end workflow: **Gerrit reviews, feature flags, IWYU, net_unittests**, and dependency hygiene.
- Deepened understanding of DNS standards and how drafts evolve (RFC 8914 + PRE drafts).
- Switched resolver registry from `std::unordered_map` to `absl::flat_hash_map` based on mentor feedback.
- Practiced separation of concerns: parsing stays in the protocol layer; URL generation is modular and testable.
- Explored I-JSON ([RFC 7493](https://www.rfc-editor.org/rfc/rfc7493)) validation: initially prototyped stricter compliance checks, then aligned with reviewer feedback that JSON compliance belongs in `base::JSONReader` rather than the net layer.

## Current status and Certificate

- Code compiles and passes `net_unittests`
- PRE metadata is parsed into `EdeOpt::FilteringDetails`
- URL generator exists and is tested
- Feature flag integrated (disabled by default)
- This establishes the foundation for future Chromium UX to explain DNS blocking clearly and responsibly

<p align="center">
  <img src="/assets/gsoc/certificate.png" width="80%">
  <br>
  <em>Certificate of my GSoC</em>
</p>

---

If you’re interested in deeper implementation details, I also wrote a longer internal [report](https://docs.google.com/document/d/1sT07ElIQ15SpwzjfprqMrbcvr1d3O6arDrKV-rL6IQs/edit?usp=sharing) during GSoC.

