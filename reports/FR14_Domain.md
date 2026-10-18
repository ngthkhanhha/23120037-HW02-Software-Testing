# FR-14 — Phân tích miền (Quản lý danh mục)

## Thông tin và phạm vi

- Nền tảng: Web Admin.
- Nguồn SRS: `eshop-sut-main/README.md`, FR-14.
- Nguồn yêu cầu bảo mật liên quan: cùng README, SEC-03 (các thao tác thay đổi dữ liệu cần token có vai trò admin).
- Nguồn hợp đồng API: `eshop-sut-main/api_specification.md`, mục 3.4.
- Trạng thái thực thi: đã thiết kế 5 ca Domain và 3 ca BVA; TC-FR14-DT-01 đến DT-03 và BVA-03 Passed; DT-05 và BVA-01 Failed; BVA-02 Inconclusive; người dùng yêu cầu bỏ qua DT-04.
- Phạm vi chính theo SRS: thêm, xem và xóa danh mục; tên danh mục là bắt buộc và không được để trống.

## Ghi chú yêu cầu và phạm vi

README của SUT gọi tính năng là “Category CRUD” nhưng nội dung FR-14 chỉ liệt kê Thêm/Xem/Xóa. Đặc tả API có ghi `PUT /api/categories/:id`, trong khi giao diện admin hiện không có chức năng sửa danh mục. Vì vậy, TC-FR14-DT-04 kiểm tra hợp đồng API đã công bố và ghi nhận điểm chưa thống nhất về phạm vi; không xem đây là yêu cầu giao diện được FR-14 nêu rõ. Kiểm tra bảo mật admin dựa trên SEC-03.

Không có giới hạn độ dài tối đa/tối thiểu cho tên danh mục. Giả định “chỉ có khoảng trắng thì được xem là trống” cần được xác nhận, chưa phải yêu cầu đã chứng minh. Hành vi với tên trùng và xóa danh mục đang được sản phẩm tham chiếu cũng chưa được quy định; các nội dung này chỉ nên xem là kiểm thử thăm dò.

## Các lớp tương đương

| Thuộc tính | Phân lớp | Kỳ vọng / căn cứ |
|---|---|---|
| Vai trò người dùng | Admin có token hợp lệ | Được xem và quản lý danh mục (FR-14 / SEC-03). |
| Vai trò người dùng | Người dùng đã xác thực nhưng không phải admin | Bị từ chối khi thay đổi danh mục (SEC-03). |
| Tên danh mục | Giá trị không rỗng, duy nhất | Tạo thành công. |
| Tên danh mục | Chuỗi rỗng | Từ chối; FR-14 quy định tên là bắt buộc và không được trống. |
| Tên danh mục | Chỉ có khoảng trắng | Thăm dò; kỳ vọng bị từ chối nếu “trống” có nghĩa là không có ký tự khác khoảng trắng. |
| Thao tác | Xem, tạo, xóa | Kiểm tra trạng thái lưu/danh sách và bảo đảm danh mục không liên quan không bị đổi. |
| Thao tác | Cập nhật qua API | Hợp đồng API có PUT; điểm khác biệt giữa API, giao diện và SRS đã ghi ở trên. |

## Test case

Tiền điều kiện, bước chạy, kết quả mong đợi, trạng thái thực thi và đường dẫn bằng chứng được ghi trong [`../test-cases/test-cases.csv`](../test-cases/test-cases.csv), với ID TC-FR14-DT-01 đến DT-05 và TC-FR14-BVA-01 đến BVA-03. TC-FR14-DT-01 Passed: trang danh mục admin tải được và hiển thị mỗi danh mục ID #1 Điện thoại, #2 Laptop, #3 Phụ kiện đúng một lần. Bằng chứng: [`../screenshots/TC-FR14-DT-01.png`](../screenshots/TC-FR14-DT-01.png). TC-FR14-DT-02 Passed: danh mục duy nhất `FR14-Test-NTHH-01` xuất hiện với ID #4 và vẫn thấy trong danh sách sau khi làm mới. Bằng chứng: [`../screenshots/TC-FR14-DT-02.png`](../screenshots/TC-FR14-DT-02.png). TC-FR14-DT-03 Passed: xóa `FR14-Test-NTHH-01` đã xóa mục thử nghiệm đó trong khi ba danh mục seed vẫn còn. Bằng chứng: [`../screenshots/TC-FR14-DT-03.png`](../screenshots/TC-FR14-DT-03.png). TC-FR14-DT-04 được bỏ qua theo yêu cầu của người dùng và vẫn là Not Executed; không gửi request API và không kết luận bug. TC-FR14-DT-05 Failed: POST `/api/categories` với JWT của người dùng thường (`test@eshop.com`) trả HTTP 200 và tạo danh mục #4 `DT05-Probe-NTHH`; backend không thực thi giới hạn chỉ admin được thao tác theo SEC-03. Admin đã xóa dữ liệu thử sau khi chụp bằng chứng. Bằng chứng: [`../screenshots/TC-FR14-DT-05.png`](../screenshots/TC-FR14-DT-05.png). Ghi nhận BUG-FR14-01. Không xóa danh mục seed. Chụp trạng thái trước/sau và không để lộ JWT.

TC-FR14-BVA-01 Failed: gửi biểu mẫu tên danh mục rỗng đã tạo danh mục #4 không có tên, được xác nhận trong danh sách/API. Danh mục do test tạo đã được xóa sau khi lưu bằng chứng; danh mục seed #1–#3 vẫn còn. Bằng chứng: [`../screenshots/TC-FR14-BVA-01.png`](../screenshots/TC-FR14-BVA-01.png). Đã ghi BUG-FR14-02.

TC-FR14-BVA-02 được chạy với đúng ba dấu cách. Ứng dụng chấp nhận đầu vào và lưu ba dấu cách (danh mục #5); mục thử nghiệm được xóa sau khi chụp bằng chứng, chỉ còn các mục seed #1–#3. Do FR-14 không quy định việc cắt khoảng trắng, kết quả là Inconclusive và không được ghi nhận là vi phạm yêu cầu. Bằng chứng: [`../screenshots/TC-FR14-BVA-02.png`](../screenshots/TC-FR14-BVA-02.png). Trạng thái thực thi FR-14 hiện tại: 7/8 ca đã chạy (4 Passed, 2 Failed, 1 Inconclusive); DT-04 được bỏ qua và vẫn là Not Executed.

TC-FR14-BVA-03 Passed: tên một ký tự `A` được chấp nhận và lưu thành danh mục #6. Mục thử nghiệm được xóa sau khi chụp bằng chứng; danh mục seed #1–#3 vẫn còn. Bằng chứng: [`../screenshots/TC-FR14-BVA-03.png`](../screenshots/TC-FR14-BVA-03.png). Như vậy đã hoàn tất các ca BVA FR-14 theo kế hoạch.
