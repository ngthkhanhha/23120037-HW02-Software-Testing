# Báo cáo lỗi

Bug đã xác nhận: BUG-FR02-01, BUG-FR02-02, BUG-FR02-03, BUG-FR02-04, BUG-FR06-01, BUG-FR06-02, BUG-FR08-01, BUG-FR08-02 và BUG-FR08-03. Chưa tạo GitHub Issues.

## BUG-FR06-01 — Chi tiết sản phẩm trên Mobile không hiển thị danh mục

- **Tính năng/phiên bản:** FR-06 — chi tiết sản phẩm trong ứng dụng Expo trên iPhone.
- **Môi trường:** iPhone, Expo Go SDK 57; ứng dụng chạy từ bản sao SDK 57 cục bộ; backend truy cập được qua LAN.
- **Mức độ nghiêm trọng:** Low (a required product detail field is missing).
- **Tiền điều kiện:** Mở trang chi tiết sản phẩm seed iPhone 15 Pro Max.
- **Các bước:** Mở ứng dụng di động, chọn iPhone 15 Pro Max hoặc MacBook Pro M3, rồi kiểm tra trang chi tiết.
- **Kết quả mong đợi (SRS FR-06):** Trang chi tiết hiển thị ảnh lớn, tên, giá, mô tả và danh mục.
- **Kết quả thực tế:** Cả hai trang đều hiển thị ảnh, tên, giá, mô tả, số lượng và nút thêm vào giỏ; không trang nào hiển thị danh mục.
- **Tái hiện:** Quan sát ở TC-FR06-MOB-DT-01 (iPhone 15 Pro Max, seed `category_id=1`) và tái hiện in TC-FR06-MOB-DT-02 (MacBook Pro M3, seed `category_id=2`). Rà soát mã nguồn xác nhận JSX trang chi tiết di động không hiển thị danh mục.
- **Bằng chứng:** [`../screenshots/TC-FR06-MOB-DT-01.jpg`](../screenshots/TC-FR06-MOB-DT-01.jpg), [`../screenshots/TC-FR06-MOB-DT-02.jpg`](../screenshots/TC-FR06-MOB-DT-02.jpg).
- **GitHub Issue:** Chưa tạo.
- **Trạng thái xác minh:** Đã xác nhận qua ảnh chạy thực tế, dữ liệu seed và rà soát mã giao diện.

## BUG-FR06-02 — Chấp nhận số lượng không hợp lệ và báo thêm thành công

- **Tính năng/phiên bản:** FR-06 — chi tiết sản phẩm và thêm vào giỏ trong ứng dụng Expo trên iPhone.
- **Môi trường:** iPhone, Expo Go SDK 57; bản ứng dụng SDK 57 cục bộ; backend truy cập được qua LAN.
- **Mức độ nghiêm trọng:** Trung bình (ứng dụng chấp nhận số lượng không hợp lệ và báo thành công).
- **Tiền điều kiện:** Mở trang chi tiết sản phẩm hiện có; trường số lượng có thể chỉnh sửa.
- **Các bước:** Để trống trường số lượng hoặc nhập `-1`, `0`, `1,5`, hoặc `abc` rồi nhấn **Thêm vào giỏ hàng**.
- **Kết quả mong đợi (SRS FR-06):** Số lượng phải là số nguyên dương, tối thiểu bằng 1; giá trị âm, 0, thập phân và không phải số không được chấp nhận như lần thêm thành công.
- **Kết quả thực tế:** Khi trường hiển thị rỗng, `-1`, `0`, `1,5` hoặc `abc`, ứng dụng hiển thị “Thành công — Đã thêm vào giỏ hàng”. Với `-1`, giỏ sau thao tác có MacBook Pro M3 số lượng 1; với đầu vào rỗng, giỏ có AirPods Pro 2 số lượng 1. Ảnh xác nhận trạng thái sau thao tác nhưng không có baseline tương ứng để xác định chính xác lượng thay đổi. Ảnh giỏ của các đầu vào sai khác cũng thiếu baseline.
- **Tái hiện:** Observed in TC-FR06-MOB-BVA-01 (0), TC-FR06-MOB-BVA-04 (`-1`), TC-FR06-MOB-BVA-05 (`1,5`, dấu phẩy thập phân), và TC-FR06-MOB-BVA-06 (`abc`), và TC-FR06-MOB-BVA-07 (rỗng). Mỗi đầu vào không hợp lệ đều tạo phản hồi thành công.
- **Bằng chứng:** [`../screenshots/TC-FR06-MOB-BVA-01.jpg`](../screenshots/TC-FR06-MOB-BVA-01.jpg), [`../screenshots/TC-FR06-MOB-BVA-04-feedback.jpg`](../screenshots/TC-FR06-MOB-BVA-04-feedback.jpg), [`../screenshots/TC-FR06-MOB-BVA-04-cart.jpg`](../screenshots/TC-FR06-MOB-BVA-04-cart.jpg), [`../screenshots/TC-FR06-MOB-BVA-05-feedback.jpg`](../screenshots/TC-FR06-MOB-BVA-05-feedback.jpg), [`../screenshots/TC-FR06-MOB-BVA-05-cart.jpg`](../screenshots/TC-FR06-MOB-BVA-05-cart.jpg), [`../screenshots/TC-FR06-MOB-BVA-06-feedback.jpg`](../screenshots/TC-FR06-MOB-BVA-06-feedback.jpg), [`../screenshots/TC-FR06-MOB-BVA-06-cart.jpg`](../screenshots/TC-FR06-MOB-BVA-06-cart.jpg), [`../screenshots/TC-FR06-MOB-BVA-07-feedback.jpg`](../screenshots/TC-FR06-MOB-BVA-07-feedback.jpg), [`../screenshots/TC-FR06-MOB-BVA-07-cart.jpg`](../screenshots/TC-FR06-MOB-BVA-07-cart.jpg).
- **GitHub Issue:** Chưa tạo.
- **Trạng thái xác minh:** Đã xác nhận qua ảnh chạy thực tế. Ảnh cho thấy MacBook số lượng 1 sau `-1` và AirPods Pro 2 số lượng 1 sau đầu vào rỗng; không khẳng định mức chênh lệch số lượng trước/sau.


## BUG-FR02-01 — Email sai định dạng không bị HTML5 chặn

- **Tính năng/phiên bản:** FR-02 — đăng nhập Web; EShop SUT bản chạy tại localhost.
- **Môi trường:** Windows, Chrome, frontend `http://localhost:5173/login`, backend `localhost:3000`.
- **Mức độ:** Thấp (lỗi kiểm tra định dạng phía giao diện; chưa có bằng chứng bỏ qua xác thực backend).
- **Tiền điều kiện:** Backend và frontend đang chạy; đang ở trang đăng nhập.
- **Bước tái hiện:**
  1. Nhập `ha@` vào trường tài khoản.
  2. Nhập một mật khẩu bất kỳ.
  3. Bấm `Sign In`.
- **Kết quả mong đợi (FR-02):** Trường email dùng `type="email"`; trình duyệt chặn email sai định dạng bằng HTML5 trước khi gửi request.
- **Kết quả thực tế:** Form gửi request tới `/api/login`; DevTools Console hiển thị HTTP 401 Unauthorized và giao diện báo đăng nhập thất bại.
- **Tần suất tái hiện:** 1 lần đã quan sát; chạy lại để xác nhận thêm nếu có thể.
- **Bằng chứng:** `../screenshots/TC-FR02-DT-02.png`.
- **GitHub Issue:** Chưa tạo.
- **Trạng thái xác minh:** Đã tái hiện một lần; đối chiếu mã `frontend-web/src/pages/Login.jsx` cho thấy trường tài khoản dùng `type="text"`.
## BUG-FR02-02 — Bộ đếm đăng nhập sai tăng 2 thay vì 1

- **Tính năng/phiên bản:** FR-02 — đăng nhập Web; EShop SUT bản chạy tại localhost.
- **Môi trường:** Windows, Chrome, frontend `http://localhost:5173/login`, backend `localhost:3000`, SQLite.
- **Mức độ:** Trung bình (làm sai ngưỡng khóa tài khoản và số lần thử còn lại).
- **Tiền điều kiện:** Tài khoản `test@eshop.com` tồn tại, không bị khóa; `login_attempts=0`.
- **Bước tái hiện:**
  1. Nhập `test@eshop.com` và mật khẩu sai `Wrong-Test-2026!`.
  2. Gửi đúng một lần đăng nhập.
  3. Kiểm tra `login_attempts` bằng truy vấn DB chỉ đọc.
- **Kết quả mong đợi (FR-02):** Đăng nhập bị từ chối và bộ đếm tăng từ 0 lên 1.
- **Kết quả thực tế:** Giao diện từ chối đăng nhập bằng thông báo chung; DB ghi `login_attempts=2`. Mã `backend/server.js` tính `user.login_attempts + 2`.
- Xác nhận BVA-02: trên tài khoản mới, hai request sai mật khẩu làm `login_attempts` tăng từ 0 lên 4; các request tiếp theo trả HTTP 403.
- **Tần suất tái hiện:** 1 lần đã quan sát; nguồn mã xác nhận phép tăng 2.
- **Bằng chứng:** `../screenshots/TC-FR02-DT-04.png`; bộ đếm được xác nhận bằng truy vấn SQLite chỉ đọc.
- **GitHub Issue:** Chưa tạo.
- **Trạng thái xác minh:** Đã xác nhận qua thực thi và đối chiếu mã nguồn.
## BUG-FR02-03 — API đăng nhập trả password dạng rõ

- Tính năng/phiên bản: FR-02 Web login; local EShop SUT.
- Môi trường: Windows, Chrome, frontend localhost:5173, backend localhost:3000.
- Mức độ nghiêm trọng: Cao; thông tin xác thực nằm trong phản hồi và có thể bị lưu trong DevTools, log hoặc công cụ giám sát.
- Tiền điều kiện: Có tài khoản thử nghiệm và có thể đăng nhập.
- Các bước: Mở DevTools Network, đăng nhập và kiểm tra phản hồi của `POST /api/login`.
- Kết quả mong đợi: Phản hồi trả JWT và các trường thông tin người dùng cần thiết, không chứa password.
- Kết quả thực tế: Phản hồi JSON chứa `user.password` ở dạng rõ.
- Tái hiện: Quan sát trong phản hồi TC-FR02-DT-06; backend trả toàn bộ đối tượng người dùng.
- Bằng chứng: `../screenshots/TC-FR02-DT-06-login-response.png` (đã che JWT và password).
- GitHub Issue: Chưa tạo.
- Trạng thái xác minh: Đã xác nhận từ phản hồi và mã nguồn.


## BUG-FR02-04 — Thời gian khóa cấu hình 180 giây thay vì 30 giây

- **Tính năng/phiên bản:** FR-02 — đăng nhập Web; EShop SUT chạy local.
- **Môi trường:** Windows, Chrome, frontend `localhost:5173`, backend `localhost:3000`, SQLite.
- **Mức độ:** Trung bình — người dùng hợp lệ bị ngăn đăng nhập lâu hơn thời gian FR-02 quy định.
- **Tiền điều kiện:** Tài khoản thử nghiệm mới; có thể tái tạo trạng thái khóa bằng các lần nhập sai.
- **Bước tái hiện:** Tạo trạng thái khóa; thử đăng nhập với thông tin đúng ở khoảng 30 giây sau thời điểm khóa bắt đầu.
- **Kết quả mong đợi:** Sau 30 giây tài khoản được mở khóa và thông tin đúng được chấp nhận (FR-02).
- **Kết quả thực tế:** TC-FR02-BVA-05 nhận HTTP 403 ở khoảng 30 giây. Đối chiếu `backend/server.js` cho thấy `locked_until = new Date(Date.now() + 180000)`, tương ứng 180 giây.
- **Tần suất tái hiện:** Quan sát trong TC-BVA-05; cấu hình 180000 ms xác nhận từ mã nguồn.
- **Bằng chứng:** [`../screenshots/TC-FR02-BVA-05.png`](../screenshots/TC-FR02-BVA-05.png); mã nguồn `backend/server.js`, dòng thiết lập `+ 180000`.
- **GitHub Issue:** Chưa tạo.
- **Trạng thái xác minh:** Xác nhận bằng kết quả thực thi và đối chiếu mã nguồn. Mốc UI được đo xấp xỉ, không phải phép đo thời gian chính xác.
## Mẫu báo cáo bug

### BUG-[ID] — [Tiêu đề ngắn]
- Tính năng/phiên bản:
- Môi trường:
- Mức độ nghiêm trọng:
- Tiền điều kiện:
- Các bước tái hiện:
  1. 
- Kết quả mong đợi (kèm nguồn yêu cầu):
- Kết quả thực tế:
- Tần suất tái hiện:
- Bằng chứng: `../screenshots/[tên-ảnh]`
- GitHub Issue: [URL sau khi tạo]
- Trạng thái xác minh:

## Quan sát cần xác minh (chưa tính là bug đã xác nhận)

### OBS-FR23-01 — Nhãn nút đăng xuất hiển thị “Thoát”
- Nguồn yêu cầu cần đối chiếu: SRS FR-23 yêu cầu nhãn “Đăng xuất”.
- Quan sát: Ảnh sau đăng nhập hiển thị nút “Thoát”.
- Bằng chứng: `../screenshots/TC-FR02-DT-01.png`.
- Bước tiếp theo: Tái hiện sau khi đăng nhập lại và xác nhận phạm vi áp dụng của FR-23. Chỉ chuyển thành bug/GitHub Issue sau khi xác minh.





## BUG-FR08-01 — Có thể sửa trực tiếp tổng tiền thanh toán

- Tính năng: FR-08 Checkout (Web).
- Mức độ nghiêm trọng: Trung bình.
- Tiền điều kiện: Tài khoản thử đã đăng nhập, tổng giỏ `E=58.000.000 VND`; đang mở trang thanh toán.
- Các bước: Chọn trường tổng tiền đang hiển thị và thay giá trị bằng 57.999.970.
- Kết quả mong đợi: Tổng tiền được tính từ nội dung giỏ và không thể sửa trực tiếp (kỳ vọng TC-FR08-DT-03).
- Kết quả thực tế: Trường nhận giá trị mới và tổng thanh toán hiển thị đổi thành 57.999.970 VND. Test này không gửi đơn hàng.
- Bằng chứng: [`../screenshots/TC-FR08-DT-03-editable-total.png`](../screenshots/TC-FR08-DT-03-editable-total.png).
- Giới hạn bằng chứng: Đã xác nhận sửa được trực tiếp; xử lý phía server được theo dõi riêng ở BUG-FR08-02.
- GitHub Issue: Chưa tạo.

## BUG-FR08-02 — Backend chấp nhận tổng thanh toán do client gửi

- Tính năng: FR-08 Checkout (Web).
- Mức độ nghiêm trọng: Cao — client có thể thay đổi tổng đơn trước khi gửi.
- Tiền điều kiện: Tài khoản đã đăng nhập, tổng giỏ `E=58.000.000 VND`.
- Các bước: Gửi thanh toán với `total_amount=E-1` hoặc `E+1`; kiểm tra lịch sử đơn đã xác thực.
- Kết quả mong đợi: Backend tính lại và lưu tổng giỏ `E=58.000.000 VND`.
- Kết quả thực tế: DT-04 và BVA-01 lưu `E-1=57.999.999 VND` (đơn #1 và #3); BVA-03 lưu `E+1=58.000.001 VND` (đơn #5). Ảnh Network cho thấy HTTP 200; lịch sử đơn xác nhận số tiền đã lưu. Ca đối chứng BVA-02 lưu đúng `E` ở đơn #4.
- Bằng chứng: [`../screenshots/TC-FR08-DT-04-checkout-response.png`](../screenshots/TC-FR08-DT-04-checkout-response.png), [`../screenshots/TC-FR08-DT-04-order-history.png`](../screenshots/TC-FR08-DT-04-order-history.png), [`../screenshots/TC-FR08-BVA-01-checkout-response.png`](../screenshots/TC-FR08-BVA-01-checkout-response.png), [`../screenshots/TC-FR08-BVA-01-order-history.png`](../screenshots/TC-FR08-BVA-01-order-history.png), [`../screenshots/TC-FR08-BVA-02-order-history.png`](../screenshots/TC-FR08-BVA-02-order-history.png), [`../screenshots/TC-FR08-BVA-03-checkout-response.png`](../screenshots/TC-FR08-BVA-03-checkout-response.png), [`../screenshots/TC-FR08-BVA-03-order-history.png`](../screenshots/TC-FR08-BVA-03-order-history.png).
- Giới hạn bằng chứng: Không đọc rõ chi tiết payload trong ảnh Network; lịch sử đơn hàng xác minh tổng tiền đã lưu.
- GitHub Issue: Chưa tạo.

## BUG-FR08-03 — Giỏ hàng vẫn còn sản phẩm sau khi thanh toán thành công

- Tính năng: FR-08 Checkout (Web).
- Mức độ nghiêm trọng: Trung bình — giỏ không được xóa có thể dẫn tới gửi đơn trùng ngoài ý muốn.
- Tiền điều kiện: Tài khoản đã đăng nhập, giỏ có iPhone 15 Pro Max x1 và Samsung Galaxy S24 Ultra x1.
- Các bước: Thanh toán thành công, sau đó quay lại kiểm tra giỏ.
- Kết quả mong đợi: Giỏ được xóa sau khi thanh toán thành công (kỳ vọng TC-FR08-DT-05).
- Kết quả thực tế: Cả hai sản phẩm vẫn còn và tạm tính vẫn là 58.000.000 VND sau khi luồng báo thành công. DT-05 không gửi đơn thứ hai.
- Bằng chứng: [`../screenshots/TC-FR08-DT-05-cart-not-cleared.png`](../screenshots/TC-FR08-DT-05-cart-not-cleared.png), [`../screenshots/TC-FR08-DT-04-checkout-response.png`](../screenshots/TC-FR08-DT-04-checkout-response.png).
- GitHub Issue: Chưa tạo.


## BUG-FR14-02 — Chấp nhận tên danh mục rỗng

- Tính năng: FR-14 Category Management (Web Admin).
- Mức độ nghiêm trọng: Trung bình.
- Tiền điều kiện: Đăng nhập với vai trò admin; danh sách có ba danh mục seed.
- Các bước: Để trống trường tên danh mục và gửi biểu mẫu thêm.
- Kết quả mong đợi: Từ chối tên rỗng và không tạo danh mục (FR-14: tên danh mục là bắt buộc và không được để trống).
- Kết quả thực tế: Danh sách hiển thị danh mục #4 không có tên; danh sách API xác nhận bản ghi đã được lưu.
- Bằng chứng: [`../screenshots/TC-FR14-BVA-01.png`](../screenshots/TC-FR14-BVA-01.png).
- Dọn dữ liệu thử: Chỉ xóa danh mục rỗng #4 do test tạo sau khi lưu bằng chứng; danh mục seed #1–#3 vẫn còn.
- GitHub Issue: Chưa tạo.



## BUG-FR14-01 — Người dùng thường có thể tạo danh mục

- Tính năng: FR-14 — Quản lý danh mục (Web Admin).
- Mức độ nghiêm trọng: Cao — người dùng không phải admin có thể thay đổi dữ liệu danh mục.
- Tiền điều kiện: Đăng nhập bằng tài khoản người dùng thường có JWT hợp lệ.
- Các bước: Gửi POST `/api/categories` bằng JWT của người dùng thường; kiểm tra phản hồi và danh sách danh mục.
- Kết quả mong đợi: Thao tác thay đổi danh mục bị từ chối với vai trò không phải admin theo SEC-03.
- Kết quả thực tế: Request trả HTTP 200 và tạo danh mục thăm dò #4 `DT05-Probe-NTHH`.
- Bằng chứng: [`../screenshots/TC-FR14-DT-05.png`](../screenshots/TC-FR14-DT-05.png).
- Dọn dữ liệu thử: Admin đã xóa danh mục thăm dò sau khi chụp bằng chứng; danh mục seed được giữ nguyên.
- GitHub Issue: Chưa tạo.
