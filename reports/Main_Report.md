# HW02 — Domain Testing and Boundary Value Analysis

## 1. General Information

- **Course:** Software Testing
- **Assignment:** HW02 — Domain Testing on EShop
- **Student ID:** 23120037
- **Student Name:** Nguyễn Thanh Khánh Hà
- **System Under Test (SUT):** EShop
- **SUT source repository:** [ttbhanh/eshop-sut](https://github.com/ttbhanh/eshop-sut)
- **Personal assignment repository:** [Add your personal repo URL here]
- **Shared group repository (GitHub Issues only):** [Add the group repo URL here]
- **Local SUT copy used:** `C:\KTPM\HW02-EShop` (copied to avoid the `#` character in the original path)
- **Testing period:** 2026-10-14 (date shown in the supplied execution screenshots)

## 2. Feature Selection

| Pool | Feature ID | Feature under test | Platform | Allocation status |
|---|---|---|---|---|
| A | FR-02 | Login and Account Lockout | Web | Selected |
| B | FR-08 | Checkout | Web | Selected |
| C | FR-14 | Category Management | Web Admin | Selected |
| D (proposed mapping) | FR-06 | Product Detail View | Mobile (React Native / Expo) | **Needs manual confirmation:** assignment lists FR-06 under Pool A and describes Pool D as Mobile App; confirm this mapping with instructor/group before claiming one feature per pool |

> **FR-14 scope note:** The SRS currently states that an admin can add, view, and delete categories, and that the category name is required and cannot be empty. It does not clearly specify an update operation. Verify the UI/API and report only the operations supported by the requirement and observed application. Do not assume full CRUD behavior from the feature title alone.

## 3. Testing Environment and Data

| Item | Value |
|---|---|
| Operating system | Windows 11 (verify edition/build if required) |
| Web browser and version | Google Chrome — [record version] |
| Mobile device/emulator and OS | iPhone, Expo Go SDK 57; iOS version not recorded in the supplied evidence |
| Backend/API | [version/commit; URL and port] |
| Web frontend | Vite — `http://localhost:5173/` |
| Admin frontend | [URL/version, if used] |
| Mobile app | Expo Go SDK 57 on iPhone; development server/API used over LAN |
| Database and seed data | [record reset/seed procedure and test accounts used; do not include real passwords in the submitted report] |
| Test date(s) | 2026-10-14 for the supplied FR-06 execution evidence |

Record environment details before execution. If the setup changes, note the change and which tests it affects.

## 4. Test Design and Reporting Method

For each feature, document the analysis before execution:

1. Cite the relevant SRS requirements and any related API/UI requirements.
2. List inputs, preconditions, and observable outcomes.
3. Partition inputs/states into valid and invalid equivalence classes. Explain the basis for each partition and identify untested or uncertain behavior.
4. Identify numeric, length, time, or state-transition boundaries that are explicitly specified. Select values at, immediately below, and immediately above each boundary where applicable.
5. Do not invent limits. Mark unspecified behavior as an open question or assumption and verify it against the SRS, schema/API, or instructor clarification.
6. Define test cases with unique IDs, preconditions, input data, steps, expected result, and requirement source in [`../test-cases/test-cases.csv`](../test-cases/test-cases.csv).
7. Execute tests and record actual results, status, and evidence. Never label a case Passed or Failed before execution.
8. Compare AI-suggested tests with the reviewed test set. Report actual omissions, corrections, and the reason; do not invent AI gaps.
9. Report only reproducible deviations from a requirement as bugs. Link each bug to a GitHub Issue and screenshot evidence.

The per-feature analysis files are linked below. Test case details and execution results are maintained in the CSV to avoid conflicting duplicate records.

## 5. Feature A — FR-02: Login and Account Lockout (Web)

- Requirement source: SRS, FR-02; related security/authentication requirements as applicable.
- Domain analysis: [FR02_Domain.md](FR02_Domain.md)
- Boundary Value Analysis: [FR02_BVA.md](FR02_BVA.md)
- Test case IDs: TC-FR02-DT-01, TC-FR02-DT-02, TC-FR02-DT-03, TC-FR02-DT-04, TC-FR02-DT-06, TC-FR02-BVA-01, TC-FR02-BVA-02, TC-FR02-BVA-04, TC-FR02-BVA-05, TC-FR02-BVA-06.
- Execution summary to date: 8 executed; 4 passed and 4 failed. Two are not executed: TC-FR02-BVA-01 was skipped because the seeded account counter was already 2, and TC-FR02-BVA-06 has not yet been run.
- Confirmed bugs: BUG-FR02-01 (malformed email not HTML5-blocked); BUG-FR02-02 (failed-login counter adds 2); BUG-FR02-03 (login response exposes plaintext password); BUG-FR02-04 (lock duration is 180 seconds instead of 30). GitHub Issues: pending.
- Evidence: [`../screenshots/TC-FR02-DT-01.png`](../screenshots/TC-FR02-DT-01.png); TC-FR02-DT-02 evidence: [`../screenshots/TC-FR02-DT-02.png`](../screenshots/TC-FR02-DT-02.png); TC-FR02-DT-03 evidence: [`../screenshots/TC-FR02-DT-03.png`](../screenshots/TC-FR02-DT-03.png); TC-FR02-DT-04 evidence: [`../screenshots/TC-FR02-DT-04.png`](../screenshots/TC-FR02-DT-04.png). TC-FR02-DT-06 evidence: [`../screenshots/TC-FR02-DT-06-login-response.png`](../screenshots/TC-FR02-DT-06-login-response.png), [`../screenshots/TC-FR02-DT-06-bearer-header.png`](../screenshots/TC-FR02-DT-06-bearer-header.png). TC-FR02-BVA-02 evidence: [`../screenshots/TC-FR02-BVA-02.png`](../screenshots/TC-FR02-BVA-02.png). TC-FR02-BVA-04 evidence: [`../screenshots/TC-FR02-BVA-04.png`](../screenshots/TC-FR02-BVA-04.png). TC-FR02-BVA-05 evidence: [`../screenshots/TC-FR02-BVA-05.png`](../screenshots/TC-FR02-BVA-05.png) 
- AI gap analysis: Coverage gaps and candidate checks are recorded in [FR02_Domain.md](FR02_Domain.md). The archived material does not contain a separate initial AI candidate set, so this is a review of current coverage rather than a claim about a specific omission by AI. BVA-01/BVA-06 remain unexecuted; candidates are not added to totals.
## 6. Feature B — FR-08: Checkout (Web)

- Requirement source: SRS, FR-08; related authentication, coupon, cart, and order requirements only where they affect checkout.
- Domain analysis: [FR08_Domain.md](FR08_Domain.md)
- Boundary Value Analysis: [FR08_BVA.md](FR08_BVA.md)
- Test case IDs: TC-FR08-DT-01 through TC-FR08-DT-05; TC-FR08-BVA-01 through TC-FR08-BVA-03.
- Execution summary: 8 designed; all 8 executed (3 Passed, 5 Failed); none Not Executed. TC-FR08-DT-01 showed the login-required alert and routed to `/login` after dismissal. Both TC-FR08-DT-01 user-provided screenshots are saved in `screenshots/`. TC-FR08-DT-02 and DT-03 checkout evidence are also saved there. DT-03 failed because the total field accepted editing; DT-04 failed because order history stored client E-1 (57,999,999 VND) instead of E (58,000,000 VND). DT-04 evidence shows HTTP 200 and order #1; payload/orderId details are not legible. After the success page, DT-05 showed that both cart items remained. BVA-01 independently reproduced the E-1 amount issue: order #3 was stored at 57,999,999 VND; BVA-02 Passed: order #4 stored E=58,000,000 VND; BVA-03 Failed: order #5 stored E+1 (58,000,001 VND), also reproducing the client-total trust issue.
- AI gap analysis: Design review is recorded in [FR08_Domain.md](FR08_Domain.md). Coupons are excluded as FR-09; empty-cart and request-failure behavior remain open because FR-08 does not define their expected result.
- Confirmed bug: BUG-FR08-01 (Checkout total is directly editable); BUG-FR08-02 (backend persisted client-supplied E-1 total); BUG-FR08-03 (cart remained populated after successful checkout).
- Evidence: DT-01 through DT-05 and BVA-01 through BVA-03 evidence is saved under `../screenshots/`; all evidence paths are listed in the test case CSV and linked from the per-feature reports.
- Source review note (not a test result): TC-FR08-DT-03 confirmed that the total input is editable and the displayed total changes when edited (BUG-FR08-01). DT-04 confirmed that the backend persisted the edited E-1 value; DT-05 confirmed the cart remained populated after checkout success.

## 7. Feature C — FR-14: Category Management (Web Admin)

- Requirement source: SRS, FR-14; FR-12 for admin access control where relevant.
- Domain analysis: [FR14_Domain.md](FR14_Domain.md)
- Boundary Value Analysis: [FR14_BVA.md](FR14_BVA.md)
- Test case design: 8 cases prepared (5 Domain and 3 BVA), all Not Executed: TC-FR14-DT-01 through DT-05 and TC-FR14-BVA-01 through BVA-03.
- Scope clarification: SRS FR-14 specifies add/view/delete; API specification also documents PUT, while the admin UI has no edit control. DT-04 therefore checks the documented API contract and tracks the scope discrepancy, not a UI requirement. Whitespace-only rejection is an assumption, not a confirmed requirement.
- Execution summary: 2 of 8 cases executed; DT-01 Passed with the three seeded categories shown once each, and DT-02 Passed with the new `FR14-Test-NTHH-01` category retained as ID #4 after refresh. Evidence: [`../screenshots/TC-FR14-DT-01.png`](../screenshots/TC-FR14-DT-01.png), [`../screenshots/TC-FR14-DT-02.png`](../screenshots/TC-FR14-DT-02.png). Six cases remain Not Executed. No FR-14 bugs have been confirmed.
- AI gap analysis: The prepared design covers SRS operations, the related SEC-03 role boundary, the documented PUT API, and specified name boundary. Duplicate-name and referenced-category deletion behavior are unspecified and remain exploratory.
- Confirmed bugs: None from FR-14 execution to date.
- Evidence: To be added after each manual case is run; keep JWT/token values out of screenshots.

## 8. Feature D — Mobile FR-06: Product Detail View

- Requirement source: SRS, FR-06 and FR-20; any mobile-specific clarification from the instructor.
- Domain analysis: [FR06_Mobile_Domain.md](FR06_Mobile_Domain.md)
- Boundary Value Analysis: [FR06_Mobile_BVA.md](FR06_Mobile_BVA.md)
- Test case IDs: TC-FR06-MOB-DT-01 through TC-FR06-MOB-DT-03, TC-FR06-MOB-BVA-01 through TC-FR06-MOB-BVA-07.
- Mobile execution setup: iPhone with Expo Go SDK 57, running `C:\KTPM\HW02-EShop\frontend-mobile-sdk57`; API configured for the laptop LAN address. Successful add-to-cart and cart views confirm the backend was reachable. The iOS version was not captured in the available evidence.
- Execution summary: TC-FR06-MOB-DT-01 and TC-FR06-MOB-DT-02 executed; both Failed because the product category was not displayed. TC-FR06-MOB-DT-03 Passed; TC-FR06-MOB-BVA-01 Failed because quantity 0 triggered a success alert; TC-FR06-MOB-BVA-04 Failed because quantity -1 triggered success feedback and appeared in the cart as quantity 1; TC-FR06-MOB-BVA-02 Passed at quantity 1; TC-FR06-MOB-BVA-03 Passed at quantity 2; TC-FR06-MOB-BVA-05 Failed because decimal input `1,5` produced success feedback; TC-FR06-MOB-BVA-06 Failed because `abc` produced success feedback; TC-FR06-MOB-BVA-07 Failed because an empty quantity produced success feedback and an AirPods Pro 2 cart line with quantity 1. All 10 FR-06 cases are executed: 3 Passed and 7 Failed; none are Not Executed.
- AI gap analysis: Coverage gaps and candidate checks are recorded in [FR06_Mobile_Domain.md](FR06_Mobile_Domain.md). No separate initial AI candidate set is archived, so this does not claim a specific AI omission. Duplicate-add and decimal-dot behavior remain unexecuted candidates; unspecified missing-product behavior is exploratory. None is added to current totals.
- Confirmed bugs: BUG-FR06-01 (category omitted) and BUG-FR06-02 (invalid quantities empty, -1, 0, `1,5`, and `abc` accepted as successful adds).
- Evidence: [`../screenshots/TC-FR06-MOB-DT-01.jpg`](../screenshots/TC-FR06-MOB-DT-01.jpg), [`../screenshots/TC-FR06-MOB-DT-02.jpg`](../screenshots/TC-FR06-MOB-DT-02.jpg), [`../screenshots/TC-FR06-MOB-DT-03.jpg`](../screenshots/TC-FR06-MOB-DT-03.jpg), [`../screenshots/TC-FR06-MOB-BVA-01.jpg`](../screenshots/TC-FR06-MOB-BVA-01.jpg), [`../screenshots/TC-FR06-MOB-BVA-02-feedback.jpg`](../screenshots/TC-FR06-MOB-BVA-02-feedback.jpg), [`../screenshots/TC-FR06-MOB-BVA-02-cart.jpg`](../screenshots/TC-FR06-MOB-BVA-02-cart.jpg), [`../screenshots/TC-FR06-MOB-BVA-03-feedback.jpg`](../screenshots/TC-FR06-MOB-BVA-03-feedback.jpg), [`../screenshots/TC-FR06-MOB-BVA-03-cart.jpg`](../screenshots/TC-FR06-MOB-BVA-03-cart.jpg), [`../screenshots/TC-FR06-MOB-BVA-04-feedback.jpg`](../screenshots/TC-FR06-MOB-BVA-04-feedback.jpg), [`../screenshots/TC-FR06-MOB-BVA-04-cart.jpg`](../screenshots/TC-FR06-MOB-BVA-04-cart.jpg), [`../screenshots/TC-FR06-MOB-BVA-05-feedback.jpg`](../screenshots/TC-FR06-MOB-BVA-05-feedback.jpg), [`../screenshots/TC-FR06-MOB-BVA-05-cart.jpg`](../screenshots/TC-FR06-MOB-BVA-05-cart.jpg), [`../screenshots/TC-FR06-MOB-BVA-06-feedback.jpg`](../screenshots/TC-FR06-MOB-BVA-06-feedback.jpg), [`../screenshots/TC-FR06-MOB-BVA-06-cart.jpg`](../screenshots/TC-FR06-MOB-BVA-06-cart.jpg), [`../screenshots/TC-FR06-MOB-BVA-07-feedback.jpg`](../screenshots/TC-FR06-MOB-BVA-07-feedback.jpg), [`../screenshots/TC-FR06-MOB-BVA-07-cart.jpg`](../screenshots/TC-FR06-MOB-BVA-07-cart.jpg)

## 9. Test Summary Report

Summary from the recorded test cases; each case has one status and the totals reconcile.

| Measure | Count |
|---|---:|
| Features in scope | 4 |
| Test cases designed | 36 |
| Test cases executed | 28 |
| Passed | 12 |
| Failed | 16 |
| Not Executed | 8 |
| Confirmed bugs | 9 |

**Reconciliation:** 36 designed = 12 Passed + 16 Failed + 8 Not Executed. The totals reconcile. FR-08 contributes 8 designed cases; all eight are executed (three Passed, five Failed). FR-14 contributes 8 designed cases; two are Passed and six remain Not Executed.

## 10. AI Use and Supporting Deliverables

- **AI Audit Report:** [`../ai-audit/AI_Audit.md`](../ai-audit/AI_Audit.md) — record each AI interaction with tool, date/time, full prompt, output, and student review.
- **AI Critique:** [`../ai-audit/AI_Critique.md`](../ai-audit/AI_Critique.md) — final critique must be 200–300 words and grounded in this testing work.
- **Bug report and issue evidence:** [`../bug-reports/bugs.md`](../bug-reports/bugs.md); screenshots in [`../screenshots/`](../screenshots/).
- **Git commit log:** [`../git-log.txt`](../git-log.txt) — export from actual commits in the personal assignment repository; do not fabricate history.
- **Agent Skill and demonstration video:** [add files/links if created/submitted].

## 11. References

- [EShop SUT repository](https://github.com/ttbhanh/eshop-sut), especially the System Requirements Specification and setup guide.
- Course lectures on Domain Testing and Boundary Value Analysis: [identify lecture/material and date/version].
- Other sources actually used: [list source and access date].









