# AI Critique — FR-02 và FR-06

Trong FR-02, AI giúp phân hoạch dữ liệu đăng nhập và gợi ý các mốc 2/3 lần sai, 29/30/31 giây. Tuy nhiên, một lần đăng nhập sai làm bộ đếm tăng từ 0 lên 2; hệ thống sau đó khóa trước lần sai thứ ba. Nếu chỉ suy luận từ yêu cầu hoặc giao diện, AI có thể bỏ sót tương tác này. Ảnh Network xác nhận mã HTTP nhưng không chứng minh chính xác thời điểm gửi, nên phép đo quanh 29/30 giây chỉ là xấp xỉ.

Ở FR-06, thông báo “Thành công” không chứng minh sản phẩm được thêm đúng số lượng: với `-1`, giỏ hiển thị dòng hàng số lượng 1. Ảnh thiếu trạng thái trước không cho biết chính xác số lượng thay đổi bao nhiêu. Kiểm tra hai sản phẩm thuộc danh mục khác nhau giúp tái hiện lỗi thiếu danh mục.

AI bỏ sót vì không thấy đầy đủ trạng thái tài khoản/giỏ, ảnh thiếu baseline và dữ liệu thay đổi giữa các ca. Tôi học được cách đặt tiền điều kiện, cô lập dữ liệu, lưu ảnh trước/sau và kiểm tra response thật. AI giúp tổ chức miền, nhưng người kiểm thử phải xác minh kết quả, nêu giới hạn bằng chứng và không biến giả thuyết thành bug hay kết luận Pass/Fail.
