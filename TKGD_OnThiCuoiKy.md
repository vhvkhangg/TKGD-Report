# Review — Thiết kế giao diện & HCI

## Tài liệu lý thuyết đã dùng

- `03_User_Usability.pdf`: Người dùng, mô hình xử lý thông tin, nhận thức, usability, Norman/Shneiderman/Nielsen.
- `04_Controls (1).pdf`: Input/output design, report design, controls/widgets.
- `05_Scenarios_UseCases(1) (1).pdf`: UCD, quy trình thiết kế, xác định nhu cầu, scenario, use case.
- `06_Prototype.pdf`: Prototype, low-fidelity/high-fidelity, screen design, menu design.
- `07_Evaluation.pdf`: Usability evaluation, DECIDE, heuristic evaluation, questionnaires, lab-based evaluation, severity.

---

# Phần 1: Tổng quan về Thiết kế Giao diện & HCI

## 1. Thiết kế Tương tác là gì? Vì sao UI tốt quan trọng với thành công của phần mềm?

**Thiết kế Tương tác** (*Interaction Design*) là quá trình xây dựng cách thức con người và hệ thống tương tác với nhau.

Một UI tốt quan trọng vì:

1. **UI là nơi người dùng trực tiếp tiếp xúc với phần mềm.** 
2. **UI ảnh hưởng trực tiếp đến usability.** 
3. **UI chiếm tỷ trọng lớn trong vòng đời phần mềm.** 
4. **UI tốt giúp giảm chi phí hỗ trợ và đào tạo.** 
5. **UI là lợi thế cạnh tranh.** 

Kết luận: Thiết kế tương tác tốt làm phần mềm **dễ học, dễ dùng, ít lỗi, hiệu quả và tạo sự hài lòng**, từ đó tăng khả năng thành công của sản phẩm.

---

## 2. HCI là gì? Định nghĩa ACM SIGCHI và mục tiêu nghiên cứu chính của HCI

**HCI** (*Human-Computer Interaction*) là lĩnh vực nghiên cứu và thiết kế sự tương tác giữa con người và máy tính/hệ thống tương tác. HCI quan tâm đến cả phía con người, phía công nghệ, nhiệm vụ, môi trường sử dụng và cách đánh giá chất lượng tương tác.

**Định nghĩa của ACM SIGCHI:**  
HCI là ngành liên quan đến **thiết kế, đánh giá và cài đặt các hệ thống máy tính tương tác cho con người sử dụng**, đồng thời nghiên cứu các hiện tượng chính xung quanh việc sử dụng các hệ thống đó.

Các mục tiêu nghiên cứu chính của HCI:

1. **Hiểu người dùng** 
2. **Thiết kế hệ thống tương tác dễ dùng** 
3. **Giảm lỗi và rủi ro** 
4. **Đánh giá usability** 
5. **Cải tiến quy trình phát triển** 

---

## 3. User-Centered Design: triết lý, nguyên tắc, lợi ích và thách thức

**User-Centered Design (UCD)** là triết lý và quy trình thiết kế đặt người dùng vào trung tâm của mọi giai đoạn phát triển sản phẩm. UCD tạo sản phẩm có usability cao bằng cách:

- đặt người dùng ở trung tâm các pha phát triển;
- tập trung vào các mục tiêu usability;
- dựa trên các yếu tố nhận thức của con người;
- xem việc phát triển hệ thống tương tác là hoạt động đa ngành.

### Nguyên tắc cơ bản của UCD

1. **Nếu có vấn đề, hãy xem hệ thống là vấn đề trước.**  

2. **Người dùng kiểm soát chương trình.**  

3. **Cung cấp phản hồi rõ ràng.**  

4. **Thông tin hướng dẫn và thông báo lỗi phải dễ hiểu, đúng ngữ cảnh.**  

5. **Thiết kế phải tự nhiên, trực quan.**  

6. **Ràng buộc và phạm vi phải rõ.**  

### Vì sao UCD quan trọng?

UCD giúp:

- giảm chi phí sửa lỗi muộn vì phát hiện vấn đề từ sớm;
- tăng sự hài lòng và năng suất của người dùng;
- tạo sản phẩm đúng nhu cầu thật;
- giảm lỗi thao tác, giảm chi phí hỗ trợ và đào tạo;
- cải thiện khả năng chấp nhận sản phẩm.

### Thách thức khi áp dụng UCD

1. **Khó tuyển được nhóm người dùng tốt** 
2. **Người dùng không phải nhà thiết kế** 
3. **Người dùng không phải lúc nào cũng biết chính xác họ muốn gì** 
4. **Dễ hiểu sai dữ liệu người dùng** 
5. **Có đánh đổi với chức năng, hiệu năng, bảo mật, chi phí và thời gian.**

---

## 4. Quy trình Thiết kế Giao diện/Tương tác và giai đoạn quan trọng nhất

Theo tài liệu, quy trình thiết kế tương tác gồm 4 hoạt động chính:

1. **Identify needs & establish requirements — Xác định nhu cầu và yêu cầu**
2. **Develop alternative designs — Thiết kế các phương án**
3. **Build interactive versions — Tạo mẫu**
4. **Evaluate — Đánh giá**

Quy trình này có tính **lặp**: kết quả đánh giá có thể quay lại sửa yêu cầu, sửa thiết kế hoặc prototype.

### 4.1. Xác định nhu cầu và yêu cầu

**Mục tiêu:** hiểu người dùng, bối cảnh xã hội, hoạt động, artifacts/công cụ hiện có và vấn đề thật cần giải quyết.

**Cách thực hiện:**

- xác định ai mua sản phẩm, ai dùng trực tiếp, ai nhận output, ai dùng sản phẩm cạnh tranh;
- hỏi người dùng cần làm gì, hiện làm như thế nào, mong đợi gì;
- thu thập dữ liệu bằng bảng hỏi, phỏng vấn, quan sát, đọc tài liệu, nghiên cứu sản phẩm tương tự.

**Kết quả mong đợi:**

- danh sách người dùng và nhóm người dùng;
- yêu cầu chức năng, dữ liệu, bối cảnh sử dụng;
- scenario và use case mô tả yêu cầu.

### 4.2. Thiết kế các phương án

**Mục tiêu:** tạo nhiều giải pháp giao diện khác nhau đáp ứng yêu cầu đã xác định.

**Cách thực hiện:**

- thiết kế luồng màn hình;
- thiết kế menu, form, bảng, màn hình chính, màn hình chi tiết;
- lựa chọn controls phù hợp;
- nhóm chức năng theo nghiệp vụ, đối tượng hoặc logic tác vụ.

**Kết quả mong đợi:**

- danh sách màn hình;
- screen map;
- main screen/menu screen;
- bản mô tả chi tiết từng màn hình;
- các phương án thay thế để so sánh.

### 4.3. Tạo mẫu

**Mục tiêu:** trình bày thiết kế trước khi code bản cuối để kiểm tra sớm.

**Kết quả mong đợi:**

- low-fidelity prototype
- medium/high-fidelity prototype

### 4.4. Đánh giá

**Mục tiêu:** thu phản hồi để cải tiến thiết kế và đo mức độ usable của sản phẩm.

**Kết quả mong đợi:**

- danh sách vấn đề usability;
- mức độ nghiêm trọng;
- đề xuất redesign;
- ưu tiên sửa lỗi theo tác động và chi phí.

### Giai đoạn quan trọng nhất

Theo tôi, **xác định nhu cầu và yêu cầu** là giai đoạn quan trọng nhất. 
Lý do: Đây là nơi lỗi thường xảy ra nhất. Nếu hiểu sai người dùng hoặc sai bài toán, các bước sau như thiết kế, prototype, code và evaluation có thể vẫn “đúng kỹ thuật” nhưng giải quyết sai vấn đề. 

---

# Phần 2: Người dùng & Nhận thức

## 5. Vì sao phải hiểu rõ người dùng trong thiết kế giao diện?

Trong HCI, con người là mục tiêu cuối cùng của mọi hệ thống. Thiết kế giao diện phải hiểu người dùng vì:

1. **Người dùng có khả năng khác nhau.**  
   Có người mới dùng, có người chuyên gia, có người dùng không thường xuyên.

2. **Người dùng có thói quen thao tác khác nhau.**  
	Nếu giao diện đi ngược quy ước quen thuộc, người dùng dễ thao tác sai hoặc mất thời gian học lại.  

3. **Người dùng thường mắc lỗi và nhầm lẫn.**  

4. **Người dùng bị giới hạn bởi nhận thức.**  

5. **Người dùng sử dụng hệ thống qua giao diện.**  

6. **Người dùng khác lập trình viên.**  

Vì vậy, hiểu người dùng giúp thiết kế giao diện đúng nhu cầu, dễ học, ít lỗi và hiệu quả hơn.

---

## 6. Mô hình xử lý thông tin của con người trong HCI

Theo tài liệu, mô hình xử lý thông tin của con người gồm 3 thành phần chính: **Input/Output, Memory, Processor**.

### 6.1. Input

Input là cách con người tiếp nhận thông tin từ hệ thống. Trong giao diện, input của con người chủ yếu gồm:

- **Looking — nhìn:** có ảnh hưởng lớn nhất đến GUI. Màu sắc, độ tương phản, kích thước chữ, khoảng cách, biểu tượng đều tác động đến khả năng nhìn và hiểu.
- **Hearing — nghe:** âm báo, thông báo bằng âm thanh, cảnh báo.
- **Touching — chạm:** đặc biệt quan trọng với thiết bị cảm ứng, mobile.

### 6.2. Output

Output là cách con người hành động để điều khiển hệ thống:

- dùng tay để gõ phím, rê chuột, click, kéo thả, chạm;
- dùng giọng nói hoặc cử chỉ trong một số hệ thống;
- thực hiện lựa chọn, nhập dữ liệu, xác nhận, hủy bỏ.

### 6.3. Memory

Memory gồm trí nhớ cảm giác, trí nhớ ngắn hạn/làm việc và trí nhớ dài hạn. Người dùng không nhớ mọi thứ; họ chỉ nhớ những gì được chú ý và nhận thức. Ngữ cảnh cũng ảnh hưởng mạnh đến trí nhớ. Vì vậy, giao diện cần hỗ trợ nhận biết thay vì bắt người dùng nhớ lại.

### 6.4. Processor

Processor là quá trình xử lý nhận thức: suy luận, giải quyết vấn đề, học kỹ năng, xử lý lỗi. Khi giao diện phức tạp, bộ xử lý nhận thức bị quá tải, người dùng thao tác chậm và dễ sai.

Kết luận: thiết kế giao diện tốt phải phù hợp với cách con người **nhìn/nghe/chạm, ghi nhớ và suy nghĩ**.

---

## 7. Cognition trong HCI: vì sao cần hiểu, các yếu tố cốt lõi, Recognition vs Recall

### 7.1. Vì sao cần tìm hiểu cognition?

**Cognition** là quá trình con người làm quen với sự vật và thu nhận tri thức. Trong HCI, hiểu cognition giúp thiết kế giao diện phù hợp với cách người dùng chú ý, nhận biết, ghi nhớ và học thao tác. Nếu bỏ qua cognition, giao diện có thể:

- làm người dùng không thấy thông tin quan trọng;
- bắt người dùng nhớ quy trình dài;
- khiến người mới khó học;
- làm tăng lỗi và giảm năng suất.

### 7.2. Các quá trình nhận thức cốt lõi

#### Attention — Chú ý

Attention là việc chọn một số thông tin để tập trung trong rất nhiều thông tin xung quanh.

Vai trò trong UI:

- làm nổi bật thông tin cần chú ý;
- tránh đặt thông tin quan trọng ở nơi người dùng ít nhìn;
- không lạm dụng màu, animation, âm thanh vì có thể gây nhiễu.

#### Perception — Tri giác/Nhận biết

Perception là việc nhận biết sự vật thông qua giác quan: nhìn, nghe, chạm. 

Vai trò trong UI:

- chữ phải dễ đọc;
- icon phải khác nhau đủ rõ;
- âm thanh phải nghe được và có ý nghĩa;
- spacing và border giúp phân nhóm thông tin.

#### Memory — Trí nhớ

Memory là khả năng nhớ kiến thức để hành động đúng. 

Vai trò trong UI:

- giảm tải trí nhớ ngắn hạn;
- dùng menu, icon, nhãn nhất quán;
- cung cấp màu, cờ đánh dấu, category để hỗ trợ tổ chức thông tin;
- hiển thị lựa chọn thay vì bắt người dùng nhớ lệnh.

#### Learning — Học

Learning là quá trình học cách dùng ứng dụng để hoàn thành nhiệm vụ. 

Vai trò trong UI:

- hỗ trợ học qua thao tác trực tiếp;
- có multimedia help, tutorial đúng lúc;
- cho phép undo để khuyến khích khám phá;
- ràng buộc để tránh lỗi khi người dùng thử nghiệm.

### 7.3. Recognition vs Recall

- **Recognition — Nhận biết:** người dùng nhìn thấy một lựa chọn/thông tin rồi nhận ra nó.  
  Ví dụ: nhìn thấy nút “In hóa đơn” trong menu và chọn.

- **Recall — Nhớ lại:** người dùng phải tự nhớ thông tin/lệnh/quy trình từ trí nhớ.  
  Ví dụ: phải nhớ cú pháp lệnh `print_invoice --id 123`.

---

## 8. Ứng dụng hiểu biết về nhận thức vào thiết kế

### 8.1. Kỹ thuật thu hút Attention hiệu quả

Dựa trên tài liệu, các kỹ thuật thiết kế cho attention gồm:

1. **Màu sắc:** dùng màu để nhấn mạnh trạng thái, cảnh báo, nút chính. Không lạm dụng quá nhiều màu.
2. **Thứ tự:** đặt thông tin quan trọng ở vị trí người dùng nhìn trước.
3. **Khoảng cách:** dùng spacing để tách nhóm chức năng và giảm nhiễu.
4. **Animation:** dùng cho thay đổi trạng thái hoặc hướng dẫn, nhưng tránh animation không cần thiết.
5. **Âm thanh:** dùng cho cảnh báo quan trọng, không dùng tùy tiện.
6. **Alert chỉ khi cần thiết:** nếu cảnh báo xuất hiện quá nhiều, người dùng sẽ bỏ qua.

Ví dụ: nút “Xóa vĩnh viễn” nên dùng màu cảnh báo và hộp xác nhận; nhưng không nên dùng cảnh báo cho mọi thao tác nhỏ.

### 8.2. Kỹ thuật hỗ trợ Memory

1. **Không bắt người dùng nhớ quy trình phức tạp.**
2. **Dùng menu, icon và chức năng nhất quán.**
3. **Hiển thị lựa chọn thay vì yêu cầu nhập tự do nếu có danh sách giá trị.**
4. **Dùng category, màu, flag, tag để giúp tổ chức thông tin.**
5. **Cung cấp default value cho trường phổ biến.**
6. **Cung cấp ví dụ định dạng cho dữ liệu đặc biệt.**
7. **Giữ ngữ cảnh thao tác:** ví dụ breadcrumb, tiêu đề màn hình, trạng thái đang chỉnh sửa.

### 8.3. Kỹ thuật tăng Learnability

1. **Learning through doing:** cho người dùng học bằng thao tác thực tế, không bắt đọc manual dài.
2. **Undo quan trọng:** cho phép thử mà không sợ hỏng dữ liệu.
3. **Thiết kế khuyến khích khám phá:** giao diện rõ, có nhãn, có tooltip.
4. **Ràng buộc lỗi:** disable nút “Submit” khi form chưa hợp lệ, date picker.
5. **Help đúng ngữ cảnh:** hướng dẫn ngắn ngay tại nơi cần.
6. **Theo quy ước quen thuộc:** icon, menu, phím tắt, bố cục nên gần với chuẩn hệ điều hành hoặc web phổ biến.

---

# Phần 3: Tính Tiện lợi (Usability)

## 9. Khái niệm Usability, các thành phần, phân biệt Effectiveness/Efficiency và ví dụ

### 9.1. Khái niệm Usability

**Usability** là thuộc tính chất lượng đánh giá mức độ người dùng có thể **học và sử dụng sản phẩm để hoàn thành nhiệm vụ**, đồng thời **hài lòng** với quá trình đó. 

### 9.2. Các thành phần chính của Usability

#### Effectiveness — Hiệu quả

Effectiveness là mức độ hệ thống cung cấp đủ chức năng và giúp người dùng hoàn thành nhiệm vụ **đúng và đầy đủ**. 

Ví dụ: phần mềm thư viện cho phép tìm sách theo tác giả, tên sách và năm xuất bản. Người dùng tìm được đúng sách và vị trí đặt sách.

#### Efficiency — Hiệu suất

Efficiency là mức độ người dùng hoàn thành nhiệm vụ **nhanh** và với ít bước sau khi đã biết dùng hệ thống.

Ví dụ: người dùng chuyên nghiệp có phím tắt `Ctrl + S` để lưu thay vì phải mở menu nhiều bước.

#### Safety — An toàn

Safety là khả năng ngăn lỗi, giảm hậu quả lỗi và bảo vệ dữ liệu.

Ví dụ: khi xóa dữ liệu, hệ thống hỏi xác nhận; có undo.

#### Learnability — Dễ học

Learnability là mức độ người dùng mới có thể học nhanh cách dùng hệ thống.

Ví dụ: màn hình có nhãn rõ, tutorial ngắn, thao tác phổ biến có hướng dẫn.

#### Memorability — Dễ nhớ

Memorability là mức độ người dùng có thể nhớ lại cách dùng sau một thời gian không sử dụng.

Ví dụ: phần mềm dùng menu và icon theo quy ước, có gợi ý cho chức năng ít dùng.

#### Satisfaction — Hài lòng/Trải nghiệm người dùng

Satisfaction là cảm xúc và mức độ hài lòng khi dùng: vui, dễ chịu, có động lực; ngược lại là nhàm chán, khó chịu, bực bội.

Ví dụ: giao diện sạch, phản hồi nhanh, thông báo thân thiện.

### 9.3. Phân biệt Effectiveness và Efficiency

| Tiêu chí | Effectiveness | Efficiency |
|---|---|---|
| Câu hỏi chính | Người dùng có hoàn thành đúng và đủ nhiệm vụ không? | Người dùng hoàn thành nhiệm vụ nhanh và ít công sức không? |
| Trọng tâm | Độ đúng, độ đầy đủ | Tốc độ, số bước, năng suất |
| Ví dụ tốt | Tìm được đúng hồ sơ bệnh nhân | Tìm hồ sơ đó chỉ trong 2 click hoặc bằng phím tắt |
| Ví dụ xấu | Không có chức năng lọc nên tìm sai dữ liệu | Có chức năng lọc nhưng phải qua quá nhiều màn hình |


### 9.4. Ví dụ minh họa cho các thành phần Usability

1. **Safety tích cực:** form nhập ngày dùng DatePicker và kiểm tra ngày không hợp lệ.
2. **Learnability tiêu cực:** ứng dụng chỉ có icon không nhãn, người mới không biết icon nào là “xuất báo cáo”.
3. **Memorability tích cực:** các chức năng ít dùng vẫn nằm trong menu nhất quán, có tooltip và shortcut hiển thị cạnh menu item.
4. **Satisfaction tiêu cực:** website có màu chữ/nền tương phản kém, popup liên tục.
5. **Efficiency tích cực:** hệ thống có tìm kiếm nhanh, filter, phím tắt và giá trị mặc định.
6. **Effectiveness tiêu cực:** Ứng dụng đặt lịch khám bệnh có giao diện đẹp nhưng không hiển thị lịch trống của bác sĩ.
7. **Effectiveness tích cực:** Hệ thống quản lý sinh viên cho phép nhập mã số sinh viên và trả về đúng hồ sơ, điểm số, lớp học, trạng thái học vụ.
8. **Efficiency tiêu cực:** Nhân viên muốn in hóa đơn nhưng phải mở từng đơn hàng, vào chi tiết, chọn xuất file, rồi mới in.   
9. **Learnability tích cực:** Khi người dùng lần đầu mở phần mềm quản lý công việc, màn hình chính có các nút như “Thêm công việc”, “Giao việc”, “Đánh dấu hoàn thành” có tên rõ ràng, dễ hiểu.  
10. **Memorability tiêu cực:** Một chức năng ít dùng như “Khôi phục dữ liệu” lúc thì nằm trong menu “Cài đặt”, lúc thì nằm trong menu “Công cụ”.

---

# Phần 4: Nguyên tắc Thiết kế

## 10. Norman, Shneiderman và Nielsen

## 10.1. Sáu nguyên tắc thiết kế của Donald A. Norman

### 1. Visibility — Tính hiển thị

**Ý nghĩa:** Người dùng phải nhìn thấy được chức năng, trạng thái hoặc hành động có thể thực hiện.

**Ví dụ tốt:** Nút “Lưu” hiển thị rõ ở cuối form; trạng thái “Đang lưu...” xuất hiện khi hệ thống xử lý.

**Giải thích:** Nếu chức năng bị ẩn hoặc trạng thái không rõ, người dùng không biết nên làm gì tiếp theo.

### 2. Affordance — Tính gợi ý thao tác

**Ý nghĩa:** Hình dạng/kiểu hiển thị của đối tượng phải gợi cho người dùng cách sử dụng.

**Ví dụ tốt:** Button có viền, nền, hover state nên người dùng hiểu là có thể click; textbox có khung nhập nên người dùng hiểu là có thể gõ.

**Ví dụ kém:** Text thường được dùng như button nhưng không có dấu hiệu click được.

### 3. Constraint — Ràng buộc

**Ý nghĩa:** Giao diện nên giới hạn các hành động không hợp lệ để phòng lỗi.

**Ví dụ tốt:** Trường “Ngày sinh” không cho chọn ngày trong tương lai; nút “Thanh toán” bị disable khi chưa nhập địa chỉ.

**Giải thích:** Ràng buộc tốt giúp người dùng không mắc lỗi ngay từ đầu.

### 4. Mapping — Ánh xạ

**Ý nghĩa:** Quan hệ giữa control và kết quả phải tự nhiên, dễ đoán.

**Ví dụ tốt:** Thanh trượt âm lượng kéo sang phải là tăng, sang trái là giảm; nút điều hướng `>` nghĩa là đi tiếp.

**Giải thích:** Mapping tốt giảm thời gian suy nghĩ và giảm thao tác nhầm.

### 5. Feedback — Phản hồi

**Ý nghĩa:** Sau mỗi hành động quan trọng, hệ thống phải phản hồi rõ việc gì đã xảy ra.

**Ví dụ tốt:** Sau khi bấm “Lưu”, hệ thống hiện “Đã lưu thành công”; khi tải dữ liệu, có loading indicator.

**Giải thích:** Không có feedback, người dùng có thể bấm lặp lại, nghi ngờ hệ thống lỗi hoặc không biết hành động đã thành công chưa.

### 6. Consistency — Nhất quán

**Ý nghĩa:** Từ ngữ, icon, bố cục, màu sắc và hành vi phải nhất quán trong toàn hệ thống.

**Ví dụ tốt:** Toàn bộ hệ thống dùng “Lưu” cho cùng một hành động, không chỗ dùng “Lưu”, chỗ dùng “Ghi file”.

**Giải thích:** Nhất quán giúp người dùng chuyển kinh nghiệm từ màn hình này sang màn hình khác, giảm học lại và giảm lỗi.

---

## 10.2. Tám quy tắc vàng của Ben Shneiderman

### 1. Strive for consistency — Cố gắng nhất quán

Giao diện phải nhất quán về thuật ngữ, vị trí nút, màu sắc, icon và luồng thao tác.

**Ví dụ:** Nút “Hủy” luôn nằm bên trái “Lưu” trong mọi dialog.

### 2. Enable frequent users to use shortcuts — Cho người dùng thường xuyên dùng phím tắt

Người dùng chuyên gia cần thao tác nhanh.

**Ví dụ:** `Ctrl + S` để lưu, `Ctrl + F` để tìm kiếm, phím tắt cho thao tác lặp lại.

### 3. Offer informative feedback — Cung cấp phản hồi có thông tin

Mỗi hành động nên có phản hồi phù hợp.

**Ví dụ:** Upload file hiển thị phần trăm tiến trình và thông báo hoàn tất.

### 4. Design dialogs to yield closure — Thiết kế hội thoại có điểm kết thúc rõ

Chuỗi thao tác phải cho người dùng biết đã hoàn thành.

**Ví dụ:** Sau khi đặt lịch khám, hệ thống hiển thị màn hình xác nhận với mã lịch hẹn.

### 5. Offer error prevention and simple error handling — Phòng lỗi và xử lý lỗi đơn giản

Tốt nhất là ngăn lỗi trước; nếu lỗi xảy ra, thông báo phải dễ hiểu và chỉ cách sửa.

**Ví dụ:** Form email kiểm tra định dạng trước khi submit; thông báo “Email thiếu ký tự @”.

### 6. Permit easy reversal of actions — Cho phép đảo ngược hành động

Người dùng cần undo, back, cancel để cảm thấy an toàn.

**Ví dụ:** Xóa ghi chú có thể khôi phục trong thùng rác.

### 7. Support internal locus of control — Hỗ trợ cảm giác người dùng kiểm soát hệ thống

Người dùng phải cảm thấy họ chủ động điều khiển, không bị hệ thống ép.

**Ví dụ:** Cho phép dừng upload, hủy thao tác, đổi lựa chọn trước khi xác nhận.

### 8. Reduce short-term memory load — Giảm tải trí nhớ ngắn hạn

Không bắt người dùng nhớ nhiều thông tin giữa các màn hình.

**Ví dụ:** Hiển thị tóm tắt đơn hàng ở bước thanh toán thay vì bắt người dùng nhớ giỏ hàng.

---

## 10.3. Mười Heuristics của Jakob Nielsen

### 1. Visibility of system status — Hiển thị trạng thái hệ thống

Hệ thống phải cho người dùng biết chuyện gì đang xảy ra.

**Ví dụ:** Loading spinner, progress bar, trạng thái “Đã lưu”.

### 2. Match between system and the real world — Khớp với thế giới thật

Dùng ngôn ngữ và khái niệm quen thuộc với người dùng, không dùng thuật ngữ kỹ thuật khó hiểu.

**Ví dụ:** Dùng “Giỏ hàng” thay vì “temporary purchase object”.

### 3. User control and freedom — Người dùng có quyền kiểm soát và tự do

Cần có hủy, quay lại, undo, thoát khỏi trạng thái không mong muốn.

**Ví dụ:** Người dùng đang soạn tin nhắn có thể thoát mà không bắt buộc gửi.

### 4. Consistency and standards — Nhất quán và chuẩn

Tuân theo chuẩn nền tảng và nhất quán trong hệ thống.

**Ví dụ:** Icon kính lúp cho tìm kiếm; link màu và hành vi giống nhau.

### 5. Error prevention — Phòng lỗi

Thiết kế để lỗi khó xảy ra.

**Ví dụ:** Dropdown danh sách tỉnh/thành thay vì nhập tự do; xác nhận trước khi xóa vĩnh viễn.

### 6. Recognition rather than recall — Nhận biết hơn nhớ lại

Hiển thị lựa chọn, gợi ý và ngữ cảnh để người dùng không phải nhớ.

**Ví dụ:** Menu chức năng, autocomplete, recent files.

### 7. Flexibility and efficiency of use — Linh hoạt và hiệu quả

Hỗ trợ cả người mới và người dùng thành thạo.

**Ví dụ:** Có giao diện rõ cho người mới và phím tắt/macro cho người dùng chuyên nghiệp.

### 8. Aesthetic and minimalist design — Thẩm mỹ và tối giản

Không hiển thị thông tin không cần thiết làm nhiễu nhiệm vụ chính.

**Ví dụ:** Form đăng nhập chỉ cần email, mật khẩu, nút đăng nhập và link hỗ trợ cần thiết.

### 9. Help users recognize, diagnose, and recover from errors — Giúp nhận ra, chẩn đoán và khôi phục lỗi

Thông báo lỗi phải nói rõ vấn đề và cách sửa.

**Ví dụ:** “Mật khẩu phải có ít nhất 8 ký tự” tốt hơn “Invalid input”.

### 10. Help and documentation — Trợ giúp và tài liệu

Dù giao diện nên dễ dùng, hệ thống vẫn cần help/documentation khi chức năng phức tạp.

**Ví dụ:** Tooltip, FAQ, hướng dẫn từng bước cho chức năng xuất báo cáo.

---

# Phần 5: Kỹ thuật & Công cụ Thiết kế

## 11. Xác định yêu cầu: Scenario và Use Case

## 11.1. Scenario là gì?

**Scenario (Kịch bản người dùng)** là câu chuyện mô tả cách một đối tượng người dùng cụ thể sử dụng sản phẩm để đạt được mục tiêu trong ngữ cảnh thực tế. Theo tài liệu, scenario:

- là câu chuyện tự sự mô tả hoạt động của con người;
- không nhất thiết nhắc trực tiếp đến công nghệ;
- dùng ngôn ngữ tự nhiên của người dùng;
- giúp khám phá yêu cầu và bối cảnh sử dụng.

### Mục đích của Scenario

1. Hiểu người dùng thật sự muốn làm gì.
2. Hiểu bối cảnh, động cơ, khó khăn và kỳ vọng.
3. Phát hiện yêu cầu chức năng và phi chức năng.
4. Làm nền tảng để viết use case và prototype.

### Ví dụ Scenario

> Lan muốn đặt lịch khám da liễu vì bị mẩn ngứa. Lan mở ứng dụng đặt lịch, đăng nhập, chọn chuyên khoa Da liễu, xem danh sách bác sĩ, chọn bác sĩ Mai vì có đánh giá tốt. Lan xem lịch làm việc, chọn thứ Năm tuần sau lúc 10 giờ, kiểm tra lại thông tin và bấm xác nhận. Sau đó Lan nhận thông báo xác nhận qua email và tin nhắn.

Từ scenario này có thể rút ra yêu cầu: đăng nhập, chọn chuyên khoa, xem bác sĩ, xem lịch, đặt lịch, xác nhận, gửi thông báo.

---

## 11.2. Use Case là gì?

**Use Case** là 1 thuật ngữ mô tả tương tác giữa người dùng/hệ thống ngoài với hệ thống để đạt một mục tiêu. Tài liệu nêu use case:

- mô tả sự tương tác giữa người và hệ thống;
- use case diagram trình bày yêu cầu chức năng;
- use case steps ghi lại đường đi từ đầu đến cuối, bao gồm cả thành công và thất bại;
- không mô tả chi tiết thiết kế giao diện;
- không mô tả chi tiết cài đặt;
- use case diagram không trình bày thứ tự hành động.

### Thành phần chính của Use Case Diagram

1. **Actor:** người dùng hoặc hệ thống khác tương tác với hệ thống.
2. **System boundary:** ranh giới hệ thống, xem hệ thống như “hộp đen”.
3. **Use case:** chức năng/mục tiêu mà hệ thống cung cấp.
4. **Association:** đường liên kết giữa actor và use case.
5. **Include/Use:** một use case luôn dùng use case khác.
6. **Extend:** use case mở rộng cho trường hợp cụ thể hơn hoặc tùy chọn.

### Ví dụ Use Case Steps

**Use case:** Đặt lịch hẹn khám bệnh  
**Actor:** Bệnh nhân  
**Mục tiêu:** Bệnh nhân đặt được lịch khám với bác sĩ.  
**Tiền điều kiện:** Bệnh nhân có tài khoản và đăng nhập được.  
**Hậu điều kiện:** Lịch hẹn được tạo và thông báo xác nhận được gửi.

**Luồng chính:**

1. Bệnh nhân đăng nhập vào hệ thống.
2. Hệ thống hiển thị màn hình đặt lịch.
3. Bệnh nhân chọn chuyên khoa.
4. Hệ thống hiển thị danh sách bác sĩ thuộc chuyên khoa.
5. Bệnh nhân chọn bác sĩ.
6. Hệ thống hiển thị lịch trống của bác sĩ.
7. Bệnh nhân chọn ngày và giờ khám.
8. Hệ thống hiển thị thông tin xác nhận.
9. Bệnh nhân bấm “Xác nhận”.
10. Hệ thống tạo lịch hẹn và gửi thông báo.

**Luồng thay thế A — Không còn lịch trống:**

A1. Hệ thống báo không còn lịch trống ở thời điểm đã chọn.  
A2. Hệ thống đề xuất thời điểm khác.  
A3. Quay lại bước 7.

**Luồng thay thế B — Người dùng chưa đăng nhập:**

B1. Hệ thống yêu cầu đăng nhập.  
B2. Sau khi đăng nhập thành công, quay lại màn hình đặt lịch.

---

## 12. Prototype là gì? Vì sao cần tạo prototype? So sánh low-fidelity và high-fidelity

### 12.1. Prototype là gì?

**Prototype** là bản trình bày thiết kế trước khi phiên bản cuối được triển khai. Prototype giúp khách hàng/người dùng nhìn thấy và tương tác với sản phẩm ở giai đoạn sớm.

### 12.2. Vì sao cần prototype?

1. **Phát hiện lỗi sớm**
2. **Thử nhiều ý tưởng rẻ**
3. **Thu phản hồi từ người dùng sớm** 
4. **So sánh phương án** 
5. **Làm rõ yêu cầu** 
6. **Giảm rủi ro code sai**

### 12.3. So sánh Low-fidelity và High-fidelity Prototype

| Tiêu chí | Low-fidelity Prototype | High-fidelity Prototype |
|---|---|---|
| Đặc điểm | Dùng phương tiện khác sản phẩm cuối: giấy, bìa, sketch, storyboard, flow diagram, Wizard of Oz | Gần giống sản phẩm cuối về look & feel, có tương tác và có thể dùng HTML, PowerPoint, Visual Basic, Flex... |
| Mục tiêu | Khám phá ý tưởng, luồng, navigation, yêu cầu | Kiểm tra tương tác chi tiết, cảm giác sử dụng, bố cục gần thật |
| Ưu điểm | Nhanh, rẻ, dễ sửa, dễ bỏ, tạo được nhiều phương án, trình bày sớm cho khách hàng | Thực tế hơn, kiểm tra được tương tác, phù hợp giai đoạn gần triển khai |
| Nhược điểm | Không mô phỏng tốt scrolling, key/mouse events, control thật, response time | Tốn thời gian hơn, dễ khiến nhóm ngại thay đổi vì đã đầu tư nhiều |
| Ví dụ | Vẽ màn hình quản lý liên hệ trên giấy; dùng giấy nhỏ làm popup xác nhận xóa | Prototype HTML của màn hình ERP trước khi code thật |

Kết luận: Nên bắt đầu bằng **low-fidelity** để thử ý tưởng nhanh, sau đó chuyển dần sang **high-fidelity** khi cần kiểm tra tương tác chi tiết.

---

## 13. Thiết kế Input/Output & Reports

## 13.1. Nguyên tắc thiết kế form nhập liệu

Theo tài liệu, input quyết định tính đúng đắn của hệ thống. Có hai loại input: real-time input dùng form/controls và batch input dùng để import lượng lớn dữ liệu có cấu trúc.

Nguyên tắc thiết kế form nhập liệu:

1. **Đơn giản và tự nhiên nhất có thể.**
2. **Khớp form với tài liệu nguồn thực tế.**  
3. **Chỉ nhập dữ liệu cần thiết.**  
4. **Có giá trị mặc định.**  
5. **Hiển thị danh sách giá trị cho trường chọn được.**  
6. **Tab order đúng.**  
7. **Nhãn trường rõ ràng.**
8. **Cung cấp ví dụ cho yêu cầu đặc biệt.**  
9. **Luôn cho phép thoát màn hình nhập mà không lưu.**
10. **Error prevention và data validation.**  

## 13.2. Nguyên tắc thiết kế output

Output có thể ra màn hình, in giấy, file hoặc kết quả tìm kiếm. Với output màn hình, grid/table control và data binding rất quan trọng.

Nguyên tắc:

1. Thông tin xuất ra phải đúng nhu cầu người dùng.
2. Dữ liệu phải rõ ràng, dễ đọc, có nhóm và thứ tự.
3. Kết quả tìm kiếm cần có tiêu đề cột, lọc/sắp xếp nếu cần.
4. Với bảng dữ liệu, cần chú ý căn lề, độ rộng cột, phân trang, trạng thái rỗng.
5. Output cần nhất quán với input và nghiệp vụ.

## 13.3. Nguyên tắc thiết kế report

1. **Dựa trên report hiện có** nếu người dùng đã quen.
2. **Được người dùng đánh giá càng sớm càng tốt.**
3. **Chú ý report header/footer và page header/footer.**
4. **Spacing quan trọng.**
5. **Nhóm thông tin hợp lý.**
6. **Thống nhất và nhất quán.**
7. **Phù hợp đầu ra.** 
8. **Hiển thị tổng, subtotal, ngày lập, người lập nếu nghiệp vụ cần.**

---

## 14. Controls/Widgets: nhóm cơ bản, chức năng và ví dụ

**Controls/Widgets** là các thành phần giao diện tái sử dụng, xử lý cả input và output, có event handling như callback/listener.

| Nhóm control | Chức năng chính | Ví dụ |
|---|---|---|
| Container | Chứa và tổ chức các control khác | Dialog/form modal, Panel, TabControl |
| Organize content | Sắp xếp, nhóm hoặc điều hướng nội dung | Scrollbar, Groupbox, Listbox, Combobox |
| Text input | Nhập và chỉnh sửa văn bản | Textbox, textarea, password field |
| Choices | Chọn một hoặc nhiều giá trị | Checkbox, Radio button, Toggle button |
| Commands | Kích hoạt hành động | Button, Menu, Toolbar, Hyperlink, Ribbon |
| Date/number/hierarchy | Nhập dữ liệu đặc thù hoặc hiển thị cấu trúc | DateTimePicker, Spinner/DomainUpDown, TreeView |
| Data display | Hiển thị dữ liệu dạng danh sách/bảng | DataGrid, Table |
| Custom/User control | Control tự xây dựng từ control chuẩn để có style/chức năng riêng | User-control nhập địa chỉ Việt Nam, custom grid, custom search box |

### Lưu ý khi chọn control

1. Chọn control phù hợp với kiểu dữ liệu.
2. Ưu tiên control phòng lỗi: DatePicker tốt hơn nhập ngày tự do.
3. Dùng nhãn rõ ràng, tab order đúng, trạng thái disabled/active dễ hiểu.
4. Không lạm dụng control phức tạp nếu nghiệp vụ đơn giản.
5. Với người dùng chuyên nghiệp, có thể thêm shortcut hoặc toolbar để tăng efficiency.

---

## 15. Thiết kế màn hình và nguyên tắc “đúng trước, tiện lợi sau”

### 15.1. Các yếu tố cần cân nhắc khi thiết kế màn hình

Theo tài liệu, kết quả thiết kế màn hình nên gồm:

- danh sách màn hình;
- screen map;
- main screen/menu screen;
- chi tiết từng màn hình.

Khi sắp xếp bố cục, cần cân nhắc:

1. **Mục tiêu nhiệm vụ của màn hình**  

2. **Menu và điều hướng**  
   Menu phải chứa đủ chức năng hệ thống.

3. **Vùng nhập liệu**  
   Nhóm trường liên quan, nhãn rõ, tab order đúng, có default value, validation.

4. **Vùng hiển thị dữ liệu**  
   Bảng/list cần tiêu đề cột, căn lề, nhóm dữ liệu, phân trang hoặc cuộn hợp lý.

5. **Vùng lệnh/hành động**  
   Nút chính phải nổi bật; nút nguy hiểm cần cảnh báo; hành động phụ không nên cạnh tranh với hành động chính.

6. **Feedback và trạng thái**  
   Hiển thị loading, lỗi, thành công, trạng thái rỗng, trạng thái disabled.

7. **Khoảng cách, màu sắc, typography**  
   Dùng spacing và border để nhóm; màu sắc phải dễ nhìn; chữ đủ đọc; không lạm dụng hiệu ứng.

8. **Tính nhất quán**  

9. **Đối tượng người dùng**  
   Người mới cần dễ học; người dùng không thường xuyên cần dễ nhớ; chuyên gia cần thao tác nhanh.

### 15.2. “Đúng trước, tiện lợi sau” nghĩa là gì?

Tài liệu nêu screen design cần **correctness first, then usability**. Nghĩa là khi thiết kế màn hình, trước hết phải đảm bảo giao diện **đúng nghiệp vụ, đúng dữ liệu, đúng luồng, đúng ràng buộc và đúng chức năng**. Sau đó mới tối ưu tiện lợi, đẹp, nhanh, ít bước.

Ví dụ: form đặt lịch khám trước hết phải đảm bảo không cho đặt vào giờ bác sĩ không làm việc, không trùng lịch, dữ liệu bệnh nhân đúng. Sau khi đúng nghiệp vụ, mới tối ưu số bước, layout đẹp, autocomplete, phím tắt.

---

# Phần 6: Đánh giá (Evaluation)

## 17. Đánh giá giao diện: mục đích, formative/summative, quy trình và DECIDE

### 17.1. Mục đích của đánh giá giao diện

Usability evaluation có hai mục tiêu chính:

1. **Cung cấp phản hồi trong quá trình thiết kế để tạo thiết kế tốt hơn.**
2. **Đánh giá mức độ usable của sản phẩm.**

### 17.2. Formative Evaluation và Summative Evaluation

| Loại đánh giá | Mục đích | Thời điểm | Câu hỏi chính |
|---|---|---|---|
| Formative Evaluation | Tìm cách cải tiến thiết kế | Trong quá trình thiết kế/phát triển | “Cần redesign cái gì và redesign như thế nào?” |
| Summative Evaluation | Đánh giá kết quả cuối | Sau khi sản phẩm/prototype đã tương đối hoàn chỉnh | “Chúng ta đã làm tốt đến mức nào?” |

Formative thiên về sửa thiết kế; summative thiên về kết luận chất lượng.

### 17.3. Các bước trong quy trình đánh giá

Tài liệu nêu 4 pha:

1. **Planning – Training:** chuẩn bị đánh giá, xác định mục tiêu, người tham gia, công cụ, kịch bản, người đánh giá.
2. **Conducting:** tiến hành đánh giá, quan sát, ghi nhận dữ liệu.
3. **Summarizing:** tổng hợp kết quả, phân loại vấn đề, tính toán số liệu.
4. **Debriefing:** trình bày và sử dụng kết quả để redesign hoặc ra quyết định.

### 17.4. Khung DECIDE

DECIDE là khung lập kế hoạch đánh giá gồm:

1. **Determine overall goals — Xác định mục tiêu tổng quát**  

2. **Explore specific questions — Xây dựng câu hỏi cụ thể**  

3. **Choose evaluation methods — Chọn phương pháp đánh giá**  

4. **Identify practical issues — Xác định vấn đề thực tế**  

5. **Decide ethical issues — Xử lý vấn đề đạo đức**  

6. **Evaluate the data — Đánh giá dữ liệu**  

---

## 18. Phương pháp đánh giá: Heuristic Evaluation, Lab-based Testing, Questionnaires

## 18.1. Heuristic Evaluation

**Heuristic Evaluation** là phương pháp đánh giá giao diện dựa trên các quy tắc/heuristics. Phương pháp này không cần người dùng và thường có 3–5 evaluator làm việc độc lập trên UI.

### Các bước tiến hành

1. **Xác định phạm vi giao diện cần đánh giá.**
2. **Chọn bộ heuristics:** ví dụ Nielsen’s 10 Heuristics.
3. **Chọn 3–5 evaluator.**
4. **Mỗi evaluator đánh giá độc lập:** đi qua màn hình/luồng thao tác, ghi lỗi.
5. **Ghi nhận mỗi vấn đề:** heuristic bị vi phạm, vị trí, mô tả, severity, fixability, đề xuất sửa.
6. **Tổng hợp kết quả:** gộp vấn đề trùng, phân loại theo severity.
7. **Ưu tiên sửa lỗi và redesign.**

### Ưu điểm

- Nhanh và rẻ.
- Không cần tuyển người dùng thật.
- Phát hiện sớm nhiều lỗi rõ ràng về consistency, feedback, error prevention.
- Phù hợp giai đoạn prototype hoặc trước khi usability test.

### Nhược điểm

- Có thể bỏ sót chi tiết sử dụng thực tế.
- Phụ thuộc chuyên môn evaluator.
- Không phản ánh đầy đủ hành vi, cảm xúc, bối cảnh thật của người dùng.
- Có thể phát hiện vấn đề “lý thuyết” nhưng chưa chắc là vấn đề lớn trong thực tế.

---

## 18.2. Lab-based Usability Testing

**Lab-based Usability Testing** là phương pháp thực nghiệm trong đó người dùng thật thực hiện các nhiệm vụ trong môi trường kiểm soát, còn nhóm đánh giá quan sát, ghi nhận và phân tích.

### Cách tiến hành

1. **Xác định mục tiêu test.**  

2. **Chọn participant đại diện.**  

3. **Chuẩn bị kịch bản/nhiệm vụ.**  

4. **Chuẩn bị môi trường lab.**  

5. **Giới thiệu và xin sự đồng ý của người tham gia.**  

6. **Cho người dùng thực hiện nhiệm vụ.**  

7. **Thu dữ liệu.**  

8. **Phỏng vấn/bảng hỏi sau test.**

9. **Phân tích và báo cáo vấn đề usability.**

### Ưu điểm

- Dựa trên hành vi sử dụng thật.
- Phát hiện vấn đề mà evaluator có thể không nghĩ ra.
- Thu được cả dữ liệu định lượng và định tính.
- Tốt để kiểm tra task flow, form, navigation, hiểu nhãn/icon.

### Nhược điểm

- Tốn thời gian và chi phí hơn heuristic evaluation.
- Participant có thể không đại diện đủ cho toàn bộ người dùng.
- Môi trường lab có thể khác môi trường sử dụng thật.
- Người dùng có thể hành xử khác khi bị quan sát.

---

## 18.3. Lưu ý khi dùng Questionnaires

**Questionnaires** (bảng câu hỏi khảo sát) là công cụ thu thập phản hồi chủ quan từ người dùng.

Theo tài liệu, khi thiết kế bảng hỏi cần:

1. **Câu hỏi rõ ràng và đơn giản.**
2. **Tránh câu hỏi phức tạp.**
3. **Thứ tự câu hỏi quan trọng.**
4. **Cẩn thận với thang đo** 
5. **Tránh thuật ngữ chuyên môn khó hiểu.**
6. **Tránh câu hỏi chủ quan/dẫn dắt.**
7. **Cung cấp hướng dẫn rõ.**
8. **Không hỏi kiểu gây thiên lệch.**  
9. **Không dùng điều kiện chuyển câu quá phức tạp.**
10. **Tránh khoảng tuổi bị overlap.**
11. **Chừa đủ chỗ cho câu trả lời mở.**
12. **Kết hợp câu hỏi chung và câu hỏi theo scenario.**  

---

## 19. Phân tích kết quả đánh giá và ưu tiên vấn đề usability theo severity

 Phản ứng đúng là: **làm thế nào redesign UI để giải quyết vấn đề usability này?** Dữ liệu và người dùng cần được xem là căn cứ để cải tiến.

### 19.1. Xác định vấn đề usability

Có thể phân loại vấn đề thành:

1. **Learning issues:** người dùng không hiểu, không thấy hoặc không biết có chức năng.  

2. **Performance issues:** người dùng làm được nhưng quá lâu, mệt, nhiều bước.  

3. **Subjective issues:** người dùng thấy khó chịu, xấu, bực bội.  

### 19.2. Đánh giá severity/importance

Tài liệu gợi ý thang **Importance 1–5**, dựa trên tác động lên nhiệm vụ và tần suất xảy ra:

- **5 = Critical:** tác động lớn, xảy ra thường xuyên, có thể làm người dùng không hoàn thành nhiệm vụ.
- **3 = Medium:** người dùng hoàn thành được nhưng khó khăn.
- **1 = Minor:** lỗi nhỏ, ít xảy ra, chỉ gây vấp nhẹ.

Có thể ghi thêm:

- vị trí lỗi;
- heuristic bị vi phạm;
- mô tả;
- severity;
- fixability;
- đề xuất sửa.

### 19.3. Ưu tiên sửa theo tỷ lệ Importance/Cost

Tài liệu gợi ý dùng:

```text
Ratio = Importance (hoặc gọi là severity) / Cost
```

Sau đó sắp xếp từ cao xuống thấp.

- **Must fix:** severity cao, chi phí sửa thấp hoặc vừa.
- **Next version:** quan trọng nhưng chi phí cao hoặc chưa ảnh hưởng nghiêm trọng.
- **Ignored:** vấn đề nhỏ, hiếm, chi phí sửa không đáng.

### 19.4. Ví dụ

**Vấn đề:** Người dùng không biết có thể zoom.  
**Severity:** 3 hoặc 4 tùy nhiệm vụ.  
**Giải pháp tốt:** đổi icon zoom rõ hơn, thêm tooltip, thêm zoom slider.  
**Không nên chỉ làm:** viết thêm tài liệu hướng dẫn dài, vì có thể giải quyết trực tiếp bằng UI.

---

# Phần 7: Chủ đề Mở rộng

## 20. Thiết kế giao diện mobile so với desktop: khác biệt và yếu tố cần cân nhắc

Thiết kế mobile và desktop đều phải đảm bảo usability.

| Yếu tố | Mobile | Desktop |
|---|---|---|
| Kích thước màn hình | Nhỏ, cần ưu tiên nội dung chính, tránh quá nhiều cột | Rộng hơn, có thể hiển thị nhiều vùng |
| Input | Chạm, gesture, bàn phím ảo, giọng nói | Chuột, bàn phím vật lý, hover, phím tắt |
| Độ chính xác | Ngón tay kém chính xác hơn chuột | Chuột chính xác hơn |
| Bối cảnh dùng | Di chuyển, bị gián đoạn, mạng không ổn định | Thường ổn định hơn, phiên làm việc dài |
| Navigation | Bottom nav, tab, hamburger, swipe | Sidebar, top menu, ribbon, context menu |
| Hiển thị dữ liệu | Tránh bảng lớn, dùng card/list | Bảng dữ liệu lớn, multi-pane |
| Hiệu năng | Cần chú ý pin, mạng, tài nguyên | Thường tài nguyên mạnh hơn |
| Feedback | Phải rõ vì không có hover; cần trạng thái chạm | Có thể dùng hover, tooltip, cursor |
| Accessibility | Kích thước tap target, one-hand use | Keyboard navigation, screen reader, zoom, shortcut |

### Các yếu tố cần cân nhắc khi thiết kế mobile

1. **Ưu tiên nhiệm vụ chính.**  

2. **Tap target đủ lớn.**  

3. **Giảm nhập liệu.**  

4. **Thiết kế theo ngữ cảnh bị gián đoạn.**  

5. **Phản hồi rõ ràng.**  

6. **Tối ưu performance và offline/poor network.**

7. **Tuân theo platform conventions.**  

---

## 21. Ưu nhược điểm của các kiểu tương tác phổ biến trên web

## 21.1. Menu điều hướng

**Ưu điểm:**

- Giúp người dùng nhận biết chức năng thay vì phải nhớ.
- Tổ chức hệ thống theo nhóm.
- Hỗ trợ memorability nếu menu nhất quán.
- Phù hợp với website nhiều trang/chức năng.

**Nhược điểm:**

- Menu quá sâu làm khó tìm.
- Tên menu mơ hồ gây hiểu sai.
- Nếu nhóm theo tư duy kỹ thuật thay vì nghiệp vụ, người dùng khó hiểu.

**Thiết kế tốt:** nhóm menu theo nhiệm vụ/nghiệp vụ, nhãn ngắn, nhất quán, có trạng thái active.

---

## 21.2. Form

**Ưu điểm:**

- Thu thập dữ liệu có cấu trúc.
- Phù hợp với nhập hồ sơ, đăng ký, đặt lịch, thanh toán.
- Có thể validation, default value, danh sách lựa chọn để phòng lỗi.

**Nhược điểm:**

- Form dài làm tăng cognitive load (tải nhận thức, là lượng thông tin hoặc khối lượng công việc mà não bộ của bạn phải xử lý cùng một lúc).
- Nhãn không rõ làm người dùng nhập sai.
- Validation muộn gây bực bội.
- Trường bắt buộc quá nhiều làm giảm satisfaction.

**Thiết kế tốt:** chỉ hỏi dữ liệu cần thiết, nhóm trường, tab order đúng, nhãn rõ, ví dụ định dạng, validation ngay tại trường.

---

## 21.3. Tìm kiếm

**Ưu điểm:**

- Rất hiệu quả khi người dùng biết họ cần gì.
- Phù hợp với hệ thống nhiều dữ liệu.

**Nhược điểm:**

- Phụ thuộc từ khóa người dùng nhập.
- Nếu ranking kém, người dùng không tìm được dù dữ liệu có tồn tại.
- Không phù hợp khi người dùng chưa biết thuật ngữ.
- Trạng thái “không có kết quả” nếu không gợi ý sẽ gây bế tắc.

**Thiết kế tốt:** hỗ trợ gợi ý, sửa lỗi chính tả, filter, highlight từ khóa, thông báo không kết quả có hướng xử lý.

---

## 21.4. Filter và Sort

**Ưu điểm:**

- Giúp thu hẹp dữ liệu lớn.
- Tăng efficiency cho danh sách/bảng.
- Hỗ trợ người dùng khám phá dữ liệu.

**Nhược điểm:**

- Quá nhiều bộ lọc làm giao diện rối.
- Người dùng có thể quên filter đang bật.
- Kết hợp filter phức tạp có thể tạo kết quả rỗng.

**Thiết kế tốt:** hiển thị filter đang bật, có nút clear, nhóm filter hợp lý, dùng default thông minh.

---

## 21.5. Button, link và CTA

**Ưu điểm:**

- Kích hoạt hành động trực tiếp.
- CTA rõ giúp người dùng biết bước tiếp theo.
- Button tốt tạo affordance rõ.

**Nhược điểm:**

- Quá nhiều button chính làm người dùng phân vân.
- Link giả button hoặc button giả link gây nhầm.
- Nút nguy hiểm đặt gần nút chính có thể gây lỗi.

**Thiết kế tốt:** phân cấp primary/secondary/destructive rõ, có feedback, nhãn hành động cụ thể như “Lưu thay đổi” thay vì “OK”.

---

## 22. Khi nào nên ưu tiên Application UI thay vì Web UI?

Ở đây có thể hiểu **Application UI** là giao diện ứng dụng cài đặt/native trên desktop hoặc mobile, còn **Web UI** là giao diện chạy qua trình duyệt.

Nên ưu tiên Application UI khi dịch vụ có các đặc điểm sau:

### 1. Cần hiệu năng cao hoặc xử lý nặng

Ví dụ: chỉnh sửa video, CAD, IDE, phần mềm đồ họa, phân tích dữ liệu lớn. 

### 2. Cần làm việc offline hoặc mạng không ổn định

Ví dụ: ứng dụng ghi chú, quản lý kho tại hiện trường, ứng dụng y tế ở khu vực mạng yếu. App có thể lưu dữ liệu cục bộ và đồng bộ sau.

### 3. Cần truy cập sâu vào phần cứng/hệ điều hành

Ví dụ: camera, GPS, Bluetooth, file system, clipboard nâng cao, thiết bị ngoại vi, cảm biến.

### 4. Tác vụ thường xuyên, dài và phức tạp

Nếu người dùng dùng hàng ngày trong phiên dài, cần phím tắt, multi-window, thao tác nhanh, custom control.

### 5. Cần trải nghiệm nhất quán với nền tảng (app mobile/desktop)

### 6. Cần bảo mật hoặc kiểm soát dữ liệu cục bộ đặc biệt

### 7. Cần tích hợp sâu với workflow chuyên nghiệp

Ví dụ: phần mềm kế toán, quản lý bệnh viện, POS, phần mềm dựng phim, IDE.

### Khi nào Web UI phù hợp hơn?

Web UI nên ưu tiên khi:

- cần truy cập nhanh, không muốn cài đặt;
- người dùng đa nền tảng;
- dịch vụ chủ yếu là nội dung, tra cứu, mua hàng, form đơn giản;
- cần cập nhật liên tục từ server;
- người dùng không thường xuyên;
- mục tiêu là truy cập rộng và triển khai nhanh.

Kết luận: Application UI phù hợp với **tác vụ nặng, thường xuyên, cần offline, cần truy cập sâu vào phần cứng/hệ điều hành và workflow phức tạp**. Web UI phù hợp với **khả năng truy cập rộng, triển khai nhanh, ít cài đặt và sử dụng không quá chuyên sâu**.
