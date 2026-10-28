# Ngữ nghĩa: mở rộng từ điển bằng vectơ từ

## Là gì?

Hướng này bắt đầu từ một tập từ mẫu nhỏ hoặc một từ điển có sẵn, rồi lan điểm sang những từ chưa có điểm dựa trên mức gần nghĩa giữa các từ. Mức gần nghĩa đo bằng vectơ từ, tức dãy số biểu diễn mỗi từ, học từ kho ngữ liệu chưa gán nhãn. Hai từ có vectơ gần nhau thì được kỳ vọng có điểm gần nhau.

## Nền tảng

Cơ sở là giả thuyết phân bố của Firth năm 1957 và Harris năm 1968: các từ gần nghĩa thường xuất hiện trong ngữ cảnh giống nhau. Các phương pháp lan điểm từ từ mẫu sang các từ lân cận trong không gian vectơ đều dựa trên giả thuyết này.

Giả thuyết này có một lỗ hổng đã được ghi nhận. Tang và cộng sự chỉ ra rằng các cặp như good và bad có ngữ cảnh giống nhau nhưng trái cực tính, nên vectơ thông thường đặt chúng cạnh nhau. Họ đề xuất vectơ từ có thêm mục tiêu cảm xúc khi huấn luyện, học từ 10 triệu bài đăng, công bố tại ACL năm 2014 và bản tạp chí năm 2016.

Hamilton, Clark, Leskovec và Jurafsky năm 2016 đề xuất SentProp. Phương pháp này gồm hai bước: dựng đồ thị các từ từ vectơ học trên kho ngữ liệu chưa gán nhãn, rồi lan nhãn của từ mẫu qua đồ thị. Vectơ được tạo bằng phương pháp phân rã giá trị suy biến, và độ tin cậy của điểm được ước lượng bằng lấy mẫu lặp. Phương pháp được thiết kế để chạy tốt với kho ngữ liệu cỡ vừa, khoảng mười triệu từ.

Hamilton và cộng sự dùng SentProp để dựng từ điển cảm xúc cho 150 năm tiếng Anh và cho 250 cộng đồng trên diễn đàn Reddit. Họ phát hiện hơn 5 phần trăm số từ có cảm xúc đã đổi hẳn cực tính trong 150 năm đó. Từ terrific là một ví dụ, từ tiêu cực chuyển thành tích cực. Từ soft có điểm khác nhau rõ giữa các cộng đồng.

## Công thức

SentProp dùng đồ thị và lan nhãn, phức tạp hơn một dòng công thức. Dạng đơn giản nhất để hiểu nguyên lý, không phải công thức của SentProp, là lấy trung bình có trọng số điểm của các từ láng giềng đã biết:

```
Điểm của w = tổng của S(w, u) nhân A(u), chia cho tổng của S(w, u)
             với u chạy qua các từ láng giềng đã có điểm
```

| Ký hiệu | Ý nghĩa |
|---|---|
| `w` | Từ chưa có điểm |
| `u` | Một từ láng giềng đã có điểm |
| `S(w, u)` | Độ giống nhau giữa vectơ của w và u |
| `A(u)` | Điểm đã biết của u |
| `Điểm của w` | Điểm suy ra cho từ w, là trung bình điểm các láng giềng có trọng số theo độ giống nhau |

## Ví dụ minh họa

Số dưới đây chỉ để minh họa lỗ hổng trái nghĩa, không phải kết quả thật. Từ "spotless" có ba láng giềng gần nhất:

| Láng giềng | Độ giống nhau | Điểm đã biết |
|---|---|---|
| clean | 0,9 | 2 |
| tidy | 0,8 | 2 |
| dirty | 0,7 | âm 2 |

Nếu chỉ có hai láng giềng đầu, điểm của "spotless" là 2,0. Khi từ trái nghĩa "dirty" lọt vào danh sách, điểm tụt xuống còn 0,83. Từ trái nghĩa kéo điểm về phía trung hòa dù nghĩa thật của "spotless" rất tích cực.

## Cách dùng khi phân tích

1. Huấn luyện vectơ từ trên kho ngữ liệu của lĩnh vực, ví dụ đánh giá khách sạn.
2. Chọn tập từ mẫu nhỏ, ưu tiên từ ít phụ thuộc ngữ cảnh.
3. Dựng đồ thị hoặc danh sách láng giềng, rồi lan điểm.
4. Với phương pháp có độ tin cậy như SentProp, giữ lại từ có độ tin cậy đủ cao và kiểm tra tay một mẫu ngẫu nhiên.
5. Gộp từ điển mở rộng với từ điển gốc, nêu rõ từ nào đến từ nguồn nào.

## Điểm mạnh

- Phủ được những từ chưa có trong từ điển gốc, kể cả từ riêng của một cộng đồng. Hamilton và cộng sự cho biết kết quả của SentProp vượt các phương pháp dựa vào từ điển ngữ nghĩa dựng tay như WordNet.
- Chỉ cần tập từ mẫu nhỏ, và SentProp trả về độ tin cậy cho từng điểm.
- Thích ứng với lĩnh vực và với thời kỳ, như kết quả về 150 năm và 250 cộng đồng.
- Tránh được chi phí và thời gian của việc gán nhãn tay, vốn là điểm Hamilton và cộng sự nêu ra làm động lực.

## Điểm yếu

- Từ trái nghĩa có ngữ cảnh giống nhau nên nằm gần nhau, gây nhiễu khi lan điểm, như Tang và cộng sự đã chỉ ra. Cần vectơ có mục tiêu cảm xúc hoặc phương pháp lan nhãn chịu được nhiễu này.
- Cần kho ngữ liệu đủ lớn và cùng lĩnh vực. Hamilton và cộng sự ghi nhận có phương pháp khác chạy tốt hơn SentProp khi kho rất lớn và dữ liệu huấn luyện dồi dào, nên không có phương pháp tốt nhất cho mọi điều kiện.
- Điểm là điểm suy ra, không do người gán, nên cần kiểm tra mẫu trước khi dùng làm thước đo chính.
- Với tiếng Việt, chất lượng phụ thuộc vào bước tách từ và vào quy mô kho ngữ liệu. Ý này là nhận xét chưa có nguồn.

## Các bài báo nên đọc và dùng để trích dẫn

| Bài | Dùng để trích khi nào |
|---|---|
| Hamilton, Clark, Leskovec & Jurafsky (2016), Inducing Domain-Specific Sentiment Lexicons from Unlabeled Corpora, EMNLP, trang 595 đến 605 | Phương pháp SentProp, từ điển theo lĩnh vực và theo thời kỳ. Nguồn chính |
| Tang, Wei, Yang, Zhou, Liu & Qin (2014), Learning Sentiment-Specific Word Embedding for Twitter Sentiment Classification, ACL | Vấn đề từ trái nghĩa nằm gần nhau và vectơ có mục tiêu cảm xúc |
| Tang, Wei, Qin, Yang, Liu & Zhou (2016), Sentiment Embeddings with Applications to Sentiment Analysis, IEEE Transactions on Knowledge and Data Engineering, tập 28, số 2, trang 496 đến 509 | Bản tạp chí của hướng trên, có thêm ứng dụng dựng từ điển |
