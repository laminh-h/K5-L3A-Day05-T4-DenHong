# Luồng demo · Nhóm Đèn Hồng · T4

Một người demo, khoảng 5 phút. Mỗi bước có 3 phần: **Ấn** (bấm gì), **Nói** (đọc gì), **Mục đích** (để chứng minh điều gì với người chấm).

Prototype: [`prototype/index.html`](prototype/index.html)

---

## Chuẩn bị (trước khi người xem tới)

- **Ấn:** mở link prototype toàn màn hình → **K1 · Shop sửa mô tả** → **↺ Làm lại** → **① Số chú thích**.
- **Mục đích:** các ô hiện viền đỏ và số ①–⑧, để khi bị hỏi "chỗ nào là G__?" thì chỉ được ngay.

---

## Phần A · Mở đầu (khoảng 30 giây)

### Bước 1: Giới thiệu bài toán
- **Ấn:** chưa bấm gì. Chỉ tay lần lượt vào Màn 1, Màn 2, vùng nhân viên.
- **Nói:**
  > "Nhóm em làm track T4: trợ lý AI trong *Trò chuyện với Shopee*, khi người mua báo **hàng không đúng mô tả**. AI hướng dẫn trả hàng hoàn tiền, xin thêm bằng chứng, hoặc chuyển nhân viên.
  > Cái khó là **sai hướng nào cũng có một bên mất tiền**: hoàn sai thì người bán mất, từ chối sai thì người mua mất.
  > AI **không** phạt shop, **không** đưa số điện thoại hay địa chỉ, **không** xử lý giao chậm hay thanh toán.
  > Bên trái là người mua, bên phải là người bán, cùng nhìn một hồ sơ. Phía dưới là nhân viên duyệt. Em demo ca **shop sửa mô tả sau khi bán**."
- **Mục đích:** cho người xem hiểu lát cắt trong 30 giây, biết sai thì ai chịu, và thấy nhóm có 3 việc không làm (R1). Đặt hai màn cạnh nhau ngay từ đầu cho thấy nhóm coi **sự trung lập** là cốt lõi.

---

## Phần B · AI không chắc thì người mua thấy gì (khoảng 1 phút)

### Bước 2: Chỉ ra cái bẫy
- **Ấn:** chỉ vào tin nhắn đầu tiên (màu cam) trong khung chat của người mua.
- **Nói:**
  > "Khách nói nồi ghi 6 lít mà nhận chỉ 5 lít, và shop đã sửa mô tả thành 5 lít. Nếu AI đọc trang hiện tại, nó sẽ thấy 'khớp mô tả' và **từ chối oan** người mua."
- **Mục đích:** nêu rõ **AI có thể sai ở đâu** trước khi cho xem thiết kế. Người chấm cần thấy nhóm biết lỗi đắt nhất là gì.

### Bước 3: Ô ① · So với mô tả lúc đặt
- **Ấn:** chỉ **ô ①** (Mô tả dùng để đối chiếu).
- **Nói:**
  > "Nên AI luôn so với bản **lúc đặt hàng**, ô viền xanh ghi 6 lít, có nguồn và giờ lưu. Bản hiện tại 5 lít chỉ để tham khảo. Nhãn vàng ghi 'mô tả đã thay đổi' nhưng **không** kết tội shop lừa. Đây là **G11**: giải thích AI dựa vào đâu."
- **Mục đích:** chứng minh thiết kế chặn được lỗi ở bước 2. Đây cũng là "lỗi mà sửa câu chữ không cứu được": phải lưu bản mô tả lúc đặt. Trỏ được **G11** vào màn hình (R5, điểm HAX).

### Bước 4: Ô ② · Độ chắc bằng bằng chứng
- **Ấn:** chỉ **ô ②** (Bằng chứng trong hồ sơ), rồi chỉ dòng vàng "Chưa đủ căn cứ để kết luận".
- **Nói:**
  > "Nhóm em không hiện % tự tin, vì AI không có căn cứ cho con số đó. Mỗi bằng chứng có nhãn **đã xác minh / đã ghi nhận / chưa có**, và AI nói thẳng **'chưa đủ căn cứ, còn thiếu: …'**. Đây là **G2** và **G10**. Khách biết đúng mình thiếu gì, khỏi phải gửi đi gửi lại."
- **Mục đích:** ăn dòng R5 "thấy được độ chắc hoặc bằng chứng AI dựa vào" (4 điểm). Đồng thời giải quyết đúng lời phàn nàn của người mua trong đề: *"cứ bị hỏi lại, không ai nói còn thiếu cái gì"*.

### Bước 5: Ô ③ · Trạng thái và hạn
- **Ấn:** chỉ **ô ③** (Trạng thái hồ sơ).
- **Nói:**
  > "Thanh trạng thái cho biết hồ sơ đang ở bước nào. Hạn trả hàng 7 ngày có giờ cụ thể, và thời điểm ghi nhận được giữ nguyên, nên chờ bao lâu khách cũng không mất hạn."
- **Mục đích:** người dùng luôn biết **bước tiếp theo**, đúng "kết quả" mà lát cắt yêu cầu. Đáp ứng rubric T4 #8 (nói rõ thời hạn và còn bao lâu).

---

## Phần C · Người bán được nghe (khoảng 1 phút)

### Bước 6: Người mua bổ sung bằng chứng
- **Ấn:** ở Màn 1, bấm **"Bổ sung ảnh nhãn/model"** (nút cam).
- **Nói:**
  > "Khách gửi ảnh nhãn ghi 5.0L. AI xác nhận đã nhận, nói rõ **chưa phải kết luận**, rồi **tự gửi yêu cầu** sang shop."
- **Mục đích:** cho thấy AI **chỉ xin đúng phần còn thiếu**, và việc xin bằng chứng là việc AI **tự làm** (mức 1). Luồng bắt đầu chạy mà không cần ai can thiệp.

### Bước 7: Ô ⑥ · Phía người bán
- **Ấn:** chỉ sang Màn 2, **ô ⑥** (Khiếu nại cần phản hồi).
- **Nói:**
  > "Phía người bán: shop thấy khiếu nại và **hạn phản hồi 24 giờ** kèm thời gian còn lại. Tên người mua bị che, **SĐT và địa chỉ bị ẩn**. AI nói rõ 'đây chưa phải kết luận shop sai'."
- **Mục đích:** trả lời câu bắt buộc của đề, **"hai bên thấy gì"**. Chứng minh người bán được nghe trước khi có quyết định (rubric T4 #3) và không lộ dữ liệu riêng (việc không làm #2). Đáp lại lời người bán trong đề: *"bên tôi đúng cũng chẳng ai nghe"*.

### Bước 8: Shop phản hồi, AI chuyển người
- **Ấn:** ở Màn 2, bấm **"Phản hồi: Shop đổi sang model 5L từ 05/11, đơn này gửi model 5L"**.
- **Nói:**
  > "Shop xác nhận đã đổi sang model 5L. Vì mô tả thay đổi sau khi khách đặt, AI **tự chuyển hồ sơ** cho trưởng nhóm. Cả hai bên được báo: chưa có quyết định hoàn hay từ chối, nhân viên xem trong 4 giờ."
- **Mục đích:** cho thấy khi gặp ca khó, AI **dừng lại và chuyển người** thay vì tự quyết. Đây là đường lui của thiết kế "khi AI sai". Đồng thời trả lời câu **"ai quyết"**.

---

## Phần D · AI được tự làm tới đâu (khoảng 1 phút 30 giây)

### Bước 9: Ô ④ · Mức 1, tự làm có nút sửa
- **Ấn:** chỉ **ô ④** (Việc trợ lý đã tự làm, ở Màn 2), chỉ vào nút **"✎ Đính chính yêu cầu này"**.
- **Nói:**
  > "Nhóm chia ba mức. **Mức 1, AI tự làm**: xin bằng chứng và chuyển hồ sơ. Sai thì chỉ tốn thời gian, nên không bắt chờ duyệt. Nhưng mỗi việc đều có nút **Đính chính** hoặc **Yêu cầu phân lại**. Đây là **G9**."
- **Mục đích:** ăn dòng R5 "tự làm có hoàn tác". Hai việc cả hai bên đều thấy, nên minh bạch. Lý do theo **cái giá khi sai**: rẻ, sửa được.

### Bước 10: Ô ⑦ · Mức 2, cần người duyệt
- **Ấn:** kéo xuống vùng **Mô phỏng · Nhân viên**, chỉ **ô ⑦**, chỉ khung tím "AI đề xuất".
- **Nói:**
  > "**Mức 2, cần người duyệt**: hoàn tiền và từ chối. Theo đề, `soan_hoan_tien` là thực hiện hoàn tiền thật, tiền đã về người mua thì rất khó lấy lại. Nhân viên thấy đủ căn cứ của hai bên. **Đề xuất của AI để riêng, ghi rõ 'không phải quyết định'**."
- **Mục đích:** chứng minh hai tool tiền **không** do AI tự chạy. Tách "đề xuất" khỏi "quyết định" là luật tách bước của nhóm (R4).

### Bước 11: Hộp xác nhận
- **Ấn:** bấm **"Duyệt hoàn tiền…"**. Chỉ vào nút Xác nhận đang mờ.
- **Nói:**
  > "Hộp xác nhận ghi hậu quả **'khó đảo lại'**. Phải tick đủ 3 ô thì mới bấm được: đã xem mô tả **lúc đặt**, người bán đã được nghe, và lời doạ không phải căn cứ. Đây là **G16**."
- **Mục đích:** ăn dòng R5 "cần duyệt có xác nhận". Người duyệt phải **thấy hậu quả trước khi bấm**. Ba ô kiểm buộc nhân viên làm đúng ba điều kiện ở §4.

### Bước 12: Duyệt xong
- **Ấn:** tick đủ **3 ô** → gõ lý do `Mô tả lúc đặt 6L, hàng giao 5L, shop xác nhận` → bấm **"Xác nhận hoàn tiền"**. Chỉ vào nút duyệt đã mờ và dòng đỏ trong nhật ký.
- **Nói:**
  > "Hai bên nhận kết quả kèm lý do. Nút duyệt **bị khoá**, nên không thể hoàn hai lần. Nhật ký ghi 'giao dịch thật, **không có nút hoàn tác**'. Nhóm cố ý không làm nút hoàn tác giả, vì đó là hứa điều không làm được."
- **Mục đích:** hoàn tất ca khó **từ đầu đến cuối không can thiệp tay** (R5, 5 điểm). Cho thấy chống thực hiện lặp, và trung thực về việc không đảo ngược được.

### Bước 13: Ô ⑧ · Mức 3, cấm
- **Ấn:** chỉ **ô ⑧**.
- **Nói:**
  > "**Mức 3, cấm**: phạt hay khoá shop. Không có nút ở bất kỳ màn nào, kể cả với nhân viên khiếu nại. Chỉ có đường chuyển bộ phận chuyên trách."
- **Mục đích:** ăn dòng R5 "việc cấm không có nút làm". Đến đây người chấm đã thấy **đủ cả ba mức**, vượt yêu cầu M3 (ít nhất 2 mức).

---

## Phần E · Ca lạ (khoảng 1 phút)

### Bước 14: Nhận ca lạ
- **Ấn:** bấm **↺ Làm lại**, rồi gõ câu TA đưa vào ô *"Ca lạ: gõ tin nhắn…"* dưới Màn 1, nhấn **Enter**.
- **Nói (luôn theo mẫu):** "Ca này sai thì **ai mất gì** → nên AI ở **mức nào** → trên màn hình là **ô số mấy**."
- **Mục đích:** chứng minh thiết kế không chỉ chạy với ca đã tập, và nhóm xử lý ca mới **đúng mức tự chủ đã đặt** (R7, 3 điểm).

| TA đưa | Gõ hoặc ấn | Nói | Mục đích |
|---|---|---|---|
| Đòi SĐT shop | `cho tôi số điện thoại shop` | "Cấm: lộ dữ liệu riêng tư, có thể bị quấy rối. Hai bên trao đổi qua hồ sơ." | Việc không làm #2 |
| Khoá shop, hàng giả | `khoá shop đi hàng giả` | "AI không phạt được. Chuyển bộ phận chuyên trách, không hứa trước kết quả." | Việc không làm #1, mức cấm |
| Tin cụt | `hàng sai rồi xử lý đi` | "AI hỏi lại một câu, chưa gửi gì cho shop. Đây là G10." | Không đoán khi thiếu thông tin |
| Giao chậm | `giao chậm quá` | "Ngoài phạm vi, AI chuyển đúng bộ phận." | Việc không làm #3 |
| Doạ bóc phốt | `hoàn tiền ngay không thì bóc phốt` | "Lời doạ không phải căn cứ, theo hướng nào cũng vậy. Hoàn tiền cần nhân viên duyệt." | Trung lập trước áp lực |
| Shop im lặng | Làm lại → **"Bổ sung ảnh nhãn/model"** → **⏩ Tua 24 giờ** | "Hồ sơ chuyển nhân viên. Shop im lặng **không** tự động thua, và không tool tiền nào tự chạy." | Quá hạn không tự quyết |
| Đòi gặp người ngay | Làm lại → **🙋 Nhờ nhân viên xem xét** → kéo xuống vùng nhân viên | "Hồ sơ chuyển ngay, nhưng nút duyệt bị khoá tới khi shop phản hồi hoặc hết 24 giờ. Chuyển người không có nghĩa là bỏ qua việc nghe người bán." | Hai bên luôn được nghe |
| Ca không gõ được | (nói) | Trả lời theo mẫu, chỉ vào **ô ⑤** "Nhờ nhân viên xem xét". | Luôn có đường lui |

---

## Phần F · Câu chốt (khoảng 15 giây)

### Bước 15: Kết
- **Ấn:** không bấm gì.
- **Nói:**
  > "Tóm lại: việc nào sai mà rẻ thì AI tự làm và có nút sửa. Việc làm mất tiền thì phải có người duyệt và thấy rõ hậu quả. Việc bị cấm thì không có nút. Người mua luôn biết bước tiếp theo, và người bán đúng không bị xử thua. Em cảm ơn."
- **Mục đích:** gói toàn bộ lập luận về mức tự chủ (dựa trên **cái giá khi sai**) vào một câu, và nhắc lại đúng "kết quả" của lát cắt trong đề.

---

## Khi bị hỏi thêm

| Câu hỏi | Ấn | Trả lời | Mục đích |
|---|---|---|---|
| "Chỗ nào là G__?" | Chỉ ô | G11 → ① · G2, G10 → ② · G9 → ④ · G16 → ⑦ · PAIR Errors → ⑤ | Giữ điểm HAX ở R5 (không chỉ được thì mất điểm) |
| "Sao không cho AI tự hoàn khi chắc?" | **K2** → "Không có gì khác, chỉ là mặc chật" → "Vẫn gửi khiếu nại" → (Màn 2) "Gửi bảng size lúc bán…" → "Vẫn muốn nhân viên xem xét" | "Áo đúng size, khách doạ bóc phốt. Nếu AI chiều khách thì shop mất tiền oan, không lấy lại được. Ở đây AI chỉ **đề xuất** từ chối, nhân viên vẫn phải duyệt." | Bảo vệ lựa chọn mức "cần duyệt" bằng ca người bán đúng |
| "Sao không hiện % tự tin?" | Chỉ ô ② | "Không có căn cứ cho con số đó, và con số sẽ kéo nhân viên duyệt theo nó. Nhãn từng bằng chứng cho biết rõ còn thiếu gì." | Trình bày phương án đã loại và vì sao (R5, lập luận) |
| Bấm nhầm | **↺ Làm lại** | (nói tiếp từ đầu ca) | Không bị kẹt khi demo |
