# Báo cáo lỗi

Confirmed bugs: BUG-FR02-01, BUG-FR02-02, BUG-FR02-03, BUG-FR02-04, BUG-FR06-01, BUG-FR06-02, BUG-FR08-01, BUG-FR08-02 and BUG-FR08-03. GitHub Issues have not been created.

## BUG-FR06-01 — Mobile product detail omits the category

- **Feature/version:** FR-06 — product detail in the iPhone Expo app.
- **Environment:** iPhone, Expo Go SDK 57; app served from the local SDK 57 copy; backend reachable over LAN.
- **Severity:** Low (a required product detail field is missing).
- **Preconditions:** Open the detail page for the seeded product iPhone 15 Pro Max.
- **Steps:** Open the mobile app, select iPhone 15 Pro Max or MacBook Pro M3, and inspect its detail page.
- **Expected (SRS FR-06):** Detail page displays the large image, name, price, description, and category.
- **Actual:** Both details show image, name, price, description, quantity, and add-to-cart control; neither shows its category.
- **Reproduction:** Observed in TC-FR06-MOB-DT-01 (iPhone 15 Pro Max, seeded `category_id=1`) and reproduced in TC-FR06-MOB-DT-02 (MacBook Pro M3, seeded `category_id=2`). Source review confirms the mobile detail JSX does not render the category.
- **Evidence:** [`../screenshots/TC-FR06-MOB-DT-01.jpg`](../screenshots/TC-FR06-MOB-DT-01.jpg), [`../screenshots/TC-FR06-MOB-DT-02.jpg`](../screenshots/TC-FR06-MOB-DT-02.jpg).
- **GitHub Issue:** Not created.
- **Verification:** Confirmed by runtime screenshot, seed data, and UI source review.

## BUG-FR06-02 — Invalid quantity is accepted and reported as a successful add

- **Feature/version:** FR-06 — product detail and add-to-cart in the iPhone Expo app.
- **Environment:** iPhone, Expo Go SDK 57; local SDK 57 app copy; backend reachable over LAN.
- **Severity:** Medium (the app accepts an invalid quantity and reports success).
- **Preconditions:** Open an existing product detail page; quantity field is editable.
- **Steps:** Leave the quantity field empty, or enter `-1`, `0`, `1,5`, or `abc` and tap **Thêm vào giỏ hàng**.
- **Expected (SRS FR-06):** Quantity must be a positive integer with a minimum of 1; negative, zero, fractional, and non-numeric values must not be accepted as successful additions.
- **Actual:** With an empty field or `-1`, `0`, `1,5`, and `abc` visible in the field, the app displayed “Thành công — Đã thêm vào giỏ hàng”. For `-1`, the resulting cart displayed MacBook Pro M3 at quantity 1; for the empty input, it displayed AirPods Pro 2 at quantity 1. These screenshots establish the resulting states but do not provide paired baselines for exact quantity deltas. The other invalid-input cart screenshots also lack paired baselines.
- **Reproduction:** Observed in TC-FR06-MOB-BVA-01 (zero), TC-FR06-MOB-BVA-04 (`-1`), TC-FR06-MOB-BVA-05 (`1,5`, decimal comma), and TC-FR06-MOB-BVA-06 (`abc`), and TC-FR06-MOB-BVA-07 (empty). Each invalid input produced success feedback.
- **Evidence:** [`../screenshots/TC-FR06-MOB-BVA-01.jpg`](../screenshots/TC-FR06-MOB-BVA-01.jpg), [`../screenshots/TC-FR06-MOB-BVA-04-feedback.jpg`](../screenshots/TC-FR06-MOB-BVA-04-feedback.jpg), [`../screenshots/TC-FR06-MOB-BVA-04-cart.jpg`](../screenshots/TC-FR06-MOB-BVA-04-cart.jpg), [`../screenshots/TC-FR06-MOB-BVA-05-feedback.jpg`](../screenshots/TC-FR06-MOB-BVA-05-feedback.jpg), [`../screenshots/TC-FR06-MOB-BVA-05-cart.jpg`](../screenshots/TC-FR06-MOB-BVA-05-cart.jpg), [`../screenshots/TC-FR06-MOB-BVA-06-feedback.jpg`](../screenshots/TC-FR06-MOB-BVA-06-feedback.jpg), [`../screenshots/TC-FR06-MOB-BVA-06-cart.jpg`](../screenshots/TC-FR06-MOB-BVA-06-cart.jpg), [`../screenshots/TC-FR06-MOB-BVA-07-feedback.jpg`](../screenshots/TC-FR06-MOB-BVA-07-feedback.jpg), [`../screenshots/TC-FR06-MOB-BVA-07-cart.jpg`](../screenshots/TC-FR06-MOB-BVA-07-cart.jpg).
- **GitHub Issue:** Not created.
- **Verification:** Confirmed by runtime screenshot. The resulting MacBook quantity 1 after `-1` and AirPods Pro 2 quantity 1 after empty input are visible; exact before/after quantity deltas are not claimed.


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
- BVA-02 confirmation: on a fresh account, two wrong-password requests moved `login_attempts` from 0 to 4; the following requests returned HTTP 403.
- **Tần suất tái hiện:** 1 lần đã quan sát; nguồn mã xác nhận phép tăng 2.
- **Bằng chứng:** `../screenshots/TC-FR02-DT-04.png`; bộ đếm được xác nhận bằng truy vấn SQLite chỉ đọc.
- **GitHub Issue:** Chưa tạo.
- **Trạng thái xác minh:** Đã xác nhận qua thực thi và đối chiếu mã nguồn.
## BUG-FR02-03 - Login API returns the password in plaintext

- Feature/version: FR-02 Web login; local EShop SUT.
- Environment: Windows, Chrome, frontend localhost:5173, backend localhost:3000.
- Severity: High; credentials are included in a response that may be retained in DevTools, logs, or monitoring tools.
- Preconditions: A test account exists and the user can log in.
- Steps: Open DevTools Network, log in, and inspect the response of `POST /api/login`.
- Expected: The response returns a JWT and necessary user fields, without the password.
- Actual: The JSON response includes `user.password` in plaintext.
- Reproduction: Observed in the TC-FR02-DT-06 response; backend returns the full user object.
- Evidence: `../screenshots/TC-FR02-DT-06-login-response.png` (JWT and password redacted).
- GitHub Issue: Not created.
- Verification: Confirmed from response and source.


## BUG-FR02-04 — Thời gian khóa cấu hình 180 giây thay vì 30 giây

- **Tính năng/phiên bản:** FR-02 — đăng nhập Web; EShop SUT chạy local.
- **Môi trường:** Windows, Chrome, frontend `localhost:5173`, backend `localhost:3000`, SQLite.
- **Mức độ:** Trung bình — người dùng hợp lệ bị ngăn đăng nhập lâu hơn thời gian FR-02 quy định.
- **Tiền điều kiện:** Tài khoản thử nghiệm mới; có thể tái tạo trạng thái khóa bằng các lần nhập sai.
- **Bước tái hiện:** Tạo trạng thái khóa; thử đăng nhập với thông tin đúng ở khoảng 30 giây sau thời điểm khóa bắt đầu.
- **Kết quả mong đợi:** Sau 30 giây tài khoản được mở khóa và thông tin đúng được chấp nhận (FR-02).
- **Kết quả thực tế:** TC-FR02-BVA-05 nhận HTTP 403 ở khoảng 30 giây. Đối chiếu `backend/server.js` cho thấy `locked_until = new Date(Date.now() + 180000)`, tương ứng 180 giây.
- **Tần suất tái hiện:** Quan sát trong TC-BVA-05; cấu hình 180000 ms xác nhận từ mã nguồn.
- **Bằng chứng:** [`../screenshots/TC-FR02-BVA-05.png`](../screenshots/TC-FR02-BVA-05.png); source `backend/server.js`, dòng thiết lập `+ 180000`.
- **GitHub Issue:** Chưa tạo.
- **Trạng thái xác minh:** Xác nhận bằng kết quả thực thi và đối chiếu source. Mốc UI được đo xấp xỉ, không phải benchmark thời gian chính xác.
## Mẫu bug

### BUG-[ID] — [Tiêu đề ngắn]
- Tính năng/phiên bản:
- Môi trường:
- Mức độ nghiêm trọng:
- Tiền điều kiện:
- Bước tái hiện:
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





## BUG-FR08-01 - Checkout total can be edited directly

- Feature: FR-08 Checkout (Web).
- Severity: Medium.
- Preconditions: Signed-in test account with cart total E=58,000,000 VND; Checkout page open.
- Steps: Focus the displayed total field and replace its value with 57,999,970.
- Expected: The total is calculated from cart contents and cannot be directly edited (TC-FR08-DT-03 expected behavior).
- Actual: The field accepted the new value and the displayed payment total changed to 57,999,970 VND. No order was submitted in this test.
- Evidence: [`../screenshots/TC-FR08-DT-03-editable-total.png`](../screenshots/TC-FR08-DT-03-editable-total.png).
- Limitation: Direct editability is confirmed; server-side handling is separately tracked as BUG-FR08-02.
- GitHub Issue: Not created.

## BUG-FR08-02 - Backend accepts a client-supplied checkout total

- Feature: FR-08 Checkout (Web).
- Severity: High - order totals can be altered by a client before submission.
- Preconditions: Signed-in account with cart total E=58,000,000 VND.
- Steps: Submit checkout with total_amount=E-1 or E+1; inspect authenticated order history.
- Expected: Backend recalculates and stores the cart total E=58,000,000 VND.
- Actual: DT-04 and BVA-01 stored E-1=57,999,999 VND (orders #1 and #3); BVA-03 stored E+1=58,000,001 VND (order #5). The Network screenshots show HTTP 200; order history confirms persisted amounts. BVA-02 positive control stored E correctly as order #4.
- Evidence: [`../screenshots/TC-FR08-DT-04-checkout-response.png`](../screenshots/TC-FR08-DT-04-checkout-response.png), [`../screenshots/TC-FR08-DT-04-order-history.png`](../screenshots/TC-FR08-DT-04-order-history.png), [`../screenshots/TC-FR08-BVA-01-checkout-response.png`](../screenshots/TC-FR08-BVA-01-checkout-response.png), [`../screenshots/TC-FR08-BVA-01-order-history.png`](../screenshots/TC-FR08-BVA-01-order-history.png), [`../screenshots/TC-FR08-BVA-02-order-history.png`](../screenshots/TC-FR08-BVA-02-order-history.png), [`../screenshots/TC-FR08-BVA-03-checkout-response.png`](../screenshots/TC-FR08-BVA-03-checkout-response.png), [`../screenshots/TC-FR08-BVA-03-order-history.png`](../screenshots/TC-FR08-BVA-03-order-history.png).
- Limitation: Request payload details are not legible in supplied Network screenshots; order history verifies the persisted totals.
- GitHub Issue: Not created.

## BUG-FR08-03 - Cart remains populated after successful checkout

- Feature: FR-08 Checkout (Web).
- Severity: Medium - the unchanged cart can lead to accidental duplicate checkout.
- Preconditions: Signed-in account with iPhone 15 Pro Max x1 and Samsung Galaxy S24 Ultra x1 in cart.
- Steps: Complete checkout successfully, then return to and inspect the cart.
- Expected: Cart is cleared after successful checkout (TC-FR08-DT-05 expected behavior).
- Actual: Both items remained and the subtotal was still 58,000,000 VND after the success flow. No second order was submitted for DT-05.
- Evidence: [`../screenshots/TC-FR08-DT-05-cart-not-cleared.png`](../screenshots/TC-FR08-DT-05-cart-not-cleared.png), [`../screenshots/TC-FR08-DT-04-checkout-response.png`](../screenshots/TC-FR08-DT-04-checkout-response.png).
- GitHub Issue: Not created.
