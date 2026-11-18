# Issue

**Title:** [daily-playwright] Add E2E tests for appointment detail page

## Description

### Summary

This PR adds comprehensive E2E tests for the appointment detail page, covering the complete appointment management workflow including viewing details, check-in, status transitions, token generation, and quick actions.

### What Changed

**New Test File**: `tests/facility/appointments/appointmentDetail.spec.ts`

Added **10 test cases** covering:

1. ✅ **Book appointment and navigate to detail page** - End-to-end flow from booking to viewing details
2. ✅ **Display appointment schedule information** - Verify all appointment details shown correctly (date, time, practitioner, facility)
3. ✅ **Check-in a booked appointment** - Test status transition from "Booked" to "Checked In" (within valid time window)
4. ✅ **Display token generation option** - Verify token UI shows empty state and "Generate Token" button
5. ✅ **Display quick actions** - Test quick action buttons (print, accounts, create encounter)
6. ✅ **Display appointment actions menu** - Verify dropdown menu with "Mark as Fulfilled" and "Reschedule"
7. ✅ **Open reschedule dialog** - Test reschedule workflow initiation with note requirement and warning
8. ✅ **Display patient information card** - Verify patient details and contact information display
9. ✅ **Navigate back using back button** - Test back button returns to patient home

### Why This Matters

The appointment detail page (`/facility/:facilityId/patient/:patientId/appointments/:appointmentId`) is the primary interface for managing individual appointments in the healthcare workflow. It provides:

- **Check-in workflow**: Transition appointments from booked to checked-in (available within 24-hour window)
- **Status management**: Mark appointments as fulfilled or no-show for past/ongoing appointments
- **Token generation**: Create queue tokens for appointment queue management
- **Quick actions**: Access printing, billing accounts, and planned encounter creation
- **Reschedule workflow**: Initiate appointment rescheduling with note and slot selection
- **Patient context**: Display patient information alongside appointment details for clinical decision-making

This PR continues the appointment coverage journey:
- 2026-08-03: Appointment listing page ✅
- 2026-08-04: Appointment booking workflow ✅
- 2026-08-07: **Appointment detail page** ✅ ← THIS PR

### Technical Highlights

- **Appointment creation**: Tests book appointments via UI first to obtain valid appointment IDs
- **Status-based UI testing**: Verifies actions are shown/hidden based on appointment status and timing
- **Time window validation**: Tests check-in button visibility (only available within 24 hours of appointment)
- **Empty states**: Verifies token generation UI when no token exists
- **Dialog workflows**: Tests reschedule dialog with note requirement and cancellation warning
- **Navigation testing**: Verifies back button navigation to patient home
- **Date handling**: Uses `date-fns` for reliable date formatting and future date selection
- **Faker integration**: Generates unique appointment reasons to prevent test collisions
- **Role-based selectors**: Follows established patterns (`getByRole`, `getByLabel`, `getByText`)
- **Web-first assertions**: Uses `toBeVisible`, `toHaveURL` for reliability

### Testing Standards Compliance

- ✅ Role-based selectors (`getByRole`, `getByLabel`, `getByText`)
- ✅ Avoids CSS selectors (only semantic selectors used)
- ✅ Proper assertions (not just navigation checks)
- ✅ Handles loading states appropriately
- ✅ Tests both success paths and UI state validations
- ✅ Independent tests (no shared state between tests)
- ✅ File naming: `appointmentDetail.spec.ts` (matches feature)
- ✅ Formatted with Prettier (331ms)
- ⚠️ ESLint check skipped (locale file missing in CI)

### How to Test Locally

``````bash
# Prerequisites
npm run build                     # Build app (required for tests)
# Backend must be running on port 9000

# Run all appointment tests
npx playwright test tests/facility/appointments/

# Run just the new detail page tests
npx playwright test tests/facility/appointments/appointmentDetail.spec.ts

# Run in UI mode for interactive debugging
npm run playwright:test:ui tests/facility/appointments/appointmentDetail.spec.ts

# Run with multiple workers for faster execution
npx playwright test tests/facility/appointments/ --workers=4
``````

### Coverage Progress

**Appointments**: 3 of ~5 core workflows (60% coverage)
- ✅ Appointment listing page
- ✅ Appointment booking workflow
- ✅ **Appointment detail page** ← THIS PR
- ⏳ Complete reschedule workflow (with slot selection)
- ⏳ Appointment cancellation (with reason)

### Next Steps

Remaining appointment workflows to test:
1. Token generation complete flow (form submission and display)
2. Complete reschedule workflow (slot selection + confirmation)
3. Appointment cancellation (reason input + token handling)
4. Status transitions (complete lifecycle: booked → checked_in → in_consultation → fulfilled)
5. Start consultation from appointment (encounter creation)

### Related

- Tracking Issue: #16623
- Previous PR: Appointment booking (2026-08-04)
- Previous PR: Appointment listing (2026-08-03)

---

<details><summary><b>Test Quality Checklist</b></summary>

- [x] Uses role-based selectors (`getByRole`, `getByLabel`, `getByText`)
- [x] Avoids CSS selectors unless absolutely necessary (none used)
- [x] Includes proper assertions (toBeVisible, toHaveURL, etc.)
- [x] Handles loading states appropriately (waitForLoadState, waitForURL)
- [x] Tests both success and UI state validation paths
- [x] Is independent of other tests (each test books its own appointment)
- [x] Follows file naming convention: `appointmentDetail.spec.ts`
- [x] JSDoc comments explain what each test verifies
- [x] Uses faker for unique data generation
- [x] Handles date pickers with date-fns formatting
- [x] Tests dialog interactions (open, cancel, continue)
- [x] Verifies empty states (token not generated)
- [x] Tests dropdown menu interactions

</details>

---

> AI generated by [Daily Playwright Test Improver](https://github.com/ohcnetwork/care_fe/actions/runs/31145919593)

> AI generated by [Daily Playwright Test Improver](https://github.com/ohcnetwork/care_fe/actions/runs/31145919593)

<!-- gh-aw-workflow-id: daily-playwright-improver -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `411df5875cc5`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.