# Mobile — FR-06 Xem chi tiết sản phẩm — Phân tích giá trị biên

## Biên được đặc tả

FR-06 yêu cầu số lượng là số nguyên dương và tối thiểu bằng 1. Do đó có thể kiểm tra các giá trị quanh cận dưới: 0, 1, 2. Đặc tả không cung cấp cận trên; không tự đặt một giá trị tối đa.

| ID | Vị trí so với cận dưới | Input | Mong đợi | Trạng thái |
|---|---|---:|---|---|
| TC-FR06-MOB-BVA-01 | Ngay dưới min | 0 | Bị từ chối; không thêm sản phẩm với số lượng thay thế | **Failed** — app hiển thị “Thành công — Đã thêm vào giỏ hàng” khi ô số lượng vẫn là 0. Badge giữ `Giỏ (2)`; chưa xác minh số lượng dòng hàng sau thao tác. Ảnh: [`../screenshots/TC-FR06-MOB-BVA-01.jpg`](../screenshots/TC-FR06-MOB-BVA-01.jpg). BUG-FR06-02. |
| TC-FR06-MOB-BVA-02 | Tại min | 1 | Được chấp nhận; giỏ có số lượng 1 và phản hồi trực quan | **Passed** — với AirPods Pro 2 và số lượng 1, app hiện thông báo thành công và nút “Đã thêm”; giỏ hiển thị AirPods Pro 2 số lượng 1. Ảnh: [`../screenshots/TC-FR06-MOB-BVA-02-feedback.jpg`](../screenshots/TC-FR06-MOB-BVA-02-feedback.jpg), [`../screenshots/TC-FR06-MOB-BVA-02-cart.jpg`](../screenshots/TC-FR06-MOB-BVA-02-cart.jpg). |
| TC-FR06-MOB-BVA-03 | Ngay trên min | 2 | Được chấp nhận; giỏ có số lượng 2 và phản hồi trực quan | **Passed** — với Keychron Q1 và số lượng 2, app hiện thông báo thành công; giỏ hiển thị Keychron Q1 số lượng 2, thành tiền 8.000.000 đ. Ảnh: [`../screenshots/TC-FR06-MOB-BVA-03-feedback.jpg`](../screenshots/TC-FR06-MOB-BVA-03-feedback.jpg), [`../screenshots/TC-FR06-MOB-BVA-03-cart.jpg`](../screenshots/TC-FR06-MOB-BVA-03-cart.jpg). |

## Giá trị ngoài miền số nguyên dương

Các lớp không hợp lệ được tách thành ca riêng để kết quả có thể tái hiện rõ ràng.

| ID | Input | Mong đợi | Trạng thái |
|---|---:|---|---|
| TC-FR06-MOB-BVA-04 | -1 | Bị từ chối; không tự chuyển thành số lượng hợp lệ | **Failed** — nhập được `-1` cho MacBook Pro M3; app vẫn hiển thị thông báo “Thành công — Đã thêm vào giỏ hàng”. Ảnh giỏ sau thao tác hiển thị MacBook Pro M3 số lượng 1 và badge `Giỏ (3)`. Kết quả cho thấy giá trị âm bị chấp nhận/chuẩn hóa thành số lượng 1. Ảnh: [`../screenshots/TC-FR06-MOB-BVA-04-feedback.jpg`](../screenshots/TC-FR06-MOB-BVA-04-feedback.jpg), [`../screenshots/TC-FR06-MOB-BVA-04-cart.jpg`](../screenshots/TC-FR06-MOB-BVA-04-cart.jpg). BUG-FR06-02. |
| TC-FR06-MOB-BVA-05 | `1,5` (decimal comma via iPhone keyboard) | Bị từ chối; không cắt phần thập phân hoặc làm tròn | **Failed** — với `1,5` hiển thị trong trường số lượng, app vẫn báo “Thành công — Đã thêm vào giỏ hàng” và nút đổi thành “Đã thêm”. Giỏ gửi kèm hiển thị iPhone số lượng 1, nhưng không có ảnh trạng thái trước để xác định quantity có đổi hay không. Ảnh: [`../screenshots/TC-FR06-MOB-BVA-05-feedback.jpg`](../screenshots/TC-FR06-MOB-BVA-05-feedback.jpg), [`../screenshots/TC-FR06-MOB-BVA-05-cart.jpg`](../screenshots/TC-FR06-MOB-BVA-05-cart.jpg). BUG-FR06-02. |
| TC-FR06-MOB-BVA-06 | `abc` | Bị từ chối; không thêm sản phẩm với số lượng mặc định | **Failed** — trường số lượng nhận `abc`; app vẫn báo “Thành công — Đã thêm vào giỏ hàng” và nút đổi thành “Đã thêm”. Ảnh giỏ kèm theo không có baseline để xác minh thay đổi số lượng. Ảnh: [`../screenshots/TC-FR06-MOB-BVA-06-feedback.jpg`](../screenshots/TC-FR06-MOB-BVA-06-feedback.jpg), [`../screenshots/TC-FR06-MOB-BVA-06-cart.jpg`](../screenshots/TC-FR06-MOB-BVA-06-cart.jpg). BUG-FR06-02. |
| TC-FR06-MOB-BVA-07 | Rỗng | Bị từ chối; không thêm sản phẩm với số lượng mặc định | **Failed** — để trống ô số lượng nhưng app vẫn hiển thị “Thành công — Đã thêm vào giỏ hàng”. Giỏ sau thao tác hiển thị AirPods Pro 2 số lượng 1, badge `Giỏ (4)`. Ảnh: [`../screenshots/TC-FR06-MOB-BVA-07-feedback.jpg`](../screenshots/TC-FR06-MOB-BVA-07-feedback.jpg), [`../screenshots/TC-FR06-MOB-BVA-07-cart.jpg`](../screenshots/TC-FR06-MOB-BVA-07-cart.jpg). BUG-FR06-02. |

## Tổng kết thực thi

Cả 7 ca BVA đã được chạy trên iPhone: **2 Passed** (BVA-02, BVA-03), **5 Failed** (BVA-01, BVA-04, BVA-05, BVA-06, BVA-07), **0 Not Executed**. Hai giá trị hợp lệ tại biên 1 và 2 được chấp nhận. Năm giá trị không hợp lệ (0, -1, 1,5, abc, rỗng) đều nhận phản hồi thành công; các ảnh giỏ hàng được mô tả theo đúng trạng thái quan sát được, không suy diễn mức thay đổi khi thiếu baseline.

## Ghi chú thực thi

Cả 7 ca BVA được chạy trên iPhone với Expo Go SDK 57; kết nối backend qua LAN hoạt động. Chi tiết kết quả thực tế, trạng thái và bằng chứng của từng ca nằm trong [`../test-cases/test-cases.csv`](../test-cases/test-cases.csv).

Trong lần thử ban đầu của BVA-04, bàn phím iPhone không có phím dấu trừ; sau đó ca đã được chạy lại và ảnh hiển thị `-1`. Cách nhập dấu trừ trong lần chạy thành công không được ghi lại; ảnh bàn phím ban đầu được giữ làm ghi chú thao tác: [`../screenshots/TC-FR06-MOB-BVA-04-keyboard.jpg`](../screenshots/TC-FR06-MOB-BVA-04-keyboard.jpg).

FR-06 không quy định cận trên cho số lượng nên không tạo test case cho giá trị tối đa. Với BVA-05/06 và các trường hợp không có baseline, báo cáo chỉ ghi nhận phản hồi và trạng thái giỏ nhìn thấy, không kết luận mức thay đổi số lượng.\n