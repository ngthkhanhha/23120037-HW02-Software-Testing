# FR-14 - Boundary Value Analysis

## Boundaries supported by the requirement

FR-14 says a category name is required and cannot be empty. It provides no maximum length and no explicit whitespace-trimming rule. The zero-character boundary and shortest non-empty value are testable. Whitespace-only input is an interpretation check and should not be declared a bug without confirmation.

| ID | Boundary/input | Expected result | Status
|---|---|---|---|
| TC-FR14-BVA-01 | Empty string (0 characters) | Reject; no category is created. | **Failed** - submitting the blank form created empty category #4; it was removed after evidence capture. Evidence: [`TC-FR14-BVA-01.png`](../screenshots/TC-FR14-BVA-01.png). |
| TC-FR14-BVA-02 | Three spaces, no visible characters | Assumption: reject as blank; confirm requirement interpretation. | Not Executed |
| TC-FR14-BVA-03 | One non-whitespace character (`A`) | Accept; clean up the disposable category after capture. | Not Executed |

There is no source-defined maximum-length boundary, so max-1/max/max+1 values are not designed. Do not infer a limit from an HTML input or database behavior. Detailed steps are in the master CSV.
