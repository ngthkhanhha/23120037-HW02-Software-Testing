# FR-02 — Boundary Value Analysis

## Các biên theo yêu cầu
- Ngưỡng đăng nhập sai: khóa khi có từ 3 lần sai liên tiếp.
- Thời gian khóa: 30 giây.
- Email: kiểm tra định dạng HTML5; SRS không chỉ định biên độ dài email.

## Thiết kế và kết quả

| TC | Biên / giá trị | Kết quả mong đợi | Kết quả thực tế | Trạng thái |
|---|---|---|---|---|
| TC-FR02-BVA-01 | 2 lần sai (ngay dưới ngưỡng 3) | Chưa khóa; đăng nhập đúng sau đó thành công | Bỏ qua vì tài khoản seeded đã có bộ đếm 2 sau DT-04; không thực hiện thêm lần sai để tránh kích hoạt khóa | Not Executed |
| TC-FR02-BVA-02 | 3 lần sai (tại ngưỡng) | Khóa tài khoản; thông tin đúng bị chặn trong 30 giây | Hai request sai được xử lý (401) và bộ đếm tăng 0→4; request sai thứ ba và request đúng kế tiếp trả 403. Khóa xuất hiện trước lần sai thứ ba | Failed |
| TC-FR02-BVA-04 | 29 giây (ngay trước hết hạn) | Còn khóa; thông tin đúng bị từ chối | Đăng nhập đúng bị từ chối HTTP 403 ở khoảng 29 giây | Passed |
| TC-FR02-BVA-05 | 30 giây (biên hết hạn) | Hết khóa; thông tin đúng được chấp nhận | Đăng nhập đúng vẫn bị từ chối HTTP 403 ở khoảng 30 giây | Failed |
| TC-FR02-BVA-06 | 31 giây (ngay sau hết hạn) | Hết khóa; thông tin đúng được chấp nhận | Không thực hiện theo quyết định của sinh viên; không có actual result | Not Executed |

## Phân tích

TC-BVA-02 không đạt ngưỡng đúng như yêu cầu do bộ đếm tăng hai lần cho một request sai. TC-BVA-05 cho thấy khóa còn hiệu lực ở khoảng 30 giây. Đối chiếu `backend/server.js` cho thấy code đặt `locked_until` bằng `Date.now() + 180000`, tức 180 giây; đây là căn cứ bổ sung cho BUG-FR02-04. TC-BVA-06 không được chạy, vì vậy báo cáo không kết luận trạng thái tại 31 giây dựa trên thực nghiệm.

Các mốc 29/30 giây được đo thủ công và có sai số thao tác. Kết quả gần biên cần được đọc cùng thời điểm gửi request và cấu hình trong source; không dùng một ảnh Network đơn lẻ để khẳng định độ chính xác mili giây.

## Bằng chứng
- TC-FR02-BVA-02: [`../screenshots/TC-FR02-BVA-02.png`](../screenshots/TC-FR02-BVA-02.png)
- TC-FR02-BVA-04: [`../screenshots/TC-FR02-BVA-04.png`](../screenshots/TC-FR02-BVA-04.png)
- TC-FR02-BVA-05: [`../screenshots/TC-FR02-BVA-05.png`](../screenshots/TC-FR02-BVA-05.png)

Chi tiết preconditions, input, steps và trạng thái đầy đủ trong [`../test-cases/test-cases.csv`](../test-cases/test-cases.csv).
