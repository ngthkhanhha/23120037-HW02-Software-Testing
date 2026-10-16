# FR-08 — Boundary Value Analysis

## Phạm vi biên

FR-08 không quy định ngưỡng tiền tối thiểu/tối đa cho đơn hàng. Không tự đặt cận min/max. Tuy nhiên, yêu cầu backend phải tự tính tổng tạo ra quan hệ so sánh rõ ràng giữa tổng đúng từ giỏ `E` và giá trị `total_amount` do client gửi. Kiểm tra ba giá trị liền kề `E-1`, `E`, `E+1` quanh điểm bằng nhau để xác định server có tin dữ liệu client hay không.

Các giá trị này chỉ dùng trong request API thử nghiệm; tổng lưu đúng phải bằng `E` trong cả ba trường hợp. Dùng giỏ có tổng `E > 1` VND để `E-1` vẫn không âm. Mỗi ca dùng baseline riêng, tránh tái sử dụng đơn hàng vừa tạo.

## Test case BVA

| ID | Vị trí so với tổng đúng `E` | Giá trị client gửi | Kỳ vọng | Trạng thái |
|---|---|---:|---|---|
| TC-FR08-BVA-01 | Immediately below equality | `E - 1` VND | Backend recalculates and stores `E`, not `E-1` | **Failed** - order #3 was saved at 57,999,999 VND (E-1), rather than E=58,000,000 VND. Evidence: [`TC-FR08-BVA-01-checkout-response.png`](../screenshots/TC-FR08-BVA-01-checkout-response.png), [`TC-FR08-BVA-01-order-history.png`](../screenshots/TC-FR08-BVA-01-order-history.png). See BUG-FR08-02. |
| TC-FR08-BVA-02 | At equality | `E` VND | Backend stores `E` | **Passed** - order #4 was saved at 58,000,000 VND, equal to E. Evidence: [`TC-FR08-BVA-02-checkout-response.png`](../screenshots/TC-FR08-BVA-02-checkout-response.png), [`TC-FR08-BVA-02-order-history.png`](../screenshots/TC-FR08-BVA-02-order-history.png). |
| TC-FR08-BVA-03 | Immediately above equality | `E + 1` VND | Backend recalculates and stores `E`, not `E+1` | **Failed** - order #5 was saved at 58,000,001 VND (E+1), rather than E=58,000,000 VND. Evidence: [`TC-FR08-BVA-03-checkout-response.png`](../screenshots/TC-FR08-BVA-03-checkout-response.png), [`TC-FR08-BVA-03-order-history.png`](../screenshots/TC-FR08-BVA-03-order-history.png). See BUG-FR08-02. |

## Cách chạy và ghi nhận

1. Đăng nhập bằng tài khoản thử nghiệm; tạo giỏ không rỗng và tính `E = tổng(đơn giá × số lượng)`.
2. Ghi baseline sản phẩm/giỏ và số đơn hàng hiện có.
3. Dùng DevTools Network “Edit and resend” cho request `/api/checkout` hoặc công cụ API tương đương; chỉ thay `total_amount` theo từng ca, giữ token hợp lệ và dữ liệu còn lại ổn định.
4. Ghi request, HTTP status, `orderId`, rồi kiểm tra đơn hàng qua `/api/orders/my-orders` để so tổng lưu với `E`.
5. Làm mới trạng thái/tài khoản thử nghiệm giữa các ca nếu cần; không dùng cùng một `orderId` làm bằng chứng cho nhiều giá trị.

TC-FR08-BVA-01 failed: order #3 stored E-1 (57,999,999 VND); TC-FR08-BVA-02 passed: order #4 stored E (58,000,000 VND); TC-FR08-BVA-03 failed: order #5 stored E+1 (58,000,001 VND). All three equality-boundary cases are executed. The two failed cases reproduce BUG-FR08-02. FR-08 specifies no minimum or maximum order total.
