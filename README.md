# HW02 — Kiểm thử miền bằng AI

## Thông tin bài làm

- Sinh viên: Nguyễn Thanh Khánh Hà
- MSSV: 23120037
- Nhóm: [Nhóm 06]
- SUT: [EShop SUT](https://github.com/ttbhanh/eshop-sut)
- Repo cá nhân nộp bài: [23120037-HW02-Software-Testing](https://github.com/ngthkhanhha/23120037-HW02-Software-Testing)
- Repo nhóm (chỉ dùng tạo GitHub Issues): https://github.com/TNhanTis/eshop-sut-Group06.git
- Thời gian kiểm thử: 2026-10-14 

## Tính năng đã chọn

| Pool | Mã tính năng | Tính năng | Nền tảng |
|---|---|---|---|
| A | FR-02 | Đăng nhập và khóa tài khoản | Web |
| B | FR-08 | Thanh toán | Web |
| C | FR-14 | Quản lý danh mục | Web Admin |
| D (cần xác nhận) | FR-06 | Xem chi tiết sản phẩm | Mobile |

> **Cần sinh viên xác nhận:** Đề xếp FR-06 trong Pool A và mô tả Pool D là Mobile App. FR-06 Mobile hiện được ghi là phương án ghép với Pool D, chưa có xác nhận của giảng viên/nhóm rằng cách ghép này hợp lệ. Chưa thể coi điều kiện “một tính năng mỗi pool” đã được xác nhận cho đến khi ghi kết quả xác minh.

## Báo cáo chính và báo cáo kỹ thuật

- **Báo cáo chính:** [`reports/Main_Report.md`](reports/Main_Report.md), tổng hợp và liên kết phân tích cùng kết quả thực thi của từng tính năng.
- **Phân tích miền:** [`FR02_Domain.md`](reports/FR02_Domain.md), [`FR08_Domain.md`](reports/FR08_Domain.md), [`FR14_Domain.md`](reports/FR14_Domain.md), [`FR06_Mobile_Domain.md`](reports/FR06_Mobile_Domain.md).
- **Phân tích giá trị biên:** [`FR02_BVA.md`](reports/FR02_BVA.md), [`FR08_BVA.md`](reports/FR08_BVA.md), [`FR14_BVA.md`](reports/FR14_BVA.md), [`FR06_Mobile_BVA.md`](reports/FR06_Mobile_BVA.md).
- **Test case và kết quả:** [`test-cases/test-cases.csv`](test-cases/test-cases.csv).
- **Báo cáo lỗi:** [`bug-reports/bugs.md`](bug-reports/bugs.md); ảnh/bằng chứng lưu trong `screenshots/`.
- **Báo cáo kiểm tra AI:** [`ai-audit/AI_Audit.md`](ai-audit/AI_Audit.md).
- **Nhận xét AI:** [`ai-audit/AI_Critique.md`](ai-audit/AI_Critique.md). Bài cuối phải dài 200–300 từ.
- **Nhật ký commit Git:** [`git-log.txt`](git-log.txt), xuất từ commit thực tế trong repo cá nhân.
- **Việc cần sinh viên hoàn tất:** [`MANUAL_ACTIONS.md`](MANUAL_ACTIONS.md) — xác nhận phân pool, tạo GitHub Issues, rà soát nhật ký AI, hoàn thiện thông tin cá nhân và đóng gói.
- **Agent Skill:** [`agent-skills/domain-bva-testing/SKILL.md`](agent-skills/domain-bva-testing/SKILL.md). Video demo YouTube: cần quay và bổ sung liên kết nếu rubric yêu cầu.

## Tổng kết kiểm thử

| Chỉ số | Số lượng |
|---|---:|
| Tính năng trong phạm vi | 4 |
| Test case đã thiết kế | 36 |
| Test case đã thực thi | 33 |
| Passed | 14 |
| Failed | 18 |
| Chưa thực thi (Not Executed) | 3 |
| Chưa kết luận (Inconclusive) | 1 |
| Bug đã xác nhận | 11 |
| Video demo | [Sinh viên bổ sung liên kết hoặc ghi rõ không có] |

## Tự đánh giá

| STT | Tiêu chí | Điểm tối đa | Tự đánh giá |
|---|---|---:|---:|
| 1 | Tính năng A (Domain + Boundary) | 25 | [ ] |
| 2 | Tính năng B (Domain + Boundary) | 25 | [ ] |
| 3 | Tính năng C (Domain + Boundary) | 25 | [ ] |
| 4 | Tính năng D Mobile (Domain + Boundary) | 15 | [ ] |
| 5 | Agent Skill | 10 | [ ] |
| | **Tổng** | **100** | **[ ]** |

> Số liệu khớp với CSV: FR-02/FR-06 có tổng 20 ca; FR-08 có 8 ca, cả 8 đã chạy (3 Passed, 5 Failed); FR-14 có 8 ca, trong đó DT-01 đến DT-03 Passed, DT-05 và BVA-01 Failed, BVA-02 Inconclusive, BVA-03 Passed, DT-04 được bỏ qua. Tổng cộng: 36 ca thiết kế, 33 đã chạy, 14 Passed, 18 Failed, 3 Not Executed, 1 Inconclusive. Bằng chứng cho FR-08 DT-01 đến DT-05, BVA-01 đến BVA-03 và FR-14 DT-01 đến DT-03, DT-05, BVA-01 đến BVA-03 nằm trong `screenshots/`. BUG-FR14-01: POST `/api/categories` từ người dùng thường trả HTTP 200 — SEC-03 không được thực thi. BUG-FR14-02: gửi tên danh mục rỗng tạo danh mục không tên. BVA-02 chấp nhận ba dấu cách; không kết luận bug vì yêu cầu chưa quy định việc cắt khoảng trắng. Các ca Not Executed còn lại: TC-FR02-BVA-01, TC-FR02-BVA-06 và TC-FR14-DT-04 đã được chủ động bỏ qua. Trước khi đóng gói, xác nhận phân pool, bổ sung liên kết repo nhóm, tạo 11 GitHub Issues cho bug đã xác nhận và thêm liên kết issue vào báo cáo lỗi; rà soát AI Audit, chỉnh AI Critique, điền thông tin môi trường/nhóm và tự đánh giá, đưa Agent Skill cùng video demo theo yêu cầu, xuất PDF cần thiết và nhật ký commit Git cuối, sau đó tạo ZIP.
