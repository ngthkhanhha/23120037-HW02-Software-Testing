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
| D (Mobile) | FR-06 | Xem chi tiết sản phẩm | Mobile |

> Phân công FR-06 vào phần Mobile của Pool D đã được giảng viên cho phép.

## Báo cáo chính và báo cáo kỹ thuật

- **Báo cáo chính:** [`reports/Main_Report.md`](reports/Main_Report.md), tổng hợp và liên kết phân tích cùng kết quả thực thi của từng tính năng.
- **Phân tích miền:** [`FR02_Domain.md`](reports/FR02_Domain.md), [`FR08_Domain.md`](reports/FR08_Domain.md), [`FR14_Domain.md`](reports/FR14_Domain.md), [`FR06_Mobile_Domain.md`](reports/FR06_Mobile_Domain.md).
- **Phân tích giá trị biên:** [`FR02_BVA.md`](reports/FR02_BVA.md), [`FR08_BVA.md`](reports/FR08_BVA.md), [`FR14_BVA.md`](reports/FR14_BVA.md), [`FR06_Mobile_BVA.md`](reports/FR06_Mobile_BVA.md).
- **Test case và kết quả:** [`test-cases/test-cases.csv`](test-cases/test-cases.csv).
- **Báo cáo lỗi:** [`bug-reports/bugs.md`](bug-reports/bugs.md); ảnh/bằng chứng lưu trong `screenshots/`.
- **Báo cáo kiểm tra AI:** [`ai-audit/AI_Audit.md`](ai-audit/AI_Audit.md).
- **Nhận xét AI:** [`ai-audit/AI_Critique.md`](ai-audit/AI_Critique.md). Bài cuối phải dài 200–300 từ.
- **Nhật ký commit Git:** [`git-log.txt`](git-log.txt), xuất từ commit thực tế trong repo cá nhân.
- **Việc cần sinh viên hoàn tất:** [`MANUAL_ACTIONS.md`](MANUAL_ACTIONS.md) — rà soát AI Audit, tự đánh giá, xuất PDF và đóng gói.
- **Agent Skill:** [`agent-skills/domain-bva-testing/SKILL.md`](agent-skills/domain-bva-testing/SKILL.md).

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
| Video demo | [Demo Agent Skill: FR-14 bằng Domain Testing và BVA](https://youtu.be/SBlovoWtv_A) |

## Tự đánh giá

| STT | Tiêu chí | Điểm tối đa | Tự đánh giá |
|---|---|---:|---:|
| 1 | Tính năng A (Domain + Boundary) | 25 | Ổn |
| 2 | Tính năng B (Domain + Boundary) | 25 | Ổn |
| 3 | Tính năng C (Domain + Boundary) | 25 | Ổn |
| 4 | Tính năng D Mobile (Domain + Boundary) | 15 | Ổn |
| 5 | Agent Skill | 10 | Ổn |
| | **Tổng** | **100** | **Ổn** |

> Số liệu khớp với CSV: FR-02/FR-06 có tổng 20 ca; FR-08 có 8 ca (3 Passed, 5 Failed); FR-14 có 8 ca (4 Passed, 2 Failed, 1 Inconclusive, 1 Not Executed). Tổng cộng: 36 ca thiết kế, 33 đã chạy, 14 Passed, 18 Failed, 3 Not Executed, 1 Inconclusive. Đã tạo 11 GitHub Issues cho bug đã xác nhận và liên kết trong `bug-reports/bugs.md`. Trước khi nộp, hoàn tất tự đánh giá, xuất PDF, tạo `git-log.txt` sau commit cuối và đóng gói ZIP.
