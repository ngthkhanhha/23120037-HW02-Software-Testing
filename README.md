# HW02 — AI Domain Testing

## Thông tin bài làm

- Sinh viên: Nguyễn Thanh Khánh Hà
- MSSV: 23120037
- Nhóm: [Tên/số nhóm]
- SUT: [EShop SUT](https://github.com/ttbhanh/eshop-sut)
- Personal assignment repository: [Add your personal repo URL here]
- Shared group repository (GitHub Issues only): [Add the group repo URL here]
- Thời gian kiểm thử: 2026-10-14 (ngày hiển thị trên các ảnh chạy FR-06)

## Tính năng đã chọn

| Pool | Tính năng | Nền tảng |
|---|---|---|
| A | FR-02 — Đăng nhập và khóa tài khoản | Web |
| B | FR-08 — Thanh toán | Web |
| C | FR-14 — Quản lý danh mục | Web Admin |
| D (cần xác nhận) | FR-06 — Xem chi tiết sản phẩm | Mobile |

> **Cần sinh viên xác nhận:** Đề xếp FR-06 trong Pool A và mô tả Pool D là Mobile App. FR-06 Mobile hiện được ghi là phương án ghép với Pool D, chưa có xác nhận của giảng viên/nhóm rằng cách ghép này hợp lệ. Không coi điều kiện “một tính năng mỗi pool” đã được xác nhận cho đến khi điền kết quả xác minh.

## Báo cáo chính và báo cáo kỹ thuật

- **Báo cáo chính:** [`reports/Main_Report.md`](reports/Main_Report.md). Đây là báo cáo tổng hợp, liên kết tới phân tích và ghi nhận thực thi của từng tính năng.
- **Domain Testing:** [`FR02_Domain.md`](reports/FR02_Domain.md), [`FR08_Domain.md`](reports/FR08_Domain.md), [`FR14_Domain.md`](reports/FR14_Domain.md), [`FR06_Mobile_Domain.md`](reports/FR06_Mobile_Domain.md).
- **Boundary Value Analysis:** [`FR02_BVA.md`](reports/FR02_BVA.md), [`FR08_BVA.md`](reports/FR08_BVA.md), [`FR14_BVA.md`](reports/FR14_BVA.md), [`FR06_Mobile_BVA.md`](reports/FR06_Mobile_BVA.md).
- **Test cases và kết quả:** [`test-cases/test-cases.csv`](test-cases/test-cases.csv).
- **Bug report:** [`bug-reports/bugs.md`](bug-reports/bugs.md); ảnh/chứng cứ lưu trong `screenshots/`.
- **AI Audit Report:** [`ai-audit/AI_Audit.md`](ai-audit/AI_Audit.md).
- **AI Critique:** [`ai-audit/AI_Critique.md`](ai-audit/AI_Critique.md). Bài cuối phải dài 200–300 từ.
- **Git commit log:** [`git-log.txt`](git-log.txt), exported from real commits in the personal assignment repository.
- **Việc cần sinh viên hoàn tất:** [`MANUAL_ACTIONS.md`](MANUAL_ACTIONS.md) — xác nhận phân pool, tạo GitHub Issues, xác nhận nhật ký AI, hoàn thiện các phần cá nhân và đóng gói.
- Agent Skill/video demo: [sinh viên bổ sung liên kết nếu có; kiểm tra rubric để xác nhận phần này áp dụng cho bài nộp].

## Tổng kết kiểm thử

| Chỉ số | Số lượng |
|---|---:|
| Tính năng trong phạm vi | 4 |
| Test case đã thiết kế | 36 |
| Test case đã thực thi | 29 |
| Passed | 13 |
| Failed | 16 |
| Not Executed | 7 |
| Bug đã xác nhận | 9 |
| Video demo | [Sinh viên bổ sung liên kết hoặc ghi rõ không có] |

## Tự đánh giá

| STT | Tiêu chí | Điểm tối đa | Tự đánh giá |
|---|---|---:|---:|
| 1 | Feature A (Domain + Boundary) | 25 | [ ] |
| 2 | Feature B (Domain + Boundary) | 25 | [ ] |
| 11 | Feature C (Domain + Boundary) | 25 | [ ] |
| 4 | Feature D Mobile (Domain + Boundary) | 15 | [ ] |
| 5 | Agent Skills | 11 | [ ] |
| | **Tổng** | **100** | **[ ]** |

> Counts reconcile with the CSV: 20 FR-02/FR-06 cases designed; 8 FR-08 cases designed, with all 8 executed (3 Passed, 5 Failed); 8 FR-14 cases designed, with DT-01 through DT-03 Passed and 5 awaiting execution. Overall: 36 designed, 29 executed, 13 Passed, 16 Failed, 7 Not Executed. Evidence for FR-08 DT-01 through DT-05, BVA-01 through BVA-03, and FR14-DT-01 through DT-03 is saved under `screenshots/`. FR-08 DT-01 Network/order-history confirmation remains unavailable; DT-04 and BVA-01 screenshots show HTTP 200 and orders #1 and #3 saved with the submitted E-1 amount; request payload details are not legible. BVA-02 order #4 stored the expected 58,000,000 VND; BVA-03 order #5 was stored at 58,000,001 VND (E+1), reproducing BUG-FR08-02. Before packaging, complete remaining FR-14 cases, confirm pool allocation, fill in group details and self-assessment, add video if required, export the main report/AI Audit/AI Critique as PDFs, and create the required ZIP.







