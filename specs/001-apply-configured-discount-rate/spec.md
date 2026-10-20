# Feature Specification: Apply Configured Discount Rate

**Feature Branch**: `mostafamos-apply-configured-discount-rate`

**Created**: 2026-10-20

**Status**: Draft

**Input**: User description: "Apply the configured discount rate in the COBOL invoice calculation instead of the hard-coded multiplier."

## User Scenarios & Testing

### User Story 1 - Calculate invoices using the configured discount (Priority: P1)

A person running the invoice sample needs the discount and total due to reflect the configured percentage, so the displayed rate and invoice amounts agree.

**Why this priority**: Applying the configured rate is the feature's sole business outcome and corrects the discrepancy between the displayed rate and calculated discount.

**Independent Test**: Run the invoice sample with its configured rate of 15 and subtotal of 100.00; verify the rate, discount, and total due are displayed consistently.

**Acceptance Scenarios**:

1. **Given** the configured rate is 15 and the invoice subtotal is 100.00, **When** the invoice is calculated, **Then** the displayed rate is 15%, the discount is 15.00, and the total due is 85.00.
2. **Given** the configured rate is zero, **When** the invoice is calculated, **Then** the discount is 0.00 and the total due equals the subtotal.
3. **Given** the configured rate and subtotal produce a fractional-cent discount, **When** the invoice is calculated, **Then** the existing two-decimal amount precision and rounding behavior are preserved.

### Edge Cases

- A zero configured rate produces no discount and leaves the subtotal due.
- A configured rate and subtotal producing fractional cents retain the existing rounded amount behavior.
- This feature does not define new policy for fractional, negative, or out-of-supported-range configured rates.

## Requirements

### Functional Requirements

- **FR-001**: The invoice discount MUST be calculated from the configured discount percentage, rather than a fixed percentage.
- **FR-002**: The displayed discount percentage MUST be the same configured percentage used to calculate the discount.
- **FR-003**: With a configured rate of 15 and subtotal of 100.00, the invoice MUST show a discount of 15.00 and total due of 85.00.
- **FR-004**: A configured rate of zero MUST produce a zero discount and leave the subtotal due.
- **FR-005**: The calculation MUST preserve the existing two-decimal amount precision and rounded calculation behavior.

### Key Entities

- **Configured discount rate**: The invoice's configured whole-number percentage used to determine the discount.
- **Invoice amounts**: The subtotal, calculated discount, and resulting total due displayed for the invoice.

## Success Criteria

### Measurable Outcomes

- **SC-001**: For the sample subtotal of 100.00 and configured rate of 15, the displayed discount is 15.00 and total due is 85.00.
- **SC-002**: For a zero configured rate, the displayed discount is 0.00 and total due equals the subtotal.
- **SC-003**: For a fractional-cent discount, the calculated amount retains the existing two-decimal precision and rounding behavior.
- **SC-004**: The displayed percentage matches the percentage used to determine the displayed discount.

## Assumptions

- The feature changes only the invoice discount calculation and directly related verification; unrelated samples and behavior remain unchanged.
- The configured rate continues to use the existing supported representation. This feature adds no policy for fractional, negative, or out-of-supported-range rates.
- Amount precision and rounding behavior remain as they are today.
- The repository does not establish a COBOL compiler or test harness; verification tooling must not be assumed.

## Source References

- GitHub issue [#2](https://github.com/mostafamos/cobol-buggy-sample/issues/2)
- Azure DevOps work item [#3](https://dev.azure.com/mostafamos2027/cobol-ado-2027/_workitems/edit/3)
- Current behavior inspected in `invoice-discount.cob`
