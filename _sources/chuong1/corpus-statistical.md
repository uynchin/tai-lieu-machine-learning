# Thống kê: PMI và đồng xuất hiện

## Là gì?

Hướng này không dùng từ điển cảm xúc có sẵn. Người làm chọn vài từ mẫu mà ai cũng đồng ý là tích cực hoặc tiêu cực, rồi đếm trong một kho ngữ liệu lớn xem mỗi từ khác hay đi cùng nhóm nào. Từ nào hay xuất hiện cùng từ mẫu tích cực thì được gán điểm dương, từ nào hay đi cùng từ mẫu tiêu cực thì được gán điểm âm. Điểm là số thực, nên có cả hướng lẫn độ mạnh.

## Nền tảng

Hatzivassiloglou và McKeown năm 1997 đặt viên gạch đầu tiên. Họ chỉ ra rằng hai tính từ nối nhau bằng "và" thường cùng hướng cảm xúc, còn khi nối bằng "nhưng" thì thường trái hướng. Mô hình của họ đoán đúng 82 phần trăm số cặp khi xét từng liên từ riêng lẻ, và độ chính xác phân loại vượt 90 phần trăm với tính từ xuất hiện trong một số vừa phải liên từ. Bộ thử gồm 1.336 tính từ, trong đó 657 tích cực và 679 tiêu cực.

Turney và Littman năm 2003 bỏ điều kiện chỉ xét tính từ nối nhau. Họ suy hướng cảm xúc của một từ từ mức liên hệ thống kê giữa từ đó với một tập từ mẫu, và thử hai độ đo là thông tin tương hỗ điểm và phân tích ngữ nghĩa ẩn. Bộ thử có 3.596 từ do người gán nhãn, gồm 1.614 từ tích cực và 1.982 từ tiêu cực. Độ chính xác trên toàn bộ là 82,8 phần trăm, và vượt 95 phần trăm khi cho phép thuật toán bỏ qua các từ có cảm xúc nhẹ. Cơ sở lý thuyết là ý của Firth năm 1957 rằng nghĩa của một từ thể hiện qua những từ đứng cùng nó.

Mohammad, Kiritchenko và Zhu năm 2013 áp dụng cùng ý tưởng cho bài đăng mạng xã hội, nhưng lấy nhãn từ thẻ bắt đầu bằng dấu thăng và từ biểu tượng cảm xúc thay cho từ mẫu. Từ điển thẻ của họ có 54.129 từ đơn và 316.531 cặp hai từ. Từ điển Sentiment140 dùng kho 1,6 triệu bài đăng của Go và cộng sự năm 2009, gán nhãn theo biểu tượng cảm xúc trong bài.

## Công thức

Thông tin tương hỗ điểm giữa hai đối tượng đo mức hai đối tượng đi cùng nhau nhiều hơn mức ngẫu nhiên:

```
PMI(w, v) = log [ P(w, v) / ( P(w) × P(v) ) ]
```

| Ký hiệu | Ý nghĩa |
|---|---|
| `w` | Từ cần chấm |
| `v` | Một từ mẫu hoặc một nhóm nhãn |
| `P(w, v)` | Xác suất w và v xuất hiện cùng nhau |
| `P(w)`, `P(v)` | Xác suất mỗi bên xuất hiện riêng |
| `PMI(w, v)` | Mức w và v đi cùng nhau nhiều hơn mức ngẫu nhiên, dương nếu đi cùng nhiều hơn dự kiến |

Độ lệch hướng cảm xúc của Turney và Littman:

```
Điểm của w = tổng PMI của w với các từ mẫu tích cực
             trừ tổng PMI của w với các từ mẫu tiêu cực
```

Mohammad và cộng sự dùng dạng tương tự trên hai nhóm bài đăng đã gắn nhãn tự động:

```
Điểm của w = PMI của w với nhóm tích cực trừ PMI của w với nhóm tiêu cực
```

| Ký hiệu | Ý nghĩa |
|---|---|
| `Điểm của w` | Điểm cảm xúc của từ w. Dương là liên hệ với tích cực, âm là liên hệ với tiêu cực, độ lớn cho biết mức liên hệ |

Khi w chưa từng đi cùng nhóm nào thì xác suất chung bằng 0 và PMI nhận giá trị âm vô cực, nên cần xử lý riêng.

## Ví dụ minh họa

Các số dưới đây chỉ để minh họa, không lấy từ nghiên cứu nào. Giả sử có 10.000 đánh giá, trong đó 5.000 đánh giá được gán nhãn tích cực và 5.000 được gán nhãn tiêu cực bằng từ mẫu.

| Từ | Số đánh giá chứa từ | Trong nhóm tích cực | Trong nhóm tiêu cực | PMI với tích cực | PMI với tiêu cực | Điểm |
|---|---|---|---|---|---|---|
| spotless | 200 | 180 | 20 | 0,848 | âm 2,322 | 3,170 |
| noisy | 120 | 30 | 90 | âm 1,000 | 0,585 | âm 1,585 |
| lobby | 200 | 100 | 100 | 0 | 0 | 0 |

Logarit lấy cơ số 2. Từ "lobby" xuất hiện đều ở hai nhóm nên điểm bằng 0, đúng với một từ chỉ vị trí không mang cảm xúc.

Một ví dụ thật nằm trong bài trình bày của Mohammad, Kiritchenko và Zhu. Cụm "unpredictable story" có điểm 0,4 còn cụm "unpredictable steering" có điểm âm 0,7. Cùng một từ nhưng điểm đổi theo từ đi kèm, và đó là lý do từ điển loại này có cả cặp hai từ.

## Cách dùng khi phân tích

1. Chọn kho ngữ liệu cùng lĩnh vực với dữ liệu cần chấm.
2. Chọn nguồn nhãn: từ mẫu, thẻ bắt đầu bằng dấu thăng, hoặc biểu tượng cảm xúc.
3. Đếm số lần mỗi từ xuất hiện trong từng nhóm.
4. Tính điểm theo công thức, có làm trơn số đếm để tránh giá trị âm vô cực.
5. Dùng điểm như một từ điển cảm xúc thông thường, rồi cộng hoặc lấy trung bình theo văn bản.

## Điểm mạnh

- Chỉ cần tập từ mẫu nhỏ, không cần người gán nhãn cho từng từ. Đây là điểm cốt lõi của bài Turney và Littman.
- Điểm có độ mạnh, không chỉ có hướng.
- Từ điển phản ánh đúng lĩnh vực của kho ngữ liệu. Hamilton và cộng sự năm 2016 lưu ý rằng từ điển tổng quát có thể làm sai lệch phân tích ở lĩnh vực riêng.
- Có thể tạo mục cho cụm hai từ, như kết quả của Mohammad và cộng sự.

## Điểm yếu

- Kết quả phụ thuộc vào từ mẫu và vào kho ngữ liệu. Đổi từ mẫu có thể đổi điểm.
- Nhãn tự động có thể sai. Một bài đăng có biểu tượng cười vẫn có thể chê, nên điểm của từ chịu nhiễu từ nhãn. Ý này là suy luận từ cách xây dựng.
- Độ chính xác ở mức từ không tuyệt đối. Turney và Littman báo cáo 82,8 phần trăm trên toàn bộ, tức vẫn còn khoảng một phần sáu số từ bị gán sai hướng.
- Từ hiếm cho số đếm nhỏ nên điểm kém ổn định, và từ chưa từng đi cùng nhóm nào cho giá trị không xác định.

## Các bài báo nên đọc và dùng để trích dẫn

| Bài | Dùng để trích khi nào |
|---|---|
| Hatzivassiloglou & McKeown (1997), Predicting the Semantic Orientation of Adjectives, ACL, trang 174 đến 181 | Ý tưởng dùng liên từ để suy hướng cảm xúc của tính từ |
| Turney & Littman (2003), Measuring Praise and Criticism: Inference of Semantic Orientation from Association, ACM Transactions on Information Systems, tập 21, số 4, trang 315 đến 346 | Phương pháp độ lệch hướng cảm xúc theo thông tin tương hỗ điểm, tên gọi trong bài gốc là SO-PMI. Nguồn chính |
| Mohammad, Kiritchenko & Zhu (2013), NRC-Canada: Building the State-of-the-Art in Sentiment Analysis of Tweets, SemEval 2013 | Dựng từ điển từ thẻ và biểu tượng cảm xúc trên bài đăng mạng xã hội |
