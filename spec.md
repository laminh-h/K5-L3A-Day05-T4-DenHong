# Bài nộp LAB5 — T4 Thương mại điện tử · Nhóm Đèn Hồng

**Lớp:** L3A · **Track:** T4 · **Repo:** [K5-L3A-Day05-T4-DenHong](https://github.com/laminh-h/K5-L3A-Day05-T4-DenHong)

> Bản nháp cần nhóm bổ sung họ tên, mã học viên và phân công thật trước khi nộp. Toàn bộ đơn hàng, ngày giờ, phản hồi shop và chính sách ghi “fixture” dưới đây là dữ liệu dựng cho prototype, không phải dữ liệu hay chính sách Shopee.

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

## §3. Khi AI sai

### Top 1 — người bán đúng, bằng chứng hiện có khớp mô tả

- **AI nói nguyên văn:** “Mình thấy tem sản phẩm bạn gửi khớp với mô tả được lưu tại thời điểm đặt hàng. Mình chưa đủ căn cứ để nói hàng sai mô tả, và cũng chưa đóng khiếu nại. Bạn có thể bổ sung ảnh/chi tiết khác hoặc yêu cầu nhân viên xem lại hồ sơ.”
- **Người mua thấy:** nhãn “Chưa đủ căn cứ — chưa có quyết định”; dữ liệu đối chiếu gồm snapshot lúc mua và ảnh tem đã gửi; thấy rõ AI không hoàn tiền cũng không từ chối.
- **Bước tiếp:** người mua có thể bổ sung bằng chứng hoặc bấm chuyển nhân viên. Không làm gì thì hồ sơ vẫn mở, không tự đóng.
- **Ai được báo:** nếu người mua gửi thêm bằng chứng, shop nhận yêu cầu phản hồi đã được người mua xem trước; nhân viên chỉ được báo khi người mua chọn chuyển hoặc quy tắc hồ sơ yêu cầu rà soát. Không gửi kết luận/địa chỉ/điện thoại cho bên kia.
- **Lựa chọn:** chọn trả lời có giới hạn và đưa nút chuyển người; loại “tự từ chối” vì ảnh hiện tại có thể chưa đầy đủ, loại “tự hoàn” vì bằng chứng đang khớp mô tả.
- **Loại lỗi:** lỗi ngữ cảnh nếu AI dùng một bằng chứng đúng nhưng thiếu các ảnh/chi tiết khác để hiểu trường hợp; lỗi hệ thống nếu không lấy được snapshot đã lưu. Câu chữ nói “chưa đủ căn cứ”, không quy lỗi cho người mua; lỗi hệ thống phải báo thiếu dữ liệu và chuyển người, không chỉ xin ảnh thêm.

### Top 2 — mô tả shop đã sửa sau thời điểm đặt

- **AI nói nguyên văn:** “Mình thấy mô tả hiện tại là 5L, còn bản lưu tại thời điểm bạn đặt ghi 6L; ảnh tem bạn gửi ghi 5L. Vì mô tả đã thay đổi, mình chưa thể kết luận bên nào đúng. Mình sẽ không hoàn tiền hay đóng khiếu nại lúc này. Bạn có muốn gửi yêu cầu shop phản hồi trên hồ sơ không?”
- **Người mua thấy:** nhãn “Chưa thể kết luận”; hai phiên bản mô tả có dấu thời điểm; ảnh tem; chính sách fixture và thời hạn được gắn nhãn “dữ liệu demo”. Có thể xem trước và xác nhận yêu cầu phản hồi shop, hoặc chuyển nhân viên.
- **Bước tiếp:** chỉ sau khi người mua xác nhận, gửi yêu cầu shop phản hồi; trong prototype, hạn phản hồi shop là SLA fixture 24 giờ, không phải chính sách Shopee. Nếu shop không phản hồi đúng hạn, chuyển nhân viên; không tự hoàn/từ chối.
- **Ai được báo:** shop nhận đúng phần khiếu nại và câu hỏi cần phản hồi, không nhận thông tin liên hệ riêng; người mua thấy trạng thái gửi và hạn; trưởng nhóm/nhân viên nhận hồ sơ khi người mua yêu cầu hoặc dữ liệu nguồn không khớp.
- **Lựa chọn:** chọn hỏi xác nhận trước khi gửi vì `yeu_cau_bang_chung` gửi tin không thể thu hồi. Loại gửi tự động vì có thể làm lộ/diễn giải sai nội dung; loại dừng ngay và bắt chờ nhân viên vì một yêu cầu phản hồi trung tính, có người mua duyệt, có thể thu thập thêm dữ kiện mà chưa chuyển tiền.
- **Loại lỗi:** lỗi hệ thống nếu không tải được snapshot/lịch sử sửa; lỗi ngữ cảnh nếu snapshot có nhưng hai bên đang nói về cách đo khác nhau. Lỗi hệ thống phải chuyển người kèm dữ liệu thiếu; lỗi ngữ cảnh cần hỏi lại/nhận thêm bằng chứng. Không xin lỗi chung chung thay cho sửa đường đi.

**Lỗi câu chữ không cứu được:** “Shop sai, đã hoàn tiền” dù hệ thống chỉ đọc mô tả hiện tại. Câu nói thận trọng hơn không làm giao dịch hoàn tiền có thể đảo ngược. Thiết kế chặn từ trước: không có nút tự hoàn/từ chối/phạt trong AI; so sánh snapshot lúc mua, yêu cầu người mua duyệt trước khi gửi tin và chuyển người khi snapshot vắng/không đáng tin.

**HAX/PAIR dùng trong thiết kế:**

- **HAX G2 — làm rõ AI làm tốt đến đâu:** nhãn “Chưa đủ căn cứ/Chưa thể kết luận” trên thẻ kết quả của prototype, không dùng phần trăm tự tạo.
- **HAX G10 — thu hẹp phạm vi khi nghi ngờ:** câu AI hỏi xác nhận gửi yêu cầu shop; không kết luận từ mô tả hiện tại.
- **PAIR Explainability + Trust:** thẻ đối chiếu ghi rõ “mô tả lúc đặt” và “mô tả hiện tại” cùng nguồn/thời điểm; người mua tự kiểm được căn cứ.
- **PAIR Errors + Graceful Failure / HAX G8-G9:** nút chuyển nhân viên và sửa/bổ sung thông tin là đường lui cụ thể; nhân viên nhận tóm tắt để người mua không phải kể lại.

## §4. Mức tự chủ

| Tool | Mức của nhóm | Ai duyệt / quá hạn | Cost-of-error và phương án đã loại |
|---|---|---|---|
| `yeu_cau_bang_chung` | **Cần người duyệt** | Người gửi yêu cầu xem trước nội dung và xác nhận. Không xác nhận thì không gửi; nếu sắp hết hạn thì báo rõ và chuyển nhân viên kiểm tra hạn. | Tin gửi rồi không thu hồi; yêu cầu sai có thể gây áp lực hoặc làm lộ diễn giải lệch. Tự gửi nhanh hơn nhưng thiệt hại niềm tin lớn hơn một lần bấm xác nhận. |
| `chuyen_truong_nhom` | **Tự làm** | Không cần duyệt; trưởng nhóm có thể trả hồ sơ về luồng nếu chuyển nhầm. | Chuyển nhầm chủ yếu tốn công và đảo lại được; bắt người mua duyệt sẽ tăng thời gian trong khi không có quyết định tiền. |
| `soan_hoan_tien` | **Cần người duyệt** | Nhân viên trung lập xem snapshot lúc đặt, phản hồi hai bên và policy; không duyệt thì không hoàn, hồ sơ chuyển tiếp/giữ mở theo chính sách có thẩm quyền. | Tiền về người mua, người bán mất tiền/hàng; khó đảo. Cấm hoàn toàn làm chậm cả ca rõ như shop nhận gửi nhầm, nên cho phép đề xuất nhưng không thực thi tự động. |
| `tu_choi_khieu_nai` | **Cấm với AI** | Nhân viên có thẩm quyền quyết định ngoài quyền AI; thiếu căn cứ thì không đóng hồ sơ tự động. | Đóng đơn và chuyển tiền cho shop khó đảo; ca tem khớp chưa đủ chứng minh mọi nội dung khiếu nại sai. Loại “AI từ chối có người duyệt” để không biến kết quả AI thành mặc định gây áp lực xác nhận. |
| `phat_shop` | **Cấm với AI trong lát cắt này** | Nếu có nghi hàng giả/vi phạm, chuyển bộ phận chuyên trách; AI không đề xuất hay thực thi hình phạt. | Khóa shop/trừ uy tín ảnh hưởng nhiều người và rất khó khôi phục. Loại “cần người duyệt” vì quyết định kỷ luật nằm ngoài thẩm quyền của luồng khiếu nại này. |

**Tool khó xếp nhất — `yeu_cau_bang_chung`:** phương án tự gửi giúp shop phản hồi sớm nhưng tin không thu hồi được và có thể yêu cầu sai; phương án chờ nhân viên an toàn hơn nhưng kéo dài thời gian cho cả hai bên. Nhóm chọn người nhận xem trước và xác nhận nội dung: một bước ngắn chặn được gửi nhầm, vẫn thu thập được phản hồi mà không phán quyết tiền. Nếu không xác nhận hoặc không có dữ liệu hạn đáng tin, AI chuyển nhân viên thay vì tự tạo deadline.

**Thử mức đã đặt:**

| Ca | Cái sai có bị chặn? | AI còn làm gì khi lẽ ra phải hỏi? | Người dùng bình thường có phải chờ vô ích? |
|---|---|---|---|
| Mô tả đã sửa (top 2) | Có: không hoàn/từ chối; so snapshot; tin xin shop phản hồi chỉ gửi sau xác nhận. | Không. Thiếu snapshot thì chuyển người; không lấy mô tả hiện tại làm kết luận. | Không phải chờ người để gửi yêu cầu trung tính sau khi xác nhận; chỉ quyết định tiền cần nhân viên. |
| Người bán đúng (top 1) | Có: `tu_choi_khieu_nai` và `soan_hoan_tien` không tự chạy; người mua còn đường bổ sung/chuyển người. | Không. AI chỉ báo phần bằng chứng đang khớp và hỏi bước tiếp theo. | Không phải chờ để xem bằng chứng/đính chính; chờ người chỉ khi muốn phán quyết cuối. |
| Bình thường — áo L đặt, nhận M, shop nhận gửi nhầm | Có: không hứa hoàn; yêu cầu ảnh/mã đơn và đưa đề xuất cho nhân viên. | Không; trước khi gửi yêu cầu shop, người gửi xác nhận nội dung. | Có một xác nhận ngắn; không chờ nhân viên cho việc nộp bằng chứng, nhưng phải chờ người duyệt tiền. |

**Lời hứa thay đổi:** thay “AI xử lý xong khiếu nại cho bạn” bằng “AI giúp bạn gửi đúng bằng chứng và theo dõi hồ sơ; người có thẩm quyền quyết định tiền”. Đổi lại một chút tốc độ để không mặc định bên nào chịu thiệt.

## §5. Prototype

- **File:** [`prototype/index.html`](prototype/index.html). Mở bằng trình duyệt; không đăng nhập, không backend, không gọi AI thật. Hội thoại và nút là mô phỏng tĩnh có tương tác; các ngày, mô tả và SLA đều là dữ liệu fixture tự tạo.
- **Ca demo:** mô tả tại thời điểm đặt là 6L, mô tả hiện tại là 5L, ảnh tem là 5L. AI nêu mâu thuẫn, không phán quyết; người mua xem trước/xác nhận yêu cầu shop phản hồi hoặc chuyển nhân viên. Tab “Góc nhìn shop” cho thấy shop nhận phần nào và hạn phản hồi fixture.
- **Độ chắc/căn cứ:** nhãn “Chưa thể kết luận”; đối chiếu snapshot lúc đặt và mô tả hiện tại có timestamp. Hạn yêu cầu dựng từ policy fixture 10 ngày từ lúc giao; ghi rõ đây không phải chính sách thật.
- **Các số chú thích trên prototype:**
  1. Nhãn “Chưa thể kết luận” → HAX G2.
  2. Snapshot lúc đặt so với mô tả hiện tại → PAIR Explainability + Trust.
  3. Xem trước/xác nhận yêu cầu shop → HAX G10, kiểm soát tool không thể thu hồi.
  4. Hạn phản hồi fixture và trạng thái hai bên → lỗi có đường lui, không kết luận vắng mặt là có lỗi.
  5. Chuyển nhân viên kèm tóm tắt → PAIR Errors + Graceful Failure.
  6. Không có nút AI hoàn tiền/từ chối/phạt; yêu cầu số điện thoại bị từ chối → giới hạn quyền và riêng tư.
- **Cách hiện đã chọn:** một màn hình hồ sơ có tab người mua/shop và thẻ chứng cứ, thay vì chat thuần. Chat thuần bị loại vì lời AI có thể che mất khác biệt giữa mô tả lúc mua và hiện tại; màn hình quyết định chia cột được chọn để người xem kiểm nguồn và mức tự chủ trước khi bấm.
- **Ảnh chụp:** [`prototype/01-buyer.png`](prototype/01-buyer.png) là góc nhìn người mua; [`prototype/02-shop.png`](prototype/02-shop.png) là góc nhìn shop. Thẻ căn cứ và điều khiển đã đánh số để đối chiếu HAX/PAIR.

## §6. Tốt là gì

1. **Không chuyển tiền khi AI chưa có căn cứ:** Pass nếu trong ca người bán đúng và ca mô tả đã sửa, AI không tự gọi hoàn tiền/từ chối/phạt; Fail nếu bất kỳ quyết định tiền nào tự chạy.
   - Người bán đúng: Pass — chỉ hiện “chưa đủ căn cứ”, có bổ sung/chuyển người.
   - Mô tả đã sửa: Pass — hiển thị mâu thuẫn, không quyết định tiền.
2. **Nguồn sự thật hiển thị:** Pass nếu ca mô tả đã sửa hiện cả snapshot lúc đặt và mô tả hiện tại; Fail nếu chỉ đọc nội dung hiện tại hoặc không nêu nguồn.
   - Người bán đúng: Pass — có dòng snapshot và ảnh tem.
   - Mô tả đã sửa: Pass — hiện hai phiên bản và dấu thời điểm.
3. **Không gửi tin hay lộ dữ liệu ngoài ý muốn:** Pass nếu yêu cầu shop cần xác nhận trước khi gửi, không chia sẻ liên hệ, và có đường chuyển nhân viên; Fail nếu gửi tự động/lộ số điện thoại/không có đường lui.
   - Người bán đúng: Pass — yêu cầu bổ sung có bước xem trước; chuyển nhân viên hiện rõ.
   - Mô tả đã sửa: Pass — yêu cầu shop chờ xác nhận; chuyển nhân viên có sẵn.

**Lỗi còn lại:** nếu snapshot hoặc timestamp phía sàn sai, giao diện minh bạch vẫn có thể làm người dùng tin dữ liệu sai. Trước khi phát hành cần xác thực nguồn snapshot, log lịch sử sửa và policy; đây không phải lỗi giải quyết được bằng câu chữ.

## §7. Demo

- **Ca demo đã chuẩn bị:** shop sửa mô tả sau khi bán; bấm qua đối chiếu snapshot → xem trước/xác nhận yêu cầu shop phản hồi → chuyển nhân viên nếu thiếu căn cứ. Chỉ ra rõ không có nút AI tự hoàn/từ chối.
- **Ca lạ nhận tại demo:** [ghi ca thực tế TA/nhóm khác đưa, kết quả prototype và điều nhóm đổi sau demo].
- **Phân công trình bày:** [điền theo thành viên thật; mỗi người trình bày phần mình đã làm].
- **Bonus:** prototype không có lời gọi AI thật; nhóm có thể xung phong demo trước lớp nếu có cơ hội.
