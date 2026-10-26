# NRC Emotion Lexicon

## 1. NRC Emotion Lexicon là gì?

NRC Emotion Lexicon, thường gọi tắt là EmoLex, là một từ điển cảm xúc. Nó cho biết mỗi từ tiếng Anh có gắn với cảm xúc nào, trong tám cảm xúc cơ bản, và có gắn với thái độ tích cực hay tiêu cực hay không. Người ta dùng nó để máy tính đếm xem một đánh giá, một bài đăng hay một cuốn sách chứa những cảm xúc nào mà không cần ai đọc và chấm tay.

Điểm khác với [SentiWordNet](bai1.md) là EmoLex không chỉ trả lời câu hỏi khen hay chê. Nó trả lời thêm câu hỏi khen hay chê vì cảm xúc gì, ví dụ chê vì giận dữ hay chê vì thất vọng và buồn bã.

## Nền tảng: mô hình Plutchik và sự liên tưởng giữa từ với cảm xúc

Tám cảm xúc của EmoLex lấy từ bánh xe cảm xúc của nhà tâm lý học Robert Plutchik. Ông cho rằng con người có tám cảm xúc cơ bản, xếp thành bốn cặp đối lập: vui sướng và buồn bã, tin tưởng và ghê tởm, sợ hãi và giận dữ, ngạc nhiên và mong đợi.

Điều cần hiểu đúng là EmoLex ghi lại sự liên tưởng của người đọc, không ghi định nghĩa của từ. Từ "abandon" không có nghĩa là sợ hãi, nhưng nhiều người đọc từ này thì nghĩ đến sợ hãi và buồn bã, nên từ được gán hai nhãn đó. Vì vậy từ trong EmoLex không cần tự nó diễn tả cảm xúc. Chỉ cần nó thường gợi ra cảm xúc ở người đọc là đủ.

## EmoLex gắn thêm gì vào từ

Với mỗi từ w, EmoLex gắn mười nhãn. Mỗi nhãn chỉ nhận một trong hai giá trị, là 1 nếu có gắn và 0 nếu không:

```
L(w, k) bằng 0 hoặc 1, với k chạy qua mười nhãn
```

| Ký hiệu | Ý nghĩa |
|---|---|
| `w` | Một từ trong danh sách |
| `k` | Một trong mười nhãn |
| `L(w, k)` | Bằng 1 nếu từ w có gắn nhãn k, bằng 0 nếu không |

Mười nhãn gồm:

| Nhãn | Ý nghĩa |
|---|---|
| Giận dữ | Từ gợi sự tức giận, bực bội |
| Mong đợi | Từ gợi sự chờ đợi, hy vọng điều sắp tới |
| Ghê tởm | Từ gợi sự khó chịu, kinh tởm |
| Sợ hãi | Từ gợi sự lo lắng, đe dọa |
| Vui sướng | Từ gợi niềm vui, sự hài lòng |
| Buồn bã | Từ gợi mất mát, thất vọng |
| Ngạc nhiên | Từ gợi sự bất ngờ |
| Tin tưởng | Từ gợi sự an tâm, đáng tin |
| Tiêu cực | Thái độ chung là chê |
| Tích cực | Thái độ chung là khen |

Có ba điểm khác với SentiWordNet. Thứ nhất, điểm gắn với từ chứ không gắn với nghĩa của từ, nên không có bước chọn nghĩa. Thứ hai, các nhãn không loại trừ nhau, một từ có thể mang nhiều nhãn cùng lúc, và cũng có từ không mang nhãn nào. Thứ ba, nhãn chỉ có hai giá trị, nên từ "furious" và từ "annoyed" đều chỉ được ghi là có gắn với giận dữ, dù mức độ khác nhau.

## Ví dụ minh họa

Hai dòng đầu là nhãn thật ở đầu tệp dữ liệu bản 0.92. Các dòng còn lại là nhãn tôi tự đặt để bạn dễ hình dung, không phải nhãn thật trong tệp. Bạn nên tra lại trực tiếp trong tệp trước khi dùng.

| Từ | Nhãn |
|---|---|
| abandon | tiêu cực, sợ hãi, buồn bã |
| abandoned | tiêu cực, giận dữ, sợ hãi, buồn bã |
| delicious | tích cực, vui sướng |
| rude | tiêu cực, giận dữ, ghê tởm |
| room | không có nhãn nào |

Hai dòng đầu cho thấy dạng chia của từ có thể có nhãn khác với dạng gốc. Từ "abandoned" có thêm giận dữ, còn "abandon" thì không. Dòng cuối cho thấy phần lớn từ chỉ sự vật thông thường không mang nhãn nào, và điều đó là bình thường.

## Cách các tác giả xây dựng nó

Quá trình đi theo các bước sau:

1. Chọn danh sách từ cần gán nhãn. Các tác giả lấy từ nhiều nguồn có sẵn, gồm Macquarie Thesaurus, General Inquirer, WordNet Affect Lexicon và các từ thường gặp trong kho văn bản lớn.
2. Thuê nhiều người gán nhãn qua nền tảng thuê việc trực tuyến Amazon Mechanical Turk. Mỗi từ do nhiều người đánh giá, ít nhất là năm người.
3. Với mỗi từ, người làm trả lời trước một câu hỏi chọn từ gần nghĩa nhất. Câu hỏi này có hai việc. Nó buộc người làm hiểu đúng nghĩa của từ đang hỏi, và nó giúp loại những người trả lời bừa.
4. Sau đó người làm cho biết từ đó gắn với từng cảm xúc ở mức nào. Họ chọn trong các mức từ không gắn đến gắn mạnh.
5. Tổng hợp câu trả lời của nhiều người theo đa số, rồi quy về nhãn có hoặc không.
6. Loại các câu trả lời kém tin cậy và công bố danh sách cuối cùng.

Điểm cần nhớ là nhãn do người gán, không phải do thuật toán. Đây là khác biệt lớn nhất so với SentiWordNet. Đổi lại, người gán nhãn là người dùng mạng đông đảo chứ không phải chuyên gia ngôn ngữ.

## Cách dùng khi phân tích một câu

Lấy câu "The room was clean but the staff were rude" làm ví dụ. Các nhãn dưới đây là số minh họa.

1. Tách từ: The, room, was, clean, but, the, staff, were, rude.
2. Đưa về dạng gốc, ví dụ was và were về be. Bước này cần vì danh sách chủ yếu chứa dạng gốc.
3. Bỏ các từ không mang ý nghĩa cảm xúc nếu muốn, ví dụ the và but. Bước này không bắt buộc, vì các từ này vốn không có nhãn.
4. Tra nhãn của từng từ trong danh sách, như bảng dưới.
5. Cộng dồn thành vectơ mười chiều cho cả câu. Trong ví dụ này tích cực bằng 1, tin tưởng bằng 1, tiêu cực bằng 1, giận dữ bằng 1, ghê tởm bằng 1, các chiều còn lại bằng 0.

| Từ | Nhãn |
|---|---|
| clean | tích cực, tin tưởng |
| rude | tiêu cực, giận dữ, ghê tởm |
| room, staff | không có nhãn |

Với một tập nhiều đánh giá, bạn cộng dồn rồi chia cho tổng số từ của từng đánh giá để so sánh công bằng giữa các đánh giá dài ngắn khác nhau:

```
Điểm của cảm xúc k trong văn bản d
    = tổng của L(w, k) với mọi từ w trong d
      chia cho số từ của d
```

| Ký hiệu | Ý nghĩa |
|---|---|
| `k` | Một cảm xúc hoặc thái độ cần đo, ví dụ giận dữ |
| `d` | Văn bản cần chấm |
| `w` | Một từ trong văn bản d |
| `L(w, k)` | Bằng 1 nếu từ w có gắn nhãn k, bằng 0 nếu không |
| `số từ của d` | Tổng số từ của văn bản d, dùng để chuẩn hóa theo độ dài |

Sau đó bạn so sánh các nhóm, ví dụ đánh giá trước và sau một mốc thời gian, hoặc đánh giá của các nhóm khách khác nhau. Cách cộng dồn và cách chuẩn hóa do người dùng tự chọn.

## Điểm mạnh

- Phủ nhiều cảm xúc cùng lúc, tám cảm xúc cộng hai thái độ, trong một danh sách duy nhất. Đây là cơ sở lý thuyết của Plutchik được các tác giả áp dụng trực tiếp (Mohammad & Turney, 2013).
- Nhãn do người gán và có kiểm soát chất lượng ngay từ khâu thu thập, nên đáng tin hơn nhãn do thuật toán tự suy ra (Mohammad & Turney, 2013).
- Đã được dùng thành công trên nhiều loại văn bản. Mohammad và Yang (2011) so sánh cách nam và nữ thể hiện cảm xúc trong thư điện tử. Mohammad (2012) vẽ diễn biến cảm xúc theo thời gian trong thư và sách.
- Dùng được làm đặc trưng cho mô hình học máy. Nhóm của Kiritchenko, Zhu và Mohammad (2014) đưa danh sách này cùng các danh sách khác vào bộ phân loại cảm xúc cho bài đăng mạng xã hội.
- Có sẵn bản dịch sang nhiều ngôn ngữ, trong đó có tiếng Việt. Mohammad, Salameh và Kiritchenko (2016) kiểm tra việc dịch từ điển cảm xúc và cho thấy phần lớn thông tin cảm xúc được giữ lại sau khi dịch.
- Có sẵn trong nhiều gói phần mềm như syuzhet của R và tidytext, nên dùng nhanh và dễ lặp lại kết quả.

## Điểm yếu

- Xét từng từ riêng lẻ nên bỏ qua phủ định như "not good", và không phân biệt nghĩa theo ngữ cảnh. Kiritchenko và cộng sự (2014) phải xử lý phủ định bằng một bước riêng.
- Nhãn chỉ có hai giá trị nên không cho biết cảm xúc mạnh hay yếu. Chính Mohammad (2018) sau đó xây thêm một danh sách riêng có điểm cường độ để khắc phục điều này.
- Nhãn phản ánh liên tưởng chung chứ không riêng cho lĩnh vực nào. Một từ có thể gợi cảm xúc khác nhau trong đánh giá khách sạn và trong tin tức. Ý này là nhận xét về cách dùng, không trích từ bài báo cụ thể.
- Với dữ liệu tiếng Việt, bản dịch có sẵn tạo bằng dịch máy, nên có từ bị dịch sai nghĩa hoặc không có từ tương ứng. Ý này cũng là nhận xét của tôi. Nếu dùng, bạn nên nêu hạn chế này trong phần bàn luận và đối chiếu với bài của Mohammad và cộng sự (2016).
- Độ phủ giới hạn. Từ lóng, từ viết tắt và biểu tượng cảm xúc của mạng xã hội phần lớn không có trong danh sách. Ý này bạn nên kiểm lại với bài gốc trước khi trích.
- Kết quả trên một câu đơn lẻ không ổn định, vì mỗi câu chỉ có ít từ có nhãn. Danh sách phù hợp hơn khi cộng dồn trên tập văn bản lớn. Ý này là nhận xét về cách dùng.
