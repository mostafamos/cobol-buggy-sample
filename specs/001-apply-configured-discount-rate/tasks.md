# Tasks: Apply Configured Discount Rate

**Input**: Design documents from `specs/001-apply-configured-discount-rate/`

**Prerequisites**: `plan.md` and `spec.md`

**Tests**: Verification tasks are included for the scenarios explicitly specified in `spec.md`. No test harness or compiler is assumed.

**Organization**: Tasks are grouped by user story.

## Format: `[ID] [P?] [Story] Description`

- **[P]** marks tasks that can run in parallel on different files with no dependencies; none apply here.
- **[Story]** maps each story task to its specification.
- Every task identifies the relevant file path.

## Phase 1: Setup

**Purpose**: No project setup is required; the existing standalone COBOL sample is the target.

## Phase 2: Foundational

**Purpose**: No shared infrastructure or blocking foundation is required.

## Phase 3: User Story 1 - Calculate invoices using the configured discount (Priority: P1)

**Goal**: Calculate the invoice discount from the configured percentage and keep the displayed percentage and invoice amounts consistent.

**Independent Test**: Run the invoice sample and verify the rate-15 baseline, zero-rate case, and fractional-cent rounding behavior in `invoice-discount.cob`.

### Implementation

- [X] T001 [US1] Update the discount calculation in `invoice-discount.cob` to use the configured percentage while preserving the existing amount precision, rounded behavior, displayed rate, and unrelated sample behavior.

### Verification

- [ ] T002 [US1] Verify in `invoice-discount.cob` that configured rate 15 and subtotal 100.00 display rate 15%, discount 15.00, and total due 85.00; record the actual compiler or test tool and result.
- [ ] T003 [US1] Verify in `invoice-discount.cob` that zero rate produces zero discount and subtotal due, and that a fractional-cent case retains the existing two-decimal rounded behavior; record the actual compiler or test tool and result, or report that verification is unavailable.

## Dependencies & Execution Order

### Phase Dependencies

- **Setup (Phase 1)**: No tasks; no setup is needed.
- **Foundational (Phase 2)**: No tasks; no shared foundation is needed.
- **User Story 1 (Phase 3)**: Independent of any other story.

### User Story Dependencies

- **User Story 1 (P1)**: No dependency on other stories.

### Within User Story 1

- **T001** implements the calculation.
- **T002** and **T003** verify the implemented behavior and depend on T001. They are not marked parallel because they target the same sample and no independent test setup is established.

### Parallel Opportunities

No parallel tasks are identified; all tasks target or validate `invoice-discount.cob`.

## Implementation Strategy

### MVP First

1. Complete T001.
2. Complete T002 to verify the issue's sample acceptance case and the consistency of the displayed rate.
3. Complete T003 for zero-rate and fractional-cent behavior.

The verification tasks must remain unchecked until performed. If no compatible compiler or verification mechanism is available, report that limitation rather than marking a check complete.

## Notes

- Task IDs are sequential and each task follows the required checklist format.
- No new test file path or test harness is specified because the repository establishes neither.
- No task introduces policy for fractional, negative, or out-of-supported-range rates.
- T002 and T003 remain unchecked: `cobc` is unavailable (`Get-Command cobc` and `where.exe cobc` found no compiler), and `wsl --list --quiet` reported no installed distribution. The configured COBOL program could not be run in this environment. A PowerShell source/formula check passed for the configured-rate expression and displayed-rate reference; independent decimal arithmetic checks passed for rate 15/subtotal 100.00 (15.00 discount, 85.00 due), zero rate (0.00 discount, 100.00 due), and rate 15/subtotal 0.05 (0.01 discount, 0.04 due). These checks do not replace execution of the COBOL program.
