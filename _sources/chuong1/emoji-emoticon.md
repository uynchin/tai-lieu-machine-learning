# Emoji và emoticon

## Là gì?

Emoticon là chuỗi ký tự, thường là dấu câu, ví dụ `:)` hoặc `:(`. Emoji là ký tự đồ họa trong bảng mã Unicode. Cả hai đều mang cảm xúc mà từ điển chữ không bắt được. Bước này gán điểm cho chúng hoặc dùng chúng làm tín hiệu cho điểm của cả văn bản.

## Nền tảng

Kralj Novak, Smailović, Sluban và Mozetič năm 2015 công bố Emoji Sentiment Ranking, từ điển cảm xúc đầu tiên cho emoji. Từ điển có 751 emoji, tính từ khoảng 70.000 bài đăng được 83 người gán nhãn thuộc 13 ngôn ngữ châu Âu. Điểm của mỗi emoji tính từ cảm xúc của các bài đăng chứa nó, và tệp dữ liệu ghi số lần emoji xuất hiện trong bài tiêu cực, trung tính và tích cực. Một số kết quả chính:

- Phần lớn emoji mang cảm xúc tích cực, nhất là emoji phổ biến.
- Bài đăng có emoji được người gán nhãn đồng thuận cao hơn.
- Emoji thường nằm cuối bài, và cực tính tăng theo khoảng cách từ đầu bài.
- Không thấy khác biệt đáng kể về thứ hạng emoji giữa 13 ngôn ngữ.

Với emoticon, Go và cộng sự năm 2009 xây kho Sentiment140 gồm 1,6 triệu bài đăng có emoticon tích cực hoặc tiêu cực, gán nhãn bài theo emoticon. Mohammad và cộng sự năm 2013 dựng từ điển cảm xúc từ kho này, và dùng biểu thức chính quy lấy từ tệp tách từ của Christopher Potts để xác định cực tính của emoticon trong bài.

## Công thức

Ý chính của điểm emoji là chênh lệch tỷ lệ xuất hiện trong bài tích cực và bài tiêu cực. Công thức chính xác nằm trong bài gốc, ở đây chỉ nêu dạng đơn giản:

```
Điểm của emoji e = tỷ lệ xuất hiện của e trong bài tích cực
                   trừ tỷ lệ xuất hiện của e trong bài tiêu cực

Điểm của d = tổng điểm từ trong d
             cộng tổng điểm emoji và emoticon trong d
```

| Ký hiệu | Ý nghĩa |
|---|---|
| `e` | Một emoji cần chấm |
| `d` | Văn bản cần chấm |
| `Điểm của e` | Điểm cảm xúc của emoji e, dương nếu hay nằm trong bài tích cực |
| `Điểm của d` | Điểm cảm xúc của cả văn bản, gộp điểm từ với điểm emoji và emoticon |

Cách gộp điểm từ với điểm emoji do người dùng chọn và cần nêu rõ trong phần phương pháp.

## Ví dụ minh họa

Số dưới đây chỉ để minh họa. Giả sử một emoji xuất hiện 100 lần: 70 lần trong bài tích cực, 20 lần trong bài trung tính và 10 lần trong bài tiêu cực. Tỷ lệ tích cực là 0,70, tỷ lệ tiêu cực là 0,10, nên điểm là 0,60.

Với emoticon, Mohammad và cộng sự dùng `:)`, `:-)` và `:))` làm nhãn tích cực, `:(` và `:-(` làm nhãn tiêu cực khi dựng từ điển Sentiment140.

## Cách dùng khi phân tích

1. Tách emoji và emoticon thành đơn vị riêng ở bước tách từ, vì tách theo khoảng trắng thường làm hỏng chúng.
2. Gom các biến thể của cùng một emoticon, ví dụ `:)` và `:-)` và `:))`.
3. Tra điểm trong bảng có sẵn, bỏ emoji không có mục.
4. Gộp với điểm từ, hoặc dùng làm đặc trưng riêng.

## Điểm mạnh

- Bắt được cảm xúc mà từ không mang. Bài có emoji được người gán nhãn đồng thuận cao hơn, theo Kralj Novak và cộng sự.
- Bảng điểm công bố tự do theo giấy phép CC BY SA 4.0, kèm số lần xuất hiện nên kiểm tra được.
- Kết quả ổn định giữa 13 ngôn ngữ, nên các tác giả đề xuất dùng làm tài nguyên không phụ thuộc ngôn ngữ cho các ngôn ngữ châu Âu.

## Điểm yếu

- Chỉ có 751 emoji, và emoji ra đời sau thời điểm xây dựng không có điểm. Bài gốc cho biết bảng mã Unicode 8.0 vào tháng 8 năm 2015 có 1.281 ký tự emoji, con số nay đã lớn hơn nhiều và cần tra số liệu hiện hành.
- Dữ liệu là bài đăng của 13 ngôn ngữ châu Âu, không có tiếng Việt, nên điểm có thể lệch với cách dùng của người Việt.
- Emoji dùng ít cho điểm kém tin cậy. Một bài báo tóm tắt nghiên cứu cho biết có emoji chỉ xuất hiện năm lần, và bài loại emoji xuất hiện dưới năm bài đăng.
- Nhãn lấy từ emoticon là nhãn yếu, vì bài chứa emoticon tích cực vẫn có thể chê. Ý này là suy luận từ cách dựng kho.
- Emoticon của người Việt như `=))`, `:v` và `^^` không có trong các bảng trên. Đây là nhận xét chưa có nguồn.

## Các bài báo nên đọc và dùng để trích dẫn

| Bài | Dùng để trích khi nào |
|---|---|
| Kralj Novak, Smailović, Sluban & Mozetič (2015), Sentiment of Emojis, PLOS ONE, tập 10, số 12, e0144296 | Bảng điểm emoji và các kết quả về vị trí, ngôn ngữ. Nguồn chính |
| Mohammad, Kiritchenko & Zhu (2013), NRC-Canada, SemEval 2013 | Dùng emoticon làm nhãn và biểu thức chính quy xác định cực tính emoticon |
| Go và cộng sự (2009), kho Sentiment140 | Kho 1,6 triệu bài đăng gán nhãn theo emoticon. Chưa tra được tên bài và đầy đủ tác giả |
