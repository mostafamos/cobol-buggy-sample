# Implementation Plan: Apply Configured Discount Rate

**Branch**: `mostafamos-apply-configured-discount-rate` | **Date**: 2026-10-20 | **Spec**: [spec.md](spec.md)

**Input**: Feature specification from `specs/001-apply-configured-discount-rate/spec.md`

## Summary

Update the invoice sample's discount calculation to use its configured whole-number percentage rather than the current fixed 5% multiplier. Preserve the existing amount precision, rounded computation, displayed rate, and all unrelated sample behavior. The issue's sample case is the acceptance baseline: rate 15 and subtotal 100.00 yield discount 15.00 and total due 85.00.

## Technical Context

**Language/Version**: COBOL; dialect and compiler version are not established in the repository.

**Primary Dependencies**: None identified.

**Storage**: None; the sample uses working-storage values.

**Testing**: No COBOL compiler or test harness is established. Verify against the acceptance cases when a compatible compiler is available; do not represent unrun checks as complete.

**Target Platform**: Not specified; the scope is the existing invoice sample.

**Project Type**: Standalone COBOL sample.

**Performance Goals**: Not applicable to this calculation change.

**Constraints**: Limit implementation to the calculation and directly related verification for `invoice-discount.cob`. Preserve the existing two-decimal amount fields and `ROUNDED` behavior. Do not define new rate-input policies.

**Scale/Scope**: One COBOL sample and its directly related verification; leave `account-summary.cob` and unrelated behavior unchanged.

## Constitution Check

The file `.specify/memory/constitution.md` remains the unresolved generated template, not a ratified set of project principles or gates. Per the user's authorization, it remains unchanged. No project-specific constitution rules can therefore be evaluated or asserted by this plan; this is an explicit governance limitation, not a claim that unknown rules pass.

## Design

### Decision

Use the configured percentage as the source of the invoice discount. Treat the rate as a percentage of the subtotal, keep the existing display tied to the same configured rate, and preserve existing amount representation and rounding. The rate-15/subtotal-100.00 expected values and zero-rate/fractional-cent checks are defined by the spec and source issue.

### Scope boundaries

- In scope: the discount calculation and direct verification of its results in `invoice-discount.cob`.
- Out of scope: other COBOL samples, new discount policies, and new behavior for fractional, negative, or out-of-supported-range rates.
- No external interfaces or persistent data are introduced.

### Validation approach

When an established compatible COBOL compiler or test harness is available, verify the spec scenarios: configured rate 15 with subtotal 100.00; zero rate; and fractional-cent rounding. Confirm the displayed rate matches the rate used by the calculation, and that the existing precision and `ROUNDED` behavior remain intact. This repository does not currently establish such tooling, so these are planned checks, not completed verification.

## Project Structure

### Documentation (this feature)

```text
specs/001-apply-configured-discount-rate/
├── spec.md
├── plan.md
└── tasks.md
```

### Source Code (repository root)

```text
invoice-discount.cob
account-summary.cob
```

**Structure Decision**: The repository contains standalone COBOL samples at its root, not a conventional source/test directory structure. This feature is scoped to `invoice-discount.cob`; no source or test files are changed in this specification-only phase.
