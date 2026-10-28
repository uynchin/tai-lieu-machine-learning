# So sánh sáu từ điển cảm xúc: EmoLex, SentiWordNet, SenticNet, AFINN, LIWC và MPQA

## 0. Phạm vi và lưu ý

Trang này so sánh sáu công cụ, gồm EmoLex và năm công cụ còn lại. Nhận định về khả năng thay thế là đánh giá dựa trên đặc điểm từng công cụ, không trích từ một bài báo cụ thể. Đặc điểm từng công cụ lấy từ các phần mô tả riêng, chưa tra lại nguồn gốc.

Trang riêng của từng công cụ: [SentiWordNet](bai1.md), [EmoLex](nrc-emolex.md), [SenticNet](senticnet.md), [AFINN](afinn.md), [MPQA](mpqa.md).

## 1. Ba trục để phân loại

Câu hỏi thứ nhất là công cụ trả lời câu hỏi gì. SentiWordNet, SenticNet, AFINN và MPQA xoay quanh việc khen hay chê, và MPQA thêm lớp từ này có mang ý kiến hay không. EmoLex trả lời khen hay chê vì cảm xúc gì, trong tám cảm xúc cơ bản. LIWC trả lời rộng nhất: người viết nghĩ gì, nói về ai và viết theo kiểu nào.

Câu hỏi thứ hai là đơn vị tra cứu. AFINN, EmoLex, MPQA và LIWC tra theo từ. SentiWordNet tra theo nghĩa của từ. SenticNet tra theo khái niệm, thường là cụm nhiều từ.

Câu hỏi thứ ba là ai gán nhãn. AFINN do một người gán. EmoLex do nhiều người gán qua nền tảng thuê việc trực tuyến. LIWC do nhóm người xây dựng và kiểm định. MPQA kết hợp người và thuật toán. SentiWordNet và SenticNet chủ yếu do thuật toán suy ra.

## 2. Bảng tổng hợp

Bảng thứ nhất so sánh bản chất của từng công cụ.

| Tiêu chí | EmoLex | SentiWordNet | SenticNet |
|---|---|---|---|
| Câu hỏi chính | Từ này gợi cảm xúc nào | Nghĩa này tích cực hay tiêu cực đến đâu | Khái niệm này tích cực hay tiêu cực đến đâu |
| Đơn vị tra cứu | Từ | Nghĩa của từ | Khái niệm đa từ |
| Đầu ra | Mười nhãn nhị phân, tám cảm xúc và hai cực tính | Ba điểm tích cực, tiêu cực, khách quan có tổng bằng 1 | Giá trị từ âm 1 đến dương 1, kèm nhãn tâm trạng |
| Ai gán nhãn | Nhiều người | Thuật toán | Thuật toán và tri thức thường thức |
| Cảm xúc cụ thể | Có, tám cảm xúc | Không | Có, nhãn tâm trạng và các chiều cảm xúc |
| Cường độ | Không, chỉ có hoặc không | Có, thang liên tục | Có, thang liên tục |
| Xử lý nghĩa và ngữ cảnh | Không | Theo nghĩa, nhưng phải tự chọn nghĩa | Theo cụm khái niệm |
| Mức công khai | Miễn phí cho nghiên cứu | Miễn phí | Miễn phí, có thư viện |

Bảng thứ hai so sánh ba công cụ còn lại.

| Tiêu chí | AFINN | LIWC | MPQA |
|---|---|---|---|
| Câu hỏi chính | Từ này tích cực hay tiêu cực đến đâu | Văn bản chứa bao nhiêu phần trăm từ thuộc nhóm tâm lý nào | Từ này có mang ý kiến không, nếu có thì khen hay chê |
| Đơn vị tra cứu | Từ | Từ, có ký tự thay thế ở cuối | Từ kèm từ loại |
| Đầu ra | Số nguyên từ âm 5 đến dương 5 | Tỷ lệ phần trăm theo từng nhóm | Nhãn độ mạnh chủ quan và nhãn cực tính trước |
| Ai gán nhãn | Một người | Nhóm người, có kiểm định | Hỗn hợp người và thuật toán |
| Cảm xúc cụ thể | Không | Có vài nhóm như lo lắng, giận dữ, buồn bã | Không |
| Cường độ | Có, mười một mức | Không áp dụng, kết quả là tỷ lệ | Chỉ hai mức |
| Xử lý nghĩa và ngữ cảnh | Không | Không | Có từ loại và có khái niệm cực tính trước |
| Mức công khai | Miễn phí | Trả phí, từ điển không công khai | Miễn phí cho nghiên cứu |

Về quy mô, SenticNet lớn nhất và tăng qua các bản. EmoLex khoảng vài chục nghìn mục nếu tính cả các từ không mang nhãn nào, và con số này là gần đúng. AFINN, LIWC và MPQA đều ở mức vài nghìn mục. Cần kiểm lại con số chính xác trong tệp dữ liệu.

## 3. Ưu nhược điểm từng công cụ

### EmoLex

Ưu điểm là phủ tám cảm xúc cộng hai cực tính trong một danh sách, nhãn do người gán có kiểm soát chất lượng, công khai và có bản dịch nhiều ngôn ngữ. Nhược điểm là nhãn chỉ có hoặc không nên không có cường độ, bỏ qua phủ định và ngữ cảnh, và bản dịch tiếng Việt tạo bằng dịch máy nên có từ sai.

### SentiWordNet

Ưu điểm là điểm gắn với nghĩa, có thang liên tục và có điểm khách quan để tách từ trung tính khỏi từ mang ý kiến. Nhược điểm là điểm do thuật toán gán nên có nhiễu, và muốn dùng đúng phải chọn nghĩa của từ trong ngữ cảnh, bước dễ sai nhất.

### SenticNet

Ưu điểm là xử lý được cụm mang cảm xúc mà từng từ riêng lẻ lại trung tính, có điểm liên tục và có danh sách khái niệm liên quan để giải thích. Nhược điểm là phụ thuộc vào bước trích khái niệm từ câu, điểm do thuật toán suy ra, và các phiên bản khác nhau nhiều nên khó lặp lại nếu không ghi rõ bản.

### AFINN

Ưu điểm là đơn giản và minh bạch, mỗi từ chỉ có một số, có cường độ và thiết kế cho văn bản ngắn trên mạng xã hội. Nhược điểm là danh sách nhỏ, điểm do một người gán nên có thể lệch theo cá nhân, không xét ngữ cảnh và không có cảm xúc cụ thể.

### LIWC

Ưu điểm là phủ nhiều khía cạnh tâm lý và ngôn ngữ, được kiểm định đo lường bài bản và đếm cả từ chức năng. Nhược điểm là trả phí, từ điển không công khai, bỏ qua phủ định và ngữ cảnh, và số nhóm quá nhiều dễ cho kết quả có ý nghĩa thống kê chỉ do ngẫu nhiên.

### MPQA

Ưu điểm là tách được tính chủ quan khỏi cực tính, có thông tin từ loại và công khai. Nhược điểm là chỉ có hai mức độ mạnh, không có cảm xúc cụ thể, chất lượng nhãn không đồng đều do nguồn gốc hỗn hợp, và xây dựng chủ yếu từ văn bản tin tức.

## 4. Có thay thế nhau được không

Câu trả lời phụ thuộc vào việc cần công cụ làm việc gì. Có thể chia thành ba mức.

### Mức một: chỉ cần biết khen hay chê

Cả sáu công cụ đều cho được thông tin này, nên về nguyên tắc thay thế được cho nhau. EmoLex làm được qua hai nhãn tích cực và tiêu cực, LIWC làm được qua hai nhóm cảm xúc tương ứng. Đầu ra có thang khác nhau:

| Công cụ | Dạng đầu ra cực tính |
|---|---|
| EmoLex | Đếm từ có nhãn tích cực và từ có nhãn tiêu cực |
| SentiWordNet | Số thực từ 0 đến 1, tính hiệu của điểm tích cực và tiêu cực |
| SenticNet | Số thực từ âm 1 đến dương 1 |
| AFINN | Số nguyên từ âm 5 đến dương 5 |
| LIWC | Tỷ lệ phần trăm của nhóm tích cực và nhóm tiêu cực |
| MPQA | Nhãn, đếm số từ mỗi loại |

Muốn thay thế phải quy về cùng một thang. Cách đơn giản nhất là đưa tất cả về ba nhãn tích cực, tiêu cực và trung tính dựa trên dấu của điểm tổng. Cách này mất thông tin về cường độ nhưng cho phép so sánh công bằng.

### Mức hai: cần biết cảm xúc cụ thể

Ba công cụ làm được là EmoLex, SenticNet và LIWC, nhưng mỗi công cụ cho kết quả khác nhau.

| Công cụ | Cảm xúc cụ thể | Điểm cần lưu ý |
|---|---|---|
| EmoLex | Tám cảm xúc theo mô hình Plutchik | Chỉ có hoặc không, không có cường độ |
| SenticNet | Nhãn tâm trạng và các chiều cảm xúc | Tên các chiều khác nhau giữa các phiên bản |
| LIWC | Vài nhóm như lo lắng, giận dữ, buồn bã | Ít loại hơn EmoLex, nhưng là tỷ lệ phần trăm |

Trong ba công cụ này, EmoLex là lựa chọn gọn nhất và dễ trích dẫn nhất vì có nền tảng lý thuyết rõ, công khai và đủ tám cảm xúc. SenticNet hơn ở cường độ. LIWC hơn ở các nhóm đi kèm nhưng bị hạn chế vì trả phí. Ba công cụ còn lại chỉ có cực tính nên không thay thế được ở mức này.

### Mức ba: cần thông tin ngoài cảm xúc

Chỉ LIWC làm được, ví dụ đo đại từ ngôi thứ nhất, định hướng thời gian hay quá trình nhận thức. Ngược lại LIWC không thay thế MPQA ở việc lọc tính chủ quan, hay SentiWordNet ở việc tách điểm khách quan.

### Chiều thay thế

Thay thế chỉ đi một chiều một cách tự nhiên. Công cụ nhiều thông tin có thể rút gọn thành công cụ ít thông tin. Ví dụ lấy hiệu điểm tích cực và tiêu cực của SentiWordNet ra một số duy nhất thì có dạng gần giống AFINN. Hai nhãn tích cực và tiêu cực của EmoLex rút gọn được thành cực tính nhị phân. Ngược lại AFINN không mở rộng được thành SentiWordNet vì thiếu thông tin về nghĩa, và cũng không mở rộng được thành EmoLex vì thiếu nhãn cảm xúc.

### Lưu ý quan trọng

Thay thế được về hình thức không có nghĩa là cho cùng kết quả. Cùng một văn bản, các từ điển có thể cho cực tính khác nhau vì nguồn gốc, độ phủ và cách gán khác nhau. Nếu đổi công cụ giữa chừng, nên gán tay một mẫu nhỏ rồi tính mức đồng thuận giữa từng công cụ với mẫu đó để chọn công cụ hợp nhất.

## 5. Cách kết hợp thay vì chọn một

Vì mỗi công cụ mạnh ở một việc khác nhau, nhiều nghiên cứu dùng kết hợp. Một số hướng hợp lý:

1. MPQA lọc các đoạn có ý kiến trước, sau đó AFINN hoặc SenticNet chấm cực tính trên các đoạn đã lọc.
2. AFINN hoặc SenticNet cho cực tính, EmoLex cho biết cảm xúc cụ thể đứng sau cực tính đó. Cách này cho phép nói đánh giá tiêu cực chủ yếu vì giận dữ hay vì buồn bã.
3. LIWC bổ sung các nhóm tâm lý và ngôn ngữ để giải thích vì sao đánh giá nghiêng về phía đó.
4. Dùng nhiều công cụ cùng lúc rồi lấy kết quả chung, hoặc đưa tất cả làm đặc trưng cho mô hình học máy.

Khi kết hợp, cần nêu rõ cách gộp và cách xử lý trường hợp các công cụ bất đồng.

## 6. Gợi ý chọn theo nhu cầu

| Nhu cầu | Công cụ nên cân nhắc trước |
|---|---|
| Cần nhanh, đơn giản, dễ giải thích | AFINN |
| Cần biết cảm xúc cụ thể, công khai, dễ trích dẫn | EmoLex |
| Cần cực tính theo nghĩa, chấp nhận thêm bước chọn nghĩa | SentiWordNet |
| Cần xử lý cụm từ và có giải thích | SenticNet |
| Cần tách ý kiến khỏi sự việc trước khi chấm | MPQA |
| Cần phân tích tâm lý, phong cách viết, không chỉ cảm xúc | LIWC |
