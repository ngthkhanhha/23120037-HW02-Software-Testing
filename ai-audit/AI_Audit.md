# AI Audit Report

## Khai báo
I use AI tools for the following tasks.

## Nhật ký tương tác

### AI-INT-001 — Lập khung hồ sơ HW02
- Công cụ AI: ChatGPT (Codex)
- Ngày, giờ: 2026-10-14 13:45 (Asia/Saigon; thời điểm tạo bộ khung)
- Prompt người dùng: “tạo các file đó” — yêu cầu tạo các file theo cấu trúc HW02 vừa nêu.
- Đầu ra AI: Tạo khung README, báo cáo Domain/BVA cho FR-02, FR-08, FR-14, Mobile FR-06, CSV test case mẫu, mẫu bug report, AI Audit, AI Critique và git-log placeholder. Các nội dung được đánh dấu dự thảo/chưa chạy; không khẳng định kết quả kiểm thử hoặc bug.
- Rà soát của sinh viên: [Ghi nội dung đã kiểm tra, chỉnh sửa và quyết định chấp nhận/từ chối.]
- Tệp chịu ảnh hưởng: [Liệt kê các tệp đã sử dụng/chỉnh sửa.]

## Trạng thái rà soát nhật ký

Các phiên AI được dùng để ghi nhận test đã được liệt kê bên dưới. Nhật ký vẫn cần sinh viên xác nhận các trường rà soát được đánh dấu chờ; AI không tự nhận phần kiểm tra của sinh viên. Các nội dung chờ được tổng hợp ở [MANUAL_ACTIONS.md](../MANUAL_ACTIONS.md).

### AI-INT-002 — Cập nhật hồ sơ liên quan đến TC-FR02-DT-01
- Công cụ AI: ChatGPT (Codex)
- Ngày, giờ: 2026-10-14 15:46 (Asia/Saigon)
- Prompt người dùng: “điền tương ứng với các file khác có liên quan đến TC-FR02-DT-01”
- Đầu ra AI: Cập nhật kết quả TC-FR02-DT-01 là Passed cho xác nhận đăng nhập giao diện; ghi JWT/header Bearer là ca riêng chưa chạy; cập nhật FR02 Domain report, Main Report, README summary, bugs.md observation pending và mục AI Audit.
- Rà soát của sinh viên: [Xác nhận nội dung và đường dẫn bằng chứng; điều chỉnh nếu cần.]
- Tệp chịu ảnh hưởng: `reports/FR02_Domain.md`, `reports/Main_Report.md`, `README.md`, `bug-reports/bugs.md`, `ai-audit/AI_Audit.md`.

### AI-INT-003 — Ghi nhận TC-FR02-DT-02
- Công cụ AI: ChatGPT (Codex)
- Ngày, giờ: 2026-10-14 15:50 (Asia/Saigon)
- Prompt người dùng: “tiếp tục điền tương ứng với TC2” kèm ảnh trang đăng nhập có email `ha@` và DevTools Console báo HTTP 401 Unauthorized tại `/api/login`.
- Đầu ra AI: Ghi TC-FR02-DT-02 là Failed; cập nhật kết quả và bằng chứng dự kiến trong CSV, báo cáo Domain FR-02, Main Report, tổng kết README và bug report BUG-FR02-01. Ảnh đã được lưu tại `screenshots/TC-FR02-DT-02.png`; GitHub Issue chưa tạo.
- Rà soát của sinh viên: [Xác nhận mô tả, lưu ảnh và tạo GitHub Issue theo yêu cầu bài tập.]
- Tệp chịu ảnh hưởng: `test-cases/test-cases.csv`, `reports/FR02_Domain.md`, `reports/Main_Report.md`, `README.md`, `bug-reports/bugs.md`, `ai-audit/AI_Audit.md`.


### AI-INT-004 — Ghi nhận TC-FR02-DT-03
- Công cụ AI: ChatGPT (Codex)
- Ngày, giờ: 2026-10-14 15:56 (Asia/Saigon)
- Prompt người dùng: “đây” kèm ảnh trang đăng nhập sau khi gửi `notfound.hw02@example.com`; giao diện hiện thông báo chung “Đăng nhập thất bại. Vui lòng kiểm tra lại.”
- Đầu ra AI: Ghi TC-FR02-DT-03 là Passed cho tiêu chí không tiết lộ lý do; cập nhật CSV, báo cáo FR-02, Main Report, README và audit log. Ảnh đã được lưu tại `screenshots/TC-FR02-DT-03.png`.
- Rà soát của sinh viên: Đã xác nhận kết quả và lưu ảnh bằng chứng tại `screenshots/TC-FR02-DT-03.png`.
- Tệp chịu ảnh hưởng: `test-cases/test-cases.csv`, `reports/FR02_Domain.md`, `reports/Main_Report.md`, `README.md`, `ai-audit/AI_Audit.md`.

### AI-INT-005 — Ghi nhận TC-FR02-DT-04
- Công cụ AI: ChatGPT (Codex)
- Ngày, giờ: 2026-10-14 (Asia/Saigon)
- Prompt người dùng: “đã xong” kèm ảnh đăng nhập thất bại với `test@eshop.com` và mật khẩu sai `Wrong-Test-2026!`.
- Đầu ra AI: Ghi TC-FR02-DT-04 là Failed. Ảnh cho thấy thông báo lỗi chung; truy vấn SQLite chỉ đọc cho thấy bộ đếm tăng từ 0 lên 2 sau một lần thử sai. Đối chiếu `backend/server.js` xác nhận phép cộng `+2`; ghi nhận BUG-FR02-02 và cập nhật thống kê.
- Rà soát của sinh viên: [Xác nhận nội dung và bằng chứng trước khi nộp.]
- Tệp chịu ảnh hưởng: `test-cases/test-cases.csv`, `reports/FR02_Domain.md`, `reports/Main_Report.md`, `README.md`, `bug-reports/bugs.md`, `ai-audit/AI_Audit.md`.


### AI-INT-006 - TC-FR02-DT-06
- Tool: ChatGPT (Codex); date: 2026-10-14 (Asia/Saigon).
- User asked to record the two matching evidence screenshots in the related files.
- Result: confirmed JWT in `POST /api/login` response and `Authorization: Bearer` on `GET /api/users/me`; marked TC-FR02-DT-06 Passed. Found plaintext `user.password` in login response and recorded BUG-FR02-03. Redacted token and password values in both evidence images before linking them.
- Files updated: test case CSV, FR02 Domain report, Main Report, README, bug report, AI Audit, and two TC-FR02-DT-06 screenshots.


### AI-INT-007 - TC-FR02-BVA-01 skip
- User agreed to skip the two-failure boundary case rather than risk another wrong-password attempt while `login_attempts=2` after TC-FR02-DT-04.
- Recorded as Not Executed with the reason in the CSV and FR02 BVA report. Execution counts remain unchanged.


### AI-INT-008 - TC-FR02-BVA-02
- User supplied a Network screenshot showing four login requests: HTTP 401, 401, 403, 403; the last request used the correct password.
- Recorded TC-FR02-BVA-02 as Failed because lockout occurred before three failed attempts. This corroborates BUG-FR02-02.
- Evidence reference: `screenshots/TC-FR02-BVA-02.png`; the screenshot is present in `screenshots/`; the student confirmed it does not need additional redaction.
- Updated CSV, FR02 BVA/Domain reports, Main Report, README, bug report, and AI Audit.

### AI-INT-009 — TC-FR02-BVA-04 và kiểm tra bằng chứng
- Công cụ: ChatGPT (Codex); ngày: 2026-10-14 (Asia/Saigon).
- Prompt: “đây” kèm ảnh Network của tài khoản BVA-04 sau khi thử đăng nhập bằng mật khẩu đúng khoảng 29 giây sau khi khóa.
- Đầu ra: Ghi TC-FR02-BVA-04 Passed khi request bị HTTP 403; cập nhật CSV, FR02 BVA, Main Report và README; phát hiện ảnh đã có trong thư mục `screenshots/`.
- Rà soát của sinh viên: [Xác nhận thời điểm khoảng 29 giây theo thao tác đã thực hiện; bổ sung nếu timer cho giá trị khác.]
- Tệp chịu ảnh hưởng: `test-cases/test-cases.csv`, `reports/FR02_BVA.md`, `reports/Main_Report.md`, `README.md`.

### AI-INT-010 — TC-FR02-BVA-05 và rà soát toàn bộ FR-02
- Công cụ: ChatGPT (Codex); ngày: 2026-10-14 (Asia/Saigon).
- Prompt: “check” kèm ảnh Network của tài khoản BVA-05 với hai request 401 và request đăng nhập đúng trả 403; tiếp theo yêu cầu “không cần TC cuối đâu, hãy dò lại và điền đầy đủ các TC và các file liên quan của phần FR-02”.
- Đầu ra: Ghi BVA-05 Failed tại khoảng 30 giây; giữ BVA-06 Not Executed theo lựa chọn của sinh viên; rà soát CSV, FR02 Domain/BVA, Main Report, README, bug report, audit và critique. Source `server.js` đặt hạn khóa `+180000`, nên thêm BUG-FR02-04 so với FR-02 quy định 30 giây. Thống kê sau rà soát: 10 thiết kế, 8 chạy, 4 Passed, 4 Failed, 2 Not Executed, 4 bug.
- Rà soát của sinh viên: [Xác nhận phép đo khoảng 30 giây và nội dung các trường hợp chưa chạy.]
- Tệp chịu ảnh hưởng: `test-cases/test-cases.csv`, `reports/FR02_Domain.md`, `reports/FR02_BVA.md`, `reports/Main_Report.md`, `README.md`, `bug-reports/bugs.md`, `ai-audit/AI_Audit.md`, `ai-audit/AI_Critique.md`.

### AI-INT-011 — Hoàn tất thực thi và rà soát hồ sơ FR-06 Mobile
- Công cụ AI: ChatGPT (Codex).
- Ngày, giờ: 2026-10-14 21:00 (Asia/Saigon).
- Prompt người dùng: “vậy là kết thúc FR-06, hãy rà soát lại toàn bộ và điền đầy đủ các file có liên quan”. Trong cùng chuỗi thực thi, sinh viên cung cấp ảnh cho TC-FR06-MOB-BVA-04 (`-1`) và TC-FR06-MOB-BVA-07 (để trống).
- Đầu ra AI: Đối chiếu 10 TC FR-06 giữa CSV, Domain/BVA reports, bug report, README, Main Report và ảnh. Ghi BVA-04 và BVA-07 Failed theo phản hồi thành công và trạng thái giỏ quan sát được; đồng bộ tổng FR-06 thành 3 Passed, 7 Failed, 0 Not Executed và tổng bài thành 18 executed (7 Passed, 11 Failed, 2 Not Executed). Ghi rõ không suy diễn quantity delta khi thiếu baseline, và iOS version chưa được ghi nhận.
- Rà soát: Đối chiếu kết quả và tên ảnh với các ảnh thực thi do sinh viên cung cấp; trạng thái từng TC được đối chiếu lại với CSV, báo cáo và thống kê tổng. Chưa có xác nhận độc lập về iOS version hoặc group-level allocation.
- Tệp chịu ảnh hưởng: `test-cases/test-cases.csv`, `reports/FR06_Mobile_Domain.md`, `reports/FR06_Mobile_BVA.md`, `reports/Main_Report.md`, `README.md`, `bug-reports/bugs.md`, `ai-audit/AI_Audit.md`, và ảnh BVA-04/BVA-07 trong `screenshots/`.

### AI-INT-012 — Hoàn thiện hồ sơ và rà soát AI gap cho FR-02/FR-06
- Công cụ AI: ChatGPT (Codex).
- Ngày, giờ: 2026-10-14 21:09 (Asia/Saigon; phiên rà soát hồ sơ).
- Prompt người dùng: “hoàn thiện giúp tôi những thứ bạn có thể làm, còn phần nào yêu cầu tự tay tôi điền tôi sẽ điền sau”.
- Đầu ra AI: Đọc lại đề và hồ sơ hiện có; bổ sung giải thích cách áp dụng Domain Testing và phần rà soát khoảng trống bao phủ cho FR-02/FR-06; cập nhật Main Report và README để phản ánh các khoảng trống thực thi và yêu cầu xác minh phân pool; soạn bản AI Critique 227 từ để sinh viên tự rà soát; tạo checklist riêng cho các thao tác còn cần sinh viên thực hiện. Không thay đổi kết quả test, không chạy test, không tạo issue/commit giả và không tính đề xuất chưa chạy vào thống kê.
- Rà soát: AI đối chiếu các cập nhật với đề, SRS, CSV và báo cáo. Sinh viên chưa xác nhận nội dung mới; cần kiểm tra các mục trong `MANUAL_ACTIONS.md` trước khi nộp.
- Tệp chịu ảnh hưởng: `reports/FR02_Domain.md`, `reports/FR06_Mobile_Domain.md`, `reports/Main_Report.md`, `README.md`, `ai-audit/AI_Audit.md`, `ai-audit/AI_Critique.md`, `MANUAL_ACTIONS.md`.

### AI-INT-013 — Thiết kế FR-08 Domain Testing và BVA
- Công cụ AI: ChatGPT (Codex).
- Ngày, giờ: 2026-10-16 08:08 (Asia/Saigon).
- Prompt người dùng: “tiến hành làm FR-08”.
- Đầu ra AI: Đối chiếu mục FR-08 trong SRS với Checkout UI/API; xác định FR-09 coupon ở ngoài phạm vi; lập 5 ca Domain và 3 ca BVA quanh quan hệ tổng đúng `E` với giá trị client `E-1`, `E`, `E+1`; thêm bước thực thi và bằng chứng vào CSV. Tất cả được ghi Not Executed. Source review có ghi chú riêng, không kết luận bug khi chưa chạy.
- Rà soát: Đối chiếu yêu cầu với SRS và các tệp `Checkout.jsx`, `Cart.jsx`, `server.js`, `AuthContext.jsx`, `CartContext.jsx`. Không gửi request, không tạo đơn hàng và không chạy test.
- Tệp chịu ảnh hưởng: `reports/FR08_Domain.md`, `reports/FR08_BVA.md`, `reports/Main_Report.md`, `README.md`, `test-cases/test-cases.csv`, `ai-audit/AI_Audit.md`.


### AI-INT-014 - Record execution of TC-FR08-DT-01
- Tool: ChatGPT (Codex).
- Date/time: 2026-10-16 14:12 (Asia/Saigon).
- User prompt: The user supplied the checkout alert screenshot and the resulting `/login` screenshot.
- Output: Marked TC-FR08-DT-01 Passed based on the observed authentication alert and redirect. At that point, the screenshots were referenced in chat but had not yet been copied to the repository. No Network or order-history evidence was available to independently verify that no order was created.
- Review: The pass is limited to the visible authentication gate and redirect.
- Files affected: `test-cases/test-cases.csv`, `reports/FR08_Domain.md`, `reports/Main_Report.md`, `README.md`, `MANUAL_ACTIONS.md`, `ai-audit/AI_Audit.md`.

### AI-INT-015 - Save the two original screenshots for TC-FR08-DT-01
- Tool: ChatGPT (Codex).
- Date/time: 2026-10-16 14:15 (Asia/Saigon).
- User prompt: ?2 anh nay nhe?, with `Screenshot (1343).png` and `Screenshot (1344).png` from `C:\Users\Admin\Pictures\Screenshots`.
- Output: Copied the two original images unchanged to `screenshots/TC-FR08-DT-01-cart-login-alert.png` and `screenshots/TC-FR08-DT-01-login-redirect.png`; updated the evidence paths in CSV and linked/updated the FR-08 Domain report, Main Report, README, and manual checklist. No new screenshots were captured.
- Review: Confirmed both destination files exist and have non-zero size. The first shows the login alert at `/cart`; the second shows `/login`. Independent Network/order-history evidence that no order was created remains unavailable.
- Files affected: both screenshots, `test-cases/test-cases.csv`, `reports/FR08_Domain.md`, `reports/Main_Report.md`, `README.md`, `MANUAL_ACTIONS.md`, `ai-audit/AI_Audit.md`.


### AI-INT-016 - Record execution of TC-FR08-DT-02
- Tool: ChatGPT (Codex).
- Date/time: 2026-10-16 14:19 (Asia/Saigon).
- User prompt: The user supplied a screenshot of the signed-in Checkout page showing iPhone 15 Pro Max x1 at 30,000,000 VND, Samsung Galaxy S24 Ultra x1 at 28,000,000 VND, and total 58,000,000 VND.
- Output: Marked TC-FR08-DT-02 Passed. Copied the original screenshot `C:\Users\Admin\Pictures\Screenshots\Screenshot (1345).png` to `screenshots/TC-FR08-DT-02-checkout-items-total.png`. Updated CSV, FR08 Domain, Main Report, README, manual checklist and aggregate counts. No checkout submission was made. Coupon UI was excluded as FR-09.
- Review: The visible product list, quantities, item amounts and total are consistent with the expected cart values.
- Files affected: `screenshots/TC-FR08-DT-02-checkout-items-total.png`, `test-cases/test-cases.csv`, `reports/FR08_Domain.md`, `reports/Main_Report.md`, `README.md`, `MANUAL_ACTIONS.md`, `ai-audit/AI_Audit.md`.


### AI-INT-017 - Record execution of TC-FR08-DT-03
- Tool: ChatGPT (Codex).
- Date/time: 2026-10-16 14:21 (Asia/Saigon).
- User prompt: The user supplied a screenshot of the Checkout amount field changed to 57999970 and displayed payment total 57,999,970 VND.
- Output: Marked TC-FR08-DT-03 Failed because the total was directly editable and recalculated on screen. Copied the original screenshot `C:\Users\Admin\Pictures\Screenshots\Screenshot (1346).png` to `screenshots/TC-FR08-DT-03-editable-total.png`. Updated CSV, FR08 Domain, Main Report, README, manual checklist and aggregate counts. No checkout confirmation was submitted.
- Review: The screenshot directly shows the edited input and changed displayed amount; no order was created during this case.
- Files affected: `screenshots/TC-FR08-DT-03-editable-total.png`, `test-cases/test-cases.csv`, `reports/FR08_Domain.md`, `reports/Main_Report.md`, `README.md`, `MANUAL_ACTIONS.md`, `ai-audit/AI_Audit.md`.


### AI-INT-018 - Document BUG-FR08-01
- Tool: ChatGPT (Codex).
- Date/time: 2026-10-16 14:21 (Asia/Saigon).
- Prompt: Follow-up to the TC-FR08-DT-03 screenshot showing an edited payment total.
- Output: Added BUG-FR08-01 to the bug report with the observed UI behavior, expected FR-08 behavior, severity, evidence link and a clear limitation that server-side acceptance is still unverified. Updated the Main Report confirmed-bug count and source-review note.
- Review: The bug describes only the UI behavior observed in the screenshot; no claim is made about backend order totals.
- Files affected: `bug-reports/bugs.md`, `reports/Main_Report.md`, `ai-audit/AI_Audit.md`.


### AI-INT-019 - Simplify TC-FR08-DT-04 execution procedure
- Tool: ChatGPT (Codex).
- Date/time: 2026-10-16 14:22 (Asia/Saigon).
- Prompt: The user requested instructions for the next test case.
- Output: Revised TC-FR08-DT-04 to use the already-confirmed editable Checkout field to send E-1 in one checkout submission, then inspect the checkout request/response and Profile order history. This avoids the original edit-and-resend path, which could create an additional baseline order. Updated the CSV, FR08 Domain report and manual checklist.
- Review: The revised path submits exactly one test order and tests whether the backend stores client-supplied E-1 or the expected cart total E.
- Files affected: `test-cases/test-cases.csv`, `reports/FR08_Domain.md`, `MANUAL_ACTIONS.md`, `ai-audit/AI_Audit.md`.


### AI-INT-020 - Record execution of TC-FR08-DT-04
- Tool: ChatGPT (Codex).
- Date/time: 2026-10-16 14:28 (Asia/Saigon).
- User prompt: The user supplied a Network screenshot showing Checkout HTTP 200 and a Profile screenshot showing order #1 at 57,999,999 VND.
- Output: Marked TC-FR08-DT-04 Failed because the stored order total matched client E-1 rather than cart E. Copied the two original screenshots `Screenshot (1347).png` and `Screenshot (1348).png` to the FR-08 evidence folder. Added BUG-FR08-02 and updated CSV, FR08 Domain, Main Report, README, checklist and aggregate counts.
- Review: The Profile screenshot confirms the persisted amount; the Network screenshot confirms HTTP 200 but does not legibly show request payload or response orderId. No bearer token was included in the recorded evidence.
- Files affected: two DT-04 screenshots, `test-cases/test-cases.csv`, `reports/FR08_Domain.md`, `bug-reports/bugs.md`, `reports/Main_Report.md`, `README.md`, `MANUAL_ACTIONS.md`, `ai-audit/AI_Audit.md`.


### AI-INT-021 - Record execution of TC-FR08-DT-05
- Tool: ChatGPT (Codex).
- Date/time: 2026-10-16 14:29 (Asia/Saigon).
- User prompt: The user supplied a screenshot of the cart after the successful Checkout in DT-04; it still showed iPhone 15 Pro Max x1 and Samsung Galaxy S24 Ultra x1, subtotal 58,000,000 VND.
- Output: Marked TC-FR08-DT-05 Failed. Copied the original screenshot `Screenshot (1349).png` to `screenshots/TC-FR08-DT-05-cart-not-cleared.png`. Added BUG-FR08-03 and updated CSV, FR08 Domain, Main Report, README, manual checklist and aggregate counts. No additional order was submitted.
- Review: The cart screenshot after the success flow confirms both items remained.
- Files affected: `screenshots/TC-FR08-DT-05-cart-not-cleared.png`, `test-cases/test-cases.csv`, `reports/FR08_Domain.md`, `bug-reports/bugs.md`, `reports/Main_Report.md`, `README.md`, `MANUAL_ACTIONS.md`, `ai-audit/AI_Audit.md`.


### AI-INT-022 - Record execution of TC-FR08-BVA-01
- Tool: ChatGPT (Codex).
- Date/time: 2026-10-16 14:34 (Asia/Saigon).
- User prompt: The user supplied a Checkout success/Network screenshot and a Profile screenshot showing new order #3 saved at 57,999,999 VND.
- Output: Marked TC-FR08-BVA-01 Failed because E-1 (57,999,999 VND) was stored instead of E (58,000,000 VND). Copied the original screenshots `Screenshot (1350).png` and `Screenshot (1351).png` into the evidence folder; updated the CSV, BVA/domain analysis, Main Report, README, BUG-FR08-02 evidence and manual checklist.
- Review: The Profile screenshot confirms the stored amount and order #3; the Network screenshot confirms HTTP 200. The request payload is not legible. One demo order was created.
- Files affected: two BVA-01 screenshots, `test-cases/test-cases.csv`, `reports/FR08_BVA.md`, `reports/FR08_Domain.md`, `bug-reports/bugs.md`, `reports/Main_Report.md`, `README.md`, `MANUAL_ACTIONS.md`, `ai-audit/AI_Audit.md`.


### AI-INT-023 - Record execution of TC-FR08-BVA-02
- Tool: ChatGPT (Codex).
- Date/time: 2026-10-16 14:37 (Asia/Saigon).
- User prompt: The user supplied a Checkout success/Network screenshot and a Profile screenshot showing new order #4 saved at 58,000,000 VND.
- Output: Marked TC-FR08-BVA-02 Passed because the stored order amount equaled E=58,000,000 VND. Copied the original screenshots `Screenshot (1352).png` and `Screenshot (1353).png`; updated CSV, FR-08 BVA/domain analysis, Main Report, README, manual checklist and aggregate counts.
- Review: Profile confirms order #4 and its amount; Network confirms HTTP 200. One demo order was created.
- Files affected: two BVA-02 screenshots, `test-cases/test-cases.csv`, `reports/FR08_BVA.md`, `reports/FR08_Domain.md`, `reports/Main_Report.md`, `README.md`, `MANUAL_ACTIONS.md`, `ai-audit/AI_Audit.md`.


### AI-INT-024 - Record execution of TC-FR08-BVA-03
- Tool: ChatGPT (Codex).
- Date/time: 2026-10-16 14:39 (Asia/Saigon).
- User prompt: The user supplied a Checkout success/Network screenshot and a Profile screenshot showing order #5 saved at 58,000,001 VND.
- Output: Confirmed TC-FR08-BVA-03 Failed because E+1 was stored instead of E. Copied original screenshots `Screenshot (1354).png` and `Screenshot (1355).png`; updated CSV, FR08 BVA/domain analysis, Main Report, README, BUG-FR08-02 evidence, checklist and aggregate counts. FR-08 now has all eight cases executed: three Passed and five Failed.
- Review: Profile confirms order #5 stored E+1; Network confirms HTTP 200. One demo order was created.
- Files affected: two BVA-03 screenshots, `test-cases/test-cases.csv`, `reports/FR08_BVA.md`, `reports/FR08_Domain.md`, `bug-reports/bugs.md`, `reports/Main_Report.md`, `README.md`, `MANUAL_ACTIONS.md`, `ai-audit/AI_Audit.md`.
### AI-INT-025 - Prepare FR-14 test design and manual run
- Tool: ChatGPT (Codex).
- Date/time: 2026-10-16 (Asia/Saigon).
- User prompt: “tiếp tục với FR cuối FR-14”.
- Output: Reviewed the SUT FR-14/SEC-03 requirements, category API specification, and admin UI source; prepared 5 Domain and 3 BVA cases in the CSV, all Not Executed. Updated FR14 analysis and aggregate report counts. The source review identified the SRS/API/UI update-operation discrepancy and led to no execution-based bug claims.
- Review: Student must execute the cases manually and provide screenshots/results. Whitespace-only rejection remains an assumption; the API PUT case is labeled as API-contract coverage because the UI and SRS operation list omit update.
- Files affected: `test-cases/test-cases.csv`, `reports/FR14_Domain.md`, `reports/FR14_BVA.md`, `reports/Main_Report.md`, `README.md`, `MANUAL_ACTIONS.md`, `ai-audit/AI_Audit.md`.
