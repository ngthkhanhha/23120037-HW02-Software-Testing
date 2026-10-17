# Các mục sinh viên cần tự hoàn tất

Tệp này liệt kê các việc cần tài khoản, xác nhận cá nhân/nhóm hoặc thao tác thực tế mà Codex không thể xác nhận thay sinh viên.

## Trước khi chốt FR-02 và FR-06

- [ ] Xác nhận với giảng viên/nhóm cách chọn Pool D. Đề ghi FR-06 trong Pool A và Pool D là Mobile App; README đang ghép FR-06 Mobile vào Pool D nhưng chưa có xác nhận phân công. Cập nhật `README.md` và `reports/Main_Report.md` theo câu trả lời thực tế.
- [ ] Tạo GitHub Issues cho 11 bug đã xác nhận trong repo nhóm; đính kèm bằng chứng và thêm URL issue vào `bug-reports/bugs.md`. Không tạo issue cho quan sát chưa xác minh.
- [ ] Đọc và xác nhận các mục AI Audit được đánh dấu “sinh viên cần xác nhận”; điền phần rà soát cá nhân, quyết định chấp nhận/chỉnh sửa, và bổ sung nguyên văn prompt còn thiếu từ lịch sử nếu cần.
- [ ] Đọc và tự chỉnh AI Critique để phản ánh đánh giá/cách diễn đạt của bạn; bản hiện tại là bản nháp do AI hỗ trợ soạn (255 từ theo bộ đếm tách từ của tài liệu).
- [ ] Bổ sung/đính chính thông tin môi trường chỉ bạn mới xác nhận được: tên/số nhóm, phiên bản Chrome, phiên bản/URL backend, frontend admin nếu có dùng, cách reset/seed DB và tài khoản thử (không ghi mật khẩu thật), phiên bản iOS, ngày kiểm thử FR-02.
- [ ] Quyết định chạy lại TC-FR02-BVA-01 và BVA-06 hay giữ trạng thái Not Executed. Nếu chạy, dùng trạng thái/tài khoản thử nghiệm cô lập, lưu bằng chứng mới và cập nhật CSV cùng báo cáo cho nhất quán.
- [ ] Cân nhắc chạy các test ứng viên trong phân tích khoảng trống AI nếu thuộc phạm vi bài; nếu không chạy, ghi rõ là đề xuất/chưa thực thi.

## FR-08 — Đã hoàn tất thực thi

- [ ] Nếu rubric yêu cầu, tự xác minh rằng TC-FR08-DT-01 không tạo đơn hàng; bằng chứng này chưa được lưu.
- [x] TC-FR08-DT-01 đến DT-05 và BVA-01 đến BVA-03 đã chạy; xem `reports/FR08_Domain.md` và `reports/FR08_BVA.md`.
- [x] Đơn thử #1 đến #5 và tổng tiền tương ứng đã được ghi lại. Không chạy lại các ca này nếu chưa chuẩn bị baseline mới.

## FR-14 — Đã thực thi thủ công (DT-04 chủ động bỏ qua)

- [x] TC-FR14-DT-05 đã chạy và Failed: POST `/api/categories` từ người dùng thường trả HTTP 200; SEC-03 không được thực thi. Đã ghi BUG-FR14-01. Admin đã xóa danh mục thăm dò. Bằng chứng: `screenshots/TC-FR14-DT-05.png`.
- [x] TC-FR14-BVA-01 đã chạy và Failed: gửi tên rỗng tạo danh mục #4 không tên (BUG-FR14-02); đã lưu bằng chứng và xóa dữ liệu thử.
- [x] Đã ghi nhận yêu cầu bỏ qua TC-FR14-DT-04; ca vẫn là Not Executed. TC-FR14-BVA-02 là Inconclusive: ứng dụng lưu đúng ba dấu cách nhưng hành vi khoảng trắng chưa được quy định. TC-FR14-BVA-03 Passed với tên một ký tự `A`; tất cả ca BVA FR-14 đã chạy.
- [ ] Với kiểm tra tạo/cập nhật, dùng tên danh mục thử nghiệm duy nhất; chụp trạng thái trước/sau và chỉ xóa danh mục do test tạo. Không xóa danh mục seed.
- [ ] Với DT-04, chỉ dùng API PUT đã được tài liệu hóa nếu có thể dùng an toàn phiên admin; che token khỏi ảnh. Điểm khác biệt giữa SRS và giao diện đã được ghi nhận.
- [ ] Xem việc từ chối tên chỉ có khoảng trắng là kiểm thử thăm dò cho đến khi xác nhận kết quả mong đợi. Không báo bug chỉ dựa trên giả định.
- [x] Sau mỗi ca đã chạy, đã cập nhật báo cáo FR14, danh sách bug xác nhận, liên kết bằng chứng, AI Audit và tổng số liệu đồng bộ.

## Phần bài tập còn lại

- [x] Tất cả ca Domain và BVA FR-08 đã có kết quả thực thi. Chỉ còn việc xác minh độc lập qua Network/lịch sử đơn rằng DT-01 không tạo đơn nếu rubric yêu cầu.
- [x] Đã commit tài liệu bài làm (báo cáo, CSV, bằng chứng, báo cáo lỗi và AI Audit) vào repo cá nhân; liên kết repo cá nhân đã ghi trong README và báo cáo chính. Repo nhóm chỉ dùng tạo GitHub Issues.

## Trước khi nộp

- [ ] Điền bảng tự đánh giá và tổng điểm trong `README.md` theo đánh giá của bạn.
- [x] Agent Skill đã được tạo tại `agent-skills/domain-bva-testing/SKILL.md`.
- [ ] Quay video demo và bổ sung liên kết nếu rubric yêu cầu; Skill đã có trong repo.
- [ ] Xuất PDF cho báo cáo chính, AI Audit và AI Critique sau khi nội dung được chốt.
