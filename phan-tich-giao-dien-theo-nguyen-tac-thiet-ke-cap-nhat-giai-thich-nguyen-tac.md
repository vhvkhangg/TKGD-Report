# Phân tích giao diện theo nguyên tắc thiết kế

## Cơ sở lý thuyết sử dụng

File phân tích này dựa trên các nhóm nguyên tắc chính trong tài liệu môn **Thiết kế giao diện - User & Usability**:

- **Cognitive process trong HCI**: Attention, Perception, Memory, Learning.
- **Usability goals**: Effectiveness, Efficiency, Safety, Learnability, Memorability, Satisfaction.
- **Donald A. Norman - 6 Principles of Design**: Visibility, Affordance, Constraint, Mapping, Feedback, Consistency.
- **Shneiderman - 8 Golden Rules**: consistency, shortcuts, informative feedback, closure, error prevention, reversal, locus of control, reduce short-term memory load.
- **Nielsen - 10 Usability Heuristics**: visibility of system status, match with real world, user control, consistency, error prevention, recognition rather than recall, flexibility/efficiency, aesthetic and minimalist design, error recovery, help/documentation.

---

## Đăng nhập bằng mã fail.png

**Nguyên tắc áp dụng:** Feedback, Constraint, Error Prevention, Help users recognize/diagnose/recover from errors, Visibility of system status.

**Phân tích:** Giao diện dùng 6 ô nhập mã để giới hạn rõ định dạng OTP/mã xác thực. Khi nhập sai hoặc chưa đủ điều kiện, hệ thống hiển thị thông báo lỗi màu đỏ ngay dưới ô nhập. Đây là feedback trực tiếp, giúp người dùng biết lỗi nằm ở đâu thay vì phải tự suy đoán. Nút **Gửi** vẫn được đặt rõ ở trung tâm, nhưng trạng thái lỗi làm người dùng hiểu rằng cần sửa mã trước khi tiếp tục.

**Nguyên tắc được áp dụng ở đâu và như thế nào:**

- **Feedback:** Áp dụng tại dòng thông báo lỗi màu đỏ bên dưới cụm 6 ô nhập mã; giao diện phản hồi ngay rằng mã không hợp lệ hoặc thao tác chưa thể tiếp tục.
- **Constraint:** Áp dụng tại 6 ô nhập tách rời; mỗi ô chỉ đại diện cho một ký tự nên người dùng hiểu đúng độ dài mã cần nhập.
- **Error Prevention:** Áp dụng ở việc giới hạn cấu trúc nhập OTP; người dùng ít có khả năng nhập sai định dạng như nhập quá dài hoặc nhập lẫn nội dung không liên quan.
- **Help users recognize/diagnose/recover from errors:** Áp dụng ở vị trí lỗi sát vùng nhập; người dùng nhìn thấy nguyên nhân lỗi và biết cần sửa lại mã.
- **Visibility of system status:** Áp dụng ở trạng thái lỗi hiển thị trực tiếp trên màn hình; người dùng biết hệ thống đã xử lý yêu cầu gửi nhưng chưa chấp nhận mã.

**Vì sao phải thiết kế như thế:** Đăng nhập là thao tác nhạy cảm. Nếu không có feedback rõ, người dùng dễ nghĩ hệ thống bị lỗi. Thông báo lỗi gần vùng nhập giúp giảm tải trí nhớ ngắn hạn và hỗ trợ sửa lỗi nhanh.

---

## Đăng nhập bằng mã.png

**Nguyên tắc áp dụng:** Constraint, Recognition rather than recall, Aesthetic and minimalist design, Consistency.

**Phân tích:** Giao diện chỉ tập trung vào một nhiệm vụ chính: nhập mã xác thực. Sáu ô nhập mã được chia tách thành từng ký tự, giúp người dùng nhận biết ngay số lượng ký tự cần nhập. Logo, email nhận mã và nút **Gửi** được sắp xếp theo trật tự từ trên xuống dưới, tạo luồng thao tác tự nhiên.

**Nguyên tắc được áp dụng ở đâu và như thế nào:**

- **Constraint:** Áp dụng tại cụm 6 ô mã xác thực; giao diện quy định rõ số lượng ký tự cần nhập.
- **Recognition rather than recall:** Áp dụng ở việc hiển thị email nhận mã và ô nhập theo từng ký tự; người dùng không phải nhớ định dạng mã, chỉ cần nhìn cấu trúc để nhập theo.
- **Aesthetic and minimalist design:** Áp dụng ở phần nội dung trung tâm chỉ gồm logo, hướng dẫn, ô nhập và nút gửi; giao diện loại bỏ thành phần phụ gây nhiễu.
- **Consistency:** Áp dụng qua màu sắc, kiểu nút và bố cục giống màn hình đăng nhập email; người dùng nhận ra đây vẫn là một bước trong cùng luồng xác thực.

**Vì sao phải thiết kế như thế:** Với màn hình xác thực, càng ít yếu tố phụ thì người dùng càng ít bị phân tâm. Thiết kế tối giản giúp tăng hiệu quả, giảm thao tác sai và giúp người dùng hoàn tất đăng nhập nhanh.

---

## Đặt hàng Mobile.png

**Nguyên tắc áp dụng:** Feedback, Design dialogs to yield closure, Visibility of system status, Mapping, User satisfaction.

**Phân tích:** Màn hình hiển thị biểu tượng dấu tick và tiêu đề **Đặt hàng thành công**, cho người dùng biết đơn hàng đã được ghi nhận. Phần tiến trình đơn hàng dùng các bước theo chiều ngang, thể hiện trạng thái hiện tại và các trạng thái tiếp theo. Thông tin đơn hàng, vận chuyển, thanh toán và danh sách sản phẩm được gom thành từng khối rõ ràng.

**Nguyên tắc được áp dụng ở đâu và như thế nào:**

- **Feedback:** Áp dụng tại biểu tượng dấu tick và dòng **Đặt hàng thành công**; giao diện xác nhận ngay kết quả của thao tác đặt hàng.
- **Design dialogs to yield closure:** Áp dụng ở phần mã đơn, thời gian đặt hàng và trạng thái đơn; người dùng biết quy trình đã kết thúc thành công.
- **Visibility of system status:** Áp dụng tại thanh tiến trình đơn hàng; trạng thái hiện tại và các bước tiếp theo được thể hiện trực quan.
- **Mapping:** Áp dụng ở thứ tự các khối thông tin: trạng thái đơn hàng → thông tin giao hàng → thanh toán → sản phẩm; thứ tự này tương ứng với cách người dùng kiểm tra lại đơn.
- **User satisfaction:** Áp dụng ở thông điệp thành công và bố cục gọn trên mobile; người dùng có cảm giác yên tâm sau khi hoàn tất giao dịch.

**Vì sao phải thiết kế như thế:** Sau khi thanh toán/đặt hàng, người dùng cần cảm giác chắc chắn rằng thao tác đã hoàn tất. Trạng thái đơn hàng và mã đơn giúp tăng độ tin cậy, đồng thời giảm nhu cầu hỏi lại hoặc thao tác lại.

---

## đánh giá.png

**Nguyên tắc áp dụng:** Perception, Recognition rather than recall, Visibility, User satisfaction, Aesthetic and minimalist design.

**Phân tích:** Giao diện đánh giá sử dụng sao, thanh tỷ lệ và danh sách bình luận. Người dùng có thể nhanh chóng nhận biết chất lượng sản phẩm thông qua biểu tượng sao thay vì phải đọc toàn bộ nội dung. Bộ lọc như **Gần đây nhất** hỗ trợ người dùng kiểm soát cách xem đánh giá.

**Nguyên tắc được áp dụng ở đâu và như thế nào:**

- **Perception:** Áp dụng ở sao đánh giá, thanh tỷ lệ và điểm trung bình; người dùng nhận biết chất lượng sản phẩm bằng tín hiệu thị giác trước khi đọc bình luận.
- **Recognition rather than recall:** Áp dụng ở biểu tượng sao và bộ lọc quen thuộc như **Gần đây nhất**; người dùng nhận diện ý nghĩa mà không cần học lại.
- **Visibility:** Áp dụng ở việc đặt tổng quan đánh giá phía trên danh sách bình luận; thông tin quan trọng nhất xuất hiện trước.
- **User satisfaction:** Áp dụng ở việc cho phép xem nhiều ý kiến người mua; giao diện hỗ trợ cảm giác tin cậy khi ra quyết định.
- **Aesthetic and minimalist design:** Áp dụng ở cách chia khu vực đánh giá tổng quan và bình luận; thông tin nhiều nhưng vẫn được gom nhóm để dễ đọc.

**Vì sao phải thiết kế như thế:** Đánh giá là yếu tố hỗ trợ quyết định mua hàng. Trực quan hóa bằng sao và thanh tỷ lệ giúp người dùng xử lý thông tin nhanh hơn, giảm tải đọc và tăng niềm tin trước khi mua.

---

## đặt hàng thành công.png

**Nguyên tắc áp dụng:** Feedback, Closure, Visibility of system status, Mapping, Error Prevention.

**Phân tích:** Màn hình desktop hiển thị rõ trạng thái **Đặt hàng thành công**, mã đơn hàng, thời gian đặt hàng, phương thức thanh toán, tiến trình xử lý và bảng sản phẩm. Các nút như **Xem chi tiết đơn hàng** và **Tiếp tục mua sắm** cung cấp lối đi tiếp theo sau khi hoàn tất tác vụ.

**Nguyên tắc được áp dụng ở đâu và như thế nào:**

- **Feedback:** Áp dụng tại tiêu đề **Đặt hàng thành công** và biểu tượng xác nhận; hệ thống phản hồi rõ thao tác đã được ghi nhận.
- **Closure:** Áp dụng ở phần mã đơn, thời gian, phương thức thanh toán và bảng sản phẩm; người dùng có đủ thông tin để kết thúc phiên mua hàng.
- **Visibility of system status:** Áp dụng ở thanh trạng thái xử lý đơn; người dùng biết đơn đang ở bước nào trong quy trình.
- **Mapping:** Áp dụng ở bố cục từ thông tin đơn đến danh sách sản phẩm và hành động tiếp theo; cách sắp xếp khớp với luồng kiểm tra sau đặt hàng.
- **Error Prevention:** Áp dụng ở nút **Xem chi tiết đơn hàng** và thông tin xác nhận; người dùng có thể kiểm tra lại thay vì đặt lại đơn vì không chắc chắn.

**Vì sao phải thiết kế như thế:** Khi người dùng vừa tạo đơn hàng, hệ thống cần xác nhận kết quả và cho biết bước tiếp theo. Thiết kế này giúp người dùng không bị lửng trạng thái, đồng thời giảm rủi ro đặt trùng đơn.

---

## địa chỉ của tôi-1.png

**Nguyên tắc áp dụng:** Visibility, Consistency, Minimalist design, Recognition rather than recall.

**Phân tích:** Đây là trạng thái rỗng của trang **Địa chỉ của tôi**. Sidebar tài khoản vẫn giữ cấu trúc giống các trang quản lý cá nhân khác, giúp người dùng nhận biết mình đang ở khu vực tài khoản. Nội dung chính thông báo chưa có địa chỉ và có nút **Thêm địa chỉ mới** ở vị trí dễ thấy.

**Nguyên tắc được áp dụng ở đâu và như thế nào:**

- **Visibility:** Áp dụng ở thông báo trạng thái rỗng trong vùng nội dung chính; người dùng thấy rõ hiện chưa có địa chỉ.
- **Consistency:** Áp dụng ở sidebar tài khoản, header và bố cục chung giống các trang cá nhân khác; người dùng không phải học lại cách điều hướng.
- **Minimalist design:** Áp dụng ở nội dung rỗng chỉ giữ thông báo và nút hành động chính; màn hình không bị lấp bằng thông tin không cần thiết.
- **Recognition rather than recall:** Áp dụng ở nút **Thêm địa chỉ mới**; người dùng nhận ra ngay hành động cần làm tiếp theo thay vì tự nhớ nơi thêm địa chỉ.

**Vì sao phải thiết kế như thế:** Trạng thái rỗng cần giải thích rõ “chưa có dữ liệu” và hướng dẫn hành động tiếp theo. Nếu chỉ để trống, người dùng dễ hiểu nhầm là lỗi tải dữ liệu.

---

## địa chỉ của tôi.png

**Nguyên tắc áp dụng:** User control and freedom, Visibility of system status, Consistency, Error Prevention, Recognition.

**Phân tích:** Danh sách địa chỉ được trình bày theo từng thẻ, mỗi thẻ có thông tin người nhận, số điện thoại, địa chỉ, nhãn trạng thái như **Cập nhật**, **Xóa**, **Đặt làm mặc định**. Địa chỉ mặc định được phân biệt rõ để người dùng biết địa chỉ nào sẽ dùng khi đặt hàng.

**Nguyên tắc được áp dụng ở đâu và như thế nào:**

- **User control and freedom:** Áp dụng tại các thao tác **Cập nhật**, **Xóa**, **Đặt làm mặc định** trên từng thẻ địa chỉ; người dùng kiểm soát trực tiếp dữ liệu giao hàng.
- **Visibility of system status:** Áp dụng ở nhãn địa chỉ mặc định; người dùng biết địa chỉ nào đang được hệ thống ưu tiên dùng khi đặt hàng.
- **Consistency:** Áp dụng ở dạng thẻ lặp lại cho từng địa chỉ; thông tin người nhận, số điện thoại và địa chỉ luôn nằm theo cùng cấu trúc.
- **Error Prevention:** Áp dụng ở việc hiển thị đầy đủ địa chỉ trước khi cho đặt mặc định/xóa; người dùng có cơ sở kiểm tra để tránh thao tác nhầm.
- **Recognition:** Áp dụng ở các nhãn hành động quen thuộc; người dùng nhận diện nhanh chức năng của từng nút.

**Vì sao phải thiết kế như thế:** Địa chỉ giao hàng ảnh hưởng trực tiếp đến đơn hàng. Hiển thị trạng thái và hành động rõ ràng giúp người dùng kiểm soát dữ liệu cá nhân và tránh giao nhầm địa chỉ.

---

## điền thông tin thanh toán.png

**Nguyên tắc áp dụng:** Constraint, Mapping, Error Prevention, Efficiency, Visibility.

**Phân tích:** Giao diện checkout chia thành hai khu vực: bên trái là thông tin nhận hàng, phương thức vận chuyển và thanh toán; bên phải là tóm tắt đơn hàng, voucher và tổng tiền. Cách chia này tạo mapping hợp lý giữa thông tin cần nhập và kết quả thanh toán cuối cùng.

**Nguyên tắc được áp dụng ở đâu và như thế nào:**

- **Constraint:** Áp dụng ở các trường thông tin nhận hàng, lựa chọn vận chuyển và phương thức thanh toán; giao diện buộc người dùng điền/chọn các dữ liệu cần thiết trước khi đặt hàng.
- **Mapping:** Áp dụng ở bố cục hai cột: bên trái là dữ liệu người dùng nhập, bên phải là kết quả đơn hàng và tổng tiền; người dùng thấy quan hệ giữa lựa chọn và chi phí.
- **Error Prevention:** Áp dụng ở phần tóm tắt đơn hàng, voucher, phí vận chuyển và tổng thanh toán; người dùng có thể rà soát trước khi bấm **Đặt hàng**.
- **Efficiency:** Áp dụng ở việc gom tất cả bước checkout trên cùng một màn hình; người dùng không cần chuyển qua nhiều trang nhỏ.
- **Visibility:** Áp dụng ở nút đặt hàng và tổng tiền nổi bật; hành động chính và số tiền cần trả dễ nhận ra.

**Vì sao phải thiết kế như thế:** Checkout là quy trình dễ phát sinh lỗi. Việc gom các trường nhập, lựa chọn và tổng tiền vào các khối riêng giúp người dùng kiểm tra lại trước khi bấm **Đặt hàng**, từ đó tăng tính an toàn và giảm sai sót.

---

## Blog.png

**Nguyên tắc áp dụng:** Visual hierarchy, Perception, Minimalist design, Consistency, Recognition.

**Phân tích:** Trang Blog dùng tiêu đề lớn **Đánh giá & Hướng dẫn Gear**, thanh điều hướng danh mục và các thẻ bài viết. Bài viết nổi bật được đặt lớn hơn các bài phụ, tạo thứ bậc thị giác rõ. Header và footer giữ cùng phong cách với các trang thương mại điện tử khác.

**Nguyên tắc được áp dụng ở đâu và như thế nào:**

- **Visual hierarchy:** Áp dụng ở tiêu đề lớn, bài viết nổi bật và các card bài viết nhỏ hơn; người dùng biết nội dung nào cần chú ý trước.
- **Perception:** Áp dụng ở ảnh minh họa, thẻ danh mục và tiêu đề bài viết; người dùng quét nhanh để nhận diện chủ đề.
- **Minimalist design:** Áp dụng ở card bài viết chỉ giữ ảnh, tiêu đề và thông tin tóm tắt; tránh làm trang blog quá nặng chữ.
- **Consistency:** Áp dụng ở header, footer và cách trình bày card đồng nhất với hệ thống website; trải nghiệm không bị rời rạc.
- **Recognition:** Áp dụng ở thanh danh mục blog; người dùng chọn chủ đề bằng cách nhận diện tên danh mục thay vì nhớ đường dẫn.

**Vì sao phải thiết kế như thế:** Blog có nhiều nội dung, nên cần phân cấp để người dùng biết đâu là nội dung chính, đâu là nội dung phụ. Cách này giúp tăng khả năng đọc lướt và khám phá nội dung.

---

## Chi tiết Blog.png

**Nguyên tắc áp dụng:** Perception, Readability, Recognition rather than recall, User control, Consistency.

**Phân tích:** Bài viết chi tiết đặt tiêu đề lớn ở đầu, sau đó là thông tin ngày đăng/tác giả, ảnh minh họa, nội dung, biểu tượng tương tác, khung bình luận và bài viết liên quan. Các thành phần được sắp xếp theo đúng mô hình đọc nội dung: nhận diện chủ đề, đọc bài, phản hồi, tiếp tục khám phá.

**Nguyên tắc được áp dụng ở đâu và như thế nào:**

- **Perception:** Áp dụng ở tiêu đề lớn, ảnh đại diện và khoảng cách đoạn văn; người đọc dễ nhận diện cấu trúc bài viết.
- **Readability:** Áp dụng ở phần nội dung chính được đặt trong vùng đọc riêng, có thứ tự từ tiêu đề đến nội dung; hỗ trợ đọc liên tục.
- **Recognition rather than recall:** Áp dụng ở khu vực bài viết liên quan; người dùng không cần nhớ tên bài khác mà có thể chọn trực tiếp.
- **User control:** Áp dụng ở khu vực bình luận, biểu tượng tương tác và điều hướng; người dùng có thể phản hồi hoặc tiếp tục khám phá sau khi đọc.
- **Consistency:** Áp dụng ở header/footer và phong cách card bài viết liên quan giống trang Blog; giữ tính thống nhất toàn hệ thống.

**Vì sao phải thiết kế như thế:** Người đọc cần hiểu nhanh bài viết nói về gì và có thể tương tác sau khi đọc. Bài viết liên quan giúp tăng khả năng tiếp tục ở lại trang mà không cần nhớ hoặc tự tìm lại danh mục.

---

## ChiTietSanPhamMobile.png

**Nguyên tắc áp dụng:** Responsive design, Visibility, Mapping, Affordance, Efficiency.

**Phân tích:** Màn hình chi tiết sản phẩm trên mobile xếp nội dung theo chiều dọc: ảnh sản phẩm, thương hiệu, tên, giá, thông số, biến thể màu, số lượng, nút mua, chính sách và mô tả. Nút **Mua ngay - Giao nhanh** được đặt nổi bật, phù hợp với hành vi mua nhanh trên điện thoại.

**Nguyên tắc được áp dụng ở đâu và như thế nào:**

- **Responsive design:** Áp dụng ở bố cục một cột theo chiều dọc; giao diện thích nghi với màn hình hẹp của điện thoại.
- **Visibility:** Áp dụng ở tên sản phẩm, giá và nút **Mua ngay - Giao nhanh**; các thông tin ra quyết định được đặt trước.
- **Mapping:** Áp dụng ở thứ tự ảnh → thông tin → biến thể → số lượng → mua hàng → chính sách; thứ tự này khớp với quá trình cân nhắc mua.
- **Affordance:** Áp dụng ở nút mua nổi bật, bộ chọn màu và bộ chỉnh số lượng; người dùng nhận ra phần tử có thể thao tác.
- **Efficiency:** Áp dụng ở CTA đặt ngay sau thông tin chính; người dùng có thể mua nhanh mà không phải cuộn quá sâu.

**Vì sao phải thiết kế như thế:** Trên mobile, không gian hẹp nên cần ưu tiên thông tin ra quyết định: ảnh, tên, giá, biến thể và CTA. Thiết kế theo chiều dọc giúp người dùng cuộn tự nhiên và tránh rối mắt.

---

## Chitietsanpham.png

**Nguyên tắc áp dụng:** Mapping, Affordance, Visibility, Recognition, Aesthetic and minimalist design.

**Phân tích:** Trang chi tiết sản phẩm desktop chia bố cục hai cột: ảnh sản phẩm và thumbnail ở bên trái, thông tin mua hàng ở bên phải. Nút mua màu xanh nổi bật thể hiện affordance rõ rằng đây là hành động chính. Phần thông số, chính sách và mô tả được đặt bên dưới để hỗ trợ người dùng tìm hiểu sâu hơn.

**Nguyên tắc được áp dụng ở đâu và như thế nào:**

- **Mapping:** Áp dụng ở bố cục hai cột: ảnh sản phẩm bên trái, thông tin mua bên phải; người dùng vừa xem hình vừa đối chiếu giá, màu và số lượng.
- **Affordance:** Áp dụng ở nút mua màu nổi bật, thumbnail ảnh và tùy chọn màu; các thành phần tương tác trông giống có thể bấm/chọn.
- **Visibility:** Áp dụng ở giá, tên sản phẩm, trạng thái và CTA chính; các thông tin quan trọng được đặt trong vùng nhìn đầu tiên.
- **Recognition:** Áp dụng ở icon/chính sách như giao hàng, bảo hành, đổi trả; người dùng nhận diện nhanh lợi ích mua hàng.
- **Aesthetic and minimalist design:** Áp dụng ở việc chia thông tin mua hàng và mô tả chi tiết thành các khối; trang nhiều dữ liệu nhưng không bị dồn cục.

**Vì sao phải thiết kế như thế:** Người mua cần xem sản phẩm và thông tin mua hàng cùng lúc. Bố cục hai cột giúp so sánh trực quan giữa hình ảnh, giá, biến thể, số lượng và nút mua, từ đó giảm thời gian ra quyết định.

---

## EXP.png

**Nguyên tắc áp dụng:** Feedback, Visibility of system status, Satisfaction, Recognition, Motivation design.

**Phân tích:** Giao diện hiển thị cấp độ thành viên, thanh tiến trình EXP và các mốc phần thưởng như đồng, bạc, vàng, kim cương. Các mục như hệ số, quà tặng, quà sinh nhật được trình bày thành hàng rõ ràng.

**Nguyên tắc được áp dụng ở đâu và như thế nào:**

- **Feedback:** Áp dụng ở thanh tiến trình EXP; người dùng thấy hệ thống đã ghi nhận điểm và cấp độ hiện tại.
- **Visibility of system status:** Áp dụng ở cấp thành viên, điểm hiện có và các mốc phần thưởng; trạng thái tài khoản được hiển thị rõ.
- **Satisfaction:** Áp dụng ở phần quyền lợi như quà tặng, hệ số, sinh nhật; giao diện tạo cảm giác được thưởng.
- **Recognition:** Áp dụng ở các mốc đồng/bạc/vàng/kim cương; người dùng nhận diện cấp bậc theo mô hình quen thuộc.
- **Motivation design:** Áp dụng ở mốc điểm tiếp theo; người dùng biết cần tích thêm bao nhiêu để đạt quyền lợi cao hơn.

**Vì sao phải thiết kế như thế:** Chương trình tích điểm cần cho người dùng biết họ đang ở đâu và cần bao nhiêu điểm để đạt mốc tiếp theo. Feedback dạng tiến trình giúp tạo động lực mua sắm và tăng sự hài lòng.

---

## Frame 33.png

**Nguyên tắc áp dụng:** Match between system and real world, Visibility, Perception, Consistency, Help and documentation.

**Phân tích:** Đây là trang **Liên hệ**, gồm banner, thông tin shop, danh sách kênh liên hệ, bản đồ và footer. Bản đồ trực quan giúp người dùng nhận biết vị trí thực tế thay vì chỉ đọc địa chỉ bằng chữ. Header/footer nhất quán với các trang khác, giúp duy trì nhận diện thương hiệu.

**Nguyên tắc được áp dụng ở đâu và như thế nào:**

- **Match between system and real world:** Áp dụng ở bản đồ, địa chỉ và thông tin liên hệ thực tế; dữ liệu trên giao diện khớp với cách người dùng tìm một cửa hàng ngoài đời.
- **Visibility:** Áp dụng ở banner liên hệ và các thông tin như số điện thoại, email, địa chỉ; kênh hỗ trợ được đặt dễ thấy.
- **Perception:** Áp dụng ở bản đồ trực quan; người dùng hiểu vị trí nhanh hơn so với chỉ đọc chữ.
- **Consistency:** Áp dụng ở header/footer và phong cách khối nội dung giống các trang khác; duy trì nhận diện thương hiệu.
- **Help and documentation:** Áp dụng ở phần cung cấp kênh liên hệ; người dùng biết nơi cần đến khi cần hỗ trợ.

**Vì sao phải thiết kế như thế:** Trang liên hệ phải tạo sự tin cậy. Việc hiển thị bản đồ, thông tin liên hệ và địa chỉ cụ thể giúp người dùng xác minh shop và biết cách liên lạc khi cần hỗ trợ.

---

## Frame 52.png

**Nguyên tắc áp dụng:** Visual hierarchy, Mapping, Affordance, Efficiency, Consistency.

**Phân tích:** Giao diện landing/sản phẩm theo bộ sưu tập đặt hero lớn ở đầu, phần mô tả và CTA bên phải, tiếp theo là lợi ích, danh sách sản phẩm, cam kết và khối liên hệ. Các card sản phẩm có nút hành động như xem chi tiết, mua hoặc thêm vào giỏ.

**Nguyên tắc được áp dụng ở đâu và như thế nào:**

- **Visual hierarchy:** Áp dụng ở hero lớn đầu trang, tiêu đề bộ sưu tập và CTA; khu vực quan trọng nhất được nhấn mạnh trước.
- **Mapping:** Áp dụng ở luồng nội dung từ giới thiệu → lợi ích → danh sách sản phẩm → cam kết → liên hệ; thứ tự này khớp với hành trình thuyết phục người mua.
- **Affordance:** Áp dụng ở các nút xem chi tiết/mua hàng trên card; người dùng nhận ra đâu là hành động có thể thực hiện.
- **Efficiency:** Áp dụng ở việc đưa sản phẩm ngay sau phần giới thiệu; người dùng có thể chuyển từ đọc thông tin sang mua nhanh.
- **Consistency:** Áp dụng ở thẻ sản phẩm, màu CTA và footer giống các trang thương mại điện tử còn lại; tạo trải nghiệm thống nhất.

**Vì sao phải thiết kế như thế:** Với trang giới thiệu bộ sưu tập, người dùng cần hiểu nhanh giá trị, sau đó chuyển sang chọn sản phẩm. Bố cục theo thứ tự “giới thiệu → lợi ích → sản phẩm → hỗ trợ” giúp luồng quyết định rõ ràng.

---

## Frame 56.png

**Nguyên tắc áp dụng:** Recognition, Filtering efficiency, Consistency, Visibility, Perception.

**Phân tích:** Trang danh sách sản phẩm desktop có banner danh mục, sidebar bộ lọc, lưới sản phẩm và phân trang. Bộ lọc theo loại sản phẩm/brand giúp người dùng thu hẹp lựa chọn. Lưới sản phẩm giữ cấu trúc thẻ nhất quán gồm ảnh, tên, giá, biến thể và trạng thái.

**Nguyên tắc được áp dụng ở đâu và như thế nào:**

- **Recognition:** Áp dụng ở card sản phẩm có ảnh, tên, giá, đánh giá và biến thể; người dùng nhận diện sản phẩm qua mẫu thông tin quen thuộc.
- **Filtering efficiency:** Áp dụng ở sidebar bộ lọc theo loại/brand; người dùng thu hẹp danh sách mà không phải xem toàn bộ sản phẩm.
- **Consistency:** Áp dụng ở lưới sản phẩm có kích thước và cấu trúc card đồng nhất; việc đọc lướt trở nên ổn định.
- **Visibility:** Áp dụng ở banner danh mục, tiêu đề và phân trang; người dùng biết mình đang xem nhóm sản phẩm nào và có thể chuyển trang.
- **Perception:** Áp dụng ở khoảng cách giữa sidebar và lưới sản phẩm; giao diện tách rõ vùng lọc và vùng kết quả.

**Vì sao phải thiết kế như thế:** Khi có nhiều sản phẩm, người dùng cần công cụ lọc để tìm đúng món nhanh hơn. Cấu trúc card lặp lại giúp người dùng nhận diện thông tin mà không cần học lại ở từng sản phẩm.

---

## Frame 82.png

**Nguyên tắc áp dụng:** Visibility of system status, Feedback, User control, Efficiency, Error Prevention.

**Phân tích:** Đây là giao diện giỏ hàng dạng drawer/popup. Danh sách sản phẩm, số lượng, nút xóa, tổng tiền và hai hành động **Xem giỏ hàng** / **Thanh toán** được đặt ngay trong một vùng nổi. Nút đóng ở góc trên giúp người dùng thoát nhanh.

**Nguyên tắc được áp dụng ở đâu và như thế nào:**

- **Visibility of system status:** Áp dụng ở drawer giỏ hàng hiển thị sản phẩm hiện có, số lượng và tổng tiền; người dùng biết trạng thái giỏ ngay lập tức.
- **Feedback:** Áp dụng ở việc giỏ hàng mở ra sau thao tác thêm/xem giỏ; hệ thống xác nhận rằng giỏ có dữ liệu để kiểm tra.
- **User control:** Áp dụng ở nút đóng, nút xóa sản phẩm và các lựa chọn **Xem giỏ hàng**/**Thanh toán**; người dùng quyết định bước tiếp theo.
- **Efficiency:** Áp dụng ở drawer nổi không buộc rời trang hiện tại; người dùng kiểm tra giỏ nhanh hơn.
- **Error Prevention:** Áp dụng ở phần tổng tiền và danh sách sản phẩm trước checkout; người dùng phát hiện sai sản phẩm/số lượng trước khi thanh toán.

**Vì sao phải thiết kế như thế:** Cart drawer giúp người dùng kiểm tra giỏ hàng mà không rời trang hiện tại. Điều này tăng hiệu quả mua sắm và giúp người dùng kiểm soát trước khi thanh toán.

---

## Frame 86.png

**Nguyên tắc áp dụng:** Affordance, Visibility, Call-to-action hierarchy, Mapping.

**Phân tích:** Giao diện tập trung vào phần mua nhanh của sản phẩm: ảnh nhỏ, tên sản phẩm, giá khuyến mãi, giá gạch, lựa chọn màu và nút **Mua ngay - Giao nhanh** màu vàng nổi bật. Nút có nền đặc làm hành động chính dễ nhận ra.

**Nguyên tắc được áp dụng ở đâu và như thế nào:**

- **Affordance:** Áp dụng ở nút **Mua ngay - Giao nhanh** nền vàng; hình dạng và màu nền cho thấy đây là nút có thể bấm.
- **Visibility:** Áp dụng ở giá khuyến mãi, giá gạch và CTA; thông tin mua hàng quan trọng được nhấn mạnh.
- **Call-to-action hierarchy:** Áp dụng ở việc CTA chính có màu nổi bật hơn các lựa chọn phụ; người dùng biết hành động ưu tiên là mua ngay.
- **Mapping:** Áp dụng ở thứ tự chọn màu/số lượng trước rồi đến mua ngay; luồng thao tác đúng với quy trình mua sản phẩm.

**Vì sao phải thiết kế như thế:** Ở khu vực mua hàng, người dùng cần nhận biết ngay hành động chính. Màu nổi bật và kích thước nút lớn giúp tăng khả năng bấm đúng CTA.

---

## Frame 87.png

**Nguyên tắc áp dụng:** Affordance, Visual hierarchy, Consistency, Minimalist design.

**Phân tích:** Giao diện tương tự Frame 86 nhưng nút **Mua ngay - Giao nhanh** dùng dạng viền đỏ thay vì nền đặc. Kiểu nút này vẫn thể hiện được khả năng bấm, nhưng mức độ nổi bật thấp hơn so với nút nền đặc.

**Nguyên tắc được áp dụng ở đâu và như thế nào:**

- **Affordance:** Áp dụng ở nút **Mua ngay - Giao nhanh** dạng viền; người dùng vẫn nhận ra đây là thành phần có thể bấm.
- **Visual hierarchy:** Áp dụng ở tương quan giữa giá, tùy chọn màu và nút mua; CTA vẫn nằm sau các lựa chọn cần thiết.
- **Consistency:** Áp dụng ở cùng cấu trúc thông tin với Frame 86; người dùng không phải học lại luồng mua hàng.
- **Minimalist design:** Áp dụng ở nút viền thay vì nút nền đặc; mức nhấn thị giác giảm, phù hợp nếu muốn giao diện nhẹ hơn hoặc CTA ít áp lực hơn.

**Vì sao phải thiết kế như thế:** Dạng nút viền phù hợp khi muốn giảm độ “gắt” của CTA hoặc dùng cho trạng thái phụ. Tuy nhiên nếu đây là hành động chính, nên cân nhắc nút nền đặc để tăng visibility và affordance.

---

## Frame 88.png

**Nguyên tắc áp dụng:** Feedback, Affordance, Recognition, Efficiency, Consistency.

**Phân tích:** Trang danh sách sản phẩm giống Frame 56 nhưng có trạng thái tương tác trên card sản phẩm, ví dụ nút hành động màu vàng xuất hiện/nổi bật trên sản phẩm. Đây là feedback trực quan cho biết sản phẩm đang được focus/hover hoặc có thể thao tác.

**Nguyên tắc được áp dụng ở đâu và như thế nào:**

- **Feedback:** Áp dụng ở trạng thái hover/focus trên card sản phẩm; giao diện cho biết sản phẩm đang được trỏ hoặc có thể thao tác.
- **Affordance:** Áp dụng ở nút hành động xuất hiện/nổi bật trên card; người dùng nhận ra có thể xem/mua sản phẩm.
- **Recognition:** Áp dụng ở cấu trúc card giữ ảnh, tên, giá, đánh giá giống trang danh sách; người dùng đọc thông tin theo mẫu quen thuộc.
- **Efficiency:** Áp dụng ở thao tác nhanh ngay trên card; người dùng không cần mở trang chi tiết cho mọi sản phẩm.
- **Consistency:** Áp dụng ở lưới, bộ lọc và phân trang tương tự Frame 56; trạng thái tương tác được thêm mà không phá vỡ bố cục chính.

**Vì sao phải thiết kế như thế:** Trạng thái hover giúp người dùng biết phần tử nào đang tương tác được. Điều này cải thiện affordance và giảm lỗi khi chọn nhầm sản phẩm.

---

## Giỏ hàng.png

**Nguyên tắc áp dụng:** Visibility, Mapping, Efficiency, Error Prevention, User control.

**Phân tích:** Trang giỏ hàng desktop dùng bảng để hiển thị sản phẩm, số lượng và tổng tiền. Khối tóm tắt bên phải hiển thị tổng phụ, tổng và nút **Thanh toán**. Bố cục bảng phù hợp vì người dùng cần so sánh nhiều dòng sản phẩm.

**Nguyên tắc được áp dụng ở đâu và như thế nào:**

- **Visibility:** Áp dụng ở bảng sản phẩm, cột số lượng, giá và tổng tiền; thông tin cần kiểm tra trước thanh toán được hiển thị rõ.
- **Mapping:** Áp dụng ở danh sách sản phẩm bên trái và tóm tắt đơn bên phải; người dùng thấy sản phẩm nào tạo ra tổng tiền nào.
- **Efficiency:** Áp dụng ở bố cục bảng; nhiều sản phẩm có thể được so sánh nhanh theo cùng cột.
- **Error Prevention:** Áp dụng ở số lượng, nút xóa và tổng thanh toán; người dùng chỉnh/sửa trước khi chuyển sang checkout.
- **User control:** Áp dụng ở các thao tác thay đổi số lượng, xóa sản phẩm và bấm **Thanh toán**; người dùng kiểm soát toàn bộ giỏ.

**Vì sao phải thiết kế như thế:** Giỏ hàng là nơi kiểm tra trước khi thanh toán. Việc tách danh sách sản phẩm và tổng tiền giúp người dùng rà soát số lượng, giá và quyết định tiếp tục mua một cách an toàn.

---

## GioHangMobile.png

**Nguyên tắc áp dụng:** Responsive design, Visibility, Efficiency, Minimalist design, Error Prevention.

**Phân tích:** Phiên bản mobile của giỏ hàng chuyển từ bảng sang danh sách dọc. Mỗi sản phẩm có ảnh, tên, thông tin biến thể, giá và số lượng. Tổng tiền và nút **Thanh toán** được đặt ở cuối, phù hợp với luồng cuộn trên điện thoại.

**Nguyên tắc được áp dụng ở đâu và như thế nào:**

- **Responsive design:** Áp dụng ở việc chuyển bảng desktop thành danh sách dọc; giao diện phù hợp chiều rộng điện thoại.
- **Visibility:** Áp dụng ở từng item có ảnh, tên, biến thể, giá và số lượng; thông tin sản phẩm vẫn đầy đủ dù màn hình nhỏ.
- **Efficiency:** Áp dụng ở nút thanh toán và tổng tiền đặt sau danh sách; người dùng kiểm tra xong có thể thực hiện ngay bước tiếp theo.
- **Minimalist design:** Áp dụng ở việc loại bỏ các cột bảng không phù hợp mobile; chỉ giữ thông tin cần thiết cho quyết định thanh toán.
- **Error Prevention:** Áp dụng ở vùng số lượng và tổng tiền; người dùng kiểm tra sai lệch trước khi đặt hàng.

**Vì sao phải thiết kế như thế:** Bảng nhiều cột không phù hợp với mobile. Danh sách dọc giúp dễ đọc, dễ kiểm tra từng sản phẩm và tránh phải zoom/phóng màn hình.

---

## Header Mobile.png

**Nguyên tắc áp dụng:** Visibility, Affordance, Consistency, Efficiency, Recognition.

**Phân tích:** Header mobile gồm hamburger menu, biểu tượng tìm kiếm, logo ở giữa và giỏ hàng ở bên phải. Các biểu tượng quen thuộc giúp người dùng nhận biết chức năng mà không cần đọc nhiều chữ.

**Nguyên tắc được áp dụng ở đâu và như thế nào:**

- **Visibility:** Áp dụng ở các icon menu, tìm kiếm, logo và giỏ hàng trên cùng màn hình; chức năng chính luôn xuất hiện trong vùng dễ chạm.
- **Affordance:** Áp dụng ở hamburger menu và icon giỏ hàng quen thuộc; người dùng hiểu đây là nút có thể bấm.
- **Consistency:** Áp dụng ở vị trí header cố định theo chuẩn website mobile; người dùng dễ dự đoán cách điều hướng.
- **Efficiency:** Áp dụng ở việc gom các chức năng thường dùng vào header; người dùng mở menu/tìm kiếm/giỏ hàng mà không phải cuộn.
- **Recognition:** Áp dụng ở icon thay cho chữ; người dùng nhận diện chức năng nhờ ký hiệu phổ biến.

**Vì sao phải thiết kế như thế:** Trên mobile, header cần tiết kiệm không gian nhưng vẫn giữ các chức năng chính: mở menu, tìm kiếm, về trang chủ và xem giỏ hàng. Cách đặt logo giữa còn giúp duy trì nhận diện thương hiệu.

---

## SanPhamMobile.png

**Nguyên tắc áp dụng:** Responsive design, Recognition, Efficiency, Perception, Consistency.

**Phân tích:** Danh sách sản phẩm mobile dùng lưới hai cột, mỗi card gồm ảnh, tên, giá, đánh giá và biểu tượng thao tác. Phân trang đặt dưới cùng giúp người dùng chuyển trang sau khi xem hết danh sách hiện tại.

**Nguyên tắc được áp dụng ở đâu và như thế nào:**

- **Responsive design:** Áp dụng ở lưới hai cột; thiết kế tận dụng chiều rộng mobile tốt hơn danh sách một cột dài.
- **Recognition:** Áp dụng ở card sản phẩm gồm ảnh, tên, giá, đánh giá và icon thao tác; người dùng nhận diện sản phẩm theo mẫu quen thuộc.
- **Efficiency:** Áp dụng ở phân trang và lưới card; người dùng xem được nhiều sản phẩm trong ít lần cuộn hơn.
- **Perception:** Áp dụng ở ảnh sản phẩm lớn trong card; người dùng phân biệt sản phẩm bằng hình ảnh trước khi đọc tên.
- **Consistency:** Áp dụng ở cấu trúc card giống danh sách sản phẩm desktop; trải nghiệm xuyên thiết bị thống nhất.

**Vì sao phải thiết kế như thế:** Lưới hai cột tận dụng chiều rộng điện thoại tốt hơn danh sách một cột, đồng thời vẫn đủ không gian cho ảnh và thông tin chính. Card nhất quán giúp đọc lướt nhanh.

---

## Tìm kiếm sản phẩm 1.png

**Nguyên tắc áp dụng:** Recognition rather than recall, Efficiency, Visibility, Minimalist design.

**Phân tích:** Giao diện tìm kiếm ở trạng thái chưa nhập từ khóa, hiển thị ô tìm kiếm và danh sách gợi ý/danh mục phổ biến như search more, chuột gaming, bàn phím, lót chuột, tai nghe, khuyến mãi. Người dùng có thể chọn nhanh thay vì phải nhớ chính xác tên sản phẩm.

**Nguyên tắc được áp dụng ở đâu và như thế nào:**

- **Recognition rather than recall:** Áp dụng ở danh sách gợi ý từ khóa/danh mục; người dùng chọn ý tưởng tìm kiếm có sẵn thay vì nhớ chính xác tên sản phẩm.
- **Efficiency:** Áp dụng ở ô tìm kiếm và gợi ý ngay trong cùng popup/trang tìm kiếm; giảm số bước bắt đầu tìm sản phẩm.
- **Visibility:** Áp dụng ở ô tìm kiếm đặt nổi bật phía trên; người dùng biết chức năng chính của màn hình.
- **Minimalist design:** Áp dụng ở trạng thái chưa nhập chỉ hiển thị các gợi ý cần thiết; không làm người dùng bị quá tải.

**Vì sao phải thiết kế như thế:** Tìm kiếm trống nên cung cấp gợi ý để định hướng. Điều này giảm tải trí nhớ và giúp người dùng bắt đầu khám phá sản phẩm nhanh hơn.

---

## Tìm kiếm sản phẩm 2.png

**Nguyên tắc áp dụng:** Feedback, Visibility of system status, Recognition, Efficiency, Perception.

**Phân tích:** Khi có từ khóa, giao diện hiển thị kết quả tìm kiếm ở bên trái và danh mục ở bên phải. Kết quả có ảnh, tên và giá, giúp người dùng nhận diện sản phẩm nhanh. Việc chia cột giúp tách rõ “sản phẩm tìm được” và “danh mục liên quan”.

**Nguyên tắc được áp dụng ở đâu và như thế nào:**

- **Feedback:** Áp dụng ở danh sách kết quả xuất hiện sau khi nhập từ khóa; hệ thống phản hồi rằng truy vấn đã được xử lý.
- **Visibility of system status:** Áp dụng ở khu vực kết quả và danh mục liên quan; người dùng biết đang có sản phẩm phù hợp với từ khóa.
- **Recognition:** Áp dụng ở mỗi kết quả có ảnh, tên và giá; người dùng nhận diện sản phẩm mà không cần mở từng trang.
- **Efficiency:** Áp dụng ở kết quả trực tiếp trong giao diện tìm kiếm; rút ngắn đường đi từ từ khóa đến sản phẩm.
- **Perception:** Áp dụng ở bố cục chia cột kết quả và danh mục; người dùng phân biệt loại thông tin dễ hơn.

**Vì sao phải thiết kế như thế:** Khi tìm kiếm, người dùng cần phản hồi ngay để biết hệ thống đã nhận từ khóa. Hiển thị kết quả trực tiếp giúp rút ngắn đường đi đến sản phẩm.

---

## Tìm kiếm sản phẩm 3.png

**Nguyên tắc áp dụng:** Feedback, Help users recover from errors, Visibility, Minimalist design.

**Phân tích:** Giao diện hiển thị thông báo **Không tìm thấy kết quả** khi từ khóa không trả về sản phẩm. Đây là trạng thái rỗng có phản hồi rõ ràng, giúp người dùng biết hệ thống vẫn hoạt động nhưng không có dữ liệu phù hợp.

**Nguyên tắc được áp dụng ở đâu và như thế nào:**

- **Feedback:** Áp dụng ở thông báo **Không tìm thấy kết quả**; hệ thống nói rõ kết quả tìm kiếm hiện không có dữ liệu.
- **Help users recover from errors:** Áp dụng ở trạng thái rỗng của tìm kiếm; người dùng hiểu cần đổi từ khóa hoặc quay lại danh mục.
- **Visibility:** Áp dụng ở thông báo đặt ngay vùng kết quả; người dùng không nhầm với trạng thái đang tải.
- **Minimalist design:** Áp dụng ở việc chỉ hiển thị thông báo cần thiết khi không có kết quả; tránh gây nhiễu bằng dữ liệu không liên quan.

**Vì sao phải thiết kế như thế:** Nếu không có thông báo, người dùng có thể nghĩ trang bị lỗi hoặc đang tải chậm. Trạng thái không có kết quả cần được nói rõ để người dùng đổi từ khóa hoặc quay lại danh mục.

---

## Trang chủ.png

**Nguyên tắc áp dụng:** Responsive design, Visual hierarchy, Recognition, Perception, Satisfaction.

**Phân tích:** Đây là phiên bản mobile của trang chủ, gồm hero/banner, danh mục/sản phẩm nổi bật, lợi ích dịch vụ, đánh giá khách hàng, đối tác và thông tin footer. Các phần được xếp dọc theo luồng cuộn tự nhiên của mobile.

**Nguyên tắc được áp dụng ở đâu và như thế nào:**

- **Responsive design:** Áp dụng ở bố cục xếp dọc các khối hero, danh mục, sản phẩm, lợi ích và footer; phù hợp hành vi cuộn trên mobile.
- **Visual hierarchy:** Áp dụng ở hero/banner đầu trang và các tiêu đề khu vực; người dùng biết phần nào quan trọng trước.
- **Recognition:** Áp dụng ở danh mục/sản phẩm nổi bật và icon lợi ích; người dùng nhận diện nhanh nội dung mua sắm.
- **Perception:** Áp dụng ở khoảng cách giữa các section; người dùng phân biệt từng nhóm thông tin khi cuộn.
- **Satisfaction:** Áp dụng ở đánh giá khách hàng, đối tác và lợi ích dịch vụ; giao diện tạo niềm tin cho người mua mới.

**Vì sao phải thiết kế như thế:** Trang chủ cần giới thiệu nhanh thương hiệu, sản phẩm và lý do nên mua. Bố cục theo từng khối giúp người dùng nhận biết nội dung mà không bị quá tải.

---

## câu hỏi thường gặp.png

**Nguyên tắc áp dụng:** Help and documentation, Recognition rather than recall, Minimalist design, User control.

**Phân tích:** Trang FAQ dùng dạng accordion cho các câu hỏi thường gặp. Người dùng chỉ mở nội dung mình cần, thay vì phải đọc toàn bộ văn bản dài. Sidebar tài khoản giữ nhất quán với các trang cá nhân khác.

**Nguyên tắc được áp dụng ở đâu và như thế nào:**

- **Help and documentation:** Áp dụng ở danh sách FAQ; giao diện cung cấp câu trả lời cho các vấn đề thường gặp mà không cần liên hệ hỗ trợ.
- **Recognition rather than recall:** Áp dụng ở tiêu đề từng câu hỏi; người dùng nhận diện vấn đề giống nhu cầu của mình rồi mở ra xem.
- **Minimalist design:** Áp dụng ở accordion; chỉ câu trả lời cần xem mới được mở, giảm lượng chữ hiển thị cùng lúc.
- **User control:** Áp dụng ở khả năng mở/đóng từng câu hỏi; người dùng tự quyết định nội dung nào cần đọc.

**Vì sao phải thiết kế như thế:** FAQ là phần hỗ trợ người dùng tự giải quyết vấn đề. Accordion giúp giảm lượng thông tin hiển thị cùng lúc, tránh quá tải và tăng khả năng tìm đúng câu trả lời.

---

## giới thiệu với bạn bè.png

**Nguyên tắc áp dụng:** Visibility, Feedback, Motivation design, User satisfaction, Recognition.

**Phân tích:** Giao diện referral hiển thị voucher, mã giới thiệu, lợi ích cho bạn và trạng thái như voucher đã nhận, đơn hàng đã hoàn thành, đơn hàng đang xử lý. Các khối màu khác nhau giúp phân biệt trạng thái.

**Nguyên tắc được áp dụng ở đâu và như thế nào:**

- **Visibility:** Áp dụng ở mã giới thiệu, voucher và trạng thái tiến trình; thông tin quan trọng của chương trình được đặt rõ.
- **Feedback:** Áp dụng ở các trạng thái như voucher đã nhận, đơn đang xử lý, đơn hoàn thành; người dùng biết lời giới thiệu đang ở bước nào.
- **Motivation design:** Áp dụng ở phần lợi ích cho người giới thiệu và bạn bè; giao diện làm rõ phần thưởng để khuyến khích chia sẻ.
- **User satisfaction:** Áp dụng ở thẻ voucher và phần thưởng trực quan; người dùng cảm thấy chương trình có giá trị cụ thể.
- **Recognition:** Áp dụng ở màu/nhãn trạng thái khác nhau; người dùng phân biệt kết quả mà không cần đọc nhiều mô tả.

**Vì sao phải thiết kế như thế:** Chương trình giới thiệu cần minh bạch phần thưởng và tiến độ. Khi người dùng thấy mã, voucher và trạng thái rõ ràng, họ có động lực chia sẻ hơn và ít phải hỏi hỗ trợ.

---

## homepage.png

**Nguyên tắc áp dụng:** Visual hierarchy, Attention, Perception, Consistency, Satisfaction.

**Phân tích:** Trang chủ desktop có banner lớn, danh mục sản phẩm, nhiều khu vực sản phẩm, lợi ích dịch vụ, đánh giá khách hàng, thương hiệu đối tác và footer. Các khối nội dung được phân chia bằng khoảng trắng, tiêu đề và lưới card.

**Nguyên tắc được áp dụng ở đâu và như thế nào:**

- **Visual hierarchy:** Áp dụng ở banner lớn, danh mục, khối sản phẩm và footer; trang dẫn mắt người dùng theo mức độ quan trọng.
- **Attention:** Áp dụng ở hero/banner và các tiêu đề section; giao diện kéo sự chú ý vào chương trình hoặc nhóm sản phẩm chính.
- **Perception:** Áp dụng ở lưới card, khoảng trắng và phân khu nội dung; người dùng dễ tách nhóm sản phẩm, lợi ích, đánh giá và thương hiệu.
- **Consistency:** Áp dụng ở header, card sản phẩm, CTA và footer; các thành phần dùng cùng phong cách thị giác.
- **Satisfaction:** Áp dụng ở phần đánh giá khách hàng, cam kết dịch vụ và thương hiệu đối tác; tăng cảm giác tin cậy khi mua sắm.

**Vì sao phải thiết kế như thế:** Trang chủ e-commerce cần dẫn người dùng từ nhận diện thương hiệu đến khám phá sản phẩm và tạo niềm tin. Banner thu hút chú ý, danh mục giúp điều hướng, đánh giá và đối tác tăng độ tin cậy.

---

## iPhone 17 - 1.png

**Nguyên tắc áp dụng:** Minimalist design, Constraint, Visibility, Efficiency.

**Phân tích:** Đây là màn hình đăng nhập mobile bằng email. Giao diện chỉ gồm logo, tiêu đề, ô nhập email và nút **Tiếp tục**. Thiết kế ít thành phần, tập trung vào một hành động chính.

**Nguyên tắc được áp dụng ở đâu và như thế nào:**

- **Minimalist design:** Áp dụng ở màn hình chỉ có logo, tiêu đề, ô email và nút **Tiếp tục**; loại bỏ thông tin phụ để tập trung vào đăng nhập.
- **Constraint:** Áp dụng ở trường email duy nhất; người dùng biết bước đầu chỉ cần nhập email.
- **Visibility:** Áp dụng ở nút **Tiếp tục** đặt ngay dưới input; hành động chính dễ thấy trên mobile.
- **Efficiency:** Áp dụng ở luồng đăng nhập một trường; giảm thời gian nhập liệu ban đầu.

**Vì sao phải thiết kế như thế:** Trên mobile, đăng nhập cần nhanh và ít gây nhiễu. Một trường email duy nhất giúp giảm số bước nhập liệu ban đầu và tạo luồng đăng nhập rõ ràng.

---

## iPhone 17 - 2.png

**Nguyên tắc áp dụng:** Feedback, Error handling, Constraint, Visibility.

**Phân tích:** Màn hình đăng nhập mobile hiển thị lỗi dưới ô email. Màu đỏ và vị trí sát trường nhập giúp người dùng biết trường nào sai. Nút **Tiếp tục** vẫn hiện rõ để người dùng sửa và thử lại.

**Nguyên tắc được áp dụng ở đâu và như thế nào:**

- **Feedback:** Áp dụng ở dòng lỗi bên dưới ô email; hệ thống phản hồi ngay sau khi email không hợp lệ.
- **Error handling:** Áp dụng ở việc chỉ rõ trường sai thay vì hiển thị lỗi chung chung; người dùng biết cần sửa phần nào.
- **Constraint:** Áp dụng ở yêu cầu định dạng email; giao diện ngăn người dùng tiếp tục với dữ liệu không hợp lệ.
- **Visibility:** Áp dụng ở màu đỏ và vị trí gần input; lỗi nổi bật mà không làm mất luồng thao tác.

**Vì sao phải thiết kế như thế:** Lỗi nhập email là lỗi phổ biến. Thông báo trực tiếp tại trường nhập giúp người dùng sửa nhanh, không phải tự tìm lỗi ở nơi khác.

---

## lịch sử exp.png

**Nguyên tắc áp dụng:** Visibility, Memorability, Consistency, Minimalist design.

**Phân tích:** Trang lịch sử EXP dùng bảng với các cột **Hoạt động**, **Ngày**, **EXP nhận được**. Khi chưa có dữ liệu, giao diện thông báo chưa có hoạt động nào. Sidebar tài khoản tiếp tục giữ cấu trúc nhất quán.

**Nguyên tắc được áp dụng ở đâu và như thế nào:**

- **Visibility:** Áp dụng ở bảng lịch sử có cột **Hoạt động**, **Ngày**, **EXP nhận được**; người dùng thấy rõ thông tin cần kiểm tra.
- **Memorability:** Áp dụng ở lịch sử điểm; người dùng có thể nhớ lại nguồn EXP mà không cần tự ghi nhớ.
- **Consistency:** Áp dụng ở sidebar tài khoản và bố cục bảng giống các trang quản lý khác; cách sử dụng quen thuộc.
- **Minimalist design:** Áp dụng ở trạng thái chưa có hoạt động; giao diện chỉ thông báo cần thiết, không tạo dữ liệu giả.

**Vì sao phải thiết kế như thế:** Lịch sử điểm cần minh bạch và dễ kiểm tra. Bảng giúp người dùng nhớ lại điểm đến từ đâu, còn trạng thái rỗng giúp tránh hiểu nhầm là lỗi tải dữ liệu.

---

## lịch sử mua hàng-1.png

**Nguyên tắc áp dụng:** Visibility, Empty state feedback, Efficiency, Consistency.

**Phân tích:** Đây là trạng thái rỗng của lịch sử đơn hàng, với bảng tiêu đề các cột và thông báo **Bạn đang có 0 đơn hàng**. Ô tìm kiếm ở góc phải vẫn được giữ để tạo cấu trúc tương tự trang có dữ liệu.

**Nguyên tắc được áp dụng ở đâu và như thế nào:**

- **Visibility:** Áp dụng ở tiêu đề bảng và thông báo **Bạn đang có 0 đơn hàng**; trạng thái dữ liệu hiện tại được nói rõ.
- **Empty state feedback:** Áp dụng ở vùng nội dung rỗng; người dùng biết không có đơn hàng chứ không phải trang bị lỗi.
- **Efficiency:** Áp dụng ở ô tìm kiếm vẫn giữ đúng vị trí; khi có đơn hàng, người dùng đã biết nơi tra cứu.
- **Consistency:** Áp dụng ở cấu trúc bảng giống trạng thái có dữ liệu; giúp trang mở rộng tự nhiên khi phát sinh đơn.

**Vì sao phải thiết kế như thế:** Người dùng cần biết hiện tại không có đơn hàng, không phải hệ thống lỗi. Giữ cấu trúc bảng giúp trạng thái rỗng vẫn đúng ngữ cảnh và dễ mở rộng khi có dữ liệu.

---

## lịch sử mua hàng.png

**Nguyên tắc áp dụng:** Visibility, Recognition, Efficiency, User control, Error Prevention.

**Phân tích:** Trang lịch sử mua hàng có bảng đơn hàng với thời gian, trạng thái, hình thức thanh toán, trạng thái thanh toán, tổng tiền và chức năng như **Chi tiết**, **Hủy đơn**. Nhãn màu giúp phân biệt trạng thái nhanh.

**Nguyên tắc được áp dụng ở đâu và như thế nào:**

- **Visibility:** Áp dụng ở bảng đơn hàng với thời gian, trạng thái, thanh toán và tổng tiền; dữ liệu quan trọng được hiển thị cùng hàng.
- **Recognition:** Áp dụng ở nhãn màu trạng thái đơn/thanh toán; người dùng nhận diện trạng thái nhanh hơn đọc văn bản dài.
- **Efficiency:** Áp dụng ở bảng nhiều dòng và ô tìm kiếm; người dùng tra cứu đơn cũ nhanh.
- **User control:** Áp dụng ở nút **Chi tiết** và **Hủy đơn**; người dùng có thể xem hoặc xử lý đơn theo trạng thái.
- **Error Prevention:** Áp dụng ở việc hiển thị trạng thái trước khi cho thao tác; người dùng tránh hủy/kiểm tra nhầm đơn.

**Vì sao phải thiết kế như thế:** Đơn hàng là dữ liệu quan trọng, cần dễ tra cứu và kiểm soát. Bảng giúp so sánh nhiều đơn, còn nhãn màu và nút thao tác giúp người dùng nhận biết hành động có thể làm.

---

## login fail.png

**Nguyên tắc áp dụng:** Feedback, Error Prevention, Help users recover from errors, Constraint.

**Phân tích:** Màn hình đăng nhập email desktop hiển thị lỗi trực tiếp dưới ô email. Khung input được nhấn mạnh bằng màu cảnh báo, giúp người dùng biết chính xác trường cần sửa.

**Nguyên tắc được áp dụng ở đâu và như thế nào:**

- **Feedback:** Áp dụng ở thông báo lỗi dưới ô email; hệ thống phản hồi rằng dữ liệu nhập chưa hợp lệ.
- **Error Prevention:** Áp dụng ở việc không cho tiếp tục khi email sai định dạng; tránh gửi yêu cầu đăng nhập không thể xử lý.
- **Help users recover from errors:** Áp dụng ở lỗi hiển thị sát trường email; người dùng biết cần sửa đúng vị trí.
- **Constraint:** Áp dụng ở input email; giao diện định hướng loại dữ liệu cần nhập là email.

**Vì sao phải thiết kế như thế:** Đăng nhập sai thông tin là tình huống thường gặp. Thiết kế lỗi tại chỗ giúp người dùng sửa nhanh và tránh mất thời gian tìm nguyên nhân.

---

## login.png

**Nguyên tắc áp dụng:** Minimalist design, Visibility, Efficiency, Consistency.

**Phân tích:** Giao diện đăng nhập desktop có logo, tiêu đề, ô email và nút **Tiếp tục**. Khoảng trắng lớn giúp phần form nổi bật, không bị cạnh tranh bởi các thành phần phụ.

**Nguyên tắc được áp dụng ở đâu và như thế nào:**

- **Minimalist design:** Áp dụng ở form đăng nhập chỉ gồm logo, tiêu đề, input và CTA; không có thành phần phụ làm phân tán chú ý.
- **Visibility:** Áp dụng ở nút **Tiếp tục** và ô email đặt giữa màn hình; luồng hành động chính rõ ràng.
- **Efficiency:** Áp dụng ở đăng nhập bắt đầu bằng một trường email; người dùng hoàn thành bước đầu nhanh.
- **Consistency:** Áp dụng ở màu sắc, logo và kiểu nút giống các màn hình xác thực khác; giữ trải nghiệm đăng nhập thống nhất.

**Vì sao phải thiết kế như thế:** Mục tiêu của màn hình này chỉ là bắt đầu đăng nhập. Giao diện tối giản làm giảm phân tâm và tăng khả năng hoàn thành tác vụ.

---

## thông tin tài khoản.png

**Nguyên tắc áp dụng:** Recognition, Consistency, User control, Visibility, Minimalist design.

**Phân tích:** Trang thông tin tài khoản hiển thị dữ liệu cá nhân theo từng dòng như họ tên, số điện thoại, giới tính, ngày sinh, chiều cao, cân nặng và nút **Cập nhật**. Sidebar tài khoản nhất quán giúp người dùng biết mình đang ở khu vực quản lý cá nhân.

**Nguyên tắc được áp dụng ở đâu và như thế nào:**

- **Recognition:** Áp dụng ở cấu trúc nhãn - giá trị như họ tên, số điện thoại, giới tính, ngày sinh; người dùng nhận diện dữ liệu cá nhân nhanh.
- **Consistency:** Áp dụng ở sidebar tài khoản và layout giống các trang quản lý cá nhân khác; người dùng biết cách di chuyển giữa các mục.
- **User control:** Áp dụng ở nút **Cập nhật**; người dùng có quyền chỉnh sửa thông tin của mình.
- **Visibility:** Áp dụng ở việc đặt toàn bộ thông tin trong vùng nội dung chính; dữ liệu tài khoản không bị ẩn sâu.
- **Minimalist design:** Áp dụng ở cách trình bày từng dòng đơn giản; tránh làm phần thông tin cá nhân trở nên rối.

**Vì sao phải thiết kế như thế:** Thông tin tài khoản cần dễ đọc, dễ kiểm tra và dễ cập nhật. Trình bày dạng nhãn - giá trị giúp người dùng nhận diện nhanh mà không cần ghi nhớ cấu trúc phức tạp.

---

## ví voucher.png

**Nguyên tắc áp dụng:** Recognition, Visibility, Satisfaction, Consistency, Perception.

**Phân tích:** Trang ví voucher hiển thị các mã giảm giá dạng thẻ, có tên voucher, điều kiện, hạn sử dụng và liên kết điều kiện. Banner khuyến mãi bên dưới tạo điểm nhấn và thu hút chú ý.

**Nguyên tắc được áp dụng ở đâu và như thế nào:**

- **Recognition:** Áp dụng ở thẻ voucher giống phiếu giảm giá; người dùng nhận ra ngay đây là mã ưu đãi có thể dùng.
- **Visibility:** Áp dụng ở tên voucher, điều kiện, hạn dùng và liên kết điều kiện; thông tin quyết định khả năng sử dụng được hiển thị rõ.
- **Satisfaction:** Áp dụng ở banner và các thẻ ưu đãi; giao diện tạo cảm giác người dùng đang sở hữu lợi ích cụ thể.
- **Consistency:** Áp dụng ở cách trình bày nhiều voucher theo cùng một mẫu thẻ; người dùng so sánh ưu đãi dễ hơn.
- **Perception:** Áp dụng ở phân tách từng voucher bằng khung/card; người dùng không nhầm điều kiện của voucher này với voucher khác.

**Vì sao phải thiết kế như thế:** Voucher cần được nhận diện nhanh để người dùng biết mã nào có thể dùng. Dạng thẻ giống phiếu giảm giá ngoài đời thực giúp tăng tính trực quan và hỗ trợ ghi nhớ.
