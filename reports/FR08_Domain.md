# FR-08 — Phân tích miền (Thanh toán)

## Thông tin

- Nền tảng: Web.
- Nguồn yêu cầu: Đặc tả yêu cầu hệ thống EShop, FR-08.
- Phạm vi: Chỉ kiểm thử thanh toán. Hành vi mã giảm giá thuộc FR-09; giỏ hàng được dùng làm dữ liệu đầu vào.
- Trạng thái thực thi: Đã thực thi 8/8 test case; 3 Passed, 5 Failed, 0 Not Executed.

## Yêu cầu được kiểm thử

1. Chỉ người dùng đã xác thực mới được tiến hành thanh toán.
2. Tổng thanh toán được tính tự động từ giỏ hàng và không thể sửa trực tiếp.
3. Trang thanh toán hiển thị tất cả sản phẩm được mua.
4. Backend tự tính lại tổng tiền và không tin giá trị `total_amount` do client gửi.
5. Sau khi thanh toán thành công, giỏ hàng được xóa.

## Các lớp tương đương

| Thuộc tính | Phân lớp | Hành vi mong đợi |
|---|---|---|
| Xác thực | Phiên đăng nhập hợp lệ | Có thể thanh toán. |
| Xác thực | Đã đăng xuất, thiếu hoặc token không hợp lệ | Bị chặn; không tạo đơn hàng. |
| Giỏ hàng | Có một hoặc nhiều sản phẩm | Trang thanh toán hiển thị từng sản phẩm và số lượng. |
| Giỏ hàng | Rỗng | FR-08 không quy định hành vi mong đợi; xem đây là kiểm thử thăm dò. |
| Tổng tiền hiển thị | Bằng tổng đơn giá nhân số lượng | Hiển thị tổng được tính từ giỏ hàng và không thể sửa. |
| Tổng tiền client gửi | Khác tổng được tính từ giỏ hàng | Backend lưu số tiền tính từ giỏ, không dùng giá trị client gửi. |
| Kết quả thanh toán | Thành công | Tạo đơn hàng và xóa giỏ hàng. |
| Kết quả thanh toán | Thất bại | FR-08 chưa quy định trạng thái giỏ; cần tìm hiểu, không tự giả định tiêu chí đạt/trượt. |

## Áp dụng kỹ thuật

Các biến được chọn gồm trạng thái xác thực, nội dung giỏ hàng, tổng tiền tính được, tổng tiền client gửi và kết quả thanh toán. Bộ ca có kiểm tra giao diện và phía server để tránh nhầm lẫn giữa giới hạn ở client với việc thực thi quy tắc ở backend. Với kiểm tra sửa tổng tiền, đặt `E` bằng tổng đơn giá nhân số lượng, sau đó so sánh giá trị `E-1` được gửi với tổng đơn hàng đã lưu. Dùng tài khoản thử nghiệm và lưu mã đơn hàng. Không để lộ token xác thực trong bằng chứng. Không đưa mã giảm giá vào phạm vi vì thuộc FR-09.

## Test case Domain

| ID | Tình huống | Kết quả mong đợi | Trạng thái và kết quả quan sát |
|---|---|---|---|
| TC-FR08-DT-01 | Người dùng chưa đăng nhập nhấn Thanh toán khi giỏ không rỗng | Yêu cầu người dùng đăng nhập; không tạo đơn hàng. | **Passed** — tại `/cart` xuất hiện cảnh báo yêu cầu đăng nhập; sau khi đóng cảnh báo, ứng dụng chuyển tới `/login`. Chưa lưu bằng chứng Network/lịch sử đơn hàng để xác minh độc lập rằng không có đơn hàng được tạo. Bằng chứng: [`TC-FR08-DT-01-cart-login-alert.png`](../screenshots/TC-FR08-DT-01-cart-login-alert.png), [`TC-FR08-DT-01-login-redirect.png`](../screenshots/TC-FR08-DT-01-login-redirect.png). |
| TC-FR08-DT-02 | Người dùng đã đăng nhập mở trang thanh toán với nhiều sản phẩm | Hiển thị mọi sản phẩm và số lượng; tổng tiền khớp với giỏ hàng. | **Passed** — iPhone 15 Pro Max x1 (30.000.000 VND) và Samsung Galaxy S24 Ultra x1 (28.000.000 VND) được hiển thị; tổng là 58.000.000 VND. Bằng chứng: [`TC-FR08-DT-02-checkout-items-total.png`](../screenshots/TC-FR08-DT-02-checkout-items-total.png). Không gửi đơn hàng. |
| TC-FR08-DT-03 | Thử sửa trực tiếp tổng tiền trên trang thanh toán | Tổng tiền được hiển thị nhưng không thể sửa trực tiếp. | **Failed** — trường nhập nhận giá trị 57.999.970 thay cho 58.000.000 và tổng thanh toán trên giao diện thay đổi theo. Bằng chứng: [`TC-FR08-DT-03-editable-total.png`](../screenshots/TC-FR08-DT-03-editable-total.png). Không gửi đơn hàng. Xem BUG-FR08-01. |
| TC-FR08-DT-04 | Gửi tổng client `E-1` và kiểm tra đơn hàng đã lưu | Backend lưu `E` tính từ giỏ, không phải `E-1` từ client. | **Failed** — thanh toán trả HTTP 200; lịch sử đơn hàng trong Hồ sơ hiển thị đơn #1 có giá 57.999.999 VND, bằng `E-1` thay vì `E=58.000.000` VND. Bằng chứng: [`TC-FR08-DT-04-checkout-response.png`](../screenshots/TC-FR08-DT-04-checkout-response.png) và [`TC-FR08-DT-04-order-history.png`](../screenshots/TC-FR08-DT-04-order-history.png). Ảnh được cung cấp không đọc rõ payload request và orderId. |
| TC-FR08-DT-05 | Kiểm tra giỏ sau khi thanh toán thành công | Hiển thị xác nhận đơn hàng và giỏ hàng rỗng. | **Failed** — sau khi trang thanh toán báo thành công, giỏ vẫn có iPhone 15 Pro Max x1 và Samsung Galaxy S24 Ultra x1; tạm tính vẫn là 58.000.000 VND. Bằng chứng: [`TC-FR08-DT-05-cart-not-cleared.png`](../screenshots/TC-FR08-DT-05-cart-not-cleared.png). Trạng thái này được kiểm tra sau DT-04; không gửi đơn thứ hai. |

DT-01 và DT-02 Passed. DT-03 Failed vì sửa được tổng tiền; DT-04 Failed vì server lưu giá trị `E-1` từ client; DT-05 Failed vì giỏ hàng vẫn còn sản phẩm sau khi thanh toán thành công. BVA-01 cũng Failed: đơn #3 được lưu với `E-1` (57.999.999 VND), tái hiện BUG-FR08-02. BVA-02 Passed: đơn #4 được lưu đúng `E=58.000.000` VND. BVA-03 Failed: đơn #5 được lưu với `E+1` (58.000.001 VND), cũng tái hiện BUG-FR08-02. Tất cả test case FR-08 đã được thực thi: 3 Passed và 5 Failed. Xem BUG-FR08-01 đến BUG-FR08-03. Bằng chứng chi tiết có trong [`../test-cases/test-cases.csv`](../test-cases/test-cases.csv).

## Rà soát khoảng trống thiết kế

Năm ca Domain bao phủ năm mệnh đề của FR-08. DT-03 kiểm tra việc sửa tổng tiền ở client; DT-04 kiểm tra cách server xử lý số tiền; DT-05 kiểm tra việc xóa giỏ hàng — cả ba đều Failed. Hành vi với giỏ rỗng, gửi thanh toán trùng lặp và lỗi API có thể được mở rộng, nhưng FR-08 chưa xác định kết quả mong đợi. DT-01 đến DT-05 đã có kết quả thực thi ở trên; BVA-01 đã chạy và Failed vì backend lưu `E-1`; BVA-02 Passed với đơn #4 lưu `E=58.000.000` VND; BVA-03 Failed vì đơn #5 lưu `E+1` (58.000.001 VND). Cả 8 ca FR-08 đã được thực thi; xem FR08_BVA.md.

## Các điểm cần lưu ý

- TC-FR08-DT-04 gửi một đơn thử nghiệm (#1). Lịch sử đơn hàng hiển thị 57.999.999 VND, bằng `E-1`. Phản hồi Network của thanh toán là HTTP 200; ảnh không hiển thị payload request hoặc orderId.
- TC-FR08-DT-05 được kiểm tra sau lần thanh toán thành công trong DT-04; giỏ vẫn còn cả hai sản phẩm. Không tạo thêm đơn hàng.
- Với TC-FR08-DT-01, cần lưu bằng chứng Network/lịch sử đơn hàng riêng nếu yêu cầu xác minh độc lập rằng không có đơn nào được tạo.
- TC-FR08-BVA-01 gửi một đơn thử nghiệm (#3); lịch sử đơn hàng hiển thị 57.999.999 VND (`E-1`), xác nhận BUG-FR08-02. Bằng chứng được dẫn trong FR08_BVA.md.
- TC-FR08-BVA-02 gửi một đơn thử nghiệm (#4) và lưu đúng `E=58.000.000` VND. Bằng chứng được dẫn trong FR08_BVA.md.
- TC-FR08-BVA-03 gửi một đơn thử nghiệm (#5); lịch sử lưu `E+1=58.000.001` VND, xác nhận BUG-FR08-02. Bằng chứng được dẫn trong FR08_BVA.md.
- Không đưa mã giảm giá vào kết quả FR-08; kiểm thử mã giảm giá thuộc FR-09.
