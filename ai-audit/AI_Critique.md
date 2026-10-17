# AI Critique — HW02

Ở FR-02, AI giúp phân hoạch dữ liệu đăng nhập và gợi ý kiểm tra quanh ngưỡng khóa. Chỉ xem thông báo giao diện không đủ phát hiện một lần đăng nhập sai làm bộ đếm tăng hai lần; cần đối chiếu trạng thái lưu và mã nguồn. Thời gian khóa 180 giây cũng cần được xác nhận bằng cấu hình backend.

Ở FR-06, thông báo “Thành công” không chứng minh số lượng được thêm đúng: với đầu vào `-1`, giỏ hiển thị mặt hàng số lượng 1. Ảnh thiếu trạng thái trước nên không thể suy ra chính xác lượng thay đổi.

FR-08 cần được kiểm tra xuyên suốt giao diện, request và lịch sử đơn hàng. Tổng tiền sửa được ở trình duyệt chưa chứng minh backend lưu sai; phải đối chiếu giá trị quanh `E` với đơn đã tạo. Ở FR-14, tên rỗng được lưu và người dùng thường tạo được danh mục, trái với yêu cầu. Ba dấu cách là Inconclusive vì đặc tả chưa quy định cách xử lý.

AI hữu ích để tổ chức miền và tạo khung ca, nhưng có thể bỏ sót trạng thái nền, ranh giới client/server hoặc giả định chưa có trong yêu cầu. Tôi học được phải đối chiếu kỳ vọng với SRS, cô lập dữ liệu, lưu bằng chứng trước/sau và chỉ kết luận khi có căn cứ. Người kiểm thử chịu trách nhiệm cuối cùng về trạng thái và báo cáo bug.
