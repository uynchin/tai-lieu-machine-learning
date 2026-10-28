# MPQA Subjectivity Lexicon

## 1. MPQA Subjectivity Lexicon là gì?

MPQA Subjectivity Lexicon là một từ điển cho biết mỗi từ tiếng Anh có mang ý kiến chủ quan hay không, mạnh hay yếu, và nếu có thì nghiêng về tích cực hay tiêu cực. Người ta dùng nó để máy tính nhận ra những đoạn văn đang bày tỏ quan điểm, rồi mới xét quan điểm đó khen hay chê, mà không cần ai đọc và chấm tay.

Điểm khác với năm từ điển trước nằm ở việc nó tách riêng hai câu hỏi. Câu hỏi thứ nhất là từ này có mang ý kiến hay chỉ nêu sự việc. Câu hỏi thứ hai là nếu có ý kiến thì khen hay chê. Các từ điển trước chủ yếu chỉ trả lời câu hỏi thứ hai. Tên MPQA lấy từ dự án Multi-Perspective Question Answering, một dự án về nhận diện ý kiến và quan điểm trong văn bản. Danh sách này do nhóm của Theresa Wilson, Janyce Wiebe và Paul Hoffmann xây dựng, gắn với Đại học Pittsburgh. Nó cũng thường được gọi là danh sách OpinionFinder, vì được dùng trong hệ thống OpinionFinder.

## Nền tảng: chủ quan và khách quan

Trong ngôn ngữ học tính toán, một câu chủ quan là câu thể hiện trạng thái bên trong của người viết như cảm xúc, đánh giá, niềm tin hay suy đoán. Một câu khách quan là câu nêu sự việc có thể kiểm chứng. Ví dụ "Khách sạn có 50 phòng" là khách quan, còn "Khách sạn này tuyệt vời" là chủ quan.

Wiebe và cộng sự cho rằng nên nhận diện tính chủ quan trước, vì nếu một đoạn không mang ý kiến thì việc chấm điểm cực tính cho nó dễ gây nhiễu. Ý tưởng này cũng gần với điểm khách quan Obj trong [SentiWordNet](bai1.md), nhưng MPQA áp dụng ở mức từ và gắn thêm độ mạnh.

## MPQA gắn thêm gì vào từ

Với mỗi mục từ w, danh sách gắn các thông tin sau:

| Thành phần | Ý nghĩa |
|---|---|
| Độ mạnh chủ quan | Mạnh hoặc yếu |
| Từ loại | Danh từ, động từ, tính từ, trạng từ hoặc bất kỳ |
| Có rút gốc hay không | Cho biết mục từ có khớp với các dạng chia của từ hay không |
| Cực tính trước | Tích cực, tiêu cực, trung tính, hoặc cả hai |

Độ mạnh chủ quan chia hai mức. Từ chủ quan mạnh là từ gần như luôn mang ý kiến dù ở ngữ cảnh nào. Từ chủ quan yếu là từ chỉ đôi khi mang ý kiến, tùy ngữ cảnh. Cực tính trước là cực tính mà từ thường mang khi đứng riêng, chưa xét ngữ cảnh, nên gọi là prior polarity.

Có bốn điểm khác với các từ điển trước. Thứ nhất, danh sách có thông tin từ loại, nên phần nào phân biệt được cùng một từ khi làm danh từ và khi làm tính từ. Thứ hai, độ mạnh là hai mức chứ không phải thang liên tục, nên thô hơn [AFINN](afinn.md). Thứ ba, cực tính có giá trị trung tính, nghĩa là từ có thể mang ý kiến nhưng không nghiêng khen hay chê. Thứ tư, danh sách có giá trị cả hai, dành cho từ có thể khen hoặc chê tùy ngữ cảnh.

## Ví dụ minh họa

Các mục từ dưới đây chỉ để minh họa, không phải dòng thật trong tệp. Cần tra trực tiếp trong tệp dữ liệu trước khi dùng.

| Từ | Độ mạnh chủ quan | Từ loại | Cực tính trước |
|---|---|---|---|
| excellent | mạnh | tính từ | tích cực |
| terrible | mạnh | tính từ | tiêu cực |
| decent | yếu | tính từ | tích cực |
| room | không có trong danh sách | | |

Ví dụ cho thấy "excellent" và "decent" cùng tích cực nhưng khác độ mạnh chủ quan. Từ chỉ sự vật thông thường như "room" không có trong danh sách, vì nó không mang ý kiến.

## Cách các tác giả xây dựng nó

Mô tả chung nhất như sau:

1. Thu thập các từ gợi ý chủ quan từ nhiều nguồn. Một phần đến từ danh sách do Riloff và Wiebe xây dựng bằng phương pháp tự học từ văn bản. Một phần lấy từ danh sách General Inquirer. Một phần do chính các tác giả bổ sung thủ công.
2. Phân loại từng từ theo độ mạnh chủ quan, dựa trên việc từ đó xuất hiện trong văn bản đã được người đọc gán nhãn là chủ quan nhiều hay ít.
3. Gán cực tính trước. Phần lớn do người gán, một phần suy ra bằng thuật toán từ các nguồn có sẵn.
4. Công bố danh sách kèm công cụ OpinionFinder.

Điểm cần nhớ là danh sách này kết hợp nhiều nguồn và nhiều cách gán, cả thủ công lẫn tự động, nên chất lượng không hoàn toàn đồng đều. Cần đối chiếu mô tả chi tiết với bài gốc trước khi viết vào phần phương pháp.

## Một điểm hay nhầm: danh sách khác với kho văn bản

Tên MPQA còn chỉ một kho văn bản tin tức đã được người đọc gán nhãn ý kiến và quan điểm, gọi là MPQA Opinion Corpus. Từ điển và kho văn bản là hai tài nguyên khác nhau, dù cùng nhóm tác giả và cùng dự án. Khi viết bài, cần ghi rõ đang dùng cái nào, và trích đúng bài tương ứng.

## Cách dùng khi phân tích một câu

Lấy câu "The room was clean but the staff were rude" làm ví dụ. Các giá trị dưới đây chỉ để minh họa.

1. Tách từ và gán từ loại, vì danh sách có thông tin từ loại.
2. Đưa về dạng gốc nếu mục từ yêu cầu.
3. Tra từng từ trong danh sách, như bảng dưới.
4. Đếm số từ tích cực và số từ tiêu cực, có thể trọng số theo độ mạnh. Ví dụ tính từ mạnh là 2 và từ yếu là 1. Khi đó điểm tích cực là 1 và điểm tiêu cực là 2, tổng là âm 1, câu hơi nghiêng về tiêu cực.

| Từ | Độ mạnh chủ quan | Cực tính trước |
|---|---|---|
| clean | yếu | tích cực |
| rude | mạnh | tiêu cực |
| room, staff, các từ còn lại | không có trong danh sách | |

Cách trọng số do người dùng tự chọn và cần nêu rõ trong phần phương pháp. Danh sách này thường được dùng theo cách đếm, chứ không cho điểm số thực, nên đầu ra thô hơn AFINN.

## Điểm mạnh

- Tách được tính chủ quan khỏi cực tính, nên lọc được các đoạn không mang ý kiến trước khi phân tích cảm xúc (Wilson, Wiebe và Hoffmann, 2005).
- Có thông tin từ loại, nên phân biệt được một phần các cách dùng khác nhau của cùng một từ.
- Có khái niệm cực tính trước, nghĩa là các tác giả thừa nhận rõ cực tính của từ có thể thay đổi theo ngữ cảnh. Đây chính là động lực của bài Wilson và cộng sự (2005).
- Công khai và miễn phí cho nghiên cứu, nên dễ lặp lại kết quả.
- Được dùng rộng rãi làm đặc trưng và mốc so sánh. Hutto và Gilbert (2014) đưa nhóm từ điển này vào các phương pháp đối chứng, nhưng cần đối chiếu bài gốc để xác nhận có nhắc riêng danh sách MPQA hay không.
- Có trong nhiều gói phần mềm, gồm hàm get_sentiments của gói tidytext trong R ở một số cấu hình. Cần kiểm tra tài liệu của gói trước khi nêu.

## Điểm yếu

- Danh sách chỉ có hai mức độ mạnh và không có thang liên tục, nên khó so sánh mức khen chê giữa các từ. Ý này là nhận xét về cách dùng.
- Cực tính trước không xét ngữ cảnh, nên phủ định và mỉa mai vẫn bị bỏ qua nếu dùng đơn giản bằng cách đếm. Wilson và cộng sự (2005) nêu rõ rằng cực tính ngữ cảnh có thể khác cực tính trước, và họ xây mô hình riêng để xử lý điều này.
- Nguồn gốc hỗn hợp nên chất lượng nhãn không đồng đều. Ý này là nhận xét về cách xây dựng, cần đối chiếu với bài gốc.
- Không có nhãn cảm xúc cụ thể như giận dữ hay buồn bã, chỉ có cực tính.
- Chủ yếu là tiếng Anh, và được xây dựng từ văn bản tin tức. Với tiếng Việt, cần dịch trước hoặc dùng bản dịch, và cả hai cách đều có thể làm lệch sắc thái. Ý này là nhận xét về cách dùng.
- Nguồn tin tức có thể không hợp với đánh giá khách sạn, nơi người viết dùng ngôn ngữ đời thường hơn. Ý này là nhận xét về cách dùng, cần cân nhắc khi nêu trong phần bàn luận.

## Các bài báo nên đọc và dùng để trích dẫn

| Bài | Dùng để trích khi nào |
|---|---|
| Wilson, Wiebe & Hoffmann (2005), Recognizing Contextual Polarity in Phrase-Level Sentiment Analysis, HLT/EMNLP | Mô tả danh sách, khái niệm cực tính trước và cực tính ngữ cảnh. Đây là nguồn chính |
| Wilson, Wiebe & Hoffmann (2009), Recognizing Contextual Polarity: An Exploration of Features for Phrase-Level Sentiment Analysis, Computational Linguistics | Bản mở rộng đầy đủ hơn của bài trên |
| Wiebe, Wilson & Cardie (2005), Annotating Expressions of Opinions and Emotions in Language, Language Resources and Evaluation | Mô tả kho văn bản MPQA và cách gán nhãn |
| Riloff & Wiebe (2003), Learning Extraction Patterns for Subjective Expressions, EMNLP | Nguồn gốc một phần các từ chủ quan trong danh sách |
| Wilson và cộng sự (2005), OpinionFinder: A System for Subjectivity Analysis, HLT/EMNLP Demonstrations | Hệ thống phần mềm dùng danh sách này |

## Lưu ý khi trích dẫn

Thông tin xuất bản, nguồn gốc các từ và cách gán nhãn trong trang này chưa được tra lại trực tiếp. Tên các cột trong tệp dữ liệu và số lượng mục cũng cần đối chiếu với tệp tải về. Trước khi đưa vào danh mục tài liệu tham khảo, cần kiểm tra tên bài, năm, nơi đăng trên Google Scholar hoặc trang của nhóm tác giả.
