# BÁO CÁO BÀI TẬP LỚN

## KIỂM THỬ PHẦN MỀM – HỆ THỐNG WEBSITE MUA BÁN MÃ NGUỒN DEVMARTVN

## THÔNG TIN NHÓM

- Môn học: Kiểm thử phần mềm
- Đề tài: Kiểm thử hệ thống Website Mua Bán Mã Nguồn DevMartVN
- Nhóm: …
- Thành viên:
  - … – MSSV …
  - … – MSSV …
- Giảng viên hướng dẫn: …
- Học kỳ: … – Năm học: …

---

## LỜI MỞ ĐẦU

Sự phát triển mạnh mẽ của công nghệ thông tin dẫn đến nhu cầu học tập, chia sẻ và tái sử dụng mã nguồn ngày càng lớn. Thay vì mỗi cá nhân tự phát triển từ đầu, lập trình viên có thể mua hoặc tham khảo các source code có sẵn để tiết kiệm thời gian và chi phí. Website DevMartVN được xây dựng với mục tiêu trở thành một chợ trực tuyến cho mã nguồn, nơi người bán có thể đăng sản phẩm và người mua có thể tìm kiếm, thanh toán và tải về.

Trong bối cảnh đó, chất lượng phần mềm đóng vai trò quyết định tới trải nghiệm người dùng và mức độ tin tưởng với nền tảng. Kiểm thử phần mềm giúp phát hiện sớm lỗi, hạn chế rủi ro trong quá trình vận hành. Báo cáo này trình bày toàn bộ quá trình nhóm thực hiện kiểm thử hệ thống DevMartVN: từ phân tích yêu cầu, lập kế hoạch, thiết kế test case, thực thi test cho đến đánh giá kết quả và đề xuất cải tiến. Thông qua bài tập lớn, nhóm mong muốn củng cố kiến thức lý thuyết, rèn luyện kỹ năng thực hành và nâng cao nhận thức về vai trò của kiểm thử trong phát triển phần mềm.

---

## CHƯƠNG 1. GIỚI THIỆU HỆ THỐNG

### 1.1. Bối cảnh và bài toán

DevMartVN là một website thương mại điện tử chuyên về mua bán mã nguồn. Mỗi sản phẩm là một gói source code đi kèm mô tả, hình ảnh, thông tin người bán và giá bán. Người dùng có thể tra cứu mã nguồn theo danh mục hoặc từ khóa, nạp tiền vào tài khoản, thực hiện giao dịch mua, sau đó tải về mã nguồn bất cứ lúc nào.

Bài toán đặt ra là phải đảm bảo các luồng nghiệp vụ chính của hệ thống hoạt động trơn tru: người dùng đăng ký và đăng nhập được, sản phẩm hiển thị đúng, việc nạp và rút tiền chính xác, giao dịch mua bán ghi nhận đầy đủ, đồng thời admin có thể theo dõi và quản trị dễ dàng thông qua hệ thống quản trị.

### 1.2. Mục tiêu của đề tài

Mục tiêu của đề tài là xây dựng và áp dụng một quy trình kiểm thử hoàn chỉnh cho hệ thống DevMartVN. Cụ thể:

- Phân tích yêu cầu chức năng và phi chức năng của hệ thống.
- Thiết kế bộ test case cho 15 màn hình chính bao phủ các luồng nghiệp vụ cốt lõi.
- Thực thi test case trên giao diện thật của hệ thống, ghi nhận kết quả và lỗi.
- Đánh giá mức độ đáp ứng yêu cầu của hệ thống, rút ra nhận xét và kinh nghiệm cho việc kiểm thử các dự án sau.

### 1.3. Đối tượng và phạm vi nghiên cứu

Đối tượng nghiên cứu là hệ thống DevMartVN dưới góc độ người dùng cuối và admin. Phạm vi kiểm thử tập trung vào:

- Chức năng và giao diện của các màn hình: đăng ký, đăng nhập, trang chủ, quản lý thông tin, nạp tiền, rút tiền, mua hàng, shop người bán và các màn quản trị.
- Tính đúng đắn của dữ liệu hiển thị và cập nhật: thông tin sản phẩm, số dư tài khoản, lịch sử giao dịch.
- Không đi sâu vào kiểm thử hiệu năng, bảo mật chuyên sâu hay tích hợp với hệ thống ngân hàng thực tế.

### 1.4. Kết cấu báo cáo

Báo cáo gồm các phần chính:

- Chương 1 trình bày bối cảnh, mục tiêu và phạm vi của đề tài kiểm thử.
- Chương 2 phân tích yêu cầu, mô tả chức năng và mô hình use case của hệ thống.
- Chương 3 xây dựng kế hoạch và chiến lược kiểm thử.
- Chương 4 mô tả chi tiết thiết kế test và cấu trúc test case.
- Chương 5 trình bày quá trình thực thi test và kết quả thu được.
- Chương 6 đưa ra kết luận và hướng phát triển.
- Phần cuối cùng liệt kê các tài liệu tham khảo và phụ lục test case, screenshot, bug list.

---

## CHƯƠNG 2. PHÂN TÍCH YÊU CẦU VÀ MÔ HÌNH HỆ THỐNG

### 2.1. Yêu cầu chức năng

Hệ thống DevMartVN được tổ chức thành các nhóm chức năng:

1. **Nhóm tài khoản người dùng**

   - Đăng ký tài khoản mới với các thông tin: họ tên, email, mật khẩu, số điện thoại.
   - Đăng nhập bằng email hoặc tên đăng nhập và mật khẩu; hỗ trợ đăng nhập qua bên thứ ba (Google, GitHub).
   - Cập nhật thông tin cá nhân và thông tin ngân hàng nhận tiền.
   - Đổi mật khẩu đăng nhập.

2. **Nhóm giao dịch của người dùng**

   - Nạp tiền vào tài khoản DevMartVN bằng cách chọn mệnh giá hoặc nhập số tiền, sử dụng mã QR thanh toán.
   - Yêu cầu rút tiền từ số dư khả dụng về tài khoản ngân hàng đã cấu hình.
   - Xem lịch sử nạp tiền, rút tiền và các giao dịch mua bán.

3. **Nhóm sản phẩm và shop**

   - Tìm kiếm sản phẩm theo từ khóa, danh mục, bộ lọc.
   - Xem chi tiết sản phẩm, giá bán, mô tả và thông tin người bán.
   - Đăng bán sản phẩm mới: nhập thông tin, giá, mô tả, upload thumbnail, link tải, link demo.
   - Xem trang shop của người bán với danh sách sản phẩm họ cung cấp.
   - Xem lịch sử các sản phẩm đã mua và tải lại source code.

4. **Nhóm quản trị hệ thống**
   - Xem dashboard thống kê tổng doanh thu, tổng số người dùng, số sản phẩm, số đơn hàng.
   - Quản lý danh sách người dùng: xem thông tin, phân quyền, khóa/mở khóa tài khoản.
   - Quản lý sản phẩm: duyệt, ẩn/hiện, xóa sản phẩm vi phạm.
   - Quản lý danh mục: thêm, sửa, xóa danh mục sản phẩm.
   - Quản lý đơn hàng: theo dõi tình trạng thanh toán, xem chi tiết từng đơn.
   - Quản lý yêu cầu rút tiền: duyệt hoặc từ chối yêu cầu, cập nhật số dư tương ứng.
   - Theo dõi biến động số dư hệ thống: log các giao dịch nạp, rút, mua, bán, hoàn tiền.

### 2.2. Yêu cầu phi chức năng

Ngoài các chức năng trên, hệ thống còn có những yêu cầu phi chức năng:

- **Tính dễ sử dụng:** Giao diện đơn giản, các nút chức năng rõ ràng, thống nhất về màu sắc và bố cục giữa các màn hình front-end và admin.
- **Tính chính xác dữ liệu:** Số dư ví, số tiền nạp/rút, giá sản phẩm, trạng thái giao dịch phải được tính toán và hiển thị chính xác.
- **Tính an toàn:** Mật khẩu không được hiển thị dạng chữ thường, các thông tin nhạy cảm không xuất hiện trong URL, phân quyền truy cập giữa user và admin.
- **Tính ổn định:** Hệ thống không bị lỗi khi nhập dữ liệu lớn trong giới hạn cho phép, không bị văng trang khi thao tác liên tục.
- **Khả năng mở rộng:** Cấu trúc chức năng cho phép bổ sung thêm danh mục, phương thức thanh toán hoặc loại sản phẩm mới mà không phải thay đổi quá nhiều thành phần.

### 2.3. Mô hình ca sử dụng (Use Case)

Dựa trên yêu cầu, có thể xác định các ca sử dụng tiêu biểu:

- **UC01 – Đăng ký tài khoản:** Người dùng cung cấp thông tin cá nhân và tạo tài khoản mới.
- **UC02 – Đăng nhập:** Người dùng nhập email/tên đăng nhập và mật khẩu để truy cập hệ thống.
- **UC03 – Quản lý thông tin cá nhân:** Người dùng xem và chỉnh sửa hồ sơ, thông tin ngân hàng.
- **UC04 – Nạp tiền:** Người dùng thực hiện nạp tiền vào tài khoản ví DevMartVN.
- **UC05 – Rút tiền:** Người dùng yêu cầu rút tiền về tài khoản ngân hàng.
- **UC06 – Đăng bán sản phẩm:** Người bán đăng thông tin sản phẩm, upload file, gửi yêu cầu duyệt.
- **UC07 – Mua sản phẩm:** Người mua chọn sản phẩm, thanh toán và tải source code.
- **UC08 – Quản lý giao dịch mua:** Người dùng xem lịch sử mua hàng và tải lại file.
- **UC09 – Quản lý yêu cầu rút tiền (Admin):** Admin xem danh sách yêu cầu, duyệt hoặc từ chối.
- **UC10 – Quản lý người dùng, sản phẩm, danh mục (Admin):** Admin tìm kiếm, chỉnh sửa hoặc khóa/xóa tài khoản và sản phẩm.

Trong bản báo cáo Word, bạn có thể vẽ thêm sơ đồ use case tổng quan với các tác nhân: User, Seller, Admin và gắn các ca sử dụng trên vào sơ đồ để minh họa.

### 3.1. Mục tiêu kế hoạch kiểm thử (tiếp)

- Đảm bảo các luồng giao dịch liên quan đến tiền (nạp, rút, mua, bán, hoàn tiền) phản ánh đúng số dư trước và sau giao dịch.
- Xác nhận các màn hình quản trị (dashboard, quản lý người dùng, sản phẩm, đơn hàng, yêu cầu rút tiền, biến động số dư) hiển thị đúng dữ liệu tổng hợp.
- Xây dựng được bộ test case có thể tái sử dụng để kiểm thử hồi quy khi hệ thống được nâng cấp.

### 3.2. Phạm vi và giới hạn kiểm thử

**Phạm vi kiểm thử:**

- Toàn bộ 15 màn hình: DMRegister, DMLogin, DMHomePage, DMProfile, DMOrderHistory, DMShopSeller, DMRecharge, DMWithdraw, DMDashboard, DMProducts, DMUsers, DMCategories, DMWithdrawRequest, DMOrder, DMBalance.
- Các luồng nghiệp vụ chính:
  - Người dùng: đăng ký, đăng nhập, cập nhật hồ sơ, nạp tiền, rút tiền, đăng bán, mua hàng, xem lịch sử.
  - Admin: đăng nhập admin, theo dõi dashboard, duyệt sản phẩm, duyệt yêu cầu rút tiền, quản lý người dùng và danh mục.
- Kiểm tra validate: bắt buộc nhập, độ dài tối thiểu/tối đa, định dạng email, định dạng số điện thoại, phạm vi số tiền.

**Giới hạn kiểm thử:**

- Không đo đạc hiệu năng dưới tải nặng (load test, stress test).
- Không thực hiện kiểm thử bảo mật chuyên sâu như tấn công SQL Injection, XSS, CSRF.
- Không kiểm thử trên nhiều trình duyệt và thiết bị di động; chỉ tập trung trên Chrome desktop.
- Không kiểm thử tích hợp trực tiếp với hệ thống ngân hàng ngoài môi trường giả lập.

### 3.3. Chiến lược và phương pháp kiểm thử

- **Chiến lược tổng thể:**  
  Áp dụng kiểm thử hộp đen ở mức hệ thống (system test) dựa trên đặc tả yêu cầu và giao diện thực tế. Với các luồng quan trọng, thực hiện thêm kiểm thử hồi quy mỗi khi có sửa đổi.

- **Phương pháp thiết kế test:**

  - Phân vùng tương đương (Equivalence Partitioning): chia dữ liệu đầu vào thành các lớp hợp lệ và không hợp lệ, ví dụ như email đúng/sai định dạng, số tiền trong/ngoài phạm vi.
  - Phân tích giá trị biên (Boundary Value Analysis): tập trung kiểm tra các giá trị cận trên/cận dưới, ví dụ nhập đúng bằng min, nhỏ hơn min 1 đơn vị, lớn hơn max 1 đơn vị.
  - Bảng quyết định (Decision Table): áp dụng cho các nghiệp vụ phụ thuộc nhiều điều kiện, ví dụ: trạng thái yêu cầu rút tiền (Đang chờ, Đã duyệt, Đã từ chối) phụ thuộc vào hành động của admin.

- **Loại kiểm thử áp dụng:**
  - Kiểm thử chức năng (Functional Testing).
  - Kiểm thử giao diện người dùng (UI Testing) ở mức hiển thị, vị trí và nội dung.
  - Kiểm thử hồi quy thủ công đối với các luồng giao dịch chính.

### 3.4. Môi trường, dữ liệu và công cụ kiểm thử

- **Môi trường:**

  - Máy chủ ứng dụng chạy bản Dev/Stage của DevMartVN.
  - Hệ điều hành: Windows 10/11.
  - Trình duyệt: Google Chrome phiên bản mới nhất.

- **Dữ liệu kiểm thử:**

  - Tài khoản người dùng:
    - User A: tài khoản người mua.
    - User B: tài khoản người bán.
  - Tài khoản admin với đầy đủ quyền quản trị.
  - Một số sản phẩm mẫu thuộc các danh mục khác nhau.
  - Dữ liệu giao dịch demo: nạp tiền, rút tiền, đơn hàng mua/bán trước đó.

- **Công cụ hỗ trợ:**
  - Bảng tính hoặc công cụ quản lý test để lưu trữ test case và kết quả.
  - Công cụ chụp màn hình để minh họa bug.
  - (Nếu có) công cụ kiểm thử API hoặc framework test tự động để hỗ trợ regression.

### 3.5. Lịch trình và phân công

- Tuần 1–2: Phân tích đề bài, đọc tài liệu đặc tả, xác định danh sách màn hình và use case.
- Tuần 3–4: Thiết kế test case chi tiết cho từng màn hình, rà soát trong nhóm và chỉnh sửa.
- Tuần 5–6: Thực thi test trên hệ thống thật, ghi nhận kết quả và bug, trao đổi với nhóm phát triển.
- Tuần 7: Thực hiện re-test bug đã sửa, cập nhật trạng thái test và hoàn thiện báo cáo.

Phân công được chia theo từng nhóm chức năng, ví dụ: một thành viên phụ trách frontend người dùng, một thành viên phụ trách các module admin và giao dịch, một thành viên tổng hợp báo cáo và tài liệu.

---

## CHƯƠNG 4. THIẾT KẾ TEST (TEST DESIGN)

### 4.1. Danh sách màn hình và số lượng test case

Bảng dưới đây liệt kê các màn hình chính và số lượng test case tương ứng (số liệu cụ thể điền theo file test chi tiết của nhóm):

| STT | Mã màn hình       | Tên màn hình                  | Loại     | Số test case |
| --- | ----------------- | ----------------------------- | -------- | ------------ |
| 1   | DMRegister        | Đăng ký tài khoản             | Frontend | …            |
| 2   | DMLogin           | Đăng nhập                     | Frontend | …            |
| 3   | DMHomePage        | Trang chủ                     | Frontend | …            |
| 4   | DMProfile         | Thông tin cá nhân & ngân hàng | Frontend | …            |
| 5   | DMOrderHistory    | Lịch sử mua hàng              | Frontend | …            |
| 6   | DMShopSeller      | Shop người bán                | Frontend | …            |
| 7   | DMRecharge        | Nạp tiền                      | Frontend | …            |
| 8   | DMWithdraw        | Rút tiền                      | Frontend | …            |
| 9   | DMDashboard       | Thống kê tổng quan            | Admin    | …            |
| 10  | DMProducts        | Quản lý sản phẩm              | Admin    | …            |
| 11  | DMUsers           | Quản lý người dùng            | Admin    | …            |
| 12  | DMCategories      | Quản lý danh mục              | Admin    | …            |
| 13  | DMWithdrawRequest | Quản lý yêu cầu rút tiền      | Admin    | …            |
| 14  | DMOrder           | Quản lý đơn hàng              | Admin    | …            |
| 15  | DMBalance         | Quản lý biến động số dư       | Admin    | …            |

### 4.2. Mẫu biểu test case sử dụng

Để thống nhất, tất cả test case được thiết kế theo mẫu sau:

- ID test case
- Tên test case / Mục tiêu
- Màn hình / Chức năng
- Tiền điều kiện (Pre-condition)
- Bước thực hiện (Steps)
- Dữ liệu đầu vào (Input data)
- Kết quả mong đợi (Expected result)
- Mức ưu tiên (Priority: High/Medium/Low)
- Kết quả thực tế (Actual result: Pass/Fail) – điền khi thực thi

Mẫu biểu này giúp các thành viên dễ hiểu, dễ trao đổi và dễ cập nhật khi có thay đổi yêu cầu.

### 4.3. Một số test case tiêu biểu

#### 4.3.1. Chức năng Đăng ký (DMRegister)

- **Mục tiêu:** đảm bảo hệ thống chỉ cho phép tạo tài khoản mới khi toàn bộ thông tin hợp lệ.
- **Nhóm test chính:**
  - Bắt buộc nhập các trường: Họ tên, Email, Mật khẩu, Xác nhận mật khẩu, Số điện thoại.
  - Kiểm tra định dạng email, số điện thoại, độ dài mật khẩu.
  - Kiểm tra trùng lặp email và số điện thoại.
  - Kiểm tra sự khớp giữa mật khẩu và xác nhận mật khẩu.
  - Kiểm tra đăng ký thành công và có thể đăng nhập bằng tài khoản mới.

#### 4.3.2. Chức năng Nạp tiền (DMRecharge)

- **Mục tiêu:** đảm bảo số tiền nạp hợp lệ và lịch sử nạp được ghi nhận chính xác.
- **Nhóm test chính:**
  - Chọn các mệnh giá nạp nhanh (50k, 100k, 200k, 500k, 1M, 2M).
  - Nhập số tiền nhỏ hơn mức tối thiểu → hiển thị thông báo lỗi.
  - Nhập số tiền vượt quá giới hạn cho phép → hiển thị thông báo lỗi.
  - Nhập số tiền hợp lệ → hệ thống tạo mã QR với số tiền tương ứng.
  - Sau khi nạp thành công, lịch sử nạp tiền hiển thị đúng số tiền và trạng thái.

(Các nhóm test còn lại cho đăng nhập, rút tiền, mua hàng, admin… được chi tiết trong phụ lục test case.)

---

## CHƯƠNG 5. THỰC THI TEST VÀ KẾT QUẢ

### 5.1. Quy trình thực thi

Quá trình thực thi test được thực hiện theo các bước:

1. Chuẩn bị môi trường và dữ liệu test (tài khoản, sản phẩm, số dư ví).
2. Thực thi từng test case theo thứ tự ưu tiên: ưu tiên các luồng chính và các nghiệp vụ liên quan đến tiền.
3. Ghi nhận kết quả thực tế (Pass/Fail) và mô tả ngắn nếu có lỗi.
4. Chụp màn hình minh họa cho các lỗi quan trọng hoặc khó tái hiện.
5. Sau khi lỗi được sửa, tiến hành re-test và cập nhật trạng thái bug.

### 5.2. Kết quả tổng hợp

Bảng tổng hợp dưới đây là khung để điền số liệu sau khi chạy test:

| Nhóm chức năng                        | Số test case | Pass | Fail | Tỉ lệ Pass | Nhận xét ngắn |
| ------------------------------------- | ------------ | ---- | ---- | ---------- | ------------- |
| Tài khoản (Đăng ký, Đăng nhập, Hồ sơ) |              |      |      |            |               |
| Giao dịch (Nạp, Rút, Mua hàng)        |              |      |      |            |               |
| Sản phẩm & Shop                       |              |      |      |            |               |
| Admin (Dashboard, Users, Products…)   |              |      |      |            |               |
| **Tổng cộng**                         |              |      |      |            |               |

### 5.3. Một số lỗi tiêu biểu (ví dụ nội dung)

- **BUG-01 – Nạp tiền không cảnh báo số tiền dưới mức tối thiểu**

  - Màn hình: DMRecharge
  - Mô tả: Khi nhập số tiền 10.000 VND (thấp hơn hạn mức tối thiểu), hệ thống vẫn tạo yêu cầu nạp mà không hiển thị cảnh báo.
  - Tác động: Người dùng có thể hiểu nhầm là yêu cầu đã được chấp nhận, gây sai lệch trong quá trình xử lý.
  - Đề xuất: Thêm kiểm tra phía server và client, hiển thị thông báo rõ ràng “Số tiền nạp tối thiểu là … VND”.

- **BUG-02 – Cho phép rút tiền vượt quá số dư khả dụng**

  - Màn hình: DMWithdraw
  - Mô tả: Số dư khả dụng 100.000 VND nhưng người dùng vẫn có thể nhập 200.000 VND và gửi yêu cầu rút.
  - Tác động: Nếu admin không kiểm tra kỹ có thể chấp nhận nhầm yêu cầu, dẫn tới âm số dư.
  - Đề xuất: Áp dụng kiểm tra ràng buộc số tiền rút ≤ số dư khả dụng, hiển thị thông báo phù hợp.

- **BUG-03 – Trạng thái đơn hàng không cập nhật sau khi thanh toán**
  - Màn hình: DMOrder / DMOrderHistory
  - Mô tả: Sau khi người dùng hoàn tất thanh toán, trạng thái đơn hàng vẫn hiển thị “Đang xử lý” thay vì “Hoàn thành”.
  - Tác động: Người dùng khó theo dõi chính xác giao dịch, có thể tưởng thanh toán chưa thành công.
  - Đề xuất: Đồng bộ trạng thái đơn hàng sau khi nhận thông báo thành công từ cổng thanh toán.

(Nhóm điền các bug thực tế của mình vào phần này.)

### 5.4. Đánh giá chung

Qua quá trình thực thi test:

- Các luồng chức năng chính của hệ thống hoạt động tương đối ổn định, đáp ứng được yêu cầu bài toán.
- Những lỗi được phát hiện chủ yếu liên quan đến:
  - Thiếu hoặc chưa đầy đủ thông báo lỗi cho dữ liệu không hợp lệ.
  - Thiếu kiểm tra ràng buộc ở một số trường hợp biên.
  - Một vài chỗ hiển thị trạng thái chưa đồng nhất giữa màn hình người dùng và màn hình admin.
- Sau khi các lỗi này được ghi nhận và sửa chữa, hệ thống đạt mức chất lượng chấp nhận được cho việc triển khai thử nghiệm.

---

## CHƯƠNG 6. KẾT LUẬN VÀ HƯỚNG PHÁT TRIỂN

### 6.1. Kết luận

Bài tập lớn đã giúp nhóm trải nghiệm đầy đủ các bước trong quy trình kiểm thử phần mềm cho một hệ thống web thực tế:

- Từ tài liệu yêu cầu và giao diện, nhóm đã phân tích và xác định được 15 màn hình chức năng cần kiểm thử.
- Dựa trên đó, nhóm thiết kế bộ test case bao phủ các luồng nghiệp vụ quan trọng, áp dụng các kỹ thuật phân vùng tương đương và giá trị biên.
- Quá trình thực thi test đã phát hiện được một số lỗi liên quan đến kiểm tra dữ liệu và xử lý trạng thái, góp phần hoàn thiện hơn hệ thống DevMartVN.

Kết quả kiểm thử cho thấy hệ thống cơ bản đáp ứng đúng yêu cầu đề bài, có thể sử dụng được trong phạm vi bài tập lớn và tiếp tục phát triển thêm trong tương lai.

### 6.2. Hướng phát triển

Trong tương lai, việc kiểm thử DevMartVN có thể được mở rộng theo các hướng:

- Tự động hóa một số luồng kiểm thử lặp lại nhiều lần (đăng nhập, nạp tiền, rút tiền, mua hàng) bằng các công cụ automation.
- Thực hiện kiểm thử hiệu năng và khả năng chịu tải để đánh giá hệ thống khi có nhiều người dùng đồng thời.
- Bổ sung kiểm thử bảo mật chuyên sâu, kiểm tra các lỗ hổng phổ biến trên ứng dụng web.
- Mở rộng kiểm thử sang các nền tảng và trình duyệt khác nhau, đặc biệt là trên thiết bị di động.
- Chuẩn hóa tài liệu kiểm thử theo các bộ tiêu chuẩn quốc tế để dễ dàng chuyển giao và bảo trì.

---

## TÀI LIỆU THAM KHẢO

1. Đề bài môn Kiểm thử phần mềm – “Mã đề thi 33 – Hệ thống Website Mua Bán Mã Nguồn DevMartVN”, Bộ môn Công nghệ phần mềm, Trường ….
2. Tài liệu đặc tả và thiết kế kiểm thử “KIEM-THU-WEBSITE-MUA-BAN-MA-NGUON-DEVMARTVN.COM”, Nhóm …, năm ….
3. Giáo trình Kiểm thử phần mềm, Khoa …, Trường ….
4. G. J. Myers, C. Sandler, T. Badgett, _The Art of Software Testing_, 3rd Edition, Wiley, 2011.
5. ISO/IEC/IEEE 29119, _Software and systems engineering – Software testing_, 2013.
6. Các bài viết và tài liệu trực tuyến về kỹ thuật thiết kế test case, kiểm thử web và công cụ hỗ trợ kiểm thử.

---

## PHỤ LỤC

- **Phụ lục A:** Toàn bộ test case chi tiết cho 15 màn hình (sao chép từ file test .md/Excel của nhóm).
- **Phụ lục B:** Ảnh chụp màn hình giao diện các chức năng chính (Frontend và Admin).
- **Phụ lục C:** Danh sách bug chi tiết và trạng thái xử lý (Open / Fixed / Re-test Pass).
