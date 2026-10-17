# FR-08 — Phân tích giá trị biên

## Phạm vi biên

FR-08 không quy định tổng đơn hàng tối thiểu/tối đa. Không tự đặt cận min/max. Tuy nhiên, yêu cầu backend tự tính tổng tạo ra quan hệ so sánh rõ ràng giữa tổng đúng từ giỏ `E` và giá trị `total_amount` do client gửi. Kiểm tra ba giá trị liền kề `E-1`, `E`, `E+1` quanh điểm bằng nhau để xác định server có tin dữ liệu client hay không.

Các giá trị này chỉ dùng trong request API thử nghiệm; tổng được lưu phải bằng `E` trong cả ba trường hợp. Dùng giỏ có tổng `E > 1` VND để `E-1` không âm. Mỗi ca dùng baseline riêng, không tái sử dụng đơn hàng vừa tạo.

## Test case BVA

| ID | Vị trí so với tổng đúng `E` | Giá trị client gửi | Kết quả mong đợi | Trạng thái và kết quả |
|---|---|---:|---|---|
| TC-FR08-BVA-01 | Ngay dưới điểm bằng nhau | `E - 1` VND | Backend tính lại và lưu `E`, không phải `E-1` | **Failed** — đơn #3 được lưu là 57.999.999 VND (`E-1`) thay vì `E=58.000.000` VND. Bằng chứng: [`TC-FR08-BVA-01-checkout-response.png`](../screenshots/TC-FR08-BVA-01-checkout-response.png), [`TC-FR08-BVA-01-order-history.png`](../screenshots/TC-FR08-BVA-01-order-history.png). Xem BUG-FR08-02. |
| TC-FR08-BVA-02 | Tại điểm bằng nhau | `E` VND | Backend lưu `E` | **Passed** — đơn #4 được lưu là 58.000.000 VND, bằng `E`. Bằng chứng: [`TC-FR08-BVA-02-checkout-response.png`](../screenshots/TC-FR08-BVA-02-checkout-response.png), [`TC-FR08-BVA-02-order-history.png`](../screenshots/TC-FR08-BVA-02-order-history.png). |
| TC-FR08-BVA-03 | Ngay trên điểm bằng nhau | `E + 1` VND | Backend tính lại và lưu `E`, không phải `E+1` | **Failed** — đơn #5 được lưu là 58.000.001 VND (`E+1`) thay vì `E=58.000.000` VND. Bằng chứng: [`TC-FR08-BVA-03-checkout-response.png`](../screenshots/TC-FR08-BVA-03-checkout-response.png), [`TC-FR08-BVA-03-order-history.png`](../screenshots/TC-FR08-BVA-03-order-history.png). Xem BUG-FR08-02. |

## Cách chạy và ghi nhận

1. Đăng nhập bằng tài khoản thử nghiệm; tạo giỏ không rỗng và tính `E = tổng(đơn giá × số lượng)`.
2. Ghi baseline sản phẩm/giỏ và số đơn hàng hiện có.
3. Dùng DevTools Network “Chỉnh sửa và gửi lại” cho request `/api/checkout` hoặc công cụ API tương đương; chỉ đổi `total_amount` theo từng ca, giữ token hợp lệ và các dữ liệu khác ổn định.
4. Ghi request, trạng thái HTTP, `orderId`, sau đó kiểm tra đơn hàng qua `/api/orders/my-orders` để so sánh tổng đã lưu với `E`.
5. Làm mới trạng thái/tài khoản thử nghiệm giữa các ca nếu cần; không dùng cùng một `orderId` làm bằng chứng cho nhiều giá trị.

TC-FR08-BVA-01 Failed: đơn #3 lưu `E-1` (57.999.999 VND); TC-FR08-BVA-02 Passed: đơn #4 lưu `E` (58.000.000 VND); TC-FR08-BVA-03 Failed: đơn #5 lưu `E+1` (58.000.001 VND). Cả ba ca kiểm tra quanh điểm bằng nhau đã được thực thi. Hai ca Failed tái hiện BUG-FR08-02. FR-08 không quy định tổng đơn hàng tối thiểu hoặc tối đa.
