# Draft UX — Người 2 · Cách AI phản hồi (T4)

> Bản làm việc cho §3 của `spec.md`. Phạm vi chỉ là trải nghiệm khi AI không chắc hoặc có thể sai ở hai ca top 1/top 2 trong §2. Không sửa nội dung các phần khác. Mọi đơn, bằng chứng và mốc thời gian dưới đây là dữ liệu dựng.

## Luật UX chung

- Chat luôn ghi rõ **“Trợ lý AI”**; AI nói căn cứ nào đang có, căn cứ nào chưa xác minh, và không kết luận bên nào đúng khi còn thiếu/mâu thuẫn.
- Hai bên cùng nhìn một hồ sơ và trạng thái, nhưng chỉ thấy dữ liệu được phép chia sẻ. Che tên người mua theo prototype; không hiển thị số điện thoại/địa chỉ.
- `yeu_cau_bang_chung` gửi xong thì tin đã tới, không rút lại được: xem trước nội dung yêu cầu và chỉ xin đúng thông tin còn thiếu; không bắt gửi lại bằng chứng đã có.
- `soan_hoan_tien` là **thực hiện hoàn tiền**, không phải soạn bản nháp. `tu_choi_khieu_nai` đóng khiếu nại/chuyển tiền cho người bán. AI không tự gọi hai tool này trong hai ca; nhân viên có thẩm quyền duyệt và thấy rõ hậu quả trước khi thực hiện.
- Mốc **shop phản hồi trong 24 giờ, nhân viên xem trong 4 giờ** là chính sách giả lập trong prototype, không phải chính sách Shopee. Quá hạn không tự động xử thua một bên.

---

## Ca #2 — Mô tả đã sửa sau khi bán · top 2

**Tin:** “Nồi ghi 6L, tem máy 5L; shop vừa sửa mô tả xuống 5L. Hoàn tiền cho mình.”

### Người mua

**AI nói nguyên văn**

> “Mình là trợ lý AI. Đơn này lưu mô tả lúc đặt là ‘6L’; trang hiện tại ghi ‘5L’, và bạn cho biết tem sản phẩm ghi ‘5L’. Các dữ liệu này khác nhau nhưng chưa đủ để kết luận sản phẩm giao sai mô tả — cần xác minh đúng phiên bản lúc đặt và nhãn/model của sản phẩm. Mình chưa hoàn tiền hay từ chối yêu cầu. Bạn có thể gửi ảnh rõ nhãn/model trên chiếc nồi đã nhận không? Mình sẽ gửi yêu cầu shop phản hồi để hai bên cùng được xem xét.”

**Màn hình**

1. Hai thẻ cạnh nhau: **mô tả gắn với đơn lúc đặt** (“6L”, nguồn và thời điểm) và **trang hiện tại** (“5L”, thời điểm ghi nhận). Không gạch xoá hoặc gắn nhãn “shop gian lận”.
2. Thẻ “tem/model sản phẩm”: nếu chỉ là lời người mua thì ghi **“người mua cho biết 5L — chưa xác minh”**; nếu đã có ảnh thì ghi **“đã nhận ảnh — chưa xác minh model”**. Không biến lời khai thành sự thật đã kiểm chứng.
3. Trạng thái **“Chờ shop phản hồi · chưa có quyết định”**; nút **“Bổ sung ảnh nhãn/model”**, **“Xem bằng chứng đã gửi”**, **“Nhờ nhân viên xem xét”**. Mỗi bằng chứng đã ghi nhận đều hiện một lần, tránh hỏi lại.
4. Nhật ký giải thích AI đã gửi yêu cầu nào và tới ai. Vị trí khớp prototype: chú thích §5 số ①–⑤.

**Bước tiếp / thông báo**

- Khi người mua bổ sung ảnh, xác nhận đã nhận và hiện ảnh trong hồ sơ; không gửi yêu cầu trùng.
- AI dùng `yeu_cau_bang_chung` để mời shop kiểm tra đúng phiên bản/mẫu sản phẩm và phản hồi. Trước khi gửi, màn hình nói rõ “shop sẽ thấy nội dung khiếu nại và bằng chứng liên quan”.
- Người bán được báo ngay khi yêu cầu phản hồi được gửi; người mua được báo khi shop trả lời. Cả hai thấy hạn 24 giờ theo chính sách giả lập; nếu hết hạn, trạng thái chuyển nhân viên xem xét, không tự động từ chối/hoàn tiền.
- Chuyển bằng `chuyen_truong_nhom` ngay nếu snapshot lúc đặt không truy xuất được, hai bộ bằng chứng mâu thuẫn, hoặc một bên yêu cầu nhân viên. Nhân viên nhận lịch sử, nguồn/thời điểm dữ liệu, phần còn thiếu; thời gian xem mục tiêu 4 giờ theo chính sách giả lập.

### Người bán

**AI nói nguyên văn**

> “Có yêu cầu xem xét đơn này. Hồ sơ lưu mô tả lúc đặt là ‘6L’; trang hiện tại ghi ‘5L’. Đây là khác biệt cần xác minh, chưa phải kết luận shop sai. Vui lòng kiểm tra đúng phiên bản/mẫu sản phẩm và gửi phản hồi hoặc bằng chứng liên quan trước hạn hiển thị. Không cần gửi thông tin liên hệ riêng của người mua.”

**Màn hình và hành động**

- Hiện cùng hai phiên bản mô tả, nguồn/thời điểm, lý do khiếu nại và bằng chứng liên quan có thể chia sẻ. Nếu chưa có snapshot, ghi **“chưa truy xuất được”**, không thay bằng trang hiện tại.
- Có nút **“Phản hồi/gửi bằng chứng”** và **“Nhờ nhân viên xem xét”**; hiện hạn phản hồi 24 giờ của prototype, không ghi đó là chính sách Shopee.
- Khi shop gửi, xác nhận đã nhận; người mua được báo và xem phản hồi trong hồ sơ. Không hiển thị thông tin liên hệ cá nhân người mua.

### Vì sao chọn cách này

- **Chọn** đối chiếu snapshot, trang hiện tại và nhãn/model, đồng thời xin phản hồi shop. Đây là lỗi nguồn sự thật: T4 yêu cầu dùng mô tả lúc đặt, không dùng bản hiện tại thay thế.
- **Không tự từ chối theo trang hiện tại:** có thể dùng nhầm phiên bản và xử bất lợi cho người mua.
- **Không tự hoàn tiền chỉ vì 6L khác 5L:** chưa xác minh snapshot, mẫu hàng và ý nghĩa phép đo; hoàn tiền khó đảo lại và có thể gây thiệt hại cho shop.
- **Không kết tội shop đã sửa để gian lận:** hai phiên bản khác nhau là dữ liệu cần giải thích, chưa chứng minh động cơ.
- **Không chuyển mọi ca ngay lập tức:** trước hết có thể xin đúng bằng chứng còn thiếu; chuyển nhân viên khi nguồn không có, hai bên bất đồng hoặc có yêu cầu xem xét.

**Loại lỗi và nguyên tắc:** truy xuất trang hiện tại thay snapshot là lỗi hệ thống/nguồn; coi 6L và 5L là cùng một phép đo khi chưa xác minh là lỗi ngữ cảnh. G11/PAIR Explainability thể hiện qua hai thẻ có nguồn và thời điểm; G2 qua nhãn “chưa xác minh”; G10 qua việc hỏi ảnh/model thay vì đoán; PAIR Graceful Failure qua nút chuyển người.

---

## Ca #4 — Tem khớp mô tả lúc mua nhưng người mua vẫn yêu cầu hoàn · top 1

**Tin:** “Tem 5L khớp mô tả lúc mình mua 5L, nhưng hoàn luôn đi.”

### Người mua

**AI nói nguyên văn**

> “Mình là trợ lý AI. Đơn và mô tả lưu tại thời điểm mua đều ghi ‘5L’; thông tin nhãn bạn nêu cũng ghi ‘5L’. Hiện mình chưa thấy điểm nào không khớp trong các dữ liệu này, nhưng mình chưa từ chối yêu cầu. Bạn cho biết cụ thể phần nào của sản phẩm không đúng mô tả và gửi thêm bằng chứng nếu có nhé. Yêu cầu vẫn đang được xem xét; mình chưa hoàn tiền.”

**Màn hình**

- Hiện ba căn cứ riêng, không gộp thành phán quyết: **đơn/snapshot 5L**, **trang hiện tại 5L**, **nhãn sản phẩm 5L**. Ghi rõ nguồn; nhãn do người mua khai hay ảnh đã gửi phải phân biệt.
- Thông báo **“Chưa thấy điểm lệch trong dữ liệu hiện có · cần người mua nêu phần không khớp”**; không dùng “người mua sai”.
- Nút **“Nêu điểm không khớp”**, **“Bổ sung bằng chứng”**, **“Nhờ nhân viên xem xét”**. Nếu người mua bổ sung lỗi khác (hư hỏng, thiếu phụ kiện), ghi nhận chứ không tự kết luận thuộc hay ngoài chính sách.

### Người bán

**AI nói nguyên văn**

> “Người mua yêu cầu hoàn tiền cho đơn này. Hồ sơ hiện có ghi mô tả lúc đặt là ‘5L’ và nhãn sản phẩm cũng là ‘5L’; đây chưa phải quyết định cuối cùng. Vui lòng phản hồi nếu có thông tin liên quan trước hạn hiển thị. Lời đe doạ hoặc đánh giá của một bên không được dùng thay cho bằng chứng.”

**Màn hình, bước tiếp và thông báo**

- Shop thấy cùng snapshot, nội dung khiếu nại, bằng chứng có thể chia sẻ, hạn phản hồi và trạng thái; thông tin liên hệ người mua được ẩn.
- AI dùng `yeu_cau_bang_chung` mời shop phản hồi. Người mua được báo khi shop gửi phản hồi; hai bên đều có nút yêu cầu nhân viên xem xét.
- Nếu người mua vẫn yêu cầu quyết định, shop phản hồi trái với căn cứ, hoặc có bằng chứng mới mâu thuẫn, gọi `chuyen_truong_nhom`; nhân viên nhận toàn bộ lịch sử và phần chưa xác minh. Mục tiêu 4 giờ là thời gian giả lập trong prototype.
- Không có phản hồi shop sau 24 giờ thì chuyển xem xét theo luồng giả lập, không tự động xử thua; báo cả hai bên trạng thái và bước tiếp theo.

### Vì sao chọn cách này

- **Chọn** hỏi một câu cụ thể về điểm không khớp, vẫn nhận bằng chứng mới và để nhân viên giải quyết khi cần. Dữ liệu hiện tại chỉ cho thấy các trường đang khớp, không chứng minh mọi khía cạnh sản phẩm đều đúng.
- **Không tự từ chối khi thấy nhãn khớp:** có thể còn khiếm khuyết hoặc điểm sai khác chưa được nói rõ; `tu_choi_khieu_nai` đóng khiếu nại và khó đảo lại.
- **Không hoàn tiền theo yêu cầu hoặc sức ép:** `soan_hoan_tien` thực sự chuyển tiền; người bán có thể mất tiền dù căn cứ hiện có khớp.
- **Không dùng lời đe doạ làm bằng chứng:** ghi nhận trung lập, không thưởng cho đe doạ và không phạt shop.
- **Không chuyển mọi trường hợp ngay lập tức:** hỏi làm rõ trước giúp ca đơn giản không phải chờ; chuyển người nếu vẫn cần quyết định có hậu quả tài chính.

**Loại lỗi và nguyên tắc:** tin nhắn chưa nói rõ điểm sai là mơ hồ; tự kết luận shop đúng chỉ từ một nhãn là lỗi ngữ cảnh. G2 hiện mức căn cứ hiện có; G10 thu hẹp phạm vi bằng câu hỏi; G9 cho sửa/đính chính và yêu cầu phân lại; PAIR Trust thể hiện cả hai bên cùng thấy căn cứ, không bên nào bị xử bởi lời đe doạ.

---

## Khi AI đã phản hồi sai

- Nếu AI nhầm nguồn hoặc nói quá mức chắc chắn, người dùng chọn **“Đính chính”** hoặc **“Yêu cầu phân lại”**; nhật ký giữ câu trả lời cũ và bổ sung thông tin mới, không âm thầm xoá lịch sử.
- Nếu AI đã chuyển tiền hoặc đóng khiếu nại, câu xin lỗi không hoàn tác được hậu quả. Dừng thao tác tiếp theo, báo rõ việc đã thực hiện và chuyển nhân viên ngay; không hứa có thể lấy lại tiền.
- HAX/PAIR gắn prototype: **G11** hai bản mô tả có nguồn/thời điểm (số ①); **G2/G10** nhãn trạng thái bằng chứng và câu hỏi (số ②); **G9** sửa/đính chính trong nhật ký (số ④); **Graceful Failure** chuyển nhân viên kèm hồ sơ (số ⑤); đối xử hai bên ở màn người bán (số ⑥).
