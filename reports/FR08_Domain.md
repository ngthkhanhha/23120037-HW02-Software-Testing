# FR-08 - Domain Testing (Checkout)

## Information

- Platform: Web.
- Requirement source: EShop System Requirements Specification, FR-08.
- Scope: Checkout only. Coupon behavior belongs to FR-09; the cart is used as input data.
- Execution status: 8 of 8 test cases executed; 3 Passed, 5 Failed, 0 Not Executed.

## Requirements under test

1. Only authenticated users can proceed to checkout.
2. The payment total is calculated automatically from the cart and is not directly editable.
3. Checkout displays every product being purchased.
4. The backend recalculates the total and does not trust a client-supplied `total_amount`.
5. After successful checkout, the cart is cleared.

## Equivalence partitions

| Attribute | Partition | Expected behavior |
|---|---|---|
| Authentication | Valid signed-in session | Checkout is available. |
| Authentication | Signed out, missing or invalid token | Checkout is blocked; no order is created. |
| Cart | One or more products | Every product and quantity is shown at checkout. |
| Cart | Empty | FR-08 does not define the expected behavior; treat as exploratory. |
| Displayed total | Equal to sum of item price times quantity | Shown as the cart-derived total and not editable. |
| Client submitted total | Different from cart-derived total | Backend stores the amount calculated from the cart, not the client value. |
| Checkout result | Success | Order is created and cart is cleared. |
| Checkout result | Failure | Cart behavior is not specified in FR-08; investigate without assuming a pass/fail criterion. |

## Technique application

The selected variables are authentication state, cart contents, computed total, client-supplied total and checkout outcome. The cases include UI checks and server-side checks so that client-side restrictions are not mistaken for backend enforcement. For total tampering, define `E` as the sum of item price multiplied by quantity, then compare a submitted `E-1` with the stored order total. Use a test account and capture order identifiers. Do not include authentication tokens in evidence. Coupon behavior is excluded because it belongs to FR-09.

## Domain test cases

| ID | Scenario | Expected result | Status and observed result |
|---|---|---|---|
| TC-FR08-DT-01 | Signed-out user clicks Checkout from a non-empty cart | User is asked to sign in; no order is created. | **Passed** - a login-required alert appeared at `/cart`; after dismissal, the app routed to `/login`. Evidence: [`TC-FR08-DT-01-cart-login-alert.png`](../screenshots/TC-FR08-DT-01-cart-login-alert.png), [`TC-FR08-DT-01-login-redirect.png`](../screenshots/TC-FR08-DT-01-login-redirect.png). Network/order history was not captured to independently verify that no order was created. |
| TC-FR08-DT-02 | Signed-in user opens Checkout with multiple products | All products and quantities appear; total matches the cart. | **Passed** - iPhone 15 Pro Max x1 (30,000,000 VND) and Samsung Galaxy S24 Ultra x1 (28,000,000 VND) appeared; total was 58,000,000 VND. Evidence: [`TC-FR08-DT-02-checkout-items-total.png`](../screenshots/TC-FR08-DT-02-checkout-items-total.png). Order was not submitted. |
| TC-FR08-DT-03 | Attempt to edit the total directly on Checkout | Total is displayed but cannot be directly changed. | **Failed** - the field accepted 57,999,970 instead of 58,000,000 and the displayed payment total changed accordingly. Evidence: [`TC-FR08-DT-03-editable-total.png`](../screenshots/TC-FR08-DT-03-editable-total.png). Checkout was not submitted. See BUG-FR08-01. |
| TC-FR08-DT-04 | Submit client total E-1 and inspect the saved order | Backend stores E from the cart, not client E-1 | **Failed** - checkout returned HTTP 200 and Profile order history showed order #1 at 57,999,999 VND, matching client E-1 rather than E=58,000,000 VND. Evidence: [`TC-FR08-DT-04-checkout-response.png`](../screenshots/TC-FR08-DT-04-checkout-response.png) and [`TC-FR08-DT-04-order-history.png`](../screenshots/TC-FR08-DT-04-order-history.png). Network request payload and orderId are not legible in the supplied image. |
| TC-FR08-DT-05 | Inspect cart after successful checkout | Order confirmation is shown and cart is empty | **Failed** - after Checkout showed success, the cart still contained iPhone 15 Pro Max x1 and Samsung Galaxy S24 Ultra x1; subtotal remained 58,000,000 VND. Evidence: [`TC-FR08-DT-05-cart-not-cleared.png`](../screenshots/TC-FR08-DT-05-cart-not-cleared.png). This post-checkout state followed DT-04; no second order was submitted. |

DT-01 and DT-02 Passed. DT-03 Failed because the total was editable; DT-04 Failed because the server persisted client E-1; DT-05 Failed because the cart retained its items after successful checkout. BVA-01 also Failed: order #3 stored E-1 (57,999,999 VND), reproducing BUG-FR08-02. BVA-02 Passed: order #4 stored E=58,000,000 VND. BVA-03 Failed: order #5 stored E+1 (58,000,001 VND), also reproducing BUG-FR08-02. All FR-08 cases are now executed: three Passed and five Failed. See BUG-FR08-01 through BUG-FR08-03. Detailed evidence is in [`../test-cases/test-cases.csv`](../test-cases/test-cases.csv).

## Design gap review

The five Domain cases cover the five FR-08 statements. DT-03 verified client-side total editability, DT-04 verified server-side amount handling and DT-05 verified cart clearing; all three failed. Empty-cart behavior, duplicate checkout requests and API-failure behavior are possible extensions without explicit expected results in FR-08. DT-01 through DT-05 have execution results above; BVA-01 was executed and failed because the backend stored E-1; BVA-02 Passed with order #4 stored at E=58,000,000 VND; BVA-03 Failed because order #5 stored E+1 (58,000,001 VND). All eight FR-08 cases are executed; see FR08_BVA.md.

## Remaining checks

- TC-FR08-DT-04 submitted one test order (#1). The order history shows 57,999,999 VND, matching E-1. The checkout Network response was HTTP 200; the screenshot does not show the request payload or orderId.
- TC-FR08-DT-05 was checked after the successful checkout in DT-04; the cart still contained both items. No additional order was submitted.
- For TC-FR08-DT-01, separate Network/order-history evidence is still needed if independent proof of no order is required.
- TC-FR08-BVA-01 submitted one demo order (#3); order history showed 57,999,999 VND (E-1), confirming BUG-FR08-02. Evidence is linked in FR08_BVA.md.
- TC-FR08-BVA-02 submitted one demo order (#4) and stored E=58,000,000 VND as expected. Evidence is linked in FR08_BVA.md.
- TC-FR08-BVA-03 submitted one demo order (#5); order history stored E+1=58,000,001 VND, confirming BUG-FR08-02. Evidence is linked in FR08_BVA.md.
- Do not include coupons in FR-08 results; coupon tests belong to FR-09.
