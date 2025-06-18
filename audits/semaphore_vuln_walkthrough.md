# Semaphore Circuit Vulnerability Walkthrough

**Project:** Semaphore
**Circuit:** `semaphore.circom`
**Date:** 2025-06-18
**Author:** Frederik Goossens (ZK Auditor)
**Type:** Simulated Audit
**Status:** Resolved

---

## Summary

During a simulated audit of Semaphore’s zero-knowledge identity circuit, I discovered a logic flaw in the way signal uniqueness was enforced. This flaw could have allowed duplicate identity commitments under certain edge-case input conditions.

---

## Vulnerability

- **Issue:** Signal duplication logic reused the same constraint path for multiple input identities.
- **Impact:** In rare edge cases, two users could generate different proofs resulting in the same signal hash, leading to potential identity spoofing.
- **Location:**
  ```circom
  signal input identityNullifier;
  signal input identityTrapdoor;
  ...
