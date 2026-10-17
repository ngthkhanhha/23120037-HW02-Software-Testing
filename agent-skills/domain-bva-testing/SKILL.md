---
name: domain-bva-testing
description: >-
  Thiết kế và rà soát ca kiểm thử phần mềm bằng phân hoạch tương đương và
  phân tích giá trị biên. Dùng khi phân tích yêu cầu tính năng, chọn dữ liệu
  đại diện, ghi kết quả mong đợi hoặc rà soát bằng chứng và kết quả kiểm thử.
---

# Kiểm thử miền và phân tích giá trị biên

Dùng quy trình này để tạo ca kiểm thử có thể truy vết và có căn cứ từ yêu cầu tính năng. Phân biệt rõ yêu cầu, mã nguồn, hành vi giao diện/API và giả định của người kiểm thử.

## 1. Xác lập cơ sở đánh giá

1. Đọc yêu cầu áp dụng và các quy tắc bảo mật, API, giao diện hoặc dữ liệu liên quan. Ghi chính xác mã yêu cầu và chỉ trích dẫn/diễn giải những điều khoản cần thiết.
2. Ghi lại từng ràng buộc tường minh: kiểu dữ liệu, giá trị được phép, tính bắt buộc, min/max, độ dài, vai trò, trạng thái và kết quả quan sát mong đợi.
3. Đánh dấu thông tin thiếu hoặc mâu thuẫn là **chưa được quy định**. Có thể kiểm tra mã nguồn hoặc lược đồ để hiểu bối cảnh, nhưng không âm thầm biến hành vi đang có thành yêu cầu. Hỏi để làm rõ khi chưa xác định được kết quả mong đợi.
4. Với hành vi chưa được quy định, gắn nhãn kiểm thử thăm dò hoặc để ngỏ kết quả mong đợi. Không đánh Passed/Failed hay báo bug nếu chưa có cơ sở đánh giá hợp lệ.

## 2. Phân hoạch miền

Với từng đầu vào hoặc trạng thái liên quan:

1. Xác định các lớp tương đương dự kiến tạo ra cùng hành vi.
2. Chỉ chia lớp hợp lệ và không hợp lệ khi yêu cầu có căn cứ cho sự phân biệt đó.
3. Chọn một giá trị đại diện cho mỗi lớp và giải thích vì sao giá trị đó đại diện cho lớp.
4. Xem xét tương tác giữa các trường, vai trò, xác thực, trạng thái đã lưu và thao tác trước đó nếu chúng có thể làm thay đổi kết quả.
5. Tránh ca trùng lặp, trừ khi chúng kiểm tra một yêu cầu hoặc rủi ro khác biệt.

Với tên danh mục, các lớp đầu vào có thể gồm tên thông thường không rỗng, đầu vào rỗng, chỉ có khoảng trắng, và độ dài/tập ký tự bị giới hạn rõ ràng. Nếu yêu cầu chỉ nói tên là bắt buộc và không được để trống, không mặc định rằng khoảng trắng cũng là rỗng sau khi cắt bỏ nếu đặc tả không nói vậy.

## 3. Áp dụng phân tích giá trị biên

1. Suy ra biên từ yêu cầu tường minh hoặc hợp đồng đã xác minh (ví dụ min, max, giới hạn độ dài hoặc khoảng số lượng hợp lệ).
2. Với biên số `b`, cân nhắc `b-1`, `b` và `b+1` khi có ý nghĩa và an toàn. Với khoảng `[min,max]`, xem xét giá trị ngay dưới, tại và ngay trên mỗi đầu mút.
3. Với độ dài chuỗi `n`, cân nhắc độ dài `n-1`, `n`, `n+1`; chỉ kiểm tra đầu vào rỗng khi phù hợp.
4. Với chuyển trạng thái, kiểm tra ngay trước và sau điều kiện chuyển trạng thái được quy định.
5. Nếu không có giới hạn được nêu, không tự đặt biên. Ghi nhận khoảng trống và chỉ dùng giá trị thăm dò với kết quả mong đợi được diễn đạt thận trọng.

## 4. Viết ca kiểm thử có thể thực hiện

Mỗi ca cần có:

- ID duy nhất, ổn định;
- nguồn yêu cầu hoặc hợp đồng;
- tiền điều kiện và vai trò;
- dữ liệu đầu vào chính xác;
- các bước được đánh số để người khác có thể lặp lại;
- kết quả quan sát được;
- lý do chọn lớp tương đương hoặc giá trị biên;
- vị trí lưu bằng chứng và, sau khi chạy, kết quả thực tế cùng trạng thái.

Kết quả mong đợi phải kiểm chứng được: nêu thông báo, đường dẫn, mã/trường phản hồi, bản ghi đã lưu hoặc thay đổi trạng thái cần kiểm tra. Không trộn kết quả mong đợi với kết quả thực tế.

## 5. Thực thi an toàn và phân loại bằng chứng

1. Xác nhận đúng môi trường kiểm thử, vai trò và trạng thái ban đầu. Khi có thao tác ghi dữ liệu, dùng dữ liệu thử nghiệm riêng, có thể xóa.
2. Lưu bằng chứng thể hiện đầu vào/thao tác và kết quả liên quan. Che thông tin đăng nhập, cookie, bearer token và dữ liệu cá nhân.
3. Chỉ dọn bản ghi do chính ca kiểm thử tạo ra, sau đó xác minh dữ liệu seed hoặc dữ liệu không liên quan vẫn nguyên vẹn.
4. Gán trạng thái dựa trên bằng chứng quan sát:
   - **Passed:** kết quả thực tế khớp kết quả mong đợi có căn cứ từ yêu cầu;
   - **Failed:** kết quả thực tế tái hiện được và vi phạm kết quả mong đợi đó;
   - **Inconclusive:** chưa đủ cơ sở đánh giá hoặc bằng chứng để kết luận;
   - **Not Executed:** chưa thực thi (kể cả ca được chủ động bỏ qua).
5. Thông báo thành công trên giao diện không tự chứng minh trạng thái backend đã thay đổi. Kiểm tra API hoặc dữ liệu đã lưu khi ca kiểm thử yêu cầu.
6. Dừng lại nếu môi trường hoặc baseline không như dự kiến, hoặc nếu tiếp tục có thể ảnh hưởng dữ liệu khác.

## 6. Báo cáo và đối soát

1. Ghi mỗi ca đúng một lần trong tệp test case nguồn của dự án; giữ nguyên ID và đường dẫn bằng chứng.
2. Chỉ báo bug khi có lỗi tái hiện được và vi phạm yêu cầu. Nêu các bước, kết quả mong đợi/thực tế, môi trường và bằng chứng. Phân biệt quan sát hoặc hành vi chưa quy định với bug đã xác nhận.
3. Khi kết quả thay đổi, cập nhật phân tích tính năng, danh sách bug, rà soát AI và số liệu tổng hợp. Đối soát để mỗi ca đã thiết kế có đúng một trạng thái hiện tại.
4. Phân biệt số ca được thiết kế với số ca đã chạy. Không tính đề xuất thăm dò vào tổng ca thiết kế/thực thi trừ khi đã chính thức bổ sung và chạy.

## Ví dụ: yêu cầu tên danh mục là bắt buộc

Giả sử yêu cầu nêu tên danh mục là bắt buộc và không được để trống nhưng không đề cập việc cắt khoảng trắng:

| Đầu vào | Cơ sở kỳ vọng | Nếu ứng dụng chấp nhận |
|---|---|---|
| `A` | Không rỗng; giá trị đại diện hợp lệ | Passed nếu danh mục được tạo đúng như dự kiến |
| chuỗi rỗng | Bị cấm rõ ràng | Failed; ghi nhận vi phạm có thể tái hiện |
| ba dấu cách | Cách xử lý khoảng trắng chưa được quy định | Inconclusive/thăm dò; không kết luận bug |

Ví dụ này cho thấy cần tách kết quả quan sát khỏi cơ sở đánh giá theo yêu cầu. Trước khi dùng cho hệ thống khác, hãy thay các giả định bằng đặc tả tính năng thực tế.
