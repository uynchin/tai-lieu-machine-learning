# Xử lý quy tắc

Từ điển thuần chỉ tra điểm từng từ rồi cộng lại, nên bỏ sót những gì nằm ở ngữ cảnh. Nhánh này gồm các bước điều chỉnh điểm bằng quy tắc, đặt trước hoặc sau bước tra từ điển. Các quy tắc không tạo từ điển mới mà sửa cách dùng điểm của từ điển có sẵn trong nhánh [Dictionary Based](dictionary-based.md).

| Quy tắc | Giải quyết vấn đề gì | Trang |
|---|---|---|
| Negation handling | Từ phủ định đứng gần từ cảm xúc, ví dụ "not good" | [Negation handling](negation.md) |
| Intensifier handling | Từ tăng cường và từ giảm nhẹ, ví dụ "very good" và "slightly bad" | [Intensifier handling](intensifier.md) |
| Emoji và emoticon | Cảm xúc nằm trong biểu tượng chứ không nằm trong chữ | [Emoji và emoticon](emoji-emoticon.md) |
| Chuẩn hóa tiếng lóng | Từ viết tắt, viết sai hoặc kéo dài chữ không khớp với mục từ trong từ điển | [Chuẩn hóa tiếng lóng](slang-normalization.md) |

Thứ tự áp dụng các bước ảnh hưởng đến kết quả. Nếu hạ chữ thường trước khi tính tăng cường theo VADER thì mất tín hiệu chữ in hoa. Nếu xử lý phủ định trước khi chuẩn hóa thì phủ định viết tắt không được nhận ra. Vì vậy cần nêu rõ trong phần phương pháp bước nào được dùng, theo thứ tự nào và với tham số gì.
