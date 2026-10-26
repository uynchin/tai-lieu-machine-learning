# SenticNet

## 1. SenticNet là gì?

SenticNet là một từ điển cảm xúc dựa trên khái niệm. Nó gán cho mỗi khái niệm một điểm cực tính từ âm một đến dương một, kèm các nhãn cảm xúc và danh sách khái niệm liên quan. Người ta dùng nó để máy tính đánh giá một câu hay một bài review là khen hay chê, kể cả khi cảm xúc không nằm ở một từ đơn mà nằm ở cả cụm.

Điểm khác với hai từ điển trước nằm ở đơn vị tra cứu. [SentiWordNet](bai1.md) gán điểm cho nghĩa của từ. [EmoLex](nrc-emolex.md) gán nhãn cho từ. SenticNet gán điểm cho khái niệm, thường gồm nhiều từ ghép lại, ví dụ "accomplish goal" hay "make good impression". Tác giả chính là Erik Cambria cùng các cộng sự, và hướng nghiên cứu này được gọi là sentic computing.

## Nền tảng: khái niệm và tri thức thường thức

Một khái niệm trong SenticNet là một từ hoặc một cụm từ biểu đạt một ý trọn vẹn. Lý do chọn khái niệm thay cho từ đơn là nhiều cụm mang cảm xúc mà từng từ trong cụm lại trung tính. Ví dụ "go to the dentist" không có từ nào rõ ràng tiêu cực, nhưng nhiều người liên tưởng đến cảm giác khó chịu. Ngược lại "small room" và "small price" có cùng từ "small" nhưng sắc thái hoàn toàn khác nhau.

SenticNet dựa vào tri thức thường thức, tức những điều mà người bình thường mặc nhiên biết về thế giới, ví dụ ăn đồ hỏng thì đau bụng. Nguồn tri thức này đến từ ConceptNet và WordNet Affect. Nhờ vậy khái niệm không có trong danh sách vẫn có thể được suy ra điểm từ các khái niệm có quan hệ gần.

## SenticNet gắn thêm gì vào khái niệm

Với mỗi khái niệm c, SenticNet gắn các thông tin sau:

| Thành phần | Ý nghĩa |
|---|---|
| Cực tính | Nhãn tích cực hoặc tiêu cực |
| Giá trị cực tính | Một số từ âm một đến dương một, càng gần hai đầu thì càng mạnh |
| Nhãn tâm trạng | Một số nhãn cảm xúc cụ thể gắn với khái niệm |
| Bốn chiều cảm xúc | Các điểm trên bốn trục của mô hình đồng hồ cát cảm xúc |
| Khái niệm liên quan | Danh sách khái niệm ngữ nghĩa gần với khái niệm đang xét |

Mô hình đồng hồ cát cảm xúc do Cambria và cộng sự đề xuất, phát triển từ bánh xe của Plutchik. Mô hình chia cảm xúc thành bốn trục độc lập, mỗi trục có mức mạnh khác nhau. Tên bốn trục khác nhau giữa các phiên bản, nên bạn cần xem đúng phiên bản mình dùng trước khi mô tả.

Có ba điểm khác với SentiWordNet và EmoLex. Thứ nhất, điểm cực tính là một số liên tục, nên phân biệt được mức mạnh yếu, điều mà EmoLex không làm được. Thứ hai, đơn vị là khái niệm đa từ, nên phần nào xử lý được ngữ cảnh cục bộ. Thứ ba, mỗi khái niệm có kèm danh sách khái niệm liên quan, nên có thể dùng để giải thích vì sao khái niệm đó mang cực tính ấy.

## Ví dụ minh họa

Các số liệu trong bảng là số tự đặt để minh họa.

| Khái niệm | Cực tính | Giá trị cực tính |
|---|---|---|
| make good impression | tích cực | 0.8 |
| go to the dentist | tiêu cực | âm 0.4 |
| wait in long queue | tiêu cực | âm 0.6 |
| book a room | tích cực | 0.1 |

Ví dụ cho thấy hai điều. Cụm như "wait in long queue" mang cực tính tiêu cực dù từng từ riêng lẻ không rõ ràng như vậy. Cụm như "book a room" gần trung tính, nên giá trị chỉ lệch rất nhẹ về một phía.

## Cách các tác giả xây dựng nó

Từ điển có nhiều phiên bản, và cách xây dựng thay đổi qua từng phiên bản. Dưới đây là mô tả chung nhất:

1. Thu thập tri thức thường thức dạng khái niệm và quan hệ giữa các khái niệm từ ConceptNet, kết hợp với danh sách cảm xúc của WordNet Affect.
2. Biểu diễn các khái niệm trong một không gian nhiều chiều, trong đó khái niệm gần nghĩa nằm gần nhau. Bản đầu dùng phép giảm chiều dựa trên phân rã ma trận để tạo không gian này, gọi là AffectiveSpace.
3. Từ một tập khái niệm đã biết cực tính, suy ra cực tính của các khái niệm lân cận trong không gian.
4. Các bản sau thay dần phần suy luận này bằng mô hình học sâu và khái niệm nguyên thủy. Khái niệm nguyên thủy là những khái niệm cơ bản mà nhiều khái niệm phức tạp khác có thể gom về. Bản 5 dùng mô hình học ngữ cảnh để khám phá các khái niệm này. Bản 6 và 7 kết hợp phần ký hiệu với phần học sâu, với mục tiêu giải thích được kết quả.

Số khái niệm tăng dần qua các bản, từ vài nghìn ở bản đầu lên hàng trăm nghìn ở các bản gần đây.

Điểm cần nhớ là cực tính do thuật toán suy ra từ tri thức thường thức và mô hình, không phải do người gán trực tiếp từng khái niệm. Điểm này giống SentiWordNet và khác EmoLex.

## Các phiên bản chính

| Phiên bản | Năm, nơi công bố | Quy mô và thay đổi chính |
|---|---|---|
| SenticNet 1 | 2010, AAAI Fall Symposium | Khoảng 5.700 khái niệm |
| SenticNet 2 | 2012, FLAIRS | Khoảng 14.000 khái niệm, thêm thông tin ngữ nghĩa và cảm xúc |
| SenticNet 3 | 2014, AAAI | Khoảng 30.000 khái niệm, kết hợp tri thức thường thức và tri thức phổ biến |
| SenticNet 4 | 2016, COLING | Khoảng 50.000 khái niệm, dùng khái niệm nguyên thủy |
| SenticNet 5 | 2018, AAAI | Khoảng 100.000 khái niệm, khám phá khái niệm nguyên thủy bằng mô hình ngữ cảnh |
| SenticNet 6 | 2020, CIKM | Khoảng 200.000 khái niệm, kết hợp phương pháp ký hiệu và học sâu |
| SenticNet 7 | 2022, LREC | Khoảng 300.000 khái niệm, hướng đến khả năng giải thích |

## Cách dùng khi phân tích một câu

Lấy câu "The room was clean but the staff were rude" làm ví dụ. Các điểm dưới đây là số minh họa.

1. Tách từ và gán từ loại cho từng từ.
2. Đưa các từ về dạng gốc.
3. Trích các khái niệm từ câu. Khác với hai từ điển trước, bước này không chỉ lấy từ đơn mà còn tìm các cụm có thể khớp với khái niệm trong danh sách, dựa vào quan hệ cú pháp giữa các từ. Trong ví dụ này có thể trích được "clean room" và "rude staff".
4. Tra giá trị cực tính của từng khái niệm tìm được, như bảng dưới.
5. Gộp lại, ví dụ lấy trung bình hai giá trị. Kết quả là âm 0.05, tức câu gần như trung hòa. Cách gộp do người dùng tự chọn, có thể dùng tổng, trung bình hoặc trọng số theo vị trí.
6. Nếu không tìm thấy khái niệm khớp, người dùng thường quay về tra từng từ đơn.

| Khái niệm | Giá trị cực tính |
|---|---|
| clean room | 0.7 |
| rude staff | âm 0.8 |

## Điểm mạnh

- Đơn vị là khái niệm nên xử lý được nhiều trường hợp mà từ đơn không làm được, như cụm cố định hay cụm mang nghĩa bóng. Đây là động lực chính khi tác giả đề xuất hướng tiếp cận này (Cambria và cộng sự, 2010).
- Có điểm cực tính liên tục, nên biết được mức mạnh yếu. Đây là điểm hơn EmoLex.
- Có kèm khái niệm liên quan, nên giải thích được vì sao một khái niệm được gán cực tính đó. Hướng giải thích được là trọng tâm của các bản gần đây (Cambria và cộng sự, 2022).
- Kết hợp được với luật cú pháp. Poria và cộng sự (2014) đề xuất các mẫu dựa trên phụ thuộc cú pháp để xử lý phủ định và các cấu trúc phức tạp trên nền SenticNet.
- Được dùng làm nguồn tri thức ngoài cho mô hình học sâu. Ma, Peng và Cambria (2018) đưa tri thức thường thức từ SenticNet vào mô hình học sâu cho phân tích cảm xúc theo khía cạnh.
- Có thư viện Python và giao diện lập trình ứng dụng, nên dùng được ngay.

## Điểm yếu

- Cực tính do thuật toán suy ra nên có nhiễu, và có khái niệm được gán điểm chưa hợp lý. Ý này là nhận xét về cách xây dựng, bạn nên đối chiếu với các bài đánh giá độc lập trước khi nêu.
- Độ phủ phụ thuộc vào việc trích khái niệm từ câu. Nếu bước trích khái niệm bỏ sót, câu không có điểm.
- Tập khái niệm chủ yếu là tiếng Anh. Với tiếng Việt, bạn phải dịch dữ liệu sang tiếng Anh trước hoặc dùng bản dịch, và cả hai cách đều có thể làm sai lệch sắc thái.
- Các phiên bản khác nhau về quy mô, cấu trúc và nhãn đi kèm. Nếu không ghi rõ phiên bản, người khác khó lặp lại kết quả của bạn.
- Điểm gán cho khái niệm chung chứ không riêng cho lĩnh vực nào. Một khái niệm có thể mang sắc thái khác trong đánh giá khách sạn và trong tin tức. Ý này là nhận xét về cách dùng.
- Hutto và Gilbert (2014) nhận xét các từ điển loại này thiếu đặc trưng của mạng xã hội như từ lóng và biểu tượng cảm xúc. Bạn nên đối chiếu với bài gốc xem họ có nhắc riêng SenticNet hay không trước khi trích.
