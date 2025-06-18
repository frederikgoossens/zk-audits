# Tornado Mixer Circuit Audit

**Project:** TornadoCash (simulated fork)
**Circuit:** `mixer.circom`
**Date:** 2025-06-18
**Author:** Frederik Goossens
**Type:** Educational Audit
**Status:** Resolved

---

## Summary

This simulated audit uncovered a constraint omission in the nullifier check of the Tornado-style mixer circuit. Specifically, the `nullifierHash` constraint was insufficiently bounded and could result in replay vulnerabilities.

---

## Vulnerability

- **Constraint Skipped:** Missing `==` between `inputNullifierHash` and `computedHash`
- **Impact:** Reused nullifiers could pass verification.
- **Severity:** High

---

## Fix

Enforce constraint:
```circom
enforce computedNullifierHash == inputNullifierHash;
