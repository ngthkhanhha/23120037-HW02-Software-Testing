# HW02 — Kiểm thử miền và phân tích giá trị biên

## 1. Thông tin chung

- **Môn học:** Kiểm thử phần mềm
- **Bài tập:** HW02 — Kiểm thử miền trên EShop
- **MSSV:** 23120037
- **Sinh viên:** Nguyễn Thanh Khánh Hà
- **Hệ thống được kiểm thử (SUT):** EShop
- **Repo mã nguồn SUT:** [ttbhanh/eshop-sut](https://github.com/ttbhanh/eshop-sut)
- **Repo cá nhân nộp bài:** [23120037-HW02-Software-Testing](https://github.com/ngthkhanhha/23120037-HW02-Software-Testing)
- **Repo nhóm (chỉ dùng tạo GitHub Issues):** [TNhanTis/eshop-sut-Group06](https://github.com/TNhanTis/eshop-sut-Group06)
- **Bản SUT cục bộ đã dùng:** `C:\KTPM\HW02-EShop` (sao chép để tránh ký tự `#` trong đường dẫn ban đầu)
- **Thời gian kiểm thử:** 2026-10-14 (ngày hiển thị trên ảnh thực thi được cung cấp)

## 2. Lựa chọn tính năng

| Pool | Mã tính năng | Tính năng được kiểm thử | Nền tảng | Trạng thái phân công |
|---|---|---|---|---|
| A | FR-02 | Đăng nhập và khóa tài khoản | Web | Đã chọn |
| B | FR-08 | Thanh toán | Web | Đã chọn |
| C | FR-14 | Quản lý danh mục | Web Admin | Đã chọn |
| D (Mobile) | FR-06 | Xem chi tiết sản phẩm | Mobile (React Native / Expo) | Đã được giảng viên cho phép phân vào phần Mobile của bài (theo xác nhận của sinh viên) |

> **Ghi chú phạm vi FR-14:** SRS hiện nêu admin có thể thêm, xem và xóa danh mục; tên danh mục là bắt buộc và không được để trống. Yêu cầu chưa mô tả rõ thao tác cập nhật. Đối chiếu giao diện/API và chỉ báo cáo thao tác có căn cứ trong yêu cầu hoặc hành vi ứng dụng đã quan sát. Không mặc định tính năng có đầy đủ CRUD chỉ dựa vào tên gọi.

## 3. Môi trường kiểm thử và dữ liệu

| Hạng mục | Giá trị |
|---|---|
| Hệ điều hành | Windows 11; phiên bản/build không ghi nhận |
| Trình duyệt và phiên bản | Google Chrome 155.0.8059.84 |
| Thiết bị/giả lập di động và hệ điều hành | iPhone 12 Pro Max, iOS 27.0.1, Expo Go SDK 57 |
| Backend/API | `http://localhost:3000`; phiên bản/commit không ghi nhận |
| Frontend Web | Vite — `http://localhost:5173/` |
| Frontend Admin | `http://localhost:5174/`; phiên bản không ghi nhận |
| Ứng dụng di động | Expo Go SDK 57 trên iPhone; máy chủ phát triển/API được truy cập qua LAN |
| Cơ sở dữ liệu và dữ liệu seed | Cách reset/seed và thông tin tài khoản thử không ghi nhận |
| Ngày kiểm thử | 2026-10-14 đối với bằng chứng thực thi FR-06 được cung cấp |

Ghi thông tin môi trường trước khi chạy test. Nếu thiết lập thay đổi, ghi lại thay đổi đó và các test bị ảnh hưởng.

## 4. Phương pháp thiết kế và báo cáo kiểm thử

Với mỗi tính năng, ghi phân tích trước khi thực thi:

1. Dẫn các yêu cầu SRS liên quan và yêu cầu API/giao diện đi kèm nếu có.
2. Liệt kê đầu vào, tiền điều kiện và kết quả có thể quan sát.
3. Phân hoạch đầu vào/trạng thái thành các lớp tương đương hợp lệ và không hợp lệ. Giải thích cơ sở phân lớp và nêu hành vi chưa kiểm tra hoặc chưa rõ.
4. Xác định các biên số, độ dài, thời gian hoặc chuyển trạng thái được nêu rõ. Khi phù hợp, chọn giá trị tại biên, ngay dưới và ngay trên biên.
5. Không tự đặt giới hạn. Ghi hành vi chưa quy định thành câu hỏi hoặc giả định và đối chiếu SRS, lược đồ/API hoặc xác nhận từ giảng viên.
6. Khai báo test case có ID duy nhất, tiền điều kiện, dữ liệu, bước chạy, kết quả mong đợi và nguồn yêu cầu trong [`../test-cases/test-cases.csv`](../test-cases/test-cases.csv).
7. Chạy test và ghi kết quả thực tế, trạng thái, bằng chứng. Không gán Passed/Failed trước khi thực thi.
8. So sánh test do AI đề xuất với bộ test đã rà soát. Chỉ ghi thiếu sót/sửa đổi thực tế cùng lý do; không tự tạo nhận định AI bỏ sót.
9. Chỉ báo cáo sai lệch tái hiện được so với yêu cầu là bug. Liên kết từng bug tới GitHub Issue và ảnh bằng chứng.

Các báo cáo phân tích từng tính năng được liên kết bên dưới. Chi tiết test case và kết quả thực thi được lưu trong CSV để tránh tạo các bản ghi trùng lặp, mâu thuẫn.

## 5. Tính năng A — FR-02: Đăng nhập và khóa tài khoản (Web)

- **Nguồn yêu cầu:** SRS FR-02; các yêu cầu bảo mật/xác thực liên quan nếu áp dụng.
- **Phân tích miền:** [FR02_Domain.md](FR02_Domain.md)
- **Phân tích giá trị biên:** [FR02_BVA.md](FR02_BVA.md)
- **ID test case:** TC-FR02-DT-01, TC-FR02-DT-02, TC-FR02-DT-03, TC-FR02-DT-04, TC-FR02-DT-06, TC-FR02-BVA-01, TC-FR02-BVA-02, TC-FR02-BVA-04, TC-FR02-BVA-05, TC-FR02-BVA-06.
- **Tóm tắt thực thi hiện tại:** 8 ca đã chạy; 4 Passed, 4 Failed. Hai ca chưa chạy: TC-FR02-BVA-01 được bỏ qua vì bộ đếm tài khoản seed đã là 2; TC-FR02-BVA-06 chưa được thực thi.
- **Bug đã xác nhận:** BUG-FR02-01 (email sai định dạng không bị HTML5 chặn); BUG-FR02-02 (bộ đếm đăng nhập sai tăng 2); BUG-FR02-03 (API đăng nhập trả password dạng rõ); BUG-FR02-04 (thời gian khóa là 180 giây thay vì 30). GitHub Issues: chưa tạo.
- **Bằng chứng:** [`../screenshots/TC-FR02-DT-01.png`](../screenshots/TC-FR02-DT-01.png); DT-02: [`../screenshots/TC-FR02-DT-02.png`](../screenshots/TC-FR02-DT-02.png); DT-03: [`../screenshots/TC-FR02-DT-03.png`](../screenshots/TC-FR02-DT-03.png); DT-04: [`../screenshots/TC-FR02-DT-04.png`](../screenshots/TC-FR02-DT-04.png). DT-06: [`../screenshots/TC-FR02-DT-06-login-response.png`](../screenshots/TC-FR02-DT-06-login-response.png), [`../screenshots/TC-FR02-DT-06-bearer-header.png`](../screenshots/TC-FR02-DT-06-bearer-header.png). BVA-02: [`../screenshots/TC-FR02-BVA-02.png`](../screenshots/TC-FR02-BVA-02.png); BVA-04: [`../screenshots/TC-FR02-BVA-04.png`](../screenshots/TC-FR02-BVA-04.png); BVA-05: [`../screenshots/TC-FR02-BVA-05.png`](../screenshots/TC-FR02-BVA-05.png).
- **Phân tích khoảng trống do AI đề xuất:** Các khoảng trống và ca ứng viên được ghi trong [FR02_Domain.md](FR02_Domain.md). Hồ sơ lưu trữ không có bộ test ứng viên ban đầu riêng do AI tạo, nên đây là rà soát độ bao phủ hiện tại chứ không khẳng định AI đã bỏ sót một ca cụ thể. BVA-01/BVA-06 chưa chạy và không được tính vào tổng.

## 6. Tính năng B — FR-08: Thanh toán (Web)

- **Nguồn yêu cầu:** SRS FR-08; các yêu cầu xác thực, mã giảm giá, giỏ hàng và đơn hàng chỉ được xét khi ảnh hưởng đến thanh toán.
- **Phân tích miền:** [FR08_Domain.md](FR08_Domain.md)
- **Phân tích giá trị biên:** [FR08_BVA.md](FR08_BVA.md)
- **ID test case:** TC-FR08-DT-01 đến TC-FR08-DT-05; TC-FR08-BVA-01 đến TC-FR08-BVA-03.
- **Tóm tắt thực thi:** Đã thiết kế và chạy đủ 8 ca (3 Passed, 5 Failed; không có Not Executed). DT-01 hiển thị cảnh báo yêu cầu đăng nhập và chuyển tới `/login` sau khi đóng cảnh báo. Đã lưu cả hai ảnh người dùng cung cấp cho DT-01 trong `screenshots/`. Ảnh thanh toán của DT-02/DT-03 cũng được lưu tại đó. DT-03 Failed vì sửa được trường tổng tiền; DT-04 Failed vì lịch sử đơn lưu `E-1` từ client (57.999.999 VND) thay vì `E` (58.000.000 VND). Bằng chứng DT-04 cho thấy HTTP 200 và đơn #1; payload/orderId không đọc rõ. Sau trang báo thành công, DT-05 cho thấy cả hai mặt hàng vẫn còn trong giỏ. BVA-01 tái hiện độc lập lỗi giá trị `E-1`: đơn #3 lưu 57.999.999 VND; BVA-02 Passed: đơn #4 lưu `E=58.000.000` VND; BVA-03 Failed: đơn #5 lưu `E+1=58.000.001` VND, cũng tái hiện việc tin tổng tiền client gửi.
- **Phân tích khoảng trống do AI đề xuất:** Rà soát thiết kế được ghi trong [FR08_Domain.md](FR08_Domain.md). Mã giảm giá thuộc FR-09 nên không đưa vào. Hành vi giỏ rỗng và lỗi request còn bỏ ngỏ vì FR-08 chưa quy định kết quả mong đợi.
- **Bug đã xác nhận:** BUG-FR08-01 (có thể sửa trực tiếp tổng thanh toán); BUG-FR08-02 (backend lưu tổng E-1 do client gửi); BUG-FR08-03 (giỏ vẫn còn sản phẩm sau thanh toán thành công).
- **Bằng chứng:** Ảnh DT-01 đến DT-05 và BVA-01 đến BVA-03 nằm trong [`../screenshots/`](../screenshots/); đường dẫn từng ảnh được liệt kê trong CSV và báo cáo từng tính năng.
- **Ghi chú rà soát mã nguồn (không phải kết quả test):** TC-FR08-DT-03 xác nhận trường tổng tiền cho phép chỉnh sửa và giao diện cập nhật theo giá trị mới (BUG-FR08-01). DT-04 xác nhận backend lưu giá trị `E-1` đã sửa; DT-05 xác nhận giỏ vẫn còn mặt hàng sau khi thanh toán thành công.

## 7. Tính năng C — FR-14: Quản lý danh mục (Web Admin)

- **Nguồn yêu cầu:** SRS FR-14; FR-12 cho kiểm soát truy cập admin nếu liên quan.
- **Phân tích miền:** [FR14_Domain.md](FR14_Domain.md)
- **Phân tích giá trị biên:** [FR14_BVA.md](FR14_BVA.md)
- **Thiết kế test case:** 8 ca (5 Domain và 3 BVA). Kết quả thực thi được tóm tắt dưới đây.
- **Làm rõ phạm vi:** SRS FR-14 nêu Thêm/Xem/Xóa; đặc tả API cũng ghi PUT trong khi giao diện admin không có điều khiển sửa. Vì vậy DT-04 kiểm tra hợp đồng API đã công bố và ghi nhận chỗ chưa thống nhất về phạm vi, không xem đó là yêu cầu giao diện. Giả định từ chối tên chỉ có khoảng trắng chưa phải yêu cầu đã xác nhận.
- **Tóm tắt thực thi:** Đã chạy 7/8 ca: DT-01, DT-02, DT-03 và BVA-03 Passed; DT-05 và BVA-01 Failed; BVA-02 Inconclusive vì FR-14 không quy định đầu vào chỉ có khoảng trắng. DT-04 được người dùng yêu cầu bỏ qua và vẫn ở trạng thái Not Executed. Tất cả ca BVA FR-14 theo kế hoạch đã chạy. Bằng chứng ở [`../screenshots/`](../screenshots/) và được liên kết trong CSV cùng các báo cáo tính năng. Đã xác nhận BUG-FR14-01 và BUG-FR14-02.
- **Phân tích khoảng trống do AI đề xuất:** Thiết kế bao phủ thao tác trong SRS, ranh giới vai trò SEC-03 liên quan, API PUT đã công bố và biên tên được chỉ định. Hành vi tên trùng và xóa danh mục đang được sản phẩm tham chiếu chưa được quy định; giữ ở dạng thăm dò.
- **Bug đã xác nhận:** BUG-FR14-01 (người dùng thường có thể tạo danh mục do SEC-03 không được áp dụng ở POST `/api/categories`) và BUG-FR14-02 (gửi tên rỗng tạo danh mục không tên được lưu).
- **Bằng chứng:** Ảnh DT-01 đến DT-03, DT-05, BVA-01 đến BVA-03 nằm trong [`../screenshots/`](../screenshots/); CSV liệt kê từng đường dẫn.

## 8. Tính năng D — FR-06 Mobile: Xem chi tiết sản phẩm

- **Nguồn yêu cầu:** SRS FR-06 và FR-20; làm rõ đặc thù di động từ giảng viên nếu có.
- **Phân tích miền:** [FR06_Mobile_Domain.md](FR06_Mobile_Domain.md)
- **Phân tích giá trị biên:** [FR06_Mobile_BVA.md](FR06_Mobile_BVA.md)
- **ID test case:** TC-FR06-MOB-DT-01 đến TC-FR06-MOB-DT-03, TC-FR06-MOB-BVA-01 đến TC-FR06-MOB-BVA-07.
- **Thiết lập thực thi di động:** iPhone dùng Expo Go SDK 57, chạy `C:\KTPM\HW02-EShop\frontend-mobile-sdk57`; API cấu hình theo địa chỉ LAN của laptop. Thêm sản phẩm vào giỏ thành công và xem được giỏ xác nhận backend có thể truy cập. Thiết bị do sinh viên xác nhận: iPhone 12 Pro Max, iOS 27.0.1.
- **Tóm tắt thực thi:** TC-FR06-MOB-DT-01 và DT-02 đã chạy, cả hai Failed vì không hiển thị danh mục sản phẩm. DT-03 Passed. BVA-01 Failed vì số lượng 0 vẫn hiện thông báo thành công; BVA-04 Failed vì số lượng -1 vẫn được báo thành công và xuất hiện trong giỏ với số lượng 1; BVA-02 Passed tại số lượng 1; BVA-03 Passed tại số lượng 2; BVA-05 Failed vì đầu vào thập phân `1,5` vẫn được báo thành công; BVA-06 Failed vì `abc` vẫn được báo thành công; BVA-07 Failed vì để trống số lượng vẫn có phản hồi thành công và giỏ xuất hiện dòng AirPods Pro 2 số lượng 1. Đã chạy cả 10 ca FR-06: 3 Passed, 7 Failed, không có Not Executed.
- **Phân tích khoảng trống do AI đề xuất:** Các khoảng trống và ca ứng viên nằm trong [FR06_Mobile_Domain.md](FR06_Mobile_Domain.md). Không lưu riêng bộ ứng viên AI ban đầu, vì vậy không khẳng định có thiếu sót cụ thể của AI. Kiểm tra thêm trường hợp thêm trùng sản phẩm và dấu thập phân dạng chấm chưa chạy; sản phẩm không tồn tại chưa được quy định nên chỉ là thăm dò. Không tính các đề xuất vào tổng hiện tại.
- **Bug đã xác nhận:** BUG-FR06-01 (thiếu danh mục) và BUG-FR06-02 (chấp nhận số lượng không hợp lệ gồm rỗng, -1, 0, `1,5`, `abc` rồi phản hồi thêm thành công).
- **Bằng chứng:** [`../screenshots/TC-FR06-MOB-DT-01.jpg`](../screenshots/TC-FR06-MOB-DT-01.jpg), [`../screenshots/TC-FR06-MOB-DT-02.jpg`](../screenshots/TC-FR06-MOB-DT-02.jpg), [`../screenshots/TC-FR06-MOB-DT-03.jpg`](../screenshots/TC-FR06-MOB-DT-03.jpg), [`../screenshots/TC-FR06-MOB-BVA-01.jpg`](../screenshots/TC-FR06-MOB-BVA-01.jpg), [`../screenshots/TC-FR06-MOB-BVA-02-feedback.jpg`](../screenshots/TC-FR06-MOB-BVA-02-feedback.jpg), [`../screenshots/TC-FR06-MOB-BVA-02-cart.jpg`](../screenshots/TC-FR06-MOB-BVA-02-cart.jpg), [`../screenshots/TC-FR06-MOB-BVA-03-feedback.jpg`](../screenshots/TC-FR06-MOB-BVA-03-feedback.jpg), [`../screenshots/TC-FR06-MOB-BVA-03-cart.jpg`](../screenshots/TC-FR06-MOB-BVA-03-cart.jpg), [`../screenshots/TC-FR06-MOB-BVA-04-feedback.jpg`](../screenshots/TC-FR06-MOB-BVA-04-feedback.jpg), [`../screenshots/TC-FR06-MOB-BVA-04-cart.jpg`](../screenshots/TC-FR06-MOB-BVA-04-cart.jpg), [`../screenshots/TC-FR06-MOB-BVA-05-feedback.jpg`](../screenshots/TC-FR06-MOB-BVA-05-feedback.jpg), [`../screenshots/TC-FR06-MOB-BVA-05-cart.jpg`](../screenshots/TC-FR06-MOB-BVA-05-cart.jpg), [`../screenshots/TC-FR06-MOB-BVA-06-feedback.jpg`](../screenshots/TC-FR06-MOB-BVA-06-feedback.jpg), [`../screenshots/TC-FR06-MOB-BVA-06-cart.jpg`](../screenshots/TC-FR06-MOB-BVA-06-cart.jpg), [`../screenshots/TC-FR06-MOB-BVA-07-feedback.jpg`](../screenshots/TC-FR06-MOB-BVA-07-feedback.jpg), [`../screenshots/TC-FR06-MOB-BVA-07-cart.jpg`](../screenshots/TC-FR06-MOB-BVA-07-cart.jpg).

## 9. Báo cáo tổng hợp kiểm thử

Tổng hợp từ kết quả đã ghi; mỗi ca có một trạng thái và tổng số liệu đã được đối soát.

| Chỉ số | Số lượng |
|---|---:|
| Tính năng trong phạm vi | 4 |
| Test case đã thiết kế | 36 |
| Test case đã thực thi | 33 |
| Passed | 14 |
| Failed | 18 |
| Not Executed | 3 |
| Inconclusive | 1 |
| Bug đã xác nhận | 11 |

**Đối soát:** 36 ca thiết kế = 14 Passed + 18 Failed + 3 Not Executed + 1 Inconclusive. Tổng khớp. FR-14 có 8 ca: 4 Passed, 2 Failed (DT-05 và BVA-01), BVA-02 Inconclusive vì hành vi chỉ có khoảng trắng chưa được quy định, DT-04 Not Executed do người dùng yêu cầu bỏ qua.

## 10. Việc sử dụng AI và tài liệu hỗ trợ

- **Báo cáo kiểm tra AI:** [`../ai-audit/AI_Audit.md`](../ai-audit/AI_Audit.md) — ghi công cụ, ngày/giờ, prompt đầy đủ, phản hồi và phần rà soát của sinh viên cho mỗi lần tương tác.
- **Nhận xét AI:** [`../ai-audit/AI_Critique.md`](../ai-audit/AI_Critique.md) — bản cuối cần 200–300 từ và gắn với quá trình kiểm thử này.
- **Báo cáo lỗi và bằng chứng:** [`../bug-reports/bugs.md`](../bug-reports/bugs.md); ảnh nằm trong [`../screenshots/`](../screenshots/).
- **Nhật ký commit Git:** [`../git-log.txt`](../git-log.txt) — xuất từ commit thật của repo cá nhân; không tạo lịch sử giả.
- **Agent Skill:** [`domain-bva-testing/SKILL.md`](../agent-skills/domain-bva-testing/SKILL.md). Liên kết video demo YouTube: cần quay và bổ sung nếu rubric yêu cầu.

## 11. Tài liệu tham khảo

- Không sử dụng tài liệu tham khảo bên ngoài. Căn cứ trực tiếp của bài là đề HW02 và tài liệu yêu cầu/API của [repo EShop SUT](https://github.com/ttbhanh/eshop-sut), đã liên kết ở phần thông tin chung.
