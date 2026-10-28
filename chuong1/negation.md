# Negation handling: xử lý phủ định

## Là gì?

Xử lý phủ định là bước điều chỉnh điểm của từ cảm xúc khi có từ phủ định đứng gần. Câu "not good" chứa từ "good" có điểm dương, nhưng cả cụm mang nghĩa chê. [AFINN](afinn.md) không xử lý việc này, và Nielsen năm 2011 đã ghi nhận hạn chế đó.

## Nền tảng

Polanyi và Zaenen năm 2006 gọi phủ định và tăng cường là các yếu tố làm dịch cực tính theo ngữ cảnh. Taboada và cộng sự năm 2011 dùng thuật ngữ này khi xây dựng SO-CAL.

Có ba cách xử lý phổ biến:

**Gắn nhãn phạm vi.** Pang, Lee và Vaithyanathan năm 2002 thêm tiền tố `NOT_` vào mọi từ nằm giữa từ phủ định và dấu câu kế tiếp. Ví dụ `didn't like this movie , but I` thành `didn't NOT_like NOT_this NOT_movie but I`. Sanjiv Das và Mike Chen năm 2001 đã dùng ý tưởng tương tự trước đó.

**Đảo điểm.** Cách này đổi dấu điểm, giữ nguyên độ lớn.

**Dịch điểm.** Taboada và cộng sự lập luận rằng dịch điểm về phía ngược lại một khoảng cố định hợp lý hơn đảo điểm, vì "not excellent" không tệ như "terrible".

VADER của Hutto và Gilbert năm 2014 chọn cách thứ ba theo dạng nhân hệ số. Nếu một trong ba từ đứng ngay trước từ cảm xúc là từ phủ định, điểm của từ cảm xúc nhân với âm 0,74. Danh sách phủ định trong mã nguồn gồm cả các từ như without, rarely và seldom.

## Công thức

```
Đảo điểm:      điểm mới = âm 1 nhân điểm cũ
Nhân hệ số:    điểm mới = âm 0,74 nhân điểm cũ, theo VADER
Dịch điểm:     điểm mới = điểm cũ trừ k, nếu điểm cũ dương
               điểm mới = điểm cũ cộng k, nếu điểm cũ âm
```

| Ký hiệu | Ý nghĩa |
|---|---|
| `điểm cũ` | Điểm của từ cảm xúc trong từ điển, trước khi xử lý phủ định |
| `điểm mới` | Điểm của từ cảm xúc sau khi xử lý phủ định |
| `k` | Mức dịch cố định. Theo một bài khảo sát mô tả SO-CAL, k bằng 4 trên thang từ âm 5 đến dương 5 |

## Ví dụ minh họa

Giả sử "good" có điểm 3 trên thang của AFINN. Đây là số minh họa.

| Cách xử lý | Điểm của "not good" |
|---|---|
| Không xử lý | 3 |
| Đảo điểm | âm 3 |
| Nhân hệ số âm 0,74 | âm 2,22 |
| Dịch điểm với k bằng 4 | âm 1 |

Cùng một câu cho ba kết quả khác nhau, nên cần nêu rõ cách xử lý trong phần phương pháp.

## Cách dùng khi phân tích

1. Chuẩn hóa chữ viết tắt của từ phủ định trước, ví dụ "didn't" và "didnt".
2. Xác định phạm vi phủ định: cửa sổ vài từ phía trước, hoặc đến dấu câu kế tiếp.
3. Chọn cách điều chỉnh điểm: đảo, nhân hệ số hoặc dịch.
4. Chạy thử trên mẫu câu có phủ định rồi đối chiếu với nhãn tay.

## Điểm mạnh

- Sửa được lỗi nặng nhất của từ điển thuần túy là chấm "not good" thành tích cực.
- Quy tắc minh bạch, dễ giải thích với người đọc.
- Giữ được cấu trúc từ điển cảm xúc, không cần dữ liệu huấn luyện.

## Điểm yếu

- Cửa sổ ba từ của VADER bỏ sót phủ định đứng xa từ cảm xúc.
- Gắn tiền tố đến dấu câu kế tiếp bao cả những từ không bị phủ định, như "this" và "movie" trong ví dụ trên.
- Đảo điểm làm "not excellent" tệ ngang "terrible", và đây chính là lý do Taboada và cộng sự đề xuất dịch điểm.
- Mức dịch k bằng 4 mới được xác nhận qua một bài khảo sát về SO-CAL bản tiếng Tây Ban Nha, chưa đối chiếu với bài gốc tiếng Anh.
- Với tiếng Việt, các từ như "không", "chưa", "chẳng", "chả" đứng trước từ cảm xúc, còn "không ... lắm" làm yếu chứ không đảo. Đây là nhận xét chưa có nguồn, và cần danh sách phủ định riêng cho tiếng Việt.

## Các bài báo nên đọc và dùng để trích dẫn

| Bài | Dùng để trích khi nào |
|---|---|
| Pang, Lee & Vaithyanathan (2002), Thumbs up? Sentiment Classification using Machine Learning Techniques, EMNLP, trang 79 đến 86 | Gắn nhãn NOT_ theo phạm vi |
| Taboada, Brooke, Tofiloski, Voll & Stede (2011), Lexicon-Based Methods for Sentiment Analysis, Computational Linguistics, tập 37, số 2, trang 267 đến 307 | Đảo điểm và dịch điểm, thuật ngữ yếu tố dịch cực tính. Nguồn chính |
| Hutto & Gilbert (2014), VADER: A Parsimonious Rule-based Model for Sentiment Analysis of Social Media Text, ICWSM | Cách nhân hệ số trong cửa sổ ba từ |
