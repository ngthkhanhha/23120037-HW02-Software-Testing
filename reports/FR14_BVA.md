# FR-14 — Phân tích giá trị biên

## Các biên có căn cứ trong yêu cầu

FR-14 quy định tên danh mục là bắt buộc và không được để trống. Yêu cầu không nêu độ dài tối đa hoặc quy tắc cắt khoảng trắng cụ thể. Có thể kiểm tra biên chuỗi rỗng (0 ký tự) và giá trị không rỗng ngắn nhất. Đầu vào chỉ có khoảng trắng là trường hợp cần xác nhận cách diễn giải; không kết luận đó là bug nếu chưa có xác nhận.

| ID | Biên/đầu vào | Kết quả mong đợi | Trạng thái và kết quả |
|---|---|---|---|
| TC-FR14-BVA-01 | Chuỗi rỗng (0 ký tự) | Từ chối; không tạo danh mục. | **Failed** — gửi biểu mẫu rỗng đã tạo danh mục #4 không có tên; mục này đã được xóa sau khi chụp bằng chứng. Bằng chứng: [`TC-FR14-BVA-01.png`](../screenshots/TC-FR14-BVA-01.png). |
| TC-FR14-BVA-02 | Ba dấu cách, không có ký tự nhìn thấy | Giả định: từ chối như chuỗi rỗng; cần xác nhận cách hiểu yêu cầu. | **Inconclusive** — ứng dụng chấp nhận và lưu đúng ba dấu cách; không kết luận bug vì FR-14 không quy định việc cắt khoảng trắng. Bằng chứng: [`TC-FR14-BVA-02.png`](../screenshots/TC-FR14-BVA-02.png). |
| TC-FR14-BVA-03 | Một ký tự không phải khoảng trắng (`A`) | Chấp nhận; xóa danh mục thử nghiệm sau khi chụp bằng chứng. | **Passed** — `A` được chấp nhận và lưu thành danh mục #6; mục thử nghiệm được xóa sau khi lưu bằng chứng. Bằng chứng: [`TC-FR14-BVA-03.png`](../screenshots/TC-FR14-BVA-03.png). |

Không có giới hạn độ dài tối đa trong nguồn yêu cầu, nên không thiết kế giá trị max-1/max/max+1. Không suy ra giới hạn từ input HTML hoặc hành vi cơ sở dữ liệu. Các bước chi tiết nằm trong CSV tổng.
