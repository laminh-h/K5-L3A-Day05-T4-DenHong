# Dàn ý bài nộp *(spec.md — nộp trước 23:59 ngày lab của lớp)*

> Copy dàn ý này vào `spec.md` của nhóm. Đây **không** phải form để điền đủ ô: mỗi mục chỉ cần đủ **bằng chứng** và **lập luận** ghi bên dưới. Viết ngắn, gạch đầu dòng là được. Hướng dẫn từng chặng: `02-guide.md`. Cách chấm: `04-rubric.md`.
>
> **Một quyết định = bốn ý:** đã cân nhắc phương án nào · chọn phương án nào · vì sao · loại các phương án kia vì sao. Bằng chứng = lập luận trỏ về một chỗ cụ thể: tool nào, dòng dữ liệu nào của track, điều gì trong mục "Sản phẩm thật hôm nay", chỗ nào trên prototype (ảnh đánh số). Không chạy agent.

```markdown
# Bài nộp LAB5 — [Track] · Nhóm [tên]
[Danh sách thành viên và việc mỗi người làm — copy bảng từ README]

## §1. Lát cắt & phạm vi
- Lát cắt (chép từ track).
- 3 việc tính năng KHÔNG làm, mỗi việc một câu vì sao.

## §2. Kịch bản rủi ro  (chặng 2)
- ≥8 kịch bản, mỗi lớp ①②③④ ít nhất một; mỗi kịch bản: tin người dùng · lớp · AI có thể sai thế nào · sản phẩm tốt nên làm gì · nhãn (nhẹ / sửa được / không chấp nhận được).
- Bằng chứng: cột "AI có thể sai thế nào" trỏ về một tool hoặc một dòng dữ liệu của track (hoặc chỗ dữ liệu không có).
- Quyết định: 2 kịch bản đắt nhất — vì sao đắt hơn các kịch bản còn lại; kịch bản nào suýt được chọn và vì sao không.

## §3. Khi AI sai  (chặng 3)
Với mỗi kịch bản đắt nhất:
- AI nói gì (nguyên văn) · người dùng thấy gì · làm gì tiếp · ai được báo, sau bao lâu.
- Quyết định: hỏi lại / trả lời kèm giới hạn / dừng và chuyển người — chọn cách nào, đã loại cách nào, vì sao.
- Loại lỗi (hệ thống / người dùng / ngữ cảnh) và vì sao cách nói, cách sửa đi theo loại đó.
- 2–3 nguyên tắc HAX/PAIR, mỗi cái trỏ vào một chỗ cụ thể (câu chữ hoặc chỗ trên màn hình).
- Lỗi nào sửa câu chữ không cứu được (nếu có), và thiết kế cứu nó thế nào.

## §4. Mức tự chủ  (chặng 4)
Với mỗi tool:
- Mức của nhóm (tự làm / cần người duyệt / cấm). Nếu cần người duyệt: ai duyệt · người duyệt thấy gì · quá hạn thì sao.
- Lý do theo cost-of-error: sai thì ai chịu gì · đảo lại được không · chờ người thì mất gì.
- Phương án đã cân nhắc và vì sao loại.
Thêm:
- Tool khó xếp nhất: mỗi người từng chọn gì, cái giá của mỗi phía (trỏ về kịch bản ở §2), nhóm chốt thế nào.
- Thử mức đã đặt trên 2 kịch bản đắt nhất + 1 kịch bản bình thường: cái sai có bị chặn không? còn việc nào làm khi lẽ ra phải hỏi? người dùng bình thường có phải chờ vô ích không?
- Luật thêm hoặc tool tách bước (nếu có), và vì sao.
- Một mức tự chủ đã đổi lời hứa nào với người dùng.

## §5. Prototype

### Link, công cụ, phần mock, lời gọi AI

- **File:** [`prototype/index.html`](prototype/index.html). Mở bằng trình duyệt, không cần cài đặt, không đăng nhập, không backend.
- **Link chạy trực tiếp:** <https://raw.githack.com/laminh-h/K5-L3A-Day05-T4-DenHong/main/prototype/index.html> (cần repo công khai).
- **Cách chạy và luồng demo:** [`prototype/README.md`](prototype/README.md).
- **Công cụ:** một file HTML/JS thuần, dựng với sự hỗ trợ của coding agent (Claude).
- **Ba ca bấm được** (chọn ở thanh trên cùng):
  - **K1 · Shop sửa mô tả:** kịch bản #2 ở §2. Lúc đặt ghi 6 lít, trang hiện tại ghi 5 lít, nhãn nồi nhận được ghi 5.0L.
  - **K2 · Người bán đúng:** đặt áo M, nhận đúng M, khách mặc chật và doạ bóc phốt. Cùng loại rủi ro "người bán đúng" với kịch bản #4 (top 1) ở §2; prototype dùng áo M để thêm cả lời doạ.
  - **K3 · Gửi nhầm size:** ca thường, kịch bản #3 ở §2.
- **Phần mock:**
  - dữ liệu đơn, mô tả lúc đặt và hiện tại, ảnh (hiện bằng chữ `[Ảnh] …`)
  - đồng hồ mô phỏng, có nút "⏩ Tua 24 giờ" để xem xử lý quá hạn
  - chính sách dựng của nhóm, không phải chính sách Shopee: 7 ngày gửi yêu cầu, shop phản hồi trong 24 giờ, nhân viên xem trong 4 giờ
  - lời gọi tool: chỉ ghi vào nhật ký trên màn hình, không gọi thật
  - câu AI nói: viết sẵn theo từng ca
- **Không có lời gọi AI thật.** Ô "ca lạ" dưới màn người mua trả lời theo luật từ khoá (đòi SĐT, khoá shop, giao chậm, tin cụt, hỏi hạn, doạ bóc phốt). Câu không nhận ra thì đi đường an toàn: hỏi lại, hoặc gợi ý chuyển nhân viên.
- **Bố cục:**
  - Màn 1 người mua và Màn 2 người bán đặt cạnh nhau, cùng nhìn một hồ sơ.
  - Bên dưới là vùng **mô phỏng nhân viên xử lý khiếu nại**. Vùng này cần có vì hai tool tiền ở mức cần người duyệt: thiếu nó thì luồng không đi tới kết quả cuối.

### Ảnh đánh số

- **Ảnh 1:** [`prototype/anh-1-cho-shop-phan-hoi.png`](prototype/anh-1-cho-shop-phan-hoi.png). Ca K1 sau khi người mua bổ sung ảnh nhãn, đang chờ shop phản hồi.
- **Ảnh 2:** [`prototype/anh-2-cho-nhan-vien-duyet.png`](prototype/anh-2-cho-nhan-vien-duyet.png). Ca K1 sau khi shop phản hồi, hồ sơ đang ở chỗ nhân viên duyệt.
- Bấm nút "① Số chú thích" trên prototype để hiện đúng các số này.

![Ảnh 1: K1 chờ shop phản hồi](prototype/anh-1-cho-shop-phan-hoi.png)
![Ảnh 2: K1 chờ nhân viên duyệt](prototype/anh-2-cho-nhan-vien-duyet.png)

| Số | Thể hiện gì | HAX/PAIR | Mức tự chủ |
|---|---|---|---|
| ① | Mô tả **lúc đặt** (viền xanh, "dùng để đối chiếu") cạnh mô tả **hiện tại** ("chỉ để tham khảo"), có nguồn và thời điểm. Nhãn "mô tả đã thay đổi" không kết tội shop. | **G11** giải thích vì sao · PAIR Explainability | Thông tin, không có hành động |
| ② | Mỗi bằng chứng có nhãn **đã xác minh / đã ghi nhận, chưa xác minh / chưa có**, kèm dòng "Chưa đủ căn cứ để kết luận · còn thiếu: …". Đây là **cách hiện độ chắc**. | **G2** làm rõ AI làm tốt tới đâu · **G10** thu hẹp khi không chắc | AI không kết luận |
| ③ | Thanh trạng thái 5 bước (Tiếp nhận → Chờ bổ sung → Chờ shop phản hồi → Chờ nhân viên duyệt → Có quyết định), hạn 7 ngày, thời điểm ghi nhận, thời gian còn lại | PAIR Mental models · rubric T4 #8 | — |
| ④ | Nhật ký việc AI tự làm (`yeu_cau_bang_chung`, `chuyen_truong_nhom`). Cả hai bên đều thấy. Mỗi dòng có nút **✎ Đính chính** hoặc **↩ Yêu cầu phân lại**. | **G9** sửa sai dễ | **Tự làm, có đường sửa** |
| ⑤ | Nút "🙋 Nhờ nhân viên xem xét" luôn có. Hồ sơ chuyển đi kèm đủ bằng chứng, người dùng không phải kể lại. | PAIR Errors + Graceful failure | Đường chuyển người |
| ⑥ | Phía người bán: hạn phản hồi 24 giờ và thời gian còn lại; người mua hiện là N\*\*\*h, ẩn SĐT và địa chỉ; ghi rõ quá hạn không tự động thua và lời doạ không phải căn cứ. | PAIR Trust · rubric T4 #3, #4, #6 | — |
| ⑦ | Thẻ duyệt của nhân viên: toàn bộ căn cứ, phần còn thiếu, **đề xuất của AI tách riêng** và ghi "không phải quyết định". Hộp xác nhận ghi hậu quả "khó đảo lại", 3 ô kiểm và lý do bắt buộc. Nút duyệt khoá khi người bán chưa được nghe, và khoá sau khi đã duyệt. | **G16** cho thấy hậu quả | **Cần người duyệt** (`soan_hoan_tien`, `tu_choi_khieu_nai`) |
| ⑧ | `phat_shop` **không có nút** ở bất kỳ màn nào, chỉ có dòng giải thích và đường "ghi chú chuyển bộ phận chuyên trách". | — | **Cấm** |

### Quyết định về cách hiện

**1. Độ chắc: nhãn trạng thái cho từng bằng chứng (chọn)**
- *Đã cân nhắc:*
  - thanh % tự tin
  - nhãn đèn xanh/đỏ "khả năng người mua đúng"
- *Vì sao loại:*
  - AI không có căn cứ để ra con số %, và con số sẽ kéo nhân viên duyệt theo nó thay vì theo bằng chứng.
  - Đèn xanh/đỏ nghiêng về một bên trước khi người bán được nghe.
- *Vì sao chọn:* nhãn từng bằng chứng trả lời đúng lời phàn nàn của người mua trong đề: "không ai nói tôi còn thiếu cái gì".

**2. Bằng chứng AI dựa vào: hai bản mô tả đặt cạnh nhau (chọn)**
- *Đã cân nhắc:*
  - chỉ hiện bản lúc đặt
  - hiện kiểu diff, gạch xoá chỗ bị sửa
  - chỉ để AI nói trong chat
- *Vì sao loại:*
  - Chỉ hiện bản lúc đặt thì người mua không hiểu vì sao trang hiện tại lại khác.
  - Diff gạch xoá trông như kết tội shop.
  - Chat thuần làm chìm mất khác biệt giữa hai bản trong một đoạn chữ dài.
- *Vì sao chọn:* đặt cạnh nhau, có viền "dùng để đối chiếu" và nguồn kèm thời điểm, thì người xem tự kiểm được AI dựa vào đâu.

**3. Điều khiển mức tự chủ: mỗi mức một hình thức riêng (chọn)**
- Ba hình thức:
  - tự làm: dòng nhật ký có nút sửa
  - cần duyệt: nút chỉ có ở vai nhân viên, kèm hộp xác nhận
  - cấm: không có nút
- *Đã cân nhắc:*
  - cho người mua bấm "Xác nhận hoàn tiền"
  - đặt mọi hành động cùng một kiểu nút và phân biệt bằng màu
- *Vì sao loại:*
  - Người mua không có quyền duyệt, và dễ hiểu nhầm là "đã được hoàn".
  - Cùng kiểu nút thì người xem không nhận ra việc nào AI tự làm, việc nào cần người.
- *Ghi chú:* K3 vẫn có hộp xác nhận cho người mua, nhưng ghi rõ "đây là gửi yêu cầu, chưa phải nhận tiền".

**4. Hai bên trên cùng một màn hình (chọn)**
- *Đã cân nhắc:* chuyển qua lại bằng tab người mua / người bán.
- *Vì sao loại:* khi demo, khó thấy một hành động bên này làm thay đổi gì bên kia.
- *Vì sao chọn:* sự trung lập là cốt lõi của track, và đặt cạnh nhau cho thấy ngay hai bên thấy cùng một hồ sơ. Trên màn hình hẹp, hai màn tự xếp dọc.

**5. Không có nút hoàn tác cho giao dịch tiền (chọn)**
- *Đã cân nhắc:* thêm nút "hoàn tác" sau khi duyệt, cho đồng bộ với các hành động tự làm.
- *Vì sao loại:* đề ghi tiền đã chuyển thì khó đảo lại, nên nút hoàn tác là lời hứa giả.
- Thay vào đó, nhật ký ghi "Giao dịch thật, không có nút hoàn tác". Chống thực hiện nhầm bằng hộp xác nhận và khoá nút sau khi duyệt.

**Giới hạn đã biết:**
- Ô ca lạ chỉ nhận diện theo từ khoá, chưa phải AI thật.
- Kiểm quyền duyệt chỉ mô phỏng bằng giao diện. Bản thật phải kiểm quyền ở backend.
- Khi bằng chứng mới tới sau lúc đã có đề xuất, prototype chưa bắt nhân viên duyệt lại.
- Chưa có màn riêng cho ca "thiếu snapshot mô tả lúc đặt".

## §6. Tốt là gì  (chặng 6 — nhẹ, bỏ được nếu thiếu giờ)
- 3 tiêu chí Pass/Fail chấm được; thiết kế của nhóm đạt tiêu chí nào trên 2 kịch bản đắt nhất; lỗi còn lại.

## §7. Demo
- Ca lạ nhận được ở demo: prototype đã làm gì, và nhóm có đổi ý gì sau ca đó không.
```