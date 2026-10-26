# SentiWordNet

## 1. SentiWordNet là gì?

SentiWordNet là một từ điển cảm xúc. Nó cho biết mỗi nghĩa của một từ tiếng Anh mang bao nhiêu phần tích cực, bao nhiêu phần tiêu cực và bao nhiêu phần trung tính. Người ta dùng nó để máy tính tự đánh giá một câu, một bài review là khen hay chê mà không cần ai đọc và chấm tay.

## Nền tảng: WordNet và synset

WordNet là một từ điển tiếng Anh khác với từ điển thường. Nó không xếp theo chữ cái mà gom các từ có cùng nghĩa vào một nhóm gọi là synset (synonym set, nhóm từ đồng nghĩa). Mỗi synset đại diện cho một nghĩa cụ thể, có kèm một câu định nghĩa ngắn gọi là gloss.

Ví dụ, từ "cold" có nhiều nghĩa nên thuộc nhiều synset khác nhau: một synset là "lạnh về nhiệt độ", một synset khác là "lạnh lùng, thiếu thân thiện". Hai nghĩa này mang sắc thái cảm xúc rất khác nhau, và đây là lý do SentiWordNet gán điểm cho synset chứ không gán cho từ.

## SentiWordNet gắn thêm gì vào WordNet

Với mỗi synset s, SentiWordNet gắn ba điểm có tổng bằng 1:

```
Pos(s) + Neg(s) + Obj(s) = 1
```

| Ký hiệu | Ý nghĩa |
|---|---|
| `s` | Một synset, tức một nghĩa cụ thể của từ |
| `Pos(s)` | Mức tích cực của nghĩa đó, từ 0 đến 1 |
| `Neg(s)` | Mức tiêu cực của nghĩa đó, từ 0 đến 1 |
| `Obj(s)` | Mức khách quan, tức không mang ý kiến, bằng 1 trừ Pos trừ Neg |

Vì tổng luôn bằng 1 nên chỉ cần biết Pos và Neg là suy ra được Obj.

Ví dụ minh họa (các con số dưới đây tôi tự đặt để bạn dễ hình dung, không phải số thật trong SentiWordNet):

| Synset | Pos | Neg | Obj |
|---|---|---|---|
| cold, nghĩa lạnh về nhiệt độ | 0.0 | 0.0 | 1.0 |
| cold, nghĩa lạnh lùng | 0.0 | 0.75 | 0.25 |
| excellent | 0.875 | 0.0 | 0.125 |

Hai nghĩa của "cold" có điểm khác hẳn nhau. Nghĩa nhiệt độ hoàn toàn khách quan, còn nghĩa lạnh lùng thì nghiêng về tiêu cực.

## Cách các tác giả xây dựng nó

Quá trình đi theo các bước sau:

1. Lấy một tập nhỏ synset đã được gán nhãn tay là dương hoặc âm, ví dụ các synset của "good", "nice" cho dương và "bad", "ugly" cho âm.
2. Mở rộng tập này qua các quan hệ có sẵn trong WordNet. Ý tưởng là synset gần với synset dương thì nhiều khả năng cũng dương, nên tập nhãn lớn dần lên.
3. Dùng tập đã mở rộng làm dữ liệu huấn luyện cho nhiều bộ phân loại. Các bộ này đọc phần gloss của synset và học xem những gloss kiểu nào thì dương, kiểu nào thì âm.
4. Cho các bộ phân loại chấm toàn bộ synset còn lại, rồi từ kết quả tính ra Pos, Neg, Obj.

Bản 3.0 gộp kết quả của nhiều bộ phân loại, rồi thêm một bước random walk trên đồ thị gloss của WordNet để tinh chỉnh điểm. Random walk ở đây hiểu đơn giản là cho điểm cảm xúc lan truyền qua các synset có gloss nhắc đến nhau, để các synset liên quan có điểm nhất quán hơn.

Điểm cần nhớ là điểm do thuật toán tự gán, không phải người chấm.

## Cách dùng khi phân tích một câu

Lấy câu "The room was clean but the staff were rude" làm ví dụ. Các điểm dưới đây cũng là số minh họa.

1. Tách từ: The, room, was, clean, but, the, staff, were, rude.
2. Gán từ loại (POS tag): clean là tính từ, rude là tính từ, room và staff là danh từ. Bước này cần vì cùng một từ khác loại thì khác synset.
3. Lemmatize, tức đưa về dạng gốc: was và were về be.
4. Chọn nghĩa đúng trong ngữ cảnh (word sense disambiguation). Đây là bước khó nhất, nên nhiều người lấy nghĩa đầu tiên cho đơn giản.
5. Tra Pos, Neg, Obj của synset đã chọn cho từng từ, như bảng dưới.

| Từ | Pos | Neg | Obj |
|---|---|---|---|
| clean | 0.5 | 0.0 | 0.5 |
| rude | 0.0 | 0.625 | 0.375 |
| room, staff | 0.0 | 0.0 | 1.0 |

Gộp lại, ví dụ lấy tổng Pos trừ tổng Neg: 0.5 trừ 0.625 bằng âm 0.125. Câu hơi nghiêng về tiêu cực. Cách gộp này do người dùng tự chọn, có thể dùng trung bình hay cách khác tùy mục đích.

## Điểm mạnh

- Điểm gắn với nghĩa chứ không gắn với từ, nên các nghĩa khác nhau của cùng một từ có thể có điểm khác nhau (Esuli & Sebastiani, 2006).
- Có thang liên tục và có điểm khách quan để phân biệt từ trung tính với từ mang ý kiến (Esuli & Sebastiani, 2006).
- Bản 3.0 báo cáo độ chính xác tốt hơn bản 1.0 (Baccianella và cộng sự, 2010).

## Điểm yếu

- Điểm do thuật toán gán tự động chứ không do người chấm, nên có nhiễu (Baccianella và cộng sự, 2010 nêu rõ cách gán tự động).
- Muốn dùng đúng phải làm word sense disambiguation, và lỗi ở bước này kéo theo sai điểm. Ý này không đến từ bài báo mà là nhận xét về cách dùng.
- Hutto & Gilbert (2014) nhận xét SentiWordNet thiếu các đặc trưng của mạng xã hội như từ lóng và biểu tượng cảm xúc. Ý này cần đối chiếu với bài gốc trước khi trích.

## Bài từ 2026 dùng SentiWordNet

Chen, Y., Chen, S., Wu, Z., Yu, S., & Du, Z. (2026). Attribute Correlation and Hotel Recommendation Based on Online Reviews. *Mathematics, 14*(14), 2482. [https://doi.org/10.3390/math14142482](https://doi.org/10.3390/math14142482)

File bài báo trên Drive: [mathematics-14-02482-v2.pdf (Q1)](https://drive.google.com/file/d/19-ZPalRwZQPt_y7ag6uYDD5ILyHDYyLh/view?usp=sharing)

## SentiWordNet trong bài chạy theo chuỗi này

Từ review đến điểm ban đầu của từng từ:

```
Review của khách
=> tiền xử lý (viết thường, sửa lỗi chính tả, bỏ stop word)
=> chỉ giữ danh từ, động từ, trạng từ, tính từ
=> tra PosScore và NegScore trong SentiWordNet cho từng từ
=> nếu một từ có nhiều synset thì lấy trung bình cộng điểm của các synset đó
   (bài không làm word sense disambiguation)
=> ra điểm ban đầu e+ và e− của từ
=> từ không có trong từ điển thì cả hai điểm bằng 0
```

Từ điểm ban đầu đến điểm sau lan truyền:

```
Điểm ban đầu e+ và e−
=> dựng đồ thị, mỗi nút là một từ, cạnh nối theo quan hệ cú pháp,
   trọng số cạnh là độ tương đồng
=> chạy PolarityRank cho điểm lan truyền giữa các nút
=> lặp tối đa 200 lần hoặc đến khi chênh lệch giữa hai lần lặp
   không quá 10 mũ âm 5
=> ra PR+ và PR− của từng từ
=> bài chỉ giữ PR+ làm điểm cảm xúc
```

Công thức lan truyền (PR− viết tương tự, thay e+ bằng e−):

```
PR+(vi) = (1 − d) × e+_i + d × Σ_j [ w_ij / Σ_k |w_jk| ] × PR+(vj)
```

| Ký hiệu | Ý nghĩa |
|---|---|
| `vi` | Từ đang được tính điểm |
| `PR+(vi)` | Điểm tích cực sau lan truyền của vi |
| `e+_i` | Điểm tích cực ban đầu của vi từ SentiWordNet |
| `d` | Hệ số lặp, bài đặt 0.85 |
| `(1 − d)` | Phần điểm giữ lại từ chính từ đó |
| `vj` | Từ lân cận của vi trên đồ thị |
| `w_ij` | Trọng số cạnh giữa vi và vj |
| `w_jk` | Trọng số các cạnh đi ra từ vj, dùng để chia đều điểm của vj |
| `PR+(vj)` | Điểm tích cực hiện tại của vj |

Từ điểm của từng từ đến điểm của từng thuộc tính:

```
Điểm PR+ của từng từ
=> Word2Vec đã gom từ liên quan vào 6 thuộc tính
=> tính trung bình có trọng số theo độ tương đồng
=> ra điểm cảm xúc của từng thuộc tính
```

```
total_senti = Σ (simi × senti) / Σ simi
```

| Ký hiệu | Ý nghĩa |
|---|---|
| `total_senti` | Điểm cảm xúc của một thuộc tính |
| `simi` | Độ tương đồng giữa từ liên quan và tên thuộc tính |
| `senti` | Điểm PR+ của từ liên quan |

Điểm cảm xúc của thuộc tính đi vào hai nơi.

Nơi 1, hồi quy OLS:

```
chuẩn hóa điểm theo từng khách sạn
=> thuộc tính lõi là biến độc lập, các thuộc tính còn lại là biến phụ thuộc
=> kiểm tra hiệu ứng hào quang
```

Nơi 2, mô hình khuyến nghị (mục 5.1.1):

```
điểm lớn hơn 0.5 là tích cực, nhỏ hơn −0.5 là tiêu cực,
ở giữa là trung lập, không nhắc đến là thiếu dữ liệu
=> đổi thành số fuzzy
=> tính trọng số
=> lọc cộng tác
```

## Vì sao bài chọn SentiWordNet

SentiWordNet chỉ là một từ điển. Vì vậy câu hỏi "vì sao chọn nó" thật ra gồm hai câu hỏi: vì sao chọn từ điển thay vì mô hình học máy, và trong các từ điển thì vì sao chọn SentiWordNet.

### Vì sao chọn cách dùng từ điển

```
Bài nói rõ ở mục 3.4
=> chọn cách không giám sát dựa trên từ điển vì hiệu quả và đã chín muồi
=> dữ liệu có 885.490 review
=> không có nhãn cảm xúc sẵn
=> muốn dùng học máy có giám sát thì phải gán nhãn tay một lượng lớn
=> từ điển bỏ qua được khâu này
```

Lý do thực tế đi kèm:

```
từ điển chạy nhanh trên dữ liệu lớn
=> điểm số của từng từ nhìn thấy và giải thích được
=> cần điểm liên tục theo từng thuộc tính để chạy hồi quy,
   không chỉ nhãn khen hoặc chê
```

### Vì sao chọn SentiWordNet mà không chọn từ điển khác

- Nó có điểm liên tục chứ không chỉ nhãn dương hoặc âm, nên hợp với bài vì cần biến số để đưa vào hồi quy OLS.
- Nó có sẵn trong NLTK, gắn với WordNet, nên dễ dùng, tra theo từ loại, không cần xây từ đầu.
- Nó có điểm riêng cho từng từ loại, nên khớp với việc bài chủ động chỉ giữ danh từ, động từ, trạng từ, tính từ.
- Nó phủ rộng, vì WordNet có hàng trăm nghìn synset, nên từ vựng review ít bị bỏ sót hơn so với từ điển nhỏ.
