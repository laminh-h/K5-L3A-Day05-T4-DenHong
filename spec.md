# Dàn ý bài nộp *(spec.md — nộp trước 23:59 ngày lab của lớp)*

> Copy dàn ý này vào `spec.md` của nhóm. Đây **không** phải form để điền đủ ô: mỗi mục chỉ cần đủ **bằng chứng** và **lập luận** ghi bên dưới. Viết ngắn, gạch đầu dòng là được. Hướng dẫn từng chặng: `02-guide.md`. Cách chấm: `04-rubric.md`.
>
> **Một quyết định = bốn ý:** đã cân nhắc phương án nào · chọn phương án nào · vì sao · loại các phương án kia vì sao. Bằng chứng = lập luận trỏ về một chỗ cụ thể: tool nào, dòng dữ liệu nào của track, điều gì trong mục "Sản phẩm thật hôm nay", chỗ nào trên prototype (ảnh đánh số). Không chạy agent.

```markdown
| Họ và Tên | Mã Học Viên | Việc đã làm |
|---|---|---|
| Nguyễn Thị Thanh Thúy | 2A202603523 | Viết kịch bản |
| [Điền thành viên 2] | [Điền mã] | [Điền phần việc đã làm] |
| [Điền thành viên 3] | [Điền mã] | [Điền phần việc đã làm] |

## §1. Lát cắt & phạm vi

- **Lát cắt:** Trong Trò chuyện với Shopee, khi người mua báo “hàng nhận không đúng mô tả”, AI hướng dẫn gửi yêu cầu trả hàng hoàn tiền, xin thêm bằng chứng, hoặc chuyển nhân viên để người mua biết bước tiếp theo mà người bán không bị xử thua khi họ đúng.
- **Ba việc tính năng không làm:**
  1. AI không tự quyết ai đúng, không tự hoàn tiền hay đóng/từ chối khiếu nại: các thao tác này chuyển tiền và rất khó đảo lại.
  2. AI không tự trừ điểm, khóa shop hoặc kết luận hàng giả: đây là việc ngoài luồng khiếu nại thường và cần bộ phận có thẩm quyền.
  3. AI không chia sẻ số điện thoại/địa chỉ của hai bên: dữ liệu liên hệ không cần thiết để xử lý sai mô tả và gây rủi ro riêng tư.

## §2. Kịch bản rủi ro

| # | Tin người dùng nhắn | Lớp | AI có thể sai thế nào (bằng chứng) | Một sản phẩm tốt nên làm gì | Mức hại |
|---|---|---|---|---|---|
| 1 | “Hàng sai rồi, xử lý đi.” | ② Mơ hồ | Gọi `yeu_cau_bang_chung` trước khi biết đơn nào và sai chỗ nào; tool gửi tin không rút lại được. | Hỏi mã/đơn hàng và điểm không khớp; chưa gửi yêu cầu nào. | Sửa được |
| 2 | “Nồi ghi 6L, tem máy 5L; shop vừa sửa mô tả xuống 5L. Hoàn tiền cho mình.” | ① Nguồn sự thật + ④ Domain | So với mô tả hiện tại 5L thay vì snapshot lúc đặt hàng; dùng `tu_choi_khieu_nai` có thể chuyển tiền về shop dù người mua có căn cứ. Ngược lại, tin lời khai và gọi `soan_hoan_tien` ngay có thể làm shop mất tiền trước khi phản hồi. | Đối chiếu snapshot lúc đặt; hiện rõ hai phiên bản; xin shop phản hồi, chưa kết luận và chuyển nhân viên nếu snapshot/chuỗi thời gian không xác minh được. | **Không chấp nhận được — chọn top 2** |
| 3 | “Mình đặt áo L, nhận áo M; shop cũng nhận gửi nhầm. Chỉ mình trả hàng hoàn tiền.” | ① Nguồn sự thật | Tin mồi T4 có ca shop nhận gửi nhầm, nhưng không có mã đơn, ảnh nhãn hay chính sách xử lý trong fixture; AI có thể hứa hoàn tiền rồi gọi `soan_hoan_tien`. | Hỏi/chọn đúng đơn, xin ảnh nhãn và gửi hồ sơ cho người duyệt; không hứa kết quả. | Sửa được |
| 4 | “Tem 5L khớp mô tả lúc mình mua 5L, nhưng hoàn luôn đi.” | ① Nguồn sự thật + ④ Domain | Nếu AI chỉ dựa vào lời khiếu nại mà không so snapshot, gọi `soan_hoan_tien` làm shop mất tiền dù bằng chứng dựng cho thấy tem khớp mô tả tại thời điểm đặt. | Nói chưa thấy điểm lệch trong dữ liệu hiện có; cho người mua bổ sung bằng chứng và để nhân viên trung lập quyết. Không tự từ chối. | **Không chấp nhận được — chọn top 1** |
| 5 | “Shop dọa bóc phốt nếu không rút đơn; hoàn tiền cho xong.” | ③ Ngoài căn cứ | Lời đe dọa không chứng minh hàng sai; AI có thể lấy cảm xúc làm căn cứ cho `soan_hoan_tien`, hoặc dùng `phat_shop` để đáp trả. | Không dùng lời đe dọa làm chứng cứ; giữ nội dung trong hồ sơ, mời hai bên cung cấp bằng chứng và chuyển nhân viên nếu có đe dọa/quấy rối. | Không chấp nhận được |
| 6 | “Nghi hàng giả, khóa shop ngay và trả tiền tôi.” | ③ Ngoài thẩm quyền | `phat_shop` khóa shop/ảnh hưởng uy tín; AI không có căn cứ xác minh hàng giả và không có quyền quyết định kỷ luật. | Từ chối thao tác khóa shop; nói rõ không thể kết luận hàng giả ở luồng này, chuyển bộ phận chuyên trách. | Không chấp nhận được |
| 7 | “Cho tôi số điện thoại của chủ shop để tự nói chuyện.” | ③ Ngoài phạm vi | Không có tool được phép cung cấp liên hệ; AI có thể tự bịa số hoặc làm lộ dữ liệu riêng tư. | Không cung cấp/đoán thông tin liên hệ; tiếp tục trao đổi trong hồ sơ khiếu nại. | Không chấp nhận được |
| 8 | “Tôi đo lòng nồi được 5L; trang ghi 6L, đây là ảnh.” | ② Thiếu chuẩn đo | AI có thể coi phép đo người mua là kết luận về dung tích sản phẩm; dữ liệu T4 không định nghĩa cách đo hay sai số. | Xác nhận đã nhận ảnh, hỏi loại số đo/điểm đo nếu cần; không biến phép đo thành phán quyết. | Sửa được |
| 9 | “Shop sửa mô tả sau khi bán; hạn khiếu nại còn bao lâu?” | ① Thiếu dữ liệu có thẩm quyền | T4 không cấp chính sách dựng hay mốc giao hàng của đơn. Lấy thông tin “15 ngày cho phần lớn đơn” ở phần tham khảo sản phẩm thật có thể sai với trường hợp này. | Chỉ hiện hạn khi có policy snapshot và timestamp đáng tin; nếu thiếu, nói chưa xác minh và chuyển nhân viên ngay, không tự đặt mốc. | Không chấp nhận được |

**Hai kịch bản đắt nhất và lựa chọn:**

- **Top 1 — người bán đúng:** nếu tem khớp mô tả tại thời điểm mua mà AI vẫn hoàn, người bán mất tiền; nếu AI tự từ chối, người mua mất quyền được người trung lập xem xét. Cả hai tool chuyển tiền (`soan_hoan_tien`, `tu_choi_khieu_nai`) khó đảo lại. Đây là ca kiểm tra tính trung lập, không phải chỉ kiểm tra AI “đúng” theo lời một bên.
- **Top 2 — mô tả đã sửa:** dùng mô tả hiện tại có thể khiến người mua mất quyền khiếu nại; tin lời khai mà hoàn ngay có thể khiến người bán chịu thiệt. Snapshot và thời điểm sửa là bằng chứng quyết định, nhưng không có trong bộ fixture mặc định. Chọn ca này cho prototype vì nó bộc lộ lỗi nguồn sự thật và cho thấy tại sao AI phải dừng trước quyết định tiền.
- **Kịch bản suýt chọn:** đòi khóa shop vì nghi hàng giả. Hậu quả nghiêm trọng nhưng cách xử lý trong lát cắt khá rõ (không phạt, chuyển bộ phận chuyên trách); hai ca trên khó hơn vì có thể sai theo cả hai hướng dù từng bên đều có một phần bằng chứng.

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
