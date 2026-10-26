# Lexicon Based

## Tài nguyên từ vựng có sẵn

### Nhóm này đo cái gì

Các từ điển cảm xúc không tự phân tích câu. Chúng chỉ cung cấp một bảng tra, trong đó mỗi từ hoặc khái niệm tương ứng với một điểm hoặc một nhãn. Phương pháp phân tích nằm ở cách tra bảng rồi gộp điểm. Vì vậy khi dùng nhóm này, câu hỏi cần giữ là điểm cuối cùng phản ánh cảm xúc của người viết, hay chỉ phản ánh việc văn bản chứa nhiều từ mà từ điển đã gán nhãn.

### Quy trình chung của mọi từ điển

Câu minh họa: "The room was not very clean, but the staff were wonderful!"

| Bước | Hành động | Kết quả trên câu minh họa |
|---|---|---|
| 1 | Tách từ, đưa về chữ thường, có thể đưa về dạng gốc | the, room, was, not, very, clean, but, the, staff, were, wonderful |
| 2 | Tra từng từ trong từ điển | "clean" và "wonderful" có điểm dương. "not", "very", "but" thường không có điểm trong từ điển thuần |
| 3 | Gộp điểm các từ tìm thấy | Có hai từ dương và không có từ âm, nên kết quả là dương |
| 4 | Chuẩn hoá theo độ dài văn bản, bước này không bắt buộc | Chia tổng điểm cho số từ |

Công thức gộp điểm phổ biến nhất:

```
Điểm của d = tổng của s(w), với mọi từ w trong văn bản d
```

| Ký hiệu | Ý nghĩa |
|---|---|
| `d` | Văn bản cần chấm, có thể là câu, bình luận hoặc bài báo |
| `w` | Một từ trong văn bản d |
| `s(w)` | Điểm của từ w trong từ điển, bằng không nếu từ không có trong từ điển |
| `Điểm của d` | Điểm cảm xúc của cả văn bản |

Ở câu minh họa, người đọc hiểu là người viết chê phòng nhưng khen nhân viên. Từ điển thuần chỉ thấy "clean" và "wonderful", cả hai đều dương. Phủ định trong "not very clean" và chuyển hướng bởi "but" đều bị bỏ qua. Đây là hạn chế chung của cả nhóm, và là lý do VADER bổ sung các quy tắc ngữ cảnh. Taboada và cộng sự năm 2011, đăng trên tạp chí Computational Linguistics, nhấn mạnh rằng chất lượng từ điển cùng cách xử lý phủ định và từ nhấn mạnh quyết định độ chính xác của hướng tiếp cận này.

## Các từ điển cảm xúc thường dùng

| Từ điển | Cách gán nhãn | Phù hợp với |
|---|---|---|
| AFINN, Nielsen 2011 | Điểm nguyên từ âm năm đến dương năm cho từng từ | Văn bản ngắn trên mạng xã hội |
| Bing Liu, Hu và Liu 2004 | Hai danh sách từ dương và từ âm, không có mức độ | Bình luận về sản phẩm và dịch vụ |
| NRC, Mohammad và Turney 2013 | Tám cảm xúc cơ bản gồm vui, giận, sợ, buồn, tin tưởng, ghê tởm, ngạc nhiên, mong đợi, cùng hai nhãn dương và âm | Bài toán cần phân loại cảm xúc chi tiết hơn hai cực |
| [SentiWordNet](bai1.md), Baccianella và cộng sự 2010 | Điểm dương, âm, trung tính theo từng nghĩa của từ | Khi cần phân biệt nghĩa của từ đa nghĩa |
| VADER, Hutto và Gilbert 2014 | Điểm liên tục từ âm bốn đến dương bốn, kèm quy tắc về ngữ cảnh | Văn bản ngắn, không chính thức |
| Loughran và McDonald 2011 | Từ điển riêng cho báo cáo tài chính | Văn bản kinh tế và tài chính |

Một từ có thể mang nghĩa khác nhau giữa các lĩnh vực. Từ "liability" là trung tính trong đời sống nhưng mang nghĩa tiêu cực trong báo cáo tài chính. Vì vậy từ điển chung chỉ nên dùng cho văn bản chung. Dữ liệu chuyên ngành cần từ điển riêng hoặc phải chỉnh lại từ điển có sẵn.

## Các quy tắc xử lý ngữ cảnh

Từ điển thuần chỉ cộng điểm từng từ, nên cần thêm các quy tắc sau để giảm sai lệch. VADER là từ điển áp dụng nhiều quy tắc trong số này.

| Hiện tượng | Cách xử lý | Ví dụ |
|---|---|---|
| Phủ định | Đảo dấu hoặc giảm điểm của từ cảm xúc nằm trong khoảng ba từ sau từ phủ định | "không sạch" tính là âm |
| Từ nhấn mạnh | Nhân điểm với hệ số lớn hơn một | "rất sạch" có điểm cao hơn "sạch" |
| Từ giảm nhẹ | Nhân điểm với hệ số nhỏ hơn một | "hơi sạch" có điểm thấp hơn "sạch" |
| Từ chuyển hướng | Tăng trọng số cho mệnh đề đứng sau từ "nhưng" | Ý khen nhân viên được ưu tiên hơn ý chê phòng |
| Chữ in hoa | Tăng điểm khi từ viết hoa toàn bộ | "TUYỆT VỜI" mạnh hơn "tuyệt vời" |
| Dấu chấm than | Tăng nhẹ cường độ | "Tốt!!!" mạnh hơn "Tốt" |
| Biểu tượng cảm xúc | Tra điểm riêng cho từng biểu tượng | Mặt cười cộng điểm, mặt khóc trừ điểm |

Trên câu minh họa, khi áp dụng phủ định và từ nhấn mạnh, cụm "not very clean" được tính là âm. Khi áp dụng thêm quy tắc từ chuyển hướng, mệnh đề "the staff were wonderful" được ưu tiên. Kết quả cuối cùng phản ánh đúng hơn việc người viết chê phòng nhưng khen nhân viên.

## Chuẩn hoá điểm và chọn ngưỡng

Tổng điểm thô phụ thuộc vào độ dài văn bản. Một bình luận dài dễ có điểm cao hơn chỉ vì chứa nhiều từ. Có hai cách chuẩn hoá phổ biến.

Cách thứ nhất là chia tổng điểm cho số từ của văn bản:

```
Điểm chuẩn hoá của d = Điểm của d / số từ của d
```

Cách thứ hai là đưa điểm về khoảng từ âm một đến dương một. VADER dùng công thức sau:

```
Điểm tổng hợp = x / √(x² + 15)
```

| Ký hiệu | Ý nghĩa |
|---|---|
| `x` | Tổng điểm thô của văn bản |
| `15` | Hằng số do nhóm tác giả chọn |
| `Điểm tổng hợp` | Điểm đã đưa về khoảng từ âm một đến dương một |

Sau khi có điểm tổng hợp, ta chia nhãn bằng ngưỡng. Với VADER, ngưỡng thường dùng là dương không phẩy không năm và âm không phẩy không năm. Điểm từ không phẩy không năm trở lên là dương, điểm từ âm không phẩy không năm trở xuống là âm, phần còn lại là trung tính. Ngưỡng này nên được kiểm tra lại trên một tập nhãn thủ công của chính dữ liệu đang nghiên cứu.

## Các hạn chế cần nêu rõ

Ngoài phủ định và chuyển hướng, phương pháp từ điển còn các hạn chế sau.

Thứ nhất là mỉa mai và châm biếm. Câu "Dịch vụ tuyệt vời, chờ có bốn mươi phút thôi" chứa từ dương nhưng ý chê. Từ điển không nhận ra điều này.

Thứ hai là từ đa nghĩa và sắc thái theo lĩnh vực. Từ "nhỏ" là khen khi nói về chi phí, nhưng là chê khi nói về diện tích phòng.

Thứ ba là từ ngoài từ điển. Từ mới, tiếng lóng và từ viết tắt không có điểm nên bị bỏ qua.

Thứ tư là độ phủ, tức tỷ lệ từ trong văn bản thực sự tra được trong từ điển. Độ phủ thấp nghĩa là điểm cuối cùng chỉ dựa trên một phần nhỏ của văn bản, nên kết quả kém tin cậy. Nên báo cáo độ phủ cùng với kết quả phân loại.

Thứ năm là văn bản không có từ cảm xúc nhưng vẫn mang cảm xúc, như câu "Mình sẽ không quay lại nữa". Câu này không chứa từ nào có điểm rõ ràng, trong khi ý chê thể hiện qua cấu trúc.

## Vấn đề với tiếng Việt

Tiếng Việt có nhiều từ ghép, nên phải tách từ trước khi tra bảng. Nếu không, "tuyệt vời" bị cắt thành hai từ riêng và mất điểm. Các công cụ tách từ thường dùng là VnCoreNLP, underthesea và PyVi.

Nguồn từ điển cảm xúc tiếng Việt có sẵn còn ít và chất lượng không đồng đều. Có ba hướng xử lý. Hướng thứ nhất là dịch một từ điển tiếng Anh như NRC sang tiếng Việt rồi kiểm tra lại thủ công. Hướng thứ hai là xây từ điển riêng theo lĩnh vực nghiên cứu, chẳng hạn từ điển cho bình luận khách sạn. Hướng thứ ba là kết hợp cả hai và bổ sung từ lóng mạng xã hội.

Văn bản mạng xã hội tiếng Việt còn có viết tắt, viết không dấu, kéo dài chữ và sai chính tả, như "ko", "k", "đc", "tuyệt vờiiii". Vì vậy cần chuẩn hoá chính tả trước khi tra bảng, nếu không nhiều từ cảm xúc sẽ không được nhận ra. Các từ phủ định tiếng Việt như "không", "chưa", "chẳng", "đâu có" cũng cần được đưa vào danh sách quy tắc phủ định.

## Cách đánh giá kết quả

Để biết điểm từ điển có phản ánh cảm xúc thật hay không, ta so kết quả của từ điển với một tập nhãn do người gán. Quy trình gồm bốn bước.

1. Lấy mẫu ngẫu nhiên vài trăm văn bản từ dữ liệu.
2. Để hai người gán nhãn độc lập, rồi tính hệ số đồng thuận giữa hai người, thường dùng hệ số Cohen kappa.
3. Chạy từ điển trên cùng tập mẫu.
4. So sánh hai bộ nhãn bằng các chỉ số trong bảng dưới.

| Chỉ số | Ý nghĩa |
|---|---|
| Độ chính xác tổng thể | Tỷ lệ văn bản được gán đúng nhãn trên tổng số văn bản |
| Độ chính xác theo lớp | Trong các văn bản được gán nhãn dương, bao nhiêu phần thực sự dương |
| Độ thu hồi | Trong các văn bản thực sự dương, bao nhiêu phần được gán đúng nhãn dương |
| Điểm F1 | Trung bình điều hoà của độ chính xác theo lớp và độ thu hồi |
| Ma trận nhầm lẫn | Bảng cho thấy nhãn nào hay bị nhầm sang nhãn nào |

Ma trận nhầm lẫn thường cho thấy từ điển nhầm nhiều nhất ở lớp trung tính và ở các câu có phủ định hoặc mỉa mai. Phần này nên được phân tích riêng trong bài.

## Vị trí so với các phương pháp khác

Nên chọn từ điển khi dữ liệu chưa có nhãn, cần kết quả nhanh, cần giải thích được vì sao một văn bản bị chấm dương hay âm, hoặc cần một đường cơ sở để so sánh.

Không nên chỉ dùng từ điển khi dữ liệu có nhiều ngữ cảnh phức tạp, nhiều mỉa mai, hoặc khi cần độ chính xác cao. Lúc đó học máy có giám sát hoặc mô hình ngôn ngữ đã huấn luyện trước thường cho kết quả tốt hơn.

Trong thực tế nghiên cứu, từ điển thường được dùng làm đường cơ sở. Kết quả của các mô hình phức tạp hơn được so với đường cơ sở này để cho thấy mô hình mới cải thiện được bao nhiêu.

## Kết luận

Điểm cuối cùng của từ điển phản ánh cảm xúc của người viết đến mức nào còn phụ thuộc vào bốn điều kiện. Thứ nhất, từ điển phải phù hợp với lĩnh vực dữ liệu. Thứ hai, các quy tắc ngữ cảnh phải được áp dụng. Thứ ba, độ phủ phải đủ cao. Thứ tư, kết quả phải được kiểm tra với nhãn của người. Nếu thiếu một trong bốn điều kiện này, điểm cuối cùng nhiều khả năng chỉ cho biết văn bản chứa bao nhiêu từ mà từ điển đã gán nhãn.
