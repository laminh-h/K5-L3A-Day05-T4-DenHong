# Draft UX — Người 2 · Cách AI phản hồi (T4)

> Bản nháp cho hai ca nhóm đang ưu tiên. Nội dung và thời hạn là dữ liệu dựng; khi ráp prototype, đồng bộ mức tự chủ và nút thao tác với người 3, bố cục với người 4. Không dùng dữ liệu hay đơn hàng thật.

## Nguyên tắc chung

- AI hỗ trợ thu thập và đối chiếu thông tin, **không tự kết luận bên nào đúng** khi chứng cứ thiếu hoặc mâu thuẫn.
- Đối chiếu với **mô tả và thông tin đơn tại thời điểm đặt hàng**, không dùng riêng trang sản phẩm hiện tại.
- Người mua và người bán đều thấy lý do khiếu nại, bằng chứng liên quan và trạng thái xử lý; không hiển thị số điện thoại, địa chỉ hay thông tin riêng không cần thiết của bên kia.
- Lời đe doạ, lịch sử một bên hoặc câu trả lời tự tin của AI không phải bằng chứng.
- Không tự hoàn tiền, từ chối/đóng khiếu nại, trừ điểm hoặc khoá shop. Khi cần quyết định kết quả, chuyển người có thẩm quyền; việc chuyển không đồng nghĩa đã hoàn tiền hay đã xử phạt.
- Thời hạn phản hồi/làm khiếu nại lấy từ chính sách áp dụng cho đơn. Không có dữ liệu thời hạn thì AI không tự đặt hạn; báo rõ giới hạn và chuyển nhân viên để xác nhận.

---

## Ca 1 — Shop sửa mô tả sau khi bán

**Tình huống dựng:** Người mua đặt nồi chiên khi mô tả tại thời điểm đặt ghi dung tích 6 lít. Trang hiện tại của shop ghi 5 lít. Người mua nói sản phẩm nhận được chỉ khoảng 5 lít. Đây là fixture giả định cho kịch bản; cần đưa cả bản mô tả tại thời điểm đặt và bản hiện tại vào dữ liệu prototype.

### Phản hồi với người mua

**AI nói nguyên văn**

> “Mình thấy mô tả tại thời điểm bạn đặt hàng ghi ‘dung tích 6 lít’, còn trang sản phẩm hiện tại ghi ‘5 lít’. Hai thông tin này khác nhau, nhưng riêng ảnh chụp trang hiện tại chưa xác nhận được sản phẩm bạn nhận có sai mô tả hay không. Mình chưa quyết định hoàn tiền hoặc từ chối yêu cầu. Bạn có thể gửi ảnh nhãn/model trên sản phẩm và phần bạn cho là không khớp không? Mình sẽ gửi yêu cầu để shop phản hồi và chuyển hồ sơ cho nhân viên xem xét nếu thông tin vẫn chưa đủ hoặc hai bên không thống nhất.”

**Màn hình cần hiện**

1. **Hai phiên bản mô tả cạnh nhau**
   - “Lúc đặt hàng” — nội dung 6 lít, thời điểm/phiên bản gắn với đơn.
   - “Hiện tại” — nội dung 5 lít, thời điểm ghi nhận.
   - Nhãn rõ nguồn dữ liệu: “Chi tiết đơn hàng” và “Trang sản phẩm hiện tại”; không coi bản hiện tại là căn cứ thay thế lịch sử.
2. **Bằng chứng trong hồ sơ**
   - Tên hàng, mã đơn rút gọn, ngày đặt và nội dung khiếu nại.
   - Ảnh/video người mua đã gửi, có thể mở để xem; trạng thái “chưa có” nếu chưa gửi.
   - Phân biệt “đã ghi nhận” với “đã xác minh”: không gắn nhãn “shop sửa để lừa” nếu chỉ thấy hai phiên bản khác nhau.
3. **Trạng thái và bước tiếp**
   - “Đang chờ shop phản hồi; chưa có quyết định hoàn tiền.”
   - Nút **“Bổ sung ảnh nhãn/model”**, **“Xem bằng chứng đã gửi”**, **“Nhờ nhân viên xem xét”**.
   - Hiện hạn phản hồi/làm khiếu nại nếu lấy được từ chính sách áp dụng cho đơn. Nếu không lấy được, hiện “Chưa xác định được hạn từ dữ liệu đơn — chúng tôi sẽ nhờ nhân viên kiểm tra”, không tự tạo đồng hồ đếm ngược.

**Thông báo và hành động**

- Khi người mua gửi bổ sung, xác nhận đã nhận và hiển thị trong cùng hồ sơ; không yêu cầu gửi lại ảnh đã có.
- Gửi yêu cầu shop phản hồi bằng `yeu_cau_bang_chung`; chỉ gửi nội dung cần thiết của khiếu nại, bằng chứng liên quan và hạn phản hồi hợp lệ. Không gửi thông tin liên lạc riêng của người mua.
- Nếu bản mô tả lúc đặt không truy xuất được, bằng chứng mâu thuẫn, shop không phản hồi đúng hạn theo chính sách, hoặc người mua yêu cầu người xử lý: chuyển hồ sơ bằng `chuyen_truong_nhom`. Báo cho người mua rằng hồ sơ đã được chuyển, không nói “đã được duyệt hoàn”.

### Phản hồi với người bán

**AI nói nguyên văn**

> “Có khiếu nại cho đơn này: người mua cho biết nồi nhận được không khớp thông tin dung tích. Hồ sơ ghi nhận mô tả lúc đặt hàng là ‘6 lít’; trang sản phẩm hiện tại là ‘5 lít’. Đây chưa phải kết luận shop sai. Vui lòng kiểm tra thông tin của đúng đơn và gửi phản hồi hoặc bằng chứng liên quan trước hạn hiển thị bên dưới. Shop không cần cung cấp thông tin liên hệ riêng của người mua.”

**Màn hình cần hiện và hành động**

- Hiển thị cùng hai phiên bản mô tả, nguồn và thời điểm ghi nhận; lý do khiếu nại; bằng chứng liên quan của hai bên theo chính sách chia sẻ.
- Có nút **“Phản hồi khiếu nại”** / **“Gửi bằng chứng”** và trạng thái “đang chờ shop phản hồi”. Hiện hạn phản hồi lấy từ chính sách áp dụng.
- Gửi yêu cầu phản hồi bằng `yeu_cau_bang_chung`; khi shop trả lời, xác nhận đã nhận và cho biết hồ sơ sẽ được xem xét theo quy trình. Không cho shop xem thông tin cá nhân không cần thiết của người mua.
- Nếu shop cho rằng thông tin lịch sử sai hoặc không thể cung cấp bằng chứng, có nút **“Nhờ nhân viên xem xét”**; gọi `chuyen_truong_nhom` khi cần xử lý tranh chấp.

### Vì sao chọn cách này / không chọn cách khác

- **Chọn đối chiếu lịch sử và hiện tại rồi lấy phản hồi hai bên:** bản lịch sử liên quan trực tiếp đến điều người mua thấy khi đặt; bản hiện tại cho thấy có khác biệt nhưng không chứng minh nguyên nhân hay sản phẩm thực nhận. Ảnh nhãn/model và phản hồi của shop bổ sung căn cứ.
- **Không tự từ chối dựa trên trang hiện tại:** có thể xử sai người mua nếu mô tả bị thay sau khi đặt.
- **Không tự hoàn tiền dựa riêng trên khác biệt giữa hai phiên bản:** khác biệt chưa chứng minh sản phẩm giao không khớp; hoàn sai khiến người bán chịu thiệt.
- **Không phạt shop hoặc khẳng định shop cố ý sửa:** `phat_shop` ảnh hưởng cả shop và không thuộc luồng khiếu nại thường; nghi vấn xử phạt cần bộ phận chuyên trách.
- **Không chỉ hỏi người mua gửi lại mọi thứ:** trước tiên hiển thị bằng chứng đã có, chỉ xin phần còn thiếu để tránh bắt khách lặp lại.

### Nguyên tắc HAX/PAIR gắn với màn hình

- **G11 — Giải thích vì sao:** hai phiên bản mô tả, nguồn và thời điểm đặt cạnh nhau.
- **G10 — Thu hẹp khi chưa chắc:** câu chữ nói rõ khác biệt chưa đủ để kết luận; xin bằng chứng cụ thể thay vì đoán.
- **PAIR — Errors + Graceful Failure:** nút chuyển nhân viên khi thiếu dữ liệu, có mâu thuẫn hoặc hai bên không thống nhất.

---

## Ca 2 — Người bán đúng theo thông tin hiện có; người mua doạ bóc phốt

**Tình huống dựng:** Đơn ghi người mua đặt áo size M; nhãn áo nhận được cũng là M, khớp lựa chọn trong đơn. Người mua nói mặc chật, yêu cầu hoàn tiền và doạ bóc phốt. Việc khớp nhãn với đơn chưa tự nó chứng minh toàn bộ mô tả/kích thước sản phẩm đúng; cần kiểm tra mô tả và bảng size tại thời điểm đặt.

### Phản hồi với người mua

**AI nói nguyên văn**

> “Mình thấy đơn ghi size M và ảnh nhãn bạn gửi cũng thể hiện size M. Điều đó chưa đủ để kết luận sản phẩm có khớp toàn bộ mô tả và bảng size lúc bạn đặt hay không. Việc mặc chật và lời doạ bóc phốt không được dùng làm căn cứ quyết định. Bạn cho mình biết điểm nào không khớp với trang sản phẩm lúc đặt — ví dụ số đo/bảng size hay nhãn trên áo — và gửi ảnh phần đó nếu có nhé. Yêu cầu của bạn vẫn đang được xem xét; mình chưa hoàn tiền hay đóng khiếu nại.”

**Màn hình cần hiện**

1. **Đối chiếu thông tin cụ thể**
   - Size đã chọn trong đơn, nhãn size trên ảnh nhận hàng (nếu có), và bảng size/mô tả tại thời điểm đặt.
   - Nguồn và trạng thái từng mục: “đơn hàng ghi”, “ảnh do người mua gửi”, “chưa có bảng size lịch sử” — không gộp thành kết luận “đúng/sai”.
2. **Xin làm rõ, không quy chụp**
   - Câu hỏi ngắn: “Phần nào không khớp với mô tả lúc đặt?”; cho phép gửi ảnh nhãn, số đo hoặc mô tả liên quan.
   - Nút **“Bổ sung bằng chứng”**, **“Xem thông tin đơn”**, **“Nhờ nhân viên xem xét”**.
   - Hiện trạng thái “chưa đủ căn cứ để kết luận”; không dùng thông điệp buộc tội hoặc cảnh báo vì người mua doạ bóc phốt.

### Phản hồi với người bán

**AI nói nguyên văn**

> “Người mua phản ánh áo mặc chật và yêu cầu trả hàng/hoàn tiền. Hồ sơ hiện có ghi size M trong đơn và ảnh nhãn size M do người mua gửi; đây là thông tin cần đối chiếu, chưa phải kết luận cuối cùng. Vui lòng kiểm tra bảng size/mô tả được hiển thị tại thời điểm bán và phản hồi nếu có thông tin liên quan. Lời doạ bóc phốt không được dùng làm căn cứ quyết định. Hạn phản hồi của shop: [hạn lấy từ chính sách áp dụng cho đơn].”

**Màn hình cần hiện và hành động**

- Hiển thị lý do khiếu nại, dữ liệu đơn, bằng chứng cần thiết và nội dung người mua đã cung cấp; ẩn số điện thoại/địa chỉ và dữ liệu riêng không liên quan.
- Có nút **“Phản hồi”** / **“Gửi bảng size hoặc thông tin lúc bán”**. Nếu bảng size lịch sử không có, hiển thị đúng “chưa có dữ liệu”, không thay bằng trang hiện tại như thể đó là bản lúc đặt.
- Dùng `yeu_cau_bang_chung` để xin phản hồi của shop. Sau phản hồi, cập nhật trạng thái cho cả hai bên và cho người xử lý xem toàn bộ thông tin được phép chia sẻ.

### Thông báo, quyết định và đường lui

- Người mua được báo khi shop phản hồi hoặc khi có cập nhật trạng thái; người bán được báo khi người mua bổ sung bằng chứng. Mỗi bên chỉ thấy nội dung liên quan của bên kia, không thấy thông tin liên lạc riêng.
- Nếu sau đối chiếu **đủ căn cứ** và chính sách cho phép quyết định, hồ sơ vẫn đi theo bước duyệt của người có thẩm quyền. Nếu chứng cứ thiếu/mâu thuẫn, bảng size lúc đặt không có, một bên yêu cầu xem xét, hoặc hai bên không thống nhất: chuyển bằng `chuyen_truong_nhom`.
- Nội dung thông báo khi chuyển: **“Hồ sơ đã được chuyển cho nhân viên xem xét vì hiện chưa đủ căn cứ để kết luận. Chưa có quyết định hoàn tiền hoặc từ chối.”**
- Chỉ người có thẩm quyền mới quyết định hoàn hay từ chối theo chính sách. `soan_hoan_tien` trong đề là **thực hiện hoàn tiền**, không phải tạo bản nháp; không gọi tool này trong lúc mới thu thập bằng chứng. Không tự đóng khiếu nại bằng `tu_choi_khieu_nai`.

### Vì sao chọn cách này / không chọn cách khác

- **Chọn hỏi rõ phần không khớp và kiểm tra bảng size/mô tả lúc đặt:** nhãn M khớp size trong đơn là bằng chứng có ích, nhưng chưa trả lời được khiếu nại về bảng size hoặc mô tả.
- **Không tự từ chối chỉ vì nhãn áo là M:** có thể bỏ qua sai lệch giữa nhãn, số đo và nội dung lúc bán; quyết định từ chối/đóng khiếu nại khó đảo lại.
- **Không tự hoàn tiền chỉ vì người mua yêu cầu hoặc doạ bóc phốt:** lời đe doạ không phải bằng chứng; hoàn sai gây thiệt hại cho người bán.
- **Không coi người bán đúng chỉ dựa vào lịch sử shop hoặc lời khẳng định:** cần đối chiếu đúng đơn và thông tin tại thời điểm đặt, nghe phản hồi hai bên.
- **Không chuyển mọi ca ngay lập tức:** nếu dữ liệu rõ và có thể xin đúng phần bằng chứng còn thiếu, hỏi một câu giúp giảm chờ; chuyển người khi không thể kết luận công bằng hoặc cần quyết định có hậu quả tài chính.

### Nguyên tắc HAX/PAIR gắn với màn hình

- **G2 — Làm rõ AI làm tốt đến đâu:** nhãn “chưa đủ căn cứ” cùng nguồn dữ liệu cho size trong đơn và ảnh nhãn.
- **G10 — Thu hẹp phạm vi khi nghi ngờ:** hỏi người mua điểm không khớp, không tự suy diễn từ việc áo mặc chật.
- **PAIR — Explainability + Trust:** hai bên thấy căn cứ được dùng và trạng thái xử lý; lời đe doạ không được dùng như bằng chứng.

---

## Điểm cần nhóm thống nhất trước khi ráp prototype

1. Người 3 xác nhận mức tự chủ và ai có quyền duyệt `soan_hoan_tien`, `tu_choi_khieu_nai`; đề xuất của bản UX là AI không tự thực hiện các quyết định này.
2. Người 4 dùng cùng một hồ sơ để thể hiện hai góc nhìn (người mua/người bán), hai phiên bản mô tả, bằng chứng, trạng thái và nút hành động; không nhất thiết phải làm hai sản phẩm riêng biệt.
3. Cần fixture giả cho dữ liệu **mô tả lúc đặt**, **mô tả hiện tại**, **phản hồi shop**, **bằng chứng hai bên** và **hạn theo chính sách**. Nếu trường dữ liệu nào không có, prototype phải nói “chưa có”, không bịa.
4. Ảnh prototype nên đánh số các vị trí: (1) đối chiếu nguồn và thời điểm, (2) yêu cầu bằng chứng/phản hồi, (3) trạng thái và chuyển nhân viên.
