# Bài nộp LAB5 — T4 Thương mại điện tử · Nhóm Đèn Hồng

**Lớp:** L3A · **Bàn / zone:** ____ · **Track:** T4 · Trợ lý khiếu nại "hàng không đúng mô tả"

| Họ và Tên | Mã Học Viên | Việc đã làm |
|---|---|---|
| Nguyễn Thị Thanh Thuỷ *(kiểm tra lại dấu)* | ____ | Người 1 · Phạm vi và kịch bản: §1, §2 (`draft-scenarios.md`): 10 kịch bản phủ 4 lớp, chọn 2 ca đắt nhất và ca suýt chọn |
| Hoàng Lâm Minh *(kiểm tra lại dấu)* | ____ | Người 2 · UX khi AI sai: §3 (`draft-ux.md`): câu AI nói nguyên văn hai phía, màn hình, thông báo, HAX/PAIR |
| Đinh Thị Hương | 2A202603569 | Người 3 · Quyền của AI và kiểm thử: §4, §6 (`draft-autonomy.md`): mức cho 5 tool, cơ chế duyệt, quá hạn, tiêu chí Pass/Fail |
| Nguyễn Thị Hồng San | ____ | Người 4 · Prototype: §5, `prototype/`: 2 màn hình và vùng mô phỏng nhân viên, 3 ca bấm được, ô ca lạ, ảnh đánh số |

> Quy ước trong bài: **K1** = shop sửa mô tả (kịch bản #2) · **K2** = người bán đúng, áo M (#3) · **K3** = gửi nhầm size, ca thường (#4).
> **Chính sách dựng của nhóm, không phải chính sách Shopee:** người mua gửi yêu cầu trong **7 ngày** từ lúc nhận hàng · người bán có **24 giờ** phản hồi · mục tiêu nhân viên xem hồ sơ trong **4 giờ** từ lúc chuyển.

---

## §1. Lát cắt & phạm vi

**Lát cắt (chép từ track):** Trong **Trò chuyện với Shopee**, khi **người mua** báo "hàng nhận không đúng mô tả", **AI tự hướng dẫn gửi yêu cầu trả hàng hoàn tiền, xin thêm bằng chứng, hay chuyển nhân viên**, để người mua biết đúng bước tiếp theo, và người bán không bị xử thua khi họ đúng.

**3 việc tính năng KHÔNG làm:**

1. **Không phạt, trừ điểm, khoá shop hay kết luận hàng giả.** `phat_shop` ảnh hưởng cả hoạt động kinh doanh của shop và khó đảo. Luồng khiếu nại thường không đủ thẩm quyền điều tra gian lận, nên việc này thuộc bộ phận chuyên trách. *Trên prototype:* không có nút phạt ở bất kỳ màn nào (ảnh, số ⑧).
2. **Không đưa số điện thoại hay địa chỉ giữa hai bên.** Thông tin liên hệ không phải căn cứ xử lý khiếu nại, mà còn tạo rủi ro quấy rối. *Trên prototype:* màn người bán che tên và ẩn SĐT, địa chỉ (số ⑥). Ô ca lạ từ chối khi được hỏi thông tin liên hệ.
3. **Không xử lý khiếu nại ngoài "hàng không đúng mô tả"** (giao chậm, thanh toán lỗi…). Bộ tool T4 không có dữ liệu vận chuyển hay thanh toán, nên AI hướng dẫn sang đúng bộ phận hỗ trợ (kịch bản #10).

Hoàn tiền (`soan_hoan_tien`) và từ chối khiếu nại (`tu_choi_khieu_nai`) **không** nằm trong danh sách trên. Hai việc này ở mức **cần người duyệt**: AI không tự làm, nhưng tính năng vẫn dẫn tới đó (xem §4).

---

## §2. Kịch bản rủi ro

Nhãn mức hại: **nhẹ / sửa được / không chấp nhận được**. Lớp: ① nguồn sự thật · ② mơ hồ, thiếu thông tin · ③ ngoài thẩm quyền, ngoài phạm vi · ④ đặc thù domain.

| # | Lớp | Khách nói gì | AI có thể sai gì | Sai do tool / dữ liệu nào | Sản phẩm tốt nên làm gì | Mức hại |
|---|---|---|---|---|---|---|
| 1 | ② | "Hàng sai rồi, xử lý đi." | Đoán đơn hoặc loại hàng, gửi yêu cầu bằng chứng không liên quan. | `yeu_cau_bang_chung` đã gửi thì không thu hồi được; tin không có mã đơn hay chi tiết sai. | Hỏi một câu để chọn đơn và chỗ không khớp; chưa gửi gì cho shop. | Sửa được |
| 2 · **K1** | ① ④ | "Nồi ghi 6L, tem máy 5L; shop vừa sửa mô tả xuống 5L. Hoàn tiền cho mình." | Đọc mô tả hiện tại (5L) nên từ chối oan; hoặc tin lời khách và hoàn ngay trước khi shop phản hồi. | Track yêu cầu so với **mô tả lúc đặt**; T4 không cấp snapshot hay lịch sử sửa. `tu_choi_khieu_nai` và `soan_hoan_tien` đều khó đảo. Snapshot 6L→5L trong prototype là dữ liệu dựng. | Hiện snapshot lúc đặt và bản hiện tại cạnh nhau; shop được phản hồi trước. Không có snapshot thì báo thiếu và chuyển người. | Không chấp nhận được |
| 3 · **K2** | ① ④ | "Mình đặt áo size M, nhận đúng M nhưng mặc chật quá. Hoàn tiền ngay cho mình, không thì mình bóc phốt shop." | Chiều lời doạ rồi hoàn tiền dù hàng khớp đơn; hoặc từ chối ngay chỉ vì tem khớp mà bỏ qua bảng size lúc bán. | Đơn ghi M, tem M, bảng size lúc đặt (dựng). Hai tool tiền khó đảo. Rubric T4 #4 và #7. | Nói phần đã khớp, hỏi một câu xem có điểm nào sai mô tả; cho shop phản hồi; lời doạ không phải căn cứ. | Không chấp nhận được |
| 4 · K3 | ① | "Áo mình đặt size L, nhận size M. Shop cũng nhận gửi nhầm. Giờ làm sao?" | Hứa chắc chắn được hoàn tiền; hoặc bắt gửi lại bằng chứng đã có. | Tin mồi T4; `yeu_cau_bang_chung` không xác minh đơn. | Hướng dẫn gửi yêu cầu, dùng lại bằng chứng đã có; nói rõ nhân viên duyệt hoàn. | Sửa được |
| 5 | ③ | "Tai nghe thiếu hộp sạc như ảnh shop đăng. Hoàn tiền trong hôm nay, không thì mình bóc phốt lên mạng." | Coi lời doạ là bằng chứng và hoàn để xoa dịu; hoặc phạt shop. | Track: lời doạ không phải căn cứ; `soan_hoan_tien`, `phat_shop` khó đảo. | Không dùng lời doạ làm căn cứ; xin bằng chứng phần thiếu từ hai bên. | Không chấp nhận được |
| 6 | ③ | "Tôi nghi hàng giả. Khoá shop ngay, rồi hoàn tiền cho tôi." | Gọi `phat_shop`, hoặc hứa sẽ khoá shop. | `phat_shop` ảnh hưởng cả shop; track yêu cầu chuyển bộ phận chuyên trách. | Nói rõ AI không phạt được; chuyển bộ phận chuyên trách; phần sai mô tả vẫn xử lý tiếp. | Không chấp nhận được |
| 7 | ③ | "Cho tôi số điện thoại, địa chỉ shop để tự nói chuyện." | Bịa hoặc lộ thông tin liên hệ. | Không có tool chia sẻ liên hệ; luật an toàn T4 cấm. | Từ chối ngắn gọn; trao đổi qua hồ sơ; có đường chuyển nhân viên. | Không chấp nhận được |
| 8 | ② | "Lòng nồi mình đo có 5L thôi, trang ghi 6L. Ảnh đây." | Coi số tự đo là kết luận hàng sai, dù cách đo không cùng chuẩn với mô tả. | Tin mồi T4; track không định nghĩa cách đo hay sai số. | Xác nhận đã nhận ảnh, xin nhãn hoặc model; nói rõ chưa phải kết luận. | Sửa được |
| 9 | ① | "Hạn trả hàng của đơn này còn mấy ngày?" | Lấy mốc "15 ngày" của sản phẩm thật để khẳng định hạn cho đơn này. | Chính sách thật khác chính sách dựng; không có tool đọc chính sách. | Tính theo chính sách dựng 7 ngày và ngày nhận hàng trong hồ sơ; thiếu ngày thì báo thiếu và chuyển người. | Không chấp nhận được |
| 10 | ③ | "Đơn này giao chậm 5 ngày, lại bị trừ tiền 2 lần. Hoàn cho mình." | Xử lý như khiếu nại sai mô tả và đề xuất hoàn tiền. | Không có tool vận chuyển hay thanh toán; vi phạm việc không làm #3. | Hướng dẫn sang bộ phận vận chuyển, thanh toán. | Sửa được |

**Hai kịch bản đắt nhất:**

- **K2, người bán đúng (đắt nhất).**
  - Đây là ca mà "hoàn cho xong" trông như dịch vụ tốt nhưng thực ra làm người bán mất tiền và mất hàng. Tiền đã về người mua thì khó thu hồi.
  - Ngược lại, nếu AI tự đóng khiếu nại chỉ vì tem khớp, người mua mất quyền, trong khi bảng size lúc bán vẫn có thể sai.
  - Lời doạ bóc phốt tạo áp lực đúng vào điểm yếu mà người bán đã kể trong track.
- **K1, shop sửa mô tả.**
  - Lỗi này nằm ở **nguồn dữ liệu**. AI làm đúng thiết kế (đọc trang sản phẩm) vẫn ra kết quả sai.
  - Hướng sai mặc định là từ chối oan người mua. Hướng ngược lại (tin lời khách) thì làm shop mất tiền khi chưa kịp phản hồi.
- **Vì sao hai ca này đắt hơn các ca khác:** cả hai đều dẫn tới hai tool tiền khó đảo, và **sai theo hướng nào cũng có một bên chịu**. Các kịch bản #1, #4, #8, #10 sai thì chỉ mất thời gian.
- **Ca suýt được chọn: #6, đòi khoá shop vì nghi hàng giả.** Hậu quả lớn, nhưng hướng xử lý đã rõ (cấm `phat_shop`, chuyển bộ phận chuyên trách). Ca này không đòi AI phải cân bằng hai phía.

---

## §3. Khi AI sai

### K1 — Shop sửa mô tả sau khi bán (đường *failure / không căn cứ*)

**Người mua: AI nói nguyên văn**
> "Mình thấy mô tả tại thời điểm bạn đặt hàng ghi 'dung tích 6 lít', còn trang sản phẩm hiện tại ghi '5 lít'. Hai thông tin này khác nhau, nhưng riêng chuyện trang hiện tại khác chưa xác nhận được sản phẩm bạn nhận có sai mô tả hay không. Mình chưa quyết định hoàn tiền hoặc từ chối yêu cầu. Bạn gửi giúp mình ảnh nhãn/model trên thân nồi nhé (ảnh đo lòng nồi đã có rồi, không cần gửi lại). Sau đó mình sẽ gửi yêu cầu để shop phản hồi."

**Người mua thấy và làm gì:**
- **Thấy:**
  - Hai bản mô tả đặt cạnh nhau. Bản "lúc đặt hàng" có viền xanh "dùng để đối chiếu", kèm nguồn và thời điểm. Bản "hiện tại" ghi "chỉ để tham khảo".
  - Bằng chứng có nhãn đã xác minh / đã ghi nhận / chưa có, và dòng "Chưa đủ căn cứ để kết luận, còn thiếu: …".
  - Hạn 7 ngày kèm thời điểm ghi nhận khiếu nại.
- **Làm:** "Bổ sung ảnh nhãn/model", "Nhờ nhân viên xem xét".
- **Nếu không làm gì:** hồ sơ vẫn mở và giữ nguyên thời điểm ghi nhận, nên không mất hạn.

**Ai được báo, sau bao lâu:**
- **Người bán:** ngay khi người mua bổ sung đủ, qua `yeu_cau_bang_chung`. Shop có 24 giờ phản hồi. Nội dung gửi shop:
  > "Có khiếu nại cho đơn DH-2611-0381: người mua cho biết nồi nhận được không khớp dung tích. Mô tả lúc đặt hàng ghi '6 lít', nhãn nồi nhận được ghi 5.0L, trang hiện tại ghi '5 lít'. Đây chưa phải kết luận shop sai. Vui lòng kiểm tra đúng đơn và gửi phản hồi hoặc bằng chứng trước [thời điểm] (24 giờ). Shop không cần và sẽ không nhận thông tin liên hệ riêng của người mua."
- **Trưởng nhóm:** được báo qua `chuyen_truong_nhom` ngay khi shop phản hồi, hoặc khi shop quá 24 giờ. Lý do: mô tả đã thay đổi sau khi đặt. Trưởng nhóm phân công cho nhân viên, mục tiêu nhân viên xem trong 4 giờ.
- **Hai bên:** đều được báo khi hồ sơ được chuyển và khi có quyết định.

**Quyết định: trả lời kèm giới hạn, xin đúng phần bằng chứng còn thiếu, rồi chuyển người.**
- *Loại "tự từ chối theo trang hiện tại":* đây đúng là lỗi cần chặn.
- *Loại "tự hoàn vì hai bản khác nhau":* hai bản khác nhau chưa chứng minh hàng giao bị sai, và shop chưa được nghe.
- *Loại "chuyển người ngay khi thấy hai bản khác nhau":* nhân viên sẽ nhận một hồ sơ còn thiếu ảnh nhãn và phản hồi của shop, rồi lại phải hỏi lại. Trong khi AI xin được hai thứ đó ngay, gần như không tốn gì.

### K2 — Người bán đúng, người mua doạ bóc phốt (đường *low-confidence* và *correction*)

**Người mua: AI nói nguyên văn**
> "Mình thấy đơn ghi size M và ảnh tem bạn gửi cũng là size M, khớp với bảng size lúc bạn đặt. Như vậy chưa đủ để kết luận sản phẩm sai mô tả, nhưng mình cũng chưa đóng yêu cầu của bạn. Việc mặc chật và lời doạ bóc phốt không được dùng làm căn cứ quyết định. Bạn cho mình biết có điểm nào không khớp với trang sản phẩm lúc đặt không, ví dụ số đo thực tế khác bảng size? Mình chưa hoàn tiền hay đóng khiếu nại."

**Người mua thấy và làm gì:**
- **Thấy:**
  - Đơn ghi M, tem M, bảng size lúc đặt, mỗi thứ có nguồn và nhãn trạng thái.
  - Một dòng "Lời doạ bóc phốt: không dùng làm căn cứ". Không có cảnh báo hay câu buộc tội người mua.
- **Làm:**
  - "Số đo thực tế khác bảng size" → gửi số đo, AI chuyển cho shop.
  - "Không có gì khác, chỉ là mặc chật" → AI nói rõ "hiện chưa đủ căn cứ cho khiếu nại không đúng mô tả", rồi cho chọn: **Vẫn gửi khiếu nại** / **Bổ sung số đo** / **Rút yêu cầu**.

**Người bán:**
- AI báo:
  > "Có khiếu nại cho đơn DH-2611-0457: người mua phản ánh áo size M mặc chật và yêu cầu trả hàng hoàn tiền. Đơn ghi M, tem áo ghi M; đây là thông tin cần đối chiếu, vui lòng kiểm tra bảng size/mô tả hiển thị lúc bán. Đây chưa phải kết luận shop sai. Vui lòng kiểm tra đúng đơn và gửi phản hồi hoặc bằng chứng trước [thời điểm] (24 giờ). Lời doạ bóc phốt không được dùng làm căn cứ quyết định. Shop không cần và sẽ không nhận thông tin liên hệ riêng của người mua."
- Shop có nút gửi bảng size lúc bán và ảnh đo, hoặc đồng ý nhận lại hàng.

**Ai được báo:**
- Người mua được báo khi shop phản hồi.
- Nếu người mua vẫn muốn tiếp tục, hồ sơ chuyển trưởng nhóm. Mục tiêu nhân viên xem trong 4 giờ.
- Nhánh "chỉ mặc chật": nhân viên thấy **đề xuất "từ chối, có lý do"** do AI chuẩn bị, nhưng phải tự bấm duyệt. Nhánh người mua gửi số đo khác shop (90 cm so với 96 cm): AI ghi "chưa đủ căn cứ, không đề xuất" và nêu bằng chứng còn thiếu.

**Quyết định: hỏi lại một câu, không đoán.**
- *Loại "từ chối ngay vì tem khớp":* khớp size chưa chứng minh mọi chi tiết khớp mô tả, và từ chối thì khó đảo.
- *Loại "hoàn cho êm":* lời doạ không phải căn cứ, và người bán sẽ mất tiền oan.
- *Loại "chuyển người ngay":* một câu hỏi lại có thể giải quyết xong ca này (người mua tự rút yêu cầu). Chuyển ngay chỉ làm hàng chờ nhân viên dài thêm.

### Loại lỗi và cách nói, cách sửa theo loại

| Loại lỗi | Ví dụ trong bài | Cách nói | Cách sửa |
|---|---|---|---|
| **Ngữ cảnh** (hệ thống chạy đúng thiết kế nhưng sai với tình huống) | K1: AI đọc trang sản phẩm, đúng như thiết kế, nhưng trang đã bị sửa sau khi bán | Không xin lỗi chung chung. Chỉ ra hai bản khác nhau, nói "chưa kết luận". | **Sửa thiết kế:** lưu và ưu tiên snapshot lúc đặt (xem lỗi bên dưới) |
| **Người dùng** (khiếu nại không đúng loại) | K2: áo đúng size nhưng mặc chật; #10 giao chậm | Không đổ lỗi, không buộc tội. Nói phần đã khớp, hỏi "điểm nào không khớp?" | Cho người dùng tự sửa: bổ sung số đo, rút yêu cầu, hoặc chuyển đúng bộ phận |
| **Hệ thống** (AI làm sai việc nó được tự làm) | AI gửi `yeu_cau_bang_chung` nhầm nội dung, hoặc chuyển hồ sơ nhầm | Nhận lỗi rõ: "Mình vừa gửi nhầm yêu cầu ở tin trước… những gì bạn đã gửi vẫn được giữ." | Nút **Đính chính** / **Yêu cầu phân lại** ngay trong nhật ký (số ④). Không giả vờ thu hồi được tin đã gửi. |

### Nguyên tắc HAX/PAIR (mỗi nguyên tắc trỏ vào một chỗ cụ thể)

- **G11, giải thích vì sao:** khung hai bản mô tả có nguồn và thời điểm (số ①), cùng câu "mô tả lúc đặt ghi 6 lít, hiện tại ghi 5 lít" ở K1.
- **G10, thu hẹp khi nghi ngờ:** câu hỏi một ý ở K2 ("có điểm nào không khớp…?") và nhãn "Chưa đủ căn cứ để kết luận, còn thiếu: …" (số ②).
- **PAIR Errors + Graceful failure:** nút "Nhờ nhân viên xem xét" luôn có (số ⑤). Khi quá hạn 24 giờ, hồ sơ chuyển nhân viên và **không** tự động có bên thắng.

### Một lỗi mà sửa câu chữ không cứu được

**Lỗi:** AI chỉ đọc được mô tả **hiện tại**.
- Ở K1, dù câu chữ trung lập đến đâu, AI vẫn so hàng nhận được với "5 lít" và kết luận "khớp mô tả", tức là từ chối oan người mua.
- Câu chữ không cứu được, vì căn cứ đã sai từ gốc.

**Thiết kế cứu nó:**
1. Mỗi đơn lưu **snapshot mô tả lúc đặt** có mốc thời gian.
2. Màn hình luôn hiện snapshot đó là "dùng để đối chiếu" và bản hiện tại chỉ "để tham khảo" (số ①).
3. Không có snapshot thì AI **không được kết luận**: báo "chưa đủ căn cứ" và chuyển người (tiêu chí P1, §6).
4. Thêm một điều kiện bắt buộc trước khi nhân viên duyệt: ô kiểm "Tôi đã xem mô tả **lúc đặt**" (số ⑦).

---

## §4. Mức tự chủ

**Nguyên tắc:** AI được thu thập bằng chứng và chuyển hồ sơ, nhưng **không tự quyết ai mất tiền**.

| Tool | Mức | Sai thì ai chịu gì · đảo được không | Chờ người thì mất gì | Phương án đã loại và vì sao |
|---|---|---|---|---|
| `yeu_cau_bang_chung` | **Tự làm có điều kiện:** chỉ sau khi xác định đúng đơn; mẫu trung lập; chỉ xin phần còn thiếu | Hai bên mất công, có thể lỡ hạn. Tin đã tới thì không thu hồi, chỉ gửi đính chính được. | Nếu bắt duyệt, mỗi tin hỏi bằng chứng phải chờ nhân viên, kể cả ca đơn giản như K3 | *Duyệt mọi tin:* chờ vô ích. *Gửi tự do:* dễ hỏi lặp hoặc đòi dữ liệu riêng (#1). |
| `chuyen_truong_nhom` | **Tự làm có điều kiện:** khi mô tả thay đổi, bằng chứng mâu thuẫn, ai đó yêu cầu gặp người, hoặc việc ngoài thẩm quyền | Thêm hàng chờ, nhân viên mất thời gian. Phân lại được, nhưng thời gian đã mất thì không lấy lại. | Nếu bắt duyệt việc chuyển, thêm một bước ngay trước khi tới tay người có quyền | *Duyệt việc chuyển:* thừa bước. *Chuyển mọi ca:* K3 rõ ràng, có thể hướng dẫn ngay. |
| `soan_hoan_tien` (theo đề là **thực hiện hoàn tiền**) | **Cần người duyệt:** nhân viên xử lý khiếu nại được phân quyền | Người bán mất tiền, có thể mất cả hàng. **Khó đảo**: tiền đã về người mua. | Người mua nhận tiền chậm hơn (K1, K3) | *AI tự hoàn:* K2 hoàn oan. *Cấm hoàn:* K1 bị giữ tiền oan. |
| `tu_choi_khieu_nai` | **Cần người duyệt:** nhân viên xử lý khiếu nại được phân quyền | Người mua mất cơ hội giải quyết, tiền về người bán. **Khó đảo.** | Tranh chấp kéo dài thêm | *AI tự từ chối theo tem khớp hoặc vì shop im lặng:* K1 bị từ chối oan. *Không bao giờ từ chối:* K2 không được bảo vệ. |
| `phat_shop` | **Cấm** trong luồng này | Ảnh hưởng doanh thu và uy tín cả shop. Khó khôi phục. | Xử phạt chậm hơn, nhưng thuộc quy trình khác | *Tự phạt theo yêu cầu khách:* #6. *Nút "duyệt phạt" cho nhân viên khiếu nại:* sai thẩm quyền. Thay bằng chuyển bộ phận chuyên trách. |

**Cơ chế duyệt:**
- **Ai duyệt:** `chuyen_truong_nhom` đưa hồ sơ tới **trưởng nhóm**, người này phân công cho **nhân viên xử lý khiếu nại được phân quyền**, và nhân viên đó bấm duyệt.
- **Người duyệt thấy:**
  - mã đơn, mặt hàng, số tiền; mốc giao và mốc tiếp nhận
  - mô tả lúc mua kèm nguồn; mô tả hiện tại
  - bằng chứng và phản hồi của hai bên; phần còn thiếu hoặc mâu thuẫn
  - đề xuất của AI (tách riêng, ghi "không phải quyết định"); hậu quả của hành động
  - **Không có % tự tin.**
- **Điều kiện trước khi duyệt:**
  - đúng đơn
  - có nguồn mô tả lúc mua
  - shop đã phản hồi, hoặc đã hết 24 giờ. Prototype **khoá nút duyệt** cho tới khi điều kiện này đúng, kể cả khi người mua bấm "Nhờ nhân viên" ngay từ đầu (lúc đó AI vẫn báo shop và mở hạn 24 giờ).
  - đủ căn cứ cho quyết định cụ thể
- **Khi duyệt:** nhập lý do, tick xác nhận, xem hậu quả "khó đảo lại". Mỗi phiên bản hồ sơ chỉ có một quyết định, và không được vừa hoàn vừa từ chối.
- **Quá hạn:**
  - Shop quá 24 giờ: nhắc shop và đưa hồ sơ cho nhân viên. **Im lặng không đồng nghĩa với thua.**
  - Nhân viên quá 4 giờ: báo chậm cho hai bên và nhắc trưởng nhóm một lần.
  - Hồ sơ vẫn mở. **Không tool tiền nào tự chạy khi hết hạn.**

**Tool khó xếp nhất: `soan_hoan_tien`.** Mức nào cũng có giá:

| Phương án | Ai trong nhóm từng chọn *(điền)* | Cái giá |
|---|---|---|
| AI tự hoàn khi bằng chứng rõ | ____ | K2: chiều lời doạ, hoàn oan; tiền khó thu hồi |
| **Nhân viên duyệt giao dịch cụ thể (chốt)** | ____ | K1, K3 phải chờ quyết định tiền. Bù lại bằng hồ sơ chuẩn bị sẵn, người dùng không phải kể lại. |
| Cấm hoàn trong luồng | ____ | K1: người mua có bằng chứng vẫn bế tắc; tính năng mất ý nghĩa |

**Cách chốt:** hoàn sai và không hoàn khi đáng hoàn đều gây thiệt hại thật, nên chọn mức giữ được cả hai hướng nhưng có người chịu trách nhiệm. Mức tự tin của AI không thay được phê duyệt dựa trên bằng chứng.

**Thử mức đã đặt trên 3 kịch bản:**

| Ca | Cái sai có bị chặn? | Còn làm khi lẽ ra phải hỏi? | Người dùng bình thường có chờ vô ích? |
|---|---|---|---|
| K1 | Có. AI không dùng bản hiện tại để từ chối, không hoàn theo lời khách. | Không. Hai tool tiền cần duyệt, phạt shop bị cấm. | Có chờ xác minh, nhưng cần thiết. Thời điểm ghi nhận được giữ. |
| K2 | Có. Lời doạ không dẫn tới hoàn; AI không tự đóng vì tem khớp. | Không. Hỏi một câu trước khi gửi shop. | Không. Nếu người mua tự rút, ca kết thúc mà không cần nhân viên. |
| K3 | Có. Không chuyển tiền trước khi duyệt; shop thừa nhận chưa đồng nghĩa đã hoàn. | Không. | Hướng dẫn ngay, không qua trưởng nhóm. Chỉ chờ quyết định tiền: chi phí nhóm chấp nhận. |

**Luật thêm: tách bước.** Nhóm tách **"chuẩn bị đề xuất"** (trạng thái nội bộ, không chuyển tiền) khỏi **"thực hiện"** (gọi `soan_hoan_tien` hoặc `tu_choi_khieu_nai`). Lý do: tên tool có chữ "soạn" nhưng theo đề, tool này thực hiện hoàn tiền thật. Tách bước giúp chặn ca K2, khi AI "soạn" mà tiền đã đi. Nếu bằng chứng mới tới sau khi đã có đề xuất, đề xuất cũ phải được xem và duyệt lại.

**Lời hứa đã đổi.** Vì hoàn tiền cần người duyệt, lời hứa với người mua đổi từ "xử lý tiền ngay" thành "cho biết ngay bước tiếp theo và trạng thái hồ sơ":
> "AI giúp kiểm tra thông tin và chuẩn bị hồ sơ. Nhân viên sẽ xem bằng chứng của cả hai bên trước khi quyết định hoàn tiền hoặc đóng khiếu nại. Gửi yêu cầu không có nghĩa là đã được hoàn tiền."

---

## §5. Prototype

- **File:** [`prototype/index.html`](prototype/index.html), mở bằng trình duyệt. Link chạy trực tiếp: ____ *(GitHub Pages hoặc raw.githack, điền sau khi repo công khai)*.
- **Công cụ:** HTML/JS thuần, dựng với sự hỗ trợ của coding agent (Claude).
- **Phần mock:**
  - dữ liệu đơn, mô tả, ảnh (hiện bằng chữ), đồng hồ mô phỏng
  - lời gọi tool: chỉ ghi vào nhật ký, không gọi thật
  - câu AI nói: viết sẵn theo §3
- **Không có lời gọi AI thật.** Ô "ca lạ" trả lời theo luật từ khoá, và đi đường an toàn khi không hiểu.
- **Cách chạy và luồng demo:** [`prototype/README.md`](prototype/README.md).
- **Bố cục:** Màn 1 người mua và Màn 2 người bán đặt cạnh nhau, cùng một vùng **mô phỏng nhân viên**. Vùng này cần có vì hai tool tiền ở mức cần duyệt.

**Ảnh đánh số:**
- [`prototype/anh-1-cho-shop-phan-hoi.png`](prototype/anh-1-cho-shop-phan-hoi.png): K1, đang chờ shop phản hồi.
- [`prototype/anh-2-cho-nhan-vien-duyet.png`](prototype/anh-2-cho-nhan-vien-duyet.png): K1, hồ sơ đang ở chỗ nhân viên.

| Số | Thể hiện gì | HAX/PAIR | Mức tự chủ |
|---|---|---|---|
| ① | Mô tả lúc đặt ("dùng để đối chiếu") cạnh bản hiện tại ("tham khảo"), có nguồn và thời điểm | G11 · PAIR Explainability | — |
| ② | Nhãn bằng chứng đã xác minh / đã ghi nhận / chưa có, và "Chưa đủ căn cứ, còn thiếu…": **cách hiện độ chắc** | G2 · G10 | AI không kết luận |
| ③ | Trạng thái 5 bước, hạn 7 ngày, thời điểm ghi nhận, thời gian còn lại | PAIR Mental model · rubric T4 #8 | — |
| ④ | Nhật ký việc AI tự làm, có nút **Đính chính** / **Yêu cầu phân lại** | G9 | **Tự làm, có đường sửa** |
| ⑤ | "Nhờ nhân viên xem xét" luôn có | PAIR Errors + Graceful failure | Đường chuyển người |
| ⑥ | Phía người bán: hạn 24 giờ, thông tin người mua đã che, lời doạ không phải căn cứ | PAIR Trust | — |
| ⑦ | Thẻ duyệt: đề xuất AI tách khỏi quyết định; hộp xác nhận ghi hậu quả, 3 ô kiểm, lý do bắt buộc; khoá sau khi duyệt | G16 | **Cần người duyệt** |
| ⑧ | `phat_shop` không có nút, chỉ có dòng giải thích và đường chuyển bộ phận chuyên trách | — | **Cấm** |

**Quyết định về cách hiện:**
- **Độ chắc bằng nhãn từng bằng chứng, không dùng % tự tin.**
  - *Đã cân nhắc:* thanh % tự tin, nhãn đèn xanh/đỏ "khả năng người mua đúng".
  - *Vì sao loại:* % không có căn cứ, và kéo nhân viên duyệt theo con số. Đèn xanh/đỏ nghiêng về một bên trước khi người bán được nghe.
  - *Vì sao chọn:* nhãn từng bằng chứng trả lời đúng câu người mua hay hỏi: "mình còn thiếu cái gì".
- **Hai bản mô tả đặt cạnh nhau.**
  - *Đã cân nhắc:* chỉ hiện bản lúc đặt; hiện kiểu diff gạch xoá.
  - *Vì sao loại:* chỉ hiện bản lúc đặt thì người mua không hiểu vì sao trang hiện tại khác. Diff gạch xoá trông như kết tội shop.
- **Ba mức tự chủ bằng ba hình thức khác nhau:** nhật ký có nút sửa / nút chỉ ở vai nhân viên kèm xác nhận / không có nút.
  - *Đã cân nhắc:* cho người mua bấm "xác nhận hoàn tiền".
  - *Vì sao loại:* người mua không có quyền duyệt, và dễ hiểu nhầm là "đã được hoàn".
- **Hai màn đặt cạnh nhau, không dùng tab.** Sự trung lập là cốt lõi của track, và đặt cạnh nhau cho thấy ngay hai bên thấy cùng một hồ sơ.
- **Không có nút hoàn tác cho giao dịch tiền.** Nút đó là lời hứa giả. Nhật ký ghi rõ "giao dịch thật, không có nút hoàn tác".

---

## §6. Tốt là gì

| Tiêu chí | Pass khi | Fail khi |
|---|---|---|
| **P1 · Đúng nguồn, nói rõ phần thiếu** | Đánh giá sai mô tả dựa trên bản lúc mua, có hiện nguồn và mốc. Thiếu bản đó thì ghi "chưa đủ căn cứ" và chuyển người. | Dùng bản hiện tại mà không báo, tự bịa bản cũ, hoặc kết luận chắc khi thiếu nguồn |
| **P2 · Quyết định tiền phải được duyệt** | Trước phê duyệt hợp lệ thì không gọi hoàn hay từ chối. Quá hạn không tự quyết. Không chạy lặp. Không có thao tác phạt shop. | AI hoặc người mua tự thực hiện quyết định tiền; hết hạn thì tự quyết; gọi trùng; có nút phạt |
| **P3 · Hai bên biết cách tiếp tục** | Người mua thấy bước tiếp theo, trạng thái, thời điểm ghi nhận. Người bán thấy khiếu nại đã che dữ liệu riêng tư và hạn cụ thể. Khi chuyển người thì kèm bằng chứng. | Thiếu đường bổ sung hoặc chuyển người; không có hạn; bắt kể lại; lộ dữ liệu riêng tư; im lặng bị coi là thua |

**Chấm thử trên prototype** (bấm thật qua từng nhánh K1, K2, K3, kể cả "Tua 24 giờ" và hộp duyệt):

| Ca | P1 | P2 | P3 |
|---|---|---|---|
| K1 | **Pass.** Khung ① luôn dùng bản 6 lít lúc đặt; nhánh mâu thuẫn hiện "AI: chưa đủ căn cứ, không đề xuất". | **Pass.** Tua 24 giờ thì hồ sơ chuyển nhân viên, không tự hoàn. Nút Xác nhận chỉ mở khi đủ 3 ô kiểm và có lý do. Sau khi duyệt, nút bị khoá. Nhờ nhân viên quá sớm thì nút duyệt khoá cho tới khi shop phản hồi hoặc hết 24 giờ. Tua nhiều lần thì trưởng nhóm chỉ được nhắc một lần. | **Pass.** Hai bên thấy hạn, trạng thái, nhật ký chung. Người bán thấy N\*\*\*h, SĐT và địa chỉ bị ẩn. |
| K2 | **Pass.** Bảng size lúc đặt có nhãn "không thay đổi". | **Pass.** AI chỉ *đề xuất* từ chối; nhân viên phải duyệt. Người mua rút yêu cầu thì không có thao tác tiền. | **Pass.** Có lựa chọn vẫn gửi / bổ sung / rút; lời doạ không phải căn cứ, hiện ở cả hai phía. |

**Lỗi và giới hạn còn lại:**
- Khi bằng chứng mới tới sau lúc đã có đề xuất, prototype **chưa** bắt nhân viên duyệt lại (§4 yêu cầu).
- Ô ca lạ dựa trên từ khoá, nên tin dài hoặc nhiều ý có thể đi sai nhánh. Nhánh mặc định thì an toàn (hỏi lại hoặc chuyển người).
- Ca "thiếu snapshot lúc đặt" chưa có màn riêng để bấm thử.
- Kiểm quyền duyệt chỉ mô phỏng bằng giao diện. Bản thật cần backend.
- Nhân viên vẫn có thể duyệt sai. Thiết kế chỉ giảm rủi ro bằng ô kiểm và lý do bắt buộc.

---

## §7. Demo

- **Ca lạ nhận được:** ____
- **Prototype đã làm gì** (đi nhánh nào, mức tự chủ nào): ____
- **Nhóm có đổi ý gì sau ca đó không:** ____
