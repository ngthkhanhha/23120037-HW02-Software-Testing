# FR-02 — Domain Testing

## Thông tin

- Nền tảng: Web
- Yêu cầu nguồn: Đặc tả yêu cầu hệ thống EShop, mục FR-02 trong `README.md` của repo
- Trạng thái: Đã hoàn tất phân tích và thực thi 8/10 test case; 4 Passed, 4 Failed, 2 Not Executed. Chi tiết và lý do các TC chưa chạy được ghi trong bảng kết quả bên dưới và `../test-cases/test-cases.csv`.

## Yêu cầu được kiểm thử

- Người dùng đăng nhập bằng email và mật khẩu.
- Sau mỗi lần đăng nhập thất bại, bộ đếm số lần thất bại tăng đúng 1.
- Sau ít nhất 3 lần đăng nhập thất bại liên tiếp, tài khoản bị khóa tạm thời 30 giây trong môi trường demo.
- Hệ thống hiển thị thông báo lỗi phù hợp nhưng không tiết lộ nguyên nhân cụ thể.
- Đăng nhập thành công trả về JWT. Client lưu token và gửi token kèm các yêu cầu cần xác thực bằng header `Authorization: Bearer <token>`.
- Trường email dùng `type="email"` và được kiểm tra định dạng bằng HTML5.

## Đầu vào và phân hoạch miền

| Thuộc tính/trạng thái | Miền tương đương | Kết quả mong đợi theo đặc tả |
|---|---|---|
| Email | Định dạng không hợp lệ | Trình duyệt từ chối form theo HTML5 trước khi gửi; cần xác minh trên giao diện |
| Email | Định dạng hợp lệ, tài khoản tồn tại | Cho phép gửi yêu cầu đăng nhập để kiểm tra mật khẩu |
| Email | Định dạng hợp lệ, tài khoản không tồn tại | Đăng nhập thất bại; thông báo không tiết lộ nguyên nhân cụ thể |
| Mật khẩu | Đúng với tài khoản chưa bị khóa | Đăng nhập thành công và nhận JWT |
| Mật khẩu | Sai với tài khoản chưa bị khóa | Đăng nhập thất bại; bộ đếm tăng đúng 1; thông báo không tiết lộ nguyên nhân cụ thể |
| Số lần thất bại liên tiếp | 1 hoặc 2 lần | Đăng nhập thất bại nhưng chưa đạt ngưỡng khóa 3 lần |
| Số lần thất bại liên tiếp | Lần thứ 3 trở lên | Tài khoản bị khóa tạm thời 30 giây |
| Trạng thái tài khoản | Đang trong thời gian khóa | Không đăng nhập được trong thời gian khóa |
| Chuỗi đăng nhập | Đăng nhập sai rồi đăng nhập đúng trước khi đủ 3 lần sai | Hành vi reset bộ đếm chưa được xác định ở phần yêu cầu này; cần xác minh |

## Test case

Các test case chi tiết được ghi trong [`../test-cases/test-cases.csv`](../test-cases/test-cases.csv). Mỗi test case cần có:

- ID và miền được kiểm tra
- Tiền điều kiện
- Dữ liệu đầu vào
- Các bước thực hiện
- Kết quả mong đợi và nguồn yêu cầu
- Kết quả thực tế, trạng thái và bằng chứng — chỉ điền sau khi chạy test

## Trạng thái rà soát yêu cầu

- Yêu cầu FR-02 đã đối chiếu với README SUT: [x] Có / [ ] Chưa
- Mã nguồn/UI đã xem: [x] Có / [ ] Chưa
- Test đã chạy: [x] Có / [ ] Chưa
- Quy tắc reset bộ đếm sau đăng nhập thành công: [x] Đã xác minh / [ ] Chưa xác minh
- Thời điểm bắt đầu và kết thúc khóa 30 giây: [ ] Đã xác minh / [x] Chưa xác minh
- Cách xử lý email không tồn tại và mật khẩu sai có cùng thông báo hay không: [x] Đã xác minh / [ ] Chưa xác minh

## Cách áp dụng Domain Testing

1. Chọn các đầu vào và trạng thái có thể làm thay đổi kết quả đăng nhập: định dạng email, email có/không có tài khoản, mật khẩu đúng/sai, số lần sai liên tiếp, trạng thái khóa và trạng thái xác thực sau đăng nhập.
2. Chia mỗi đầu vào thành các miền có hành vi mong đợi khác nhau. Ví dụ, email hợp lệ được chia tiếp theo việc tài khoản có tồn tại; mật khẩu chia đúng/sai; bộ đếm chia dưới ngưỡng 3 và đạt/vượt ngưỡng.
3. Kết hợp các miền thành ca kiểm thử đại diện, đồng thời giữ riêng các chuyển trạng thái cần quan sát (nhập sai, khóa, đăng nhập đúng, nhận JWT và gửi Bearer token).
4. Đối chiếu kết quả với giao diện, Network, cơ sở dữ liệu chỉ đọc và mã nguồn khi cần phân biệt lỗi hiển thị với lỗi xử lý phía server. Ghi Failed chỉ khi có sai khác xác định được với yêu cầu.

## Phân tích khoảng trống do AI đề xuất (rà soát bổ sung)

Giới hạn: nhật ký và hồ sơ hiện có không lưu một bộ ứng viên ban đầu do AI tạo riêng để đối chiếu từng mục. Vì vậy, phần dưới đây là rà soát khoảng trống bao phủ của bộ kiểm thử hiện tại; không khẳng định những điểm này chắc chắn đã bị AI bỏ sót.

Đối chiếu các miền yêu cầu với bộ ca hiện tại cho thấy các miền chính đã có đại diện: đăng nhập thành công (DT-01), email sai định dạng (DT-02), email không tồn tại (DT-03), mật khẩu sai và bộ đếm (DT-04), JWT/Bearer (DT-06), ngưỡng khóa (BVA-01/02) và thời gian khóa (BVA-04/05/06). DT-03 cùng DT-04 ghi nhận thông báo chung; BVA-01 và BVA-06 đã được thiết kế nhưng chưa thực thi.

Các điểm còn thiếu hoặc cần hoàn tất:

- **Ưu tiên cao — chạy lại BVA-01 và BVA-06 với trạng thái tài khoản sạch, cô lập.** BVA-01 bị bỏ qua do bộ đếm seeded đã ở mức 2; BVA-06 tại khoảng 31 giây chưa chạy. Hiện chưa có bằng chứng thực nghiệm đầy đủ cho đúng hai điểm biên này. Không dùng tài khoản dùng chung nếu việc chạy có thể khóa tài khoản ngoài dự kiến.
- **Ưu tiên vừa — kiểm tra trường email/mật khẩu để trống và các dạng email sai khác** (ví dụ thiếu phần tên miền hoặc có khoảng trắng). Bộ hiện tại chỉ chạy một mẫu `ha@`; chưa có căn cứ để khẳng định toàn bộ miền lỗi định dạng được xử lý nhất quán. Đây là kiểm tra bổ sung; đặc tả chưa nêu rõ thông báo/validation riêng cho trường rỗng.
- **Ưu tiên vừa — xác minh độc lập việc đặt lại bộ đếm sau khi đăng nhập thành công.** Báo cáo hiện nói quy tắc đã xác minh từ mã nguồn; chưa thấy ca chạy riêng trong CSV chứng minh chuỗi sai → đúng → sai và giá trị counter sau từng bước. Giữ đây là khoảng trống bằng chứng thực thi, không phải khẳng định tính năng sai.
- **Đã phát hiện trong bộ hiện tại:** response đăng nhập để lộ password dạng rõ (DT-06/BUG-FR02-03). Đây là phát hiện kiểm tra phản hồi bảo mật bên cạnh mục tiêu JWT/Bearer, không phải test bị bỏ sót hiện tại.

Các đề xuất chưa chạy ở trên không được tính vào tổng 10 ca FR-02 hoặc các bug đã xác nhận. Cần sinh viên bổ sung/chạy và ghi kết quả nếu muốn đưa chúng vào phạm vi thực thi.

## Giả định và giới hạn

Quy tắc reset bộ đếm đã được xác minh bằng mã nguồn; email không tồn tại và mật khẩu sai cho cùng thông báo chung đã được quan sát khi chạy test. Thời điểm chính xác bắt đầu/kết thúc khóa chưa được xác minh đầy đủ; các phép thử 29/30 giây là xấp xỉ và BVA-06 tại 31 giây chưa chạy.
