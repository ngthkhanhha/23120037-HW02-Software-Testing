# Các mục sinh viên cần tự hoàn tất

Tệp này chỉ liệt kê việc cần tài khoản, xác nhận cá nhân/nhóm hoặc thao tác thật mà Codex không thể xác nhận thay sinh viên. Các test đã ghi trong CSV không bị sửa trong lần rà soát hồ sơ này.

## Trước khi chốt FR-02 và FR-06

- [ ] Xác nhận với giảng viên/nhóm cách chọn Pool D. Đề ghi FR-06 trong Pool A và Pool D là Mobile App; README hiện ghép FR-06 Mobile vào D nhưng chưa có xác nhận phân công. Cập nhật `README.md` và `reports/Main_Report.md` theo câu trả lời thực tế.
- [ ] Create GitHub Issues for the 9 confirmed bugs in the shared group repository only; attach evidence and add each issue URL to `bug-reports/bugs.md`. Do not file unverified observations as bugs.
- [ ] Đọc và xác nhận các phần AI Audit ghi “sinh viên cần xác nhận”; điền nội dung rà soát cá nhân, quyết định chấp nhận/chỉnh sửa, và bổ sung nguyên văn prompt còn thiếu từ lịch sử nếu cần.
- [ ] Đọc và tự chỉnh AI Critique để phản ánh đánh giá/cách diễn đạt của bạn; bản hiện tại là bản nháp do AI hỗ trợ soạn (227 từ theo bộ đếm tách từ của tài liệu).
- [ ] Bổ sung/đính chính thông tin môi trường chỉ bạn xác nhận được: tên/số nhóm, Chrome version, backend/version/URL, admin frontend nếu dùng, cách reset/seed DB và tài khoản thử nghiệm (không ghi mật khẩu thật), iOS version, ngày kiểm thử cho FR-02.
- [ ] Quyết định có chạy lại TC-FR02-BVA-01 và BVA-06 hay giữ Not Executed. Nếu chạy, dùng trạng thái/tài khoản thử nghiệm cô lập, lưu bằng chứng mới và cập nhật CSV cùng báo cáo nhất quán.
- [ ] Cân nhắc chạy các test ứng viên nêu trong AI gap analysis nếu nằm trong phạm vi bài; nếu không chạy, giữ rõ trạng thái là đề xuất/chưa thực thi.

## FR-08 - Completed execution
- [ ] If required by the rubric, independently verify no order was created for TC-FR08-DT-01; this evidence was not captured.
- [x] TC-FR08-DT-01 through DT-05 and BVA-01 through BVA-03 are executed; see `reports/FR08_Domain.md` and `reports/FR08_BVA.md`.
- [x] Demo orders #1 through #5 and their totals are documented. Do not rerun these cases without preparing a fresh baseline.

## FR-14 - Manual execution in progress
- [ ] Run TC-FR14-DT-03 through DT-05 and TC-FR14-BVA-01 through BVA-03 in the admin web app; record actual result, status, and evidence in the CSV and per-feature reports after each case.
- [ ] Use a unique disposable category name for create/update probes; capture before/after state and remove only categories created for testing. Do not delete seeded categories.
- [ ] For DT-04, use the documented PUT API only if you can safely obtain/use an admin session; redact tokens from screenshots. The SRS/UI discrepancy is already documented.
- [ ] Treat whitespace-only rejection as exploratory until its expected behavior is confirmed. Do not file it as a bug based on assumption alone.
- [ ] After execution, update FR14 reports, confirmed bug records, evidence links, AI Audit, and aggregate counts together.
## Phần bài tập còn lại

- [x] All FR-08 Domain and BVA cases have execution results. Only independent Network/order-history confirmation for DT-01 remains open if required.
- [ ] Commit the assignment deliverables (reports, CSV, evidence, bug report and AI audit) to your personal course repository; add that repository URL to README.md and reports/Main_Report.md. Keep the shared group repository limited to GitHub Issues.

## Trước khi nộp

- [ ] Điền bảng tự đánh giá và tổng điểm trong `README.md` theo đánh giá của bạn.
- [ ] Thêm link video demo hoặc ghi rõ không có; kiểm tra rubric xem Agent Skill/video áp dụng ra sao.
- [ ] Xuất PDF cho báo cáo chính, AI Audit và AI Critique sau khi nội dung được chốt.
