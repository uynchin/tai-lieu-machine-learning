# Chuẩn hóa tiếng lóng

## Là gì?

Chuẩn hóa tiếng lóng là đưa các dạng viết không chuẩn về dạng chuẩn trước khi tra từ điển cảm xúc. Mục đích là để từ viết tắt, viết sai hoặc kéo dài chữ vẫn khớp được với mục từ trong từ điển.

## Nền tảng

Han và Baldwin năm 2011 định nghĩa nhiệm vụ này là ánh xạ từ ngoài từ vựng, tức dạng viết sai chuẩn, sang dạng chuẩn. Họ liệt kê nguồn gốc của dạng sai chuẩn trên Twitter: lỗi gõ, viết tắt tùy tiện, thay âm, cấu trúc sai ngữ pháp và biểu tượng cảm xúc. Bài so sánh tỷ lệ từ ngoài từ vựng giữa tin tức, Twitter và tin nhắn SMS, và đề xuất phương pháp kết hợp tra từ điển với nhiều nguồn dữ liệu khác.

Một bản báo cáo của Han, Lui và Baldwin cho thấy cách làm trong thực tế. Họ chọn tra từ điển với độ chính xác cao nhưng phủ thấp, tức thay một từ khi chắc chắn, như "u" thành "you", và tránh chuẩn hóa quá tay những từ lạ nhưng đúng. Trong 5.478.459 bài đăng tiếng Anh, họ chuẩn hóa 1.279.169 từ, ảnh hưởng đến 868.993 bài đăng.

Nhóm NRC của Mohammad và cộng sự cũng có bước chuẩn hóa riêng, ví dụ tách thẻ ghép nhiều từ như `#biggestdaythisyear` thành các từ rời.

## Công thức

Bước này không có công thức tính điểm. Nó là bảng ánh xạ, và hiệu quả đo bằng thay đổi điểm trước và sau.

```
Dạng gốc  →  Dạng chuẩn  →  Điểm lấy từ từ điển
```

## Ví dụ minh họa

Các dòng dưới chỉ để minh họa, giả sử "love" có điểm 3 trong từ điển.

| Dạng gốc | Dạng chuẩn | Điểm trước chuẩn hóa | Điểm sau chuẩn hóa |
|---|---|---|---|
| luv | love | 0, vì không có trong từ điển | 3 |
| u | you | 0 | 0 |
| soooo goood | so good | 0 | điểm của good, cộng thêm điều chỉnh tăng cường của so |

Dòng thứ hai cho thấy chuẩn hóa không đổi điểm khi từ chuẩn không mang cảm xúc. Việc chuẩn hóa chỉ có giá trị với từ cảm xúc bị viết sai chuẩn.

## Cách dùng khi phân tích

1. Phát hiện các từ không có trong từ vựng chuẩn.
2. Sinh các dạng chuẩn có thể có cho mỗi từ.
3. Chọn dạng chuẩn dựa trên từ điển, độ giống về chữ viết và ngữ cảnh. Đây là quy trình tổng quát được tóm lại, không phải tả lại từng bước trong bài của Han và Baldwin.
4. Thay thế, và ghi lại các từ đã thay để kiểm tra sau.

Thứ tự bước quan trọng. Nếu hạ chữ thường trước khi tính tăng cường theo VADER thì mất tín hiệu chữ in hoa. Nếu xử lý phủ định trước khi chuẩn hóa thì phủ định viết tắt không được nhận ra.

## Điểm mạnh

- Tăng số từ khớp được với từ điển, vì từ ngoài từ vựng phổ biến trên Twitter và SMS hơn trên tin tức, theo so sánh của Han và Baldwin.
- Cho phép dùng nguyên từ điển đã có mà không cần mở rộng.
- Bảng ánh xạ kiểm tra và sửa tay được.

## Điểm yếu

- Chuẩn hóa quá tay có thể làm hỏng từ đúng. Báo cáo của Han, Lui và Baldwin chọn độ chính xác cao vì lý do này. [AFINN](afinn.md) còn chứa nhiều từ đời thường và từ thô tục, nên thay chúng bằng từ chuẩn có thể làm mất điểm vốn có.
- Một dạng viết tắt có thể ứng với nhiều dạng chuẩn, cần ngữ cảnh để chọn.
- Với tiếng Việt, chưa kiểm chứng được tài nguyên chuẩn hóa công khai nào. Các dạng viết tắt quen thuộc như "ko", "k", "hok" cho "không", "dc" và "đc" cho "được", "j" cho "gì", "ntn" cho "như thế nào" là hiểu biết chung, chưa có nguồn. Dạng "ko" còn là từ phủ định, nên chuẩn hóa là điều kiện để xử lý phủ định tiếng Việt chạy đúng. Dữ liệu viết không dấu cũng cần bước khôi phục dấu. Nên lập bảng ánh xạ từ chính dữ liệu đang nghiên cứu.

## Các bài báo nên đọc và dùng để trích dẫn

| Bài | Dùng để trích khi nào |
|---|---|
| Han & Baldwin (2011), Lexical Normalisation of Short Text Messages: Makn Sens a #twitter, ACL, trang 368 đến 378 | Định nghĩa nhiệm vụ, nguồn gốc dạng sai chuẩn, phương pháp. Nguồn chính |
| Han, Lui & Baldwin, Melbourne Language Technology Group Microblog Track Report, TREC | Ví dụ chuẩn hóa độ chính xác cao và số liệu quy mô. Chưa tra năm đăng chính xác |
| Mohammad, Kiritchenko & Zhu (2013), NRC-Canada, SemEval 2013 | Tách thẻ ghép từ và các đặc trưng chữ in hoa |
