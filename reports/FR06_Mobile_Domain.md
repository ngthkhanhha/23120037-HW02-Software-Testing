# Mobile — FR-06 Xem chi tiết sản phẩm — Domain Testing

## Thông tin

- **Nền tảng:** iPhone, ứng dụng React Native / Expo Go SDK 57
- **Yêu cầu nguồn:** EShop SRS, FR-06 (hiển thị ảnh, tên, giá, mô tả, danh mục; số lượng nguyên dương tối thiểu 1; thêm giỏ hàng có phản hồi trực quan)
- **Trạng thái:** Hoàn tất 10/10 ca FR-06 trên iPhone. Domain Testing: 1 Passed, 2 Failed; BVA: 2 Passed, 5 Failed. Tổng FR-06: 3 Passed, 7 Failed, 0 Not Executed. Các lỗi đã xác nhận được tổng hợp trong BUG-FR06-01 và BUG-FR06-02.

## Phân hoạch miền

| Thuộc tính / trạng thái | Miền tương đương | Mong đợi theo FR-06 |
|---|---|---|
| Sản phẩm | ID tồn tại và có dữ liệu | Màn hình chi tiết hiển thị ảnh, tên, giá, mô tả và danh mục |
| Sản phẩm | Không tồn tại / lỗi tải dữ liệu | Hành vi lỗi cần đối chiếu yêu cầu/API; chưa đưa ra tiêu chí pass/fail khi SRS chưa quy định |
| Số lượng | Số nguyên dương | Chấp nhận |
| Số lượng | 0, số âm, số thập phân, chữ hoặc rỗng | Không hợp lệ theo yêu cầu số nguyên dương tối thiểu 1 |
| Thêm giỏ | Thao tác thành công | Có phản hồi trực quan và giỏ phản ánh sản phẩm/số lượng đã chọn |

## Test case Domain

| ID | Trường hợp | Mong đợi | Kết quả / trạng thái |
|---|---|---|---|
| TC-FR06-MOB-DT-01 | Mở chi tiết sản phẩm có sẵn | Hiển thị ảnh, tên, giá, mô tả, danh mục và ô số lượng | **Failed** — ảnh hiển thị đủ ảnh/tên/giá/mô tả/số lượng; danh mục không xuất hiện. Bằng chứng: [`../screenshots/TC-FR06-MOB-DT-01.jpg`](../screenshots/TC-FR06-MOB-DT-01.jpg). Đã xác nhận dữ liệu seed của iPhone có `category_id=1`; mã màn hình không render danh mục. |
| TC-FR06-MOB-DT-02 | Mở MacBook Pro M3 thuộc danh mục khác | Hiển thị đúng ảnh, tên, giá, mô tả, danh mục Laptop và số lượng mặc định 1 | **Failed** — ảnh, tên, giá, mô tả và số lượng 1 hiển thị đúng; danh mục Laptop không xuất hiện. Bằng chứng: [`../screenshots/TC-FR06-MOB-DT-02.jpg`](../screenshots/TC-FR06-MOB-DT-02.jpg). Tái hiện BUG-FR06-01. |
| TC-FR06-MOB-DT-03 | Thêm sản phẩm có sẵn vào giỏ với số lượng hợp lệ 1 | Có phản hồi trực quan; giỏ phản ánh đúng sản phẩm và số lượng 1 | **Passed** — sau khi thêm Samsung Galaxy S24 Ultra, giỏ hiển thị iPhone và Samsung, mỗi món số lượng 1; tổng 58.000.000 đ, badge `Giỏ (2)` (trạng thái trước có iPhone và `Giỏ (1)`). Bằng chứng: [`../screenshots/TC-FR06-MOB-DT-03.jpg`](../screenshots/TC-FR06-MOB-DT-03.jpg). |

## Tổng kết thực thi FR-06

- **Domain Testing:** 3 ca đã chạy; TC-DT-03 Passed, TC-DT-01 và TC-DT-02 Failed do thiếu danh mục.
- **Boundary Value Analysis:** 7 ca đã chạy; BVA-02 và BVA-03 Passed; BVA-01, BVA-04, BVA-05, BVA-06 và BVA-07 Failed vì dữ liệu số lượng không hợp lệ vẫn được báo thêm thành công.
- **Tổng:** 10 ca đã chạy; 3 Passed, 7 Failed, 0 Not Executed. Chi tiết từng lần chạy và đường dẫn ảnh nằm trong CSV và báo cáo BVA.

## Cách áp dụng Domain Testing

1. Tách chức năng thành hai phần quan sát được: dữ liệu chi tiết của sản phẩm và hành động thêm sản phẩm vào giỏ.
2. Với dữ liệu chi tiết, phân lớp sản phẩm có sẵn theo danh mục khác nhau; so sánh các trường ảnh, tên, giá, mô tả, danh mục và số lượng mặc định. Chọn iPhone và MacBook để kiểm tra hai giá trị danh mục đã seed.
3. Với số lượng, phân miền theo đặc tả: số nguyên dương hợp lệ và các lớp không hợp lệ (0, âm, thập phân, chữ, rỗng). Chọn ca đại diện ở Domain/BVA, không tự đặt cận trên vì yêu cầu không quy định.
4. Với thao tác thêm giỏ, kiểm tra phản hồi trên màn hình và xác nhận sản phẩm/số lượng trong giỏ. So sánh baseline khi có; nếu thiếu baseline thì chỉ ghi trạng thái nhìn thấy, không suy luận lượng thay đổi.

## AI gap analysis (rà soát bổ sung)

Giới hạn: không tìm thấy một bộ ứng viên kiểm thử ban đầu do AI tạo riêng trong hồ sơ để so sánh từng mục. Đây là rà soát khoảng trống bao phủ hiện tại; không khẳng định các mục dưới đây chắc chắn đã bị AI bỏ sót.

Các miền cốt lõi đã được đưa vào bộ hiện tại: hai sản phẩm thuộc hai danh mục cho kiểm tra nội dung (DT-01/02), thêm hàng hợp lệ (DT-03), giá trị cận 0/1/2 và các lớp âm, thập phân, chữ, rỗng (BVA-01…07). Bộ hiện tại đã phát hiện thiếu nhãn danh mục (BUG-FR06-01) và phản hồi thành công với đầu vào số lượng không hợp lệ (BUG-FR06-02); đây là các lỗi đã được phát hiện, không phải khoảng trống.

Rà soát bổ sung nêu các kiểm tra ứng viên sau, chưa chạy và không được cộng vào thống kê hiện tại:

- **Thêm cùng một sản phẩm nhiều lần:** xác minh số lượng trong giỏ có cộng dồn đúng theo số lượng yêu cầu hay không. TC-DT-03 thêm một sản phẩm khác với sản phẩm đã có, nên chưa kiểm tra hành vi cộng dồn cùng mã sản phẩm.
- **Định dạng thập phân theo locale khác:** BVA-05 dùng dấu phẩy `1,5` trên iPhone; cân nhắc kiểm tra thêm `1.5` nếu bàn phím/locale cho phép để xác định cả hai cách nhập đều bị từ chối. Yêu cầu chỉ cho phép số nguyên dương.
- **Lỗi tải sản phẩm hoặc ID không tồn tại:** chưa có ca kiểm tra trạng thái lỗi. FR-06 được cung cấp không quy định cụ thể giao diện lỗi/empty state, nên cần ghi là câu hỏi yêu cầu hoặc kiểm tra thăm dò, không chấm Pass/Fail theo tiêu chí tự đặt.
- **Số lượng hợp lệ rất lớn:** không đề xuất một giá trị “max” vì yêu cầu không nêu giới hạn tối đa; chỉ thêm khi SRS/API/giảng viên xác định giới hạn.

Đề xuất trên là kết quả rà soát AI hậu kiểm dựa trên SRS, CSV và bằng chứng hiện có; chưa phải kết quả chạy test và chưa được xác nhận thành lỗi.

## Nguồn và ghi chú

- Bản yêu cầu: `C:\KTPM\HW02-EShop\README.md`, mục FR-06.
- Mã UI được đối chiếu: `C:\KTPM\HW02-EShop\frontend-mobile\App.js` (màn hình chi tiết không render category).
- Dữ liệu seed được đối chiếu: `C:\KTPM\HW02-EShop\backend\database.js` (iPhone 15 Pro Max gắn `category_id=1`; category ID 1 được seed).
- Chi tiết tiền điều kiện, input, bước chạy và kết quả được quản lý tại [`../test-cases/test-cases.csv`](../test-cases/test-cases.csv).
- Không thiết lập biên tối đa vì FR-06 không nêu giới hạn tối đa.
