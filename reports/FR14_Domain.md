# FR-14 - Domain Testing (Category Management)

## Information and scope

- Platform: Web Admin.
- SRS source: `eshop-sut-main/README.md`, FR-14.
- Related security source: the same README, SEC-03 (admin mutations require an admin-role token).
- API contract source: `eshop-sut-main/api_specification.md`, section 3.4.
- Execution status: 5 Domain cases and 3 BVA cases designed; TC-FR14-DT-01 and TC-FR14-DT-02 Passed, with the other 6 cases Not Executed.
- Core SRS scope: add, view, and delete categories; category name is required and cannot be empty.

## Requirement and scope notes

The SUT README names the feature ?Category CRUD? but its FR-14 text lists Add/View/Delete only. The API specification documents `PUT /api/categories/:id`, while the admin UI currently has no category-edit control. TC-FR14-DT-04 therefore covers the documented API contract and records the scope discrepancy; do not represent it as an explicit FR-14 UI requirement. The admin security check uses shared SEC-03.

No maximum or minimum category-name length is specified. ?Whitespace-only is blank? is a test assumption to confirm, not a proven requirement. Duplicate-name behavior and deletion of a category referenced by a product are unspecified and remain exploratory.

## Equivalence partitions

| Attribute | Partition | Expected / basis |
|---|---|---|
| User role | Admin with valid token | May view and manage categories (FR-14 / SEC-03). |
| User role | Authenticated non-admin | Must be denied category mutation (SEC-03). |
| Category name | Non-empty unique value | Create successfully. |
| Category name | Empty string | Reject; FR-14 says required and not empty. |
| Category name | Whitespace only | Exploratory; expected rejection if ?blank? means no non-whitespace characters. |
| Operation | View, create, delete | Check stored/list state and ensure unrelated categories remain unchanged. |
| Operation | Update through API | API contract lists PUT; UI/SRS discrepancy is documented above. |

## Test cases

Detailed preconditions, steps, expected results, execution status, and evidence slots are in [`../test-cases/test-cases.csv`](../test-cases/test-cases.csv), IDs TC-FR14-DT-01 through DT-05 and TC-FR14-BVA-01 through BVA-03. TC-FR14-DT-01 Passed: the admin category page loaded and displayed IDs #1 Điện thoại, #2 Laptop, and #3 Phụ kiện once each. Evidence: [`../screenshots/TC-FR14-DT-01.png`](../screenshots/TC-FR14-DT-01.png). TC-FR14-DT-02 Passed: the unique category `FR14-Test-NTHH-01` appeared as ID #4 and remained visible in the list after the refresh step. Evidence: [`../screenshots/TC-FR14-DT-02.png`](../screenshots/TC-FR14-DT-02.png). Six cases remain Not Executed. Keep the disposable category for TC-FR14-DT-03; never delete seeded categories. Capture before/after state and avoid exposing JWT values.

## Open questions

- Does the instructor expect Update as part of FR-14 despite the SRS operation list omitting it?
- Should whitespace-only names be treated as empty?
- What should happen for duplicate names or deleting a category referenced by a product? No result should be called a bug until an expected rule is confirmed.
