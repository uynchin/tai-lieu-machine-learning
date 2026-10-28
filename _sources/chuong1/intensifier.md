# Intensifier handling: xử lý từ tăng cường

## Là gì?

Từ tăng cường như "very" làm mạnh điểm của từ cảm xúc đứng sau, từ giảm nhẹ như "slightly" làm yếu điểm đó. Bước này điều chỉnh độ lớn của điểm theo các từ đi kèm. [AFINN](afinn.md) có thang cường độ cho từng từ nhưng không có cơ chế này.

## Nền tảng

Kennedy và Inkpen năm 2006 tạo các đặc trưng riêng cho phủ định và tăng cường. Taboada và cộng sự năm 2011 gắn cho mỗi từ tăng cường một hệ số phần trăm, lớn hơn một với từ tăng và nhỏ hơn một với từ giảm nhẹ. Điểm của từ cảm xúc đứng sau được nhân với hệ số đó.

VADER chọn cách cộng giá trị cố định. Mọi từ tăng cường trong danh sách cộng 0,293 vào độ lớn của điểm, và mọi từ giảm nhẹ trừ 0,293. Dấu được xếp theo chiều của từ cảm xúc, nên từ tăng cường làm điểm âm càng âm hơn. Khi từ tăng cường nằm cách từ cảm xúc một hoặc hai vị trí, ảnh hưởng bị giảm dần theo khoảng cách. Hệ số giảm cụ thể nằm trong mã nguồn. VADER còn cộng 0,733 khi từ cảm xúc viết chữ in hoa toàn bộ trong khi các từ khác của câu thì không.

## Công thức

```
Cộng cố định:    điểm mới = điểm cũ cộng b, nếu điểm cũ dương
                 điểm mới = điểm cũ trừ b, nếu điểm cũ âm

Theo phần trăm:  điểm mới = điểm cũ nhân (1 cộng p)
```

| Ký hiệu | Ý nghĩa |
|---|---|
| `điểm cũ` | Điểm của từ cảm xúc trong từ điển, trước khi xử lý từ tăng cường |
| `điểm mới` | Điểm của từ cảm xúc sau khi điều chỉnh |
| `b` | Giá trị cố định của từ tăng cường. VADER dùng 0,293 cho từ tăng, và dấu âm cho từ giảm nhẹ |
| `p` | Tỷ lệ phần trăm điều chỉnh. Dương với từ tăng, âm với từ giảm nhẹ. Giá trị cụ thể do người dùng đặt |

## Ví dụ minh họa

Số dưới đây chỉ để minh họa, không phải giá trị trong tệp từ điển. Giả sử "good" có điểm 1,9 và "bad" có điểm âm 2,5, dùng giá trị cộng cố định của VADER.

| Cụm | Tính | Điểm |
|---|---|---|
| very good | 1,9 cộng 0,293 | 2,193 |
| very bad | âm 2,5 trừ 0,293 | âm 2,793 |
| slightly bad | âm 2,5 cộng 0,293 | âm 2,207 |
| GOOD, khi các từ khác viết thường | 1,9 cộng 0,733 | 2,633 |

Với cách theo phần trăm, giả sử "good" có điểm 3, "very" có p bằng 0,5 và "slightly" có p bằng âm 0,5. Khi đó "very good" là 4,5 và "slightly good" là 1,5.

## Cách dùng khi phân tích

1. Lập danh sách từ tăng cường và từ giảm nhẹ, kèm giá trị điều chỉnh.
2. Xác định vị trí tìm từ tăng cường so với từ cảm xúc.
3. Áp dụng điều chỉnh, rồi giới hạn điểm trong thang của từ điển nếu cần. Ví dụ "very superb" có thể vượt mức tối đa của thang.
4. Giữ nguyên chữ in hoa cho đến khi tính xong, nếu dùng tín hiệu chữ in hoa như VADER.

## Điểm mạnh

- Phân biệt được "good", "very good" và "slightly good" mà không cần thêm mục từ.
- Quy tắc đơn giản, dễ kiểm tra từng bước.
- Cách theo phần trăm giữ được thang tương đối, còn cách cộng cố định dễ cài đặt.

## Điểm yếu

- VADER dùng một giá trị chung 0,293 cho mọi từ tăng cường, nên "really" và "extremely" nhận cùng mức tăng. Các giá trị này theo mô tả của tác giả là mức tăng trung bình rút ra từ dữ liệu, không phân biệt từng từ.
- Một số từ trong danh sách của VADER, như "so", "more" và "most", không phải lúc nào cũng là từ tăng cường, nên có thể làm điểm sai. Ý này là suy luận từ nội dung danh sách.
- Cách cộng cố định không tự giới hạn theo thang, và cách theo phần trăm cũng cần giới hạn riêng.
- Chưa tra được bảng phần trăm cụ thể của SO-CAL, nên không nêu giá trị nào.
- Với tiếng Việt, từ tăng cường như "rất", "quá", "cực kỳ", "hơi", "khá" có thể đứng trước hoặc sau từ cảm xúc, ví dụ "đẹp quá", "tốt lắm". Từ "quá" còn có thể đi với nghĩa chê, như "quá đắt". Đây là nhận xét chưa có nguồn.

## Các bài báo nên đọc và dùng để trích dẫn

| Bài | Dùng để trích khi nào |
|---|---|
| Taboada, Brooke, Tofiloski, Voll & Stede (2011), Lexicon-Based Methods for Sentiment Analysis, Computational Linguistics, tập 37, số 2, trang 267 đến 307 | Tăng cường theo phần trăm. Nguồn chính |
| Hutto & Gilbert (2014), VADER, ICWSM | Cộng giá trị cố định, tín hiệu chữ in hoa, suy giảm theo khoảng cách |
| Polanyi & Zaenen (2006), Contextual Valence Shifters | Khái niệm yếu tố dịch cực tính theo ngữ cảnh. Chưa đọc bài gốc, chỉ thấy qua lời dẫn của Taboada và cộng sự, nên cần tra tên đầy đủ và nơi đăng |
