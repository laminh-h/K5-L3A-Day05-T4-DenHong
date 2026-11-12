# Phần người 3 — Mức tự chủ & kiểm thử · Nhóm Đèn Hồng · T4

Nội dung để ghép vào §4 và §6 của `spec.md`. Đây là đề xuất thiết kế theo hai ca nhóm đã chốt; chưa phải kết quả kiểm thử prototype. Các mã K1–K3 bên dưới là mã tạm, cần đối chiếu với bảng kịch bản của người 1.

## §4. Mức tự chủ

### 4.1. Nguyên tắc và giới hạn

AI được thu thập bằng chứng và chuyển hồ sơ, nhưng không tự quyết định ai mất tiền. Hoàn tiền và từ chối đều cần nhân viên xử lý khiếu nại duyệt; xử phạt shop nằm ngoài quyền của trợ lý này.

- So sánh hàng nhận với **mô tả tại thời điểm đặt hàng**, không lấy mô tả hiện tại thay thế. Thiếu bản lúc mua thì nói rõ thiếu và chuyển người, không suy đoán.
- Người bán được phản hồi trước khi nhân viên quyết định. Lời doạ bóc phốt, lịch sử một bên hoặc im lặng không tự tạo thành kết luận thắng/thua.
- Không trao đổi số điện thoại, địa chỉ giữa hai bên. Nhân viên chỉ thấy dữ liệu cần xử lý, thông tin nhạy cảm được che.
- Track không cấp tool tra cứu đơn hay lấy lịch sử mô tả. Prototype dùng hồ sơ giả nạp sẵn; bản thật cần nguồn lưu phiên bản đáng tin cậy. Không giả định AI tự khôi phục được bản mô tả đã mất.

### 4.2. Quyền của từng tool và cái giá khi sai

| Tool theo đề | Mức nhóm đề xuất | Sai thì ai chịu gì; có đảo được không? | Vì sao chọn; phương án bị loại; cái giá khi chờ |
|---|---|---|---|
| `yeu_cau_bang_chung` | **Tự làm có điều kiện** | Hỏi sai làm hai bên mất công, có thể lỡ hạn; tin đã gửi không thu hồi được. Có thể gửi đính chính nhưng không xoá tác động của tin cũ. | Cho tự gửi mẫu trung lập, chỉ xin đúng phần đang thiếu sau khi xác định đúng đơn và kiểm tra tài liệu đã có. Loại duyệt mọi tin vì làm ca đơn giản chờ vô ích; loại gửi tự do vì dễ hỏi lặp hoặc đòi dữ liệu riêng tư. Tin mơ hồ chưa xác định được đơn thì chỉ hỏi làm rõ trong chat, chưa gửi yêu cầu sang người bán. |
| `chuyen_truong_nhom` | **Tự làm có điều kiện** | Chuyển nhầm gây thêm hàng chờ và nhân viên mất thời gian; có thể phân lại hồ sơ, nhưng thời gian đã mất không lấy lại được. | Tự chuyển khi mô tả thay đổi, bằng chứng mâu thuẫn/thiếu nguồn gốc, người dùng yêu cầu gặp người hoặc có dấu hiệu ngoài thẩm quyền. Loại chờ duyệt việc chuyển vì tăng một bước trước khi người có quyền nhận hồ sơ; loại chuyển mọi ca vì ca áo gửi nhầm rõ ràng có thể được hướng dẫn ngay. Không tạo hồ sơ trùng. |
| `soan_hoan_tien` | **Cần người duyệt: nhân viên xử lý khiếu nại được phân quyền** | Theo đề, tool này **thực hiện hoàn tiền**, dù tên có chữ “soạn”. Hoàn sai khiến người bán mất tiền, có thể cả hàng; khó đảo khi tiền đã về người mua. | AI chỉ chuẩn bị đề xuất; nhân viên duyệt giao dịch cụ thể sau khi đủ điều kiện. Loại AI tự hoàn dù khách nói rất chắc vì ca K2 người bán có thể đúng. Loại cấm hoàn trong mọi ca vì người mua K1 có thể bị giữ tiền oan. Chờ duyệt làm hoàn tiền chậm hơn, nên hiển thị trạng thái và chuyển hồ sơ sớm. |
| `tu_choi_khieu_nai` | **Cần người duyệt: nhân viên xử lý khiếu nại được phân quyền** | Đóng sai làm người mua mất cơ hội giải quyết và tiền về người bán; khó đảo. K1 có thể bị từ chối oan nếu dùng mô tả đã sửa. | Nhân viên kiểm tra bản mô tả lúc mua, phản hồi hai bên và lý do trước khi duyệt. Loại AI tự từ chối theo tem hoặc im lặng vì tem chưa đủ chứng minh toàn bộ đặc tính, im lặng chưa chứng minh sai. Loại không bao giờ từ chối vì K2 cần bảo vệ người bán đúng. Chờ duyệt kéo dài tranh chấp nhưng tránh đóng hồ sơ bằng suy đoán. |
| `phat_shop` | **Cấm đối với trợ lý trong luồng này** | Trừ điểm/khoá nhầm ảnh hưởng doanh thu và uy tín cả shop; khó khôi phục hoàn toàn. | Luồng hàng sai mô tả không đủ thẩm quyền kết luận gian lận. Loại tự phạt theo yêu cầu khách; cũng loại thêm nút “duyệt phạt” ngay trong prototype vì cần quy trình chuyên trách khác. Chuyển trưởng nhóm để phân tuyến, không hứa mức phạt. Chậm xử phạt có giá, nhưng không biện minh cho phạt khi thiếu xác minh. |

### 4.3. Điều kiện và cơ chế duyệt

**Chính sách dựng của nhóm để demo, không phải chính sách Shopee:** hạn gửi yêu cầu là 7 ngày từ lúc nhận hàng; người bán có 24 giờ từ lúc được thông báo để phản hồi; mục tiêu nhân viên xem hồ sơ là 4 giờ từ lúc chuyển. Hệ thống hiển thị thời điểm cụ thể. Nhóm phải dùng các mốc này thống nhất trong spec và prototype.

Yêu cầu gửi thành công trong hạn được ghi nhận thời điểm tiếp nhận; chờ bằng chứng, phản hồi hoặc nhân viên không làm mất thời điểm này. Mốc 24 giờ và 4 giờ là mốc xử lý, **không phải điều kiện tự động hoàn hay tự động từ chối**. Ngoại lệ quá hạn được chuyển nhân viên xem xét, AI không hứa được chấp nhận.

**Người duyệt thấy:** mã đơn, mặt hàng/số tiền, mốc giao và tiếp nhận, mô tả lúc mua cùng thời điểm/nguồn lưu, mô tả hiện tại để đối chiếu, bằng chứng và phản hồi của cả hai bên, phần còn thiếu hoặc mâu thuẫn, hạn phản hồi, đề xuất AI và hậu quả của hành động. Không hiển thị phần trăm tự tin không có căn cứ.

**Điều kiện trước khi duyệt hoàn hoặc từ chối:** đúng đơn; xác định được nguồn mô tả lúc mua; đã mời người bán phản hồi và nhận được phản hồi hoặc hết hạn; có đủ căn cứ cho quyết định cụ thể. Nếu vẫn thiếu căn cứ, nhân viên yêu cầu bổ sung hoặc chuyển trưởng nhóm, không bấm quyết định cho xong.

**Khi duyệt:** nhân viên chọn quyết định, nhập lý do, kiểm tra đúng người nhận/số tiền nếu hoàn rồi xác nhận hậu quả trước khi hệ thống gọi tool. Người mua bấm “Gửi yêu cầu” chỉ là gửi khiếu nại, không thay thế phê duyệt tài chính. Nếu hồ sơ/bằng chứng thay đổi, đề xuất cũ phải được xem và duyệt lại.

**Quá hạn:** sau 24 giờ chưa có phản hồi thì nhắc người bán và đưa hồ sơ cho nhân viên đánh giá; sau mục tiêu 4 giờ chưa được xem thì báo chậm cho người mua và người bán, nhắc trưởng nhóm phân công. Hồ sơ tiếp tục mở, không tự gọi hai tool quyết định tiền. Không gửi nhắc lặp liên tục.

**Chống thực hiện nhầm:** nút duyệt chỉ có ở vai nhân viên; backend phải kiểm quyền và điều kiện, không chỉ ẩn nút. Một quyết định chỉ được thực hiện một lần cho một phiên bản hồ sơ; không cho vừa hoàn vừa từ chối. Khi tool lỗi hoặc chưa rõ kết quả, kiểm tra trạng thái trước khi thử lại. Không hiện nút hoàn tác giả cho giao dịch khó đảo.

### 4.4. Tool khó xếp nhất: `soan_hoan_tien`

| Phương án đã cân nhắc | Lợi ích | Cái giá theo kịch bản |
|---|---|---|
| AI tự hoàn khi cho là bằng chứng rõ | Người mua nhận tiền nhanh | K2: có thể chiều lời doạ, hoàn oan dù shop giao đúng; tiền khó thu hồi. |
| Nhân viên duyệt giao dịch cụ thể — **chọn** | Kiểm tra hai phía trước khi tiền chuyển | K1 và K3 phải chờ quyết định tiền; giảm thời gian chờ bằng hồ sơ được chuẩn bị đầy đủ, không bắt khách kể lại. |
| Cấm hoàn tiền hoàn toàn trong quy trình | Chặn AI làm mất tiền shop | K1: người mua có bằng chứng vẫn bị bế tắc; không giải quyết được công việc của tính năng. |

Chốt cần người duyệt vì cả hoàn sai và không hoàn khi đáng hoàn đều gây thiệt hại. Không dùng mức tự tin của AI thay cho phê duyệt có bằng chứng.

**Phần cần nhóm xác nhận khi ráp bài:** mỗi thành viên ghi ngắn phương án mình thực sự từng chọn và lý do. Hiện chưa có trao đổi thực tế nên không gán ý kiến cho bất kỳ ai.

### 4.5. Thử mức trên 2 ca khó + 1 ca thường

Đây là kiểm tra logic thiết kế trên giấy; chưa xác nhận các nút hoặc rào chặn đã được lập trình.

| Ca và dữ liệu giả | Luồng theo mức đã đặt | Sai có bị chặn không? | Còn hành động nào cần hỏi trước? | Có chờ vô ích không? |
|---|---|---|---|---|
| **K1 — Shop sửa mô tả:** bản lúc đặt ghi nồi 6 lít, bản hiện tại ghi 5 lít; khách báo nhận 5 lít. Hai phiên bản có mốc lưu. | Hiện hai phiên bản và chỗ lệch; nếu ảnh chưa đủ thì xin phần thiếu; báo người bán và tự chuyển trưởng nhóm. Nhân viên xem trước khi duyệt hoàn/từ chối. Nếu thiếu bản lúc mua thì ghi thiếu, không tự kết luận. | Chặn AI dùng bản hiện tại để tự từ chối hoặc chỉ theo lời khách để tự hoàn. | Khách xác định đúng đơn nếu chưa rõ; nhân viên phê duyệt giao dịch. Cấm phạt shop. | Có chờ xác minh nhưng cần thiết do bằng chứng có thay đổi; hồ sơ và thời điểm tiếp nhận được giữ. |
| **K2 — Người bán đúng:** bản lúc đặt ghi áo M, tem nhận M; khách nói mặc chật và doạ bóc phốt. Không có bằng chứng sai đặc tính khác. | Nêu căn cứ khớp size; hỏi một câu làm rõ có điểm nào khác sai mô tả; cho người bán phản hồi. Nếu vẫn tranh chấp, chuyển trưởng nhóm; chỉ nhân viên được duyệt từ chối có lý do. | Chặn hoàn theo lời doạ và chặn AI đóng ngay chỉ vì tem khớp. Khớp size không tự chứng minh mọi đặc tính đều đúng. | Hỏi rõ điểm sai còn lại, không đoán khách chỉ đổi ý. Nhân viên duyệt nếu đóng. | Không tự chuyển chỉ vì một câu doạ; chuyển khi tranh chấp chưa giải quyết. Chờ quyết định đóng là cần thiết. |
| **K3 — Gửi nhầm rõ ràng:** đơn ghi áo L, ảnh tem M, tin nhắn shop thừa nhận gửi nhầm; khách muốn trả hàng hoàn tiền. | Tự hướng dẫn gửi yêu cầu, tận dụng ảnh/tin nhắn đã có; xin đúng tài liệu còn thiếu nếu có. AI chuẩn bị đề xuất để nhân viên duyệt hoàn sau khi kiểm tra điều kiện trả hàng. | Không chuyển tiền trước duyệt; không đồng nhất shop thừa nhận gửi nhầm với đã hoàn tất điều kiện hoàn. | Khách xác nhận đúng đơn và gửi yêu cầu; nhân viên duyệt tiền. Không tự tạo thao tác trả hàng ngoài bộ tool. | Hướng dẫn và chuẩn bị hồ sơ ngay, không chờ nhân viên chỉ để biết bước tiếp theo. Vẫn phải chờ quyết định tài chính; đây là chi phí nhóm chấp nhận. |

### 4.6. Tách bước và lời hứa với người dùng

Tách **chuẩn bị đề xuất** khỏi **thực hiện quyết định**. Chuẩn bị là trạng thái nội bộ/mock mới do nhóm đề xuất, không đổi nghĩa tool gốc và không chuyển tiền. Nếu triển khai thật phải có nơi lưu đề xuất và kiểm quyền duyệt. Prototype không gọi tool thật.

Lời hứa hiển thị cho người mua và người bán:

> “AI giúp kiểm tra thông tin và chuẩn bị hồ sơ. Nhân viên sẽ xem bằng chứng của cả hai bên trước khi quyết định hoàn tiền hoặc đóng khiếu nại. Gửi yêu cầu không có nghĩa là đã được hoàn tiền.”

Mức cần người duyệt làm lời hứa chuyển từ “xử lý tiền ngay” sang “cho biết bước tiếp theo và trạng thái xử lý”. Không hiển thị “đã hoàn” khi mới gửi đề xuất.

## §6. Tốt là gì — 3 tiêu chí Pass/Fail

| Tiêu chí | Pass khi | Fail khi |
|---|---|---|
| **P1 — Đúng nguồn, nói rõ phần thiếu** | Khi đánh giá sai mô tả, hiển thị bản lúc mua và nguồn/mốc lưu. Thiếu bản đó thì ghi chưa đủ căn cứ và chuyển người. | Dùng bản hiện tại thay bản lúc mua mà không báo, tự bịa bản cũ hoặc kết luận chắc khi thiếu nguồn. |
| **P2 — Quyết định tiền phải được duyệt** | Trước phê duyệt hợp lệ: không gọi hoàn/từ chối, hồ sơ chưa bị đóng; quá hạn không tự quyết; giao dịch đã duyệt không chạy lặp. Không có thao tác phạt shop trong luồng. | Người mua/AI tự thực hiện quyết định tiền; timeout tự quyết; bằng chứng mới vẫn dùng duyệt cũ; gọi trùng hoặc có nút phạt shop. |
| **P3 — Hai bên biết cách tiếp tục** | Khi tiếp nhận: người mua thấy bước tiếp theo, trạng thái và thời điểm ghi nhận. Khi xin phản hồi: người bán thấy nội dung khiếu nại đã che dữ liệu riêng tư và hạn cụ thể. Khi chuyển người: hồ sơ kèm bằng chứng; chậm xử lý có thông báo, không đóng tự động. | Thiếu đường bổ sung/chuyển người, không có hạn phản hồi, bắt kể lại từ đầu, lộ dữ liệu riêng tư hoặc coi im lặng là thua tự động. |

### Chấm thử thiết kế trên giấy

| Ca | P1 | P2 | P3 | Việc chưa kiểm chứng |
|---|---|---|---|---|
| K1 — Mô tả đã sửa | Pass theo thiết kế §4.1/4.5: đối chiếu hai phiên bản, không có bản cũ thì dừng kết luận. | Pass theo thiết kế §4.3: cần người duyệt, không phạt hoặc tự quyết theo hạn. | Pass theo thiết kế §4.3: thông báo hai bên và giữ hồ sơ khi chuyển. | Chưa kiểm chứng lưu phiên bản thật, giao diện, phân quyền hay xử lý timeout. |
| K2 — Người bán đúng | Pass theo thiết kế §4.5: dùng bản lúc mua, chỉ kết luận phần size có căn cứ. | Pass theo thiết kế §4.2/4.3: không hoàn theo lời doạ, không tự đóng. | Pass theo thiết kế §4.5: hỏi điểm sai còn lại, nghe phản hồi, có đường chuyển người. | Chưa kiểm chứng nút hỏi lại, phản hồi phía shop hoặc rào chặn giao dịch. |

**Giới hạn còn lại:** nhân viên vẫn có thể duyệt sai; bản mô tả lưu có thể không đáng tin; cơ chế chặn giao dịch cần backend nếu dùng thật. Prototype chỉ chứng minh luồng và cách hiển thị, không chứng minh an toàn giao dịch thật. Khi có prototype, chạy lại K1–K3, ghi kết quả quan sát và lỗi thật thay vì coi Pass trên giấy là đã kiểm thử phần mềm.

## Bàn giao cho người 2 và người 4

- Có các trạng thái riêng: chờ bổ sung → chờ shop phản hồi → chờ nhân viên duyệt → có quyết định. “Chuyển trưởng nhóm” không đồng nghĩa “đã giải quyết”.
- Màn người mua: xem bản lúc mua, bổ sung bằng chứng, gửi yêu cầu, gặp nhân viên; không có nút trực tiếp hoàn tiền hay đóng khiếu nại.
- Màn người bán: thấy khiếu nại, bằng chứng liên quan đã che thông tin riêng tư và hạn phản hồi; có thể gửi phản hồi/bằng chứng.
- Nếu demo duyệt, dùng khu vực mô phỏng vai nhân viên trong tối đa 2 màn hình: thẻ quyết định ghi căn cứ, hậu quả và bước xác nhận. Ghi rõ đây là mô phỏng, không phải kiểm quyền thật.
- Thao tác tự làm phải có đường sửa: bổ sung/đính chính yêu cầu bằng chứng và yêu cầu phân lại hồ sơ chuyển nhầm. Không giả vờ thu hồi được tin đã gửi; việc hủy chuyển không được làm mất khiếu nại gốc.
- Đánh số vị trí thể hiện bằng chứng, trạng thái duyệt và đường chuyển người để người 2 nối với HAX/PAIR và ảnh trong §5.

## Nói khi demo — khoảng 45 giây

“Phần mình phụ trách là AI được làm tới đâu. Nhóm cho AI tự xin bằng chứng và chuyển hồ sơ khi cần, vì chờ người duyệt từng bước sẽ làm khách mất thời gian. Nhưng hoàn tiền và từ chối khiếu nại đều cần nhân viên duyệt: sai hướng nào cũng có một bên mất tiền, và khó đảo lại. Phạt shop bị cấm trong luồng này. Với ca shop sửa mô tả, AI phải dùng bản lúc mua; thiếu bản đó thì báo thiếu và chuyển người. Với ca người bán đúng, lời doạ không làm phát sinh quyền hoàn tiền. Hết hạn phản hồi cũng không tự động có bên thắng. Đổi lại, người dùng phải chờ quyết định tài chính, nhưng được biết ngay bước tiếp theo và trạng thái hồ sơ.”
