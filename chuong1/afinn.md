# AFINN

## 1. AFINN là gì?

AFINN là một từ điển cảm xúc dạng danh sách đơn giản. Mỗi từ tiếng Anh được gán một số nguyên từ âm 5 đến dương 5. Số âm là tiêu cực, số dương là tích cực, và số càng xa 0 thì cảm xúc càng mạnh. Người ta dùng nó để máy tính cộng điểm các từ trong một câu hay một bài review và biết văn bản nghiêng về khen hay chê, mà không cần ai đọc và chấm tay.

So với ba từ điển trước, AFINN là loại gọn nhất. [SentiWordNet](bai1.md) gán điểm cho nghĩa của từ, [EmoLex](nrc-emolex.md) gán nhãn cảm xúc cho từ, [SenticNet](senticnet.md) gán điểm cho khái niệm. AFINN chỉ gán một con số cho từ, không có nhãn cảm xúc cụ thể, không có nghĩa, không có khái niệm. Tác giả là Finn Årup Nielsen, và tên AFINN lấy từ tên ông.

## Nền tảng: ANEW và văn bản mạng xã hội

Nielsen đặt tên bài báo gốc là "A new ANEW", nên cần hiểu ANEW trước. ANEW là danh sách các từ tiếng Anh do Bradley và Lang xây dựng, trong đó người tham gia chấm mức dễ chịu, mức kích thích và mức kiểm soát của từng từ trên thang từ 1 đến 9. ANEW có hạn chế là chỉ khoảng hơn một nghìn từ và không chứa nhiều từ thông dụng trên mạng xã hội.

Nielsen muốn có một danh sách dùng được cho các bài đăng ngắn trên mạng xã hội, nên ông tự soạn danh sách riêng và chọn thang cực tính thay cho ba chiều của ANEW. Vì vậy AFINN mang nhiều từ đời thường và cả từ thô tục, vốn thường thấy trong bình luận trực tuyến.

## AFINN gắn thêm gì vào từ

Với mỗi từ w, AFINN gắn một điểm duy nhất:

```
A(w) là một số nguyên từ âm 5 đến dương 5
```

| Ký hiệu | Ý nghĩa |
|---|---|
| `w` | Một từ trong danh sách |
| `A(w)` | Điểm cảm xúc của từ w, là số nguyên từ âm 5 đến dương 5 |

| Thành phần | Ý nghĩa |
|---|---|
| Dấu của điểm | Dương là tích cực, âm là tiêu cực |
| Độ lớn của điểm | Từ 1 là nhẹ đến 5 là rất mạnh |
| Từ không có trong danh sách | Coi như không mang cảm xúc |

Có ba điểm khác với các từ điển trước. Thứ nhất, điểm gắn với từ, không có bước chọn nghĩa, giống EmoLex. Thứ hai, điểm là số nguyên chứ không phải số thực, nên chỉ có tối đa mười một mức. Thứ ba, chỉ có một con số cho mỗi từ, nên không biết từ đó gợi cảm xúc cụ thể nào, ví dụ giận dữ hay buồn bã.

## Ví dụ minh họa

Điểm của từ abandon là âm 2 theo tệp gốc, cần đối chiếu lại với tệp trước khi trích. Các dòng còn lại chỉ để minh họa, không phải giá trị thật trong tệp.

| Từ | Điểm |
|---|---|
| abandon | âm 2 |
| excellent | dương 3 |
| terrible | âm 3 |
| superb | dương 5 |
| room | không có trong danh sách |

Ví dụ cho thấy hai điều. Các từ mạnh hơn nhận số lớn hơn, nên "superb" cao hơn "excellent". Từ chỉ sự vật thông thường như "room" không có trong danh sách và được tính là 0.

## Cách tác giả xây dựng nó

Nielsen công bố nhiều phiên bản, và mô tả chung nhất như sau:

1. Thu thập từ từ nhiều nguồn. Theo bài gốc, nguồn gồm các bài đăng trên mạng xã hội Twitter về hội nghị khí hậu năm 2009 ở Copenhagen, một danh sách từ thô tục lấy từ một từ điển trực tuyến, và một số từ lấy từ ANEW.
2. Chính tác giả đọc từng từ và gán điểm nguyên trên thang từ âm 5 đến dương 5. Không dùng thuật toán và không thuê đám đông gán nhãn.
3. Phiên bản sau bổ sung thêm từ và sửa các điểm cũ. Bản đầu có khoảng 1.468 mục, bản 111 có khoảng 2.477 mục, bản 165 có khoảng 3.382 mục.
4. Để kiểm tra, Nielsen so sánh kết quả của AFINN với các danh sách có sẵn khác trên một tập bài đăng đã được người đọc chấm điểm.

Điểm cần nhớ là điểm do một người gán thủ công. Đây là điểm khác với SentiWordNet và SenticNet, vốn do thuật toán suy ra, và cũng khác với EmoLex, vốn do nhiều người gán. Một người gán thì nhất quán nhưng mang thiên lệch cá nhân.

## Các phiên bản chính

| Phiên bản | Quy mô gần đúng |
|---|---|
| AFINN 96 | Khoảng 1.468 mục |
| AFINN 111 | Khoảng 2.477 mục |
| AFINN 165 | Khoảng 3.382 mục |

Các con số này là gần đúng, cần đối chiếu với tệp dữ liệu và trang của tác giả. Ngoài ra còn có một tệp nhỏ riêng cho biểu tượng cảm xúc.

## Cách dùng khi phân tích một câu

Lấy câu "The room was clean but the staff were rude" làm ví dụ. Các điểm dưới đây chỉ để minh họa.

1. Tách từ: The, room, was, clean, but, the, staff, were, rude.
2. Chuyển về chữ thường. AFINN gồm nhiều dạng chia của từ, nên bước đưa về dạng gốc ít quan trọng hơn so với EmoLex.
3. Tra điểm của từng từ, như bảng dưới.
4. Cộng các điểm lại. Trong ví dụ này tổng bằng 0, tức câu trung hòa.

| Từ | Điểm |
|---|---|
| clean | dương 2 |
| rude | âm 2 |
| các từ còn lại | 0 |

Công thức tính điểm của cả văn bản:

```
Điểm của d = tổng của A(w), với mọi từ w trong d
```

| Ký hiệu | Ý nghĩa |
|---|---|
| `d` | Văn bản cần chấm |
| `w` | Một từ trong văn bản d |
| `A(w)` | Điểm của từ w trong AFINN, bằng 0 nếu từ không có trong danh sách |
| `Điểm của d` | Điểm cảm xúc của cả văn bản |

Vì văn bản dài thường có tổng lớn hơn, nhiều người chia tổng cho số từ để so sánh công bằng giữa các đánh giá dài ngắn khác nhau. Cách tính tổng, trung bình hay chuẩn hóa theo cách khác do người dùng tự chọn và cần nêu rõ trong phần phương pháp. Nielsen cũng ghi nhận rằng danh sách không xử lý phủ định, nên "not good" vẫn bị tính là tích cực nếu không thêm bước riêng.

## Điểm mạnh

- Rất đơn giản và minh bạch. Mỗi từ chỉ có một con số, nên kiểm tra và giải thích kết quả dễ dàng. Đây là lý do chính khiến các nghiên cứu sau thường dùng làm mốc so sánh.
- Có thang cường độ, nên phân biệt được từ nhẹ và từ mạnh. Đây là điểm hơn EmoLex vốn chỉ có nhãn nhị phân (Nielsen, 2011).
- Được thiết kế cho văn bản ngắn trên mạng xã hội, gồm cả từ đời thường và từ thô tục (Nielsen, 2011).
- Không cần chọn nghĩa của từ, nên quy trình xử lý nhẹ hơn SentiWordNet.
- Được dùng làm mốc so sánh trong các bài đánh giá. Hutto và Gilbert (2014) đưa AFINN vào nhóm các phương pháp đối chứng khi giới thiệu VADER.
- Có sẵn trong nhiều gói phần mềm, gồm gói Python tên afinn và hàm get_sentiments của gói tidytext trong R, nên dùng nhanh và dễ lặp lại kết quả.

## Điểm yếu

- Danh sách nhỏ, chỉ khoảng vài nghìn mục, nên nhiều từ trong văn bản thực tế không được tính. Nên đếm tỷ lệ từ được phủ trên chính dữ liệu đang dùng rồi báo cáo.
- Điểm do một người gán, nên có thể mang thiên lệch cá nhân và không có thước đo mức đồng thuận như EmoLex. Ý này là nhận xét về cách xây dựng.
- Không xét ngữ cảnh. Phủ định, mỉa mai và nghĩa khác nhau của cùng một từ đều bị bỏ qua. Nielsen (2011) cũng nêu hạn chế liên quan đến phủ định.
- Chỉ có một chiều cực tính, nên không cho biết cảm xúc cụ thể như giận dữ hay buồn bã.
- Chủ yếu là tiếng Anh. Với dữ liệu tiếng Việt, cần dịch trước hoặc dùng bản dịch, và cả hai cách đều có thể làm lệch sắc thái. Ý này là nhận xét về cách dùng.
- Danh sách được xây dựng từ bình luận về một chủ đề nhất định và từ nguồn mạng xã hội, nên có thể không hợp với lĩnh vực khác như đánh giá khách sạn. Ý này là nhận xét về cách dùng, cần cân nhắc khi nêu trong phần bàn luận.

## Các bài báo nên đọc và dùng để trích dẫn

| Bài | Dùng để trích khi nào |
|---|---|
| Nielsen (2011), A new ANEW: Evaluation of a word list for sentiment analysis in microblogs, ESWC Workshop on Making Sense of Microposts | Mô tả công cụ, cách xây dựng, so sánh với các danh sách khác. Đây là nguồn chính |
| Bradley & Lang (1999), Affective Norms for English Words, báo cáo kỹ thuật của trung tâm nghiên cứu cảm xúc và chú ý | Cơ sở của danh sách ANEW mà Nielsen dựa vào |
| Hutto & Gilbert (2014), VADER: A Parsimonious Rule-based Model for Sentiment Analysis of Social Media Text, ICWSM | Ví dụ AFINN được dùng làm mốc so sánh |

## Lưu ý khi trích dẫn

Thông tin xuất bản, số lượng mục và nguồn dữ liệu trong trang này chưa được tra lại trực tiếp. Điểm của từ abandon cũng cần đối chiếu với tệp dữ liệu tải về. Trước khi đưa vào danh mục tài liệu tham khảo, cần kiểm tra tên bài, năm, tập, số trang trên Google Scholar hoặc trang của Finn Årup Nielsen.
