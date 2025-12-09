# BÁO CÁO KIỂM THỬ PHẦN MỀM

## HỆ THỐNG WEBSITE MUA BÁN MÃ NGUỒN DEVMARTVN

---

## CHƯƠNG 1: TỔNG QUAN BÀI TOÁN

### 1.1. Giới thiệu đề tài

Đề tài của nhóm em là **“Kiểm thử hệ thống Website Mua Bán Mã Nguồn DevMartVN”** – một nền tảng giao dịch source code trực tuyến cho cộng đồng lập trình viên. Thông qua website, người dùng có thể đăng bán sản phẩm là mã nguồn, tìm kiếm và mua source code, nạp tiền, rút tiền và quản lý các giao dịch liên quan. [1]

Yêu cầu, đặc tả ban đầu của hệ thống được lấy từ tài liệu đề bài môn Kiểm thử phần mềm và file phân tích thiết kế “Website Mua Bán Mã Nguồn DevMartVN”, trong đó mô tả chi tiết các chức năng: đăng ký, đăng nhập, trang chủ, quản lý hồ sơ, nạp/rút tiền, đăng bán sản phẩm, shop người bán và các module quản trị của admin (dashboard, quản lý người dùng, sản phẩm, danh mục, đơn hàng, yêu cầu rút tiền, biến động số dư). [1][2]

Bài toán cần giải quyết là đảm bảo hệ thống DevMartVN vận hành đúng yêu cầu, đặc biệt ở các luồng nghiệp vụ liên quan đến giao dịch tài chính (nạp, rút, mua, bán), đồng thời cung cấp giao diện thân thiện, rõ ràng cho cả người dùng cuối (buyer/seller) và quản trị viên (admin). Thông qua hoạt động kiểm thử, nhóm em đánh giá mức độ hoàn thiện của hệ thống, phát hiện sớm lỗi và đề xuất điều chỉnh phù hợp.

---

### 1.2. Đặc tả yêu cầu

#### 1.2.1. Các luồng nghiệp vụ chính

Dựa trên tài liệu yêu cầu và các test case được thiết kế trong file TEST_CASE.MD, nhóm em xác định các luồng nghiệp vụ end‑to‑end (E2E) quan trọng như sau: [2][3]

1. **Luồng Đăng ký – Đăng nhập – Vào hệ thống**

   - Người dùng truy cập trang chủ, chọn chức năng “Đăng ký”.
   - Nhập họ tên, email, mật khẩu, xác nhận mật khẩu, số điện thoại; hệ thống kiểm tra định dạng email, độ dài mật khẩu, tính duy nhất của email/số điện thoại.
   - Đăng ký thành công, hệ thống lưu thông tin user và cho phép đăng nhập.
   - Người dùng đăng nhập bằng email hoặc tên đăng nhập và mật khẩu; nếu đúng, hệ thống chuyển đến trang chủ và hiển thị avatar, số dư. [3]

2. **Luồng Cập nhật thông tin cá nhân và ngân hàng**

   - Sau khi đăng nhập, người dùng truy cập màn “Thông tin cá nhân”.
   - Hệ thống hiển thị sẵn họ tên, tên đăng nhập, email, số điện thoại và các trường ngân hàng, số tài khoản, chủ tài khoản.
   - Người dùng chỉnh sửa số điện thoại hoặc thông tin ngân hàng, nhấn “Lưu thay đổi”; hệ thống validate dữ liệu (chỉ số, không để trống, độ dài hợp lệ) và cập nhật thành công. [3]

3. **Luồng Nạp tiền ví DevMartVN**

   - Người dùng vào màn “Nạp tiền”, xem số dư hiện tại.
   - Chọn 1 mệnh giá nhanh (50k, 100k, 200k, 500k, 1M, 2M) hoặc nhập số tiền khác thỏa điều kiện min/max.
   - Hệ thống sinh mã QR VietQR chứa thông tin tài khoản nhận, số tiền và nội dung chuyển khoản.
   - Sau khi người dùng chuyển khoản thành công và bấm “Xác nhận đã chuyển khoản”, hệ thống tạo record yêu cầu nạp tiền, cập nhật lịch sử nạp và chờ admin hoặc hệ thống cổng thanh toán xác nhận. [3]

4. **Luồng Rút tiền về ngân hàng**

   - Người dùng truy cập màn “Rút tiền”, xem số dư khả dụng.
   - Chọn mệnh giá hoặc nhập số tiền rút (không nhỏ hơn min, không lớn hơn số dư).
   - Nhấn “Tạo yêu cầu rút”; hệ thống ghi nhận yêu cầu với trạng thái “Đang xử lý/Đang chờ” và hiển thị trong lịch sử rút tiền.
   - Admin đăng nhập màn “Yêu cầu rút tiền” để duyệt hoặc từ chối, đồng thời cập nhật số dư và trạng thái giao dịch. [3]

5. **Luồng Đăng bán sản phẩm và duyệt sản phẩm**

   - Người bán đăng nhập, vào màn “Đăng bán sản phẩm”.
   - Nhập thông tin tên sản phẩm, danh mục, giá bán (có thể để 0 để tạo sản phẩm miễn phí), mô tả chi tiết, link tải, link demo và upload ảnh thumbnail đúng định dạng.
   - Nhấn “Gửi yêu cầu duyệt”; hệ thống lưu sản phẩm với trạng thái “Chờ duyệt”.
   - Admin truy cập màn “Quản lý sản phẩm” để xem danh sách, duyệt hoặc từ chối sản phẩm; các sản phẩm đã duyệt sẽ hiển thị trên trang chủ và shop người bán. [3]

6. **Luồng Mua sản phẩm và tải lại source code**

   - Người mua duyệt danh sách sản phẩm ở trang chủ, dùng thanh tìm kiếm hoặc menu danh mục.
   - Chọn một sản phẩm, xem chi tiết, xác nhận mua và thanh toán bằng số dư trong ví.
   - Sau khi thanh toán thành công, hệ thống:
     - Ghi log đơn hàng, cập nhật lịch sử mua hàng của user.
     - Trừ số dư của người mua, cộng số dư cho người bán (hoặc ghi nhận doanh thu chờ rút).
   - Người mua có thể vào màn “Lịch sử mua hàng” để xem lại các giao dịch và tải lại source khi cần. [3]

7. **Luồng Quản trị hệ thống (Admin)**
   - Admin đăng nhập vào trang quản trị, truy cập Dashboard để xem các chỉ số tổng quan: tổng doanh thu, số người dùng, số sản phẩm, đơn hàng mới, đồ thị doanh thu.
   - Sử dụng các màn quản lý người dùng, sản phẩm, danh mục, đơn hàng, yêu cầu rút tiền, lịch sử biến động số dư để:
     - Tìm kiếm, lọc, sắp xếp theo điều kiện.
     - Xem chi tiết, sửa, xóa hoặc duyệt đối tượng tương ứng.
   - Các hành động của admin phản ánh lên dữ liệu hiển thị ở frontend và đảm bảo tính nhất quán. [2][3]

Trong báo cáo Word, nhóm em có thể biểu diễn lại các luồng này dưới dạng sơ đồ hoạt động (activity diagram) hoặc flowchart cho từng luồng chính.

#### 1.2.2. Các màn hình chức năng chính

Dựa trên bản thiết kế giao diện (wireframe và screenshot) và file TEST_CASE.MD, nhóm em xác định các màn hình chính sau: [2][3]

- **Đăng nhập (dangnhap.jpg)**

  - Trường: Email/Tên đăng nhập, Mật khẩu, Ghi nhớ đăng nhập; nút Đăng nhập; liên kết Quên mật khẩu, Đăng ký; nút đăng nhập Google, GitHub.
  - Ràng buộc:
    - Email/Username: bắt buộc, độ dài 1–255, định dạng email nếu là email.
    - Mật khẩu: bắt buộc, độ dài 8–128, hiển thị dạng ẩn.
  - Hành vi:
    - Bỏ trống hoặc sai định dạng → hiển thị thông báo lỗi.
    - Nhập đúng email/mật khẩu → chuyển sang Trang chủ.

- **Đăng ký (Dang-ki.jpg)**

  - Trường: Họ và tên, Email, Mật khẩu, Xác nhận mật khẩu, Số điện thoại; nút Đăng ký.
  - Ràng buộc:
    - Họ và tên: bắt buộc, độ dài tối đa 255.
    - Email: bắt buộc, định dạng đúng, duy nhất trong hệ thống.
    - Mật khẩu: bắt buộc, dài tối thiểu 8 ký tự, thoả chính sách mật khẩu.
    - Xác nhận mật khẩu: bắt buộc, trùng mật khẩu.
    - Số điện thoại: bắt buộc, chỉ chứa số, độ dài 9–12, duy nhất.

- **Trang chủ (Trang-chu.jpg)**

  - Thành phần: Header (logo, tìm kiếm, menu danh mục, nút Đăng bán, Đăng nhập/Avatar), banner khuyến mãi, block “Top lượt xem”, block “Ưu đãi đặc biệt”, danh sách sản phẩm dạng card, footer.
  - Mỗi card sản phẩm: ảnh, tên, giá, badge “Miễn phí” nếu giá = 0, thông tin lượt xem/lượt mua.
  - Hành vi:
    - Tìm kiếm bằng từ khóa → load danh sách sản phẩm khớp.
    - Chọn danh mục → filter sản phẩm theo danh mục.
    - Click card → chuyển sang chi tiết sản phẩm.

- **Thông tin cá nhân (Thong-tin-ca-nhan.jpg)**

  - Thành phần:
    - Khối thông tin tài khoản: họ tên, tên đăng nhập (read‑only), email (read‑only), số điện thoại.
    - Khối thông tin ngân hàng: ngân hàng nhận tiền (select), số tài khoản, chủ tài khoản.
    - Nút “Lưu thay đổi”.
  - Ràng buộc:
    - Số điện thoại: không chứa ký tự chữ, độ dài hợp lệ.
    - Ngân hàng, số tài khoản, chủ tài khoản: bắt buộc nhập nếu muốn rút tiền.

- **Nạp tiền (Nap-tien.jpg / Nap-Tien.jpg)**

  - Thành phần: hiển thị số dư hiện tại, các button mệnh giá, ô nhập số tiền khác, QR VietQR, nút “Xác nhận đã chuyển khoản”, bảng lịch sử nạp.
  - Ràng buộc:
    - Số tiền nạp tối thiểu (ví dụ 50.000 VND), tối đa tuỳ cấu hình hệ thống.
    - Chỉ cho phép nhập số nguyên dương.

- **Rút tiền (Rut-tien.jpg)**

  - Thành phần: số dư khả dụng, các button mệnh giá, ô nhập số tiền rút, nút “Tạo yêu cầu rút tiền”, lịch sử rút.
  - Ràng buộc:
    - Số tiền rút ≥ min, ≤ số dư khả dụng, ≤ hạn mức tối đa.

- **Lịch sử biến động số dư (Lich-su-bien-dong-so-du.jpg – Admin)**

  - Thành phần: thanh tab filter (Tất cả/Nạp tiền/Rút tiền/Mua/Bán/Hoàn tiền), bảng danh sách với các cột: Người dùng, Số tiền, Số dư sau, Nội dung, Thời gian; phân trang.
  - Ràng buộc:
    - Số tiền dương (màu xanh, dấu +) cho giao dịch cộng; âm (màu đỏ, dấu –) cho giao dịch trừ.

- **Lịch sử mua hàng (Lich-su-mua-hang.jpg – User)**

  - Thành phần: danh sách giao dịch đã mua với thông tin: mã giao dịch, tên sản phẩm, thời gian, giá, nút Xem chi tiết, nút Tải xuống.

- **Shop của tôi (Shop-cua-toi.jpg – Seller)**

  - Thành phần: thông tin seller (avatar, tên, ngày tham gia), danh sách sản phẩm của seller, nút Theo dõi, Nhắn tin (nếu có).

- **Đăng bán sản phẩm (Dang-ban-san-pham.jpg)**

  - Trường: tên sản phẩm, danh mục, giá bán, mô tả chi tiết (editor), link tải nguồn, link demo (tuỳ chọn), ảnh thumbnail, nút Gửi yêu cầu duyệt.
  - Ràng buộc:
    - Thumbnail định dạng JPG/PNG, kích thước/tải trọng trong giới hạn.
    - Nếu giá rỗng hoặc 0 → sản phẩm miễn phí.

- **Các màn hình admin (Thong-ke-tong-quan.jpg, Quan-ly-nguoi-dung.jpg, Quan-ly-danh-muc.jpg, Quan-ly-san-pham.jpg, Quan-ly-don-hang.jpg, Yeu-cau-rut-tien.jpg)**
  - Cấu trúc chung: sidebar menu, ô tìm kiếm, bảng danh sách, các nút thao tác (Sửa/Xóa/Chi tiết/Duyệt/Từ chối).
  - Dữ liệu bảng: ID, thông tin chính (tên user, tên sản phẩm, số tiền…), trạng thái. [2][3]

#### 1.2.3. Các module chính của chương trình

Từ góc nhìn kiểm thử, nhóm em chia hệ thống thành các module chính như sau: [2][3]

1. **Module Quản lý tài khoản**

   - **Input:**
     - Thông tin đăng ký: họ tên, email, mật khẩu, xác nhận mật khẩu, số điện thoại.
     - Thông tin đăng nhập: email/tên đăng nhập, mật khẩu.
     - Thông tin cập nhật hồ sơ: họ tên, số điện thoại, thông tin ngân hàng.
   - **Xử lý:**
     - Kiểm tra dữ liệu đầu vào (bắt buộc, định dạng, độ dài).
     - Lưu user mới, mã hóa mật khẩu, kiểm tra trùng lặp email/số điện thoại.
     - Xác thực thông tin đăng nhập, thiết lập phiên làm việc (session).
     - Cập nhật hồ sơ và thông tin ngân hàng.
   - **Output:**
     - Thông báo đăng ký/đăng nhập thành công hoặc lỗi.
     - Hồ sơ người dùng được cập nhật và hiển thị trong các màn hình liên quan.

2. **Module Quản lý ví và giao dịch tiền**

   - **Input:**
     - Thông tin nạp tiền: số tiền, nội dung chuyển khoản, xác nhận đã chuyển.
     - Thông tin rút tiền: số tiền rút, thông tin ngân hàng user, action duyệt/từ chối của admin.
   - **Xử lý:**
     - Sinh mã QR với tham số phù hợp.
     - Tạo bản ghi yêu cầu nạp/rút với trạng thái ban đầu “Đang chờ”.
     - Khi được xác nhận, cập nhật số dư ví, cập nhật lịch sử biến động số dư và trạng thái yêu cầu.
   - **Output:**
     - Số dư ví mới của user.
     - Bảng lịch sử nạp/rút và biến động số dư phản ánh đúng các giao dịch.

3. **Module Quản lý sản phẩm và shop**

   - **Input:**
     - Thông tin sản phẩm: tên, danh mục, giá, mô tả, link tải, link demo, ảnh thumbnail.
     - Action của admin: duyệt, ẩn, xóa sản phẩm.
   - **Xử lý:**
     - Validate dữ liệu sản phẩm (bắt buộc, định dạng link, file upload).
     - Lưu sản phẩm với trạng thái “Chờ duyệt” hoặc “Đã duyệt”.
     - Filter, tìm kiếm theo danh mục, từ khóa.
   - **Output:**
     - Danh sách sản phẩm hiển thị ở trang chủ và shop người bán.
     - Trạng thái sản phẩm trong màn hình admin.

4. **Module Quản lý đơn hàng và lịch sử mua**

   - **Input:**
     - Yêu cầu mua sản phẩm: user, sản phẩm, số tiền.
   - **Xử lý:**
     - Kiểm tra số dư ví của người mua.
     - Tạo đơn hàng, cập nhật lịch sử mua hàng.
     - Trừ số dư người mua, cộng số dư (hoặc doanh thu) cho người bán.
   - **Output:**
     - Đơn hàng với trạng thái “Hoàn thành” hoặc “Thất bại”.
     - Bản ghi trong lịch sử mua hàng cho người dùng và lịch sử đơn hàng trong admin.

5. **Module Quản trị (Admin)**
   - **Input:**
     - Dữ liệu từ các module khác (user, sản phẩm, đơn hàng, yêu cầu rút tiền, giao dịch số dư).
     - Các thao tác quản trị của admin: duyệt, từ chối, sửa, xóa, thay đổi trạng thái.
   - **Xử lý:**
     - Tổng hợp số liệu cho dashboard (doanh thu, số user, số sản phẩm, đơn hàng mới).
     - Áp dụng quy tắc nghiệp vụ: duyệt rút tiền, duyệt sản phẩm, khóa user,…
   - **Output:**
     - Bảng thống kê và báo cáo trên dashboard.
     - Trạng thái cập nhật của user, sản phẩm, đơn hàng, yêu cầu rút tiền, biến động số dư.

---

## CHƯƠNG 2: PHÂN TÍCH VÀ THIẾT KẾ TEST

### 2.1. Unit Test Case

#### 2.1.1. Phương pháp, kỹ thuật

Ở mức Unit, nhóm em tập trung vào các hàm xử lý riêng lẻ (ví dụ: hàm validate email, validate mật khẩu, tính toán số dư sau giao dịch). Các kỹ thuật áp dụng: [4][5]

- **Equivalence Partitioning (EP):**  
  Chia không gian đầu vào thành các lớp tương đương (hợp lệ và không hợp lệ) để giảm số lượng test cần thiết nhưng vẫn bao phủ được logic, ví dụ:

  - Email hợp lệ / email sai định dạng / email rỗng.
  - Số tiền nạp nằm trong khoảng hợp lệ / nhỏ hơn min / lớn hơn max.

- **Boundary Value Analysis (BVA):**  
  Tập trung test tại các giá trị biên, ví dụ:

  - Mật khẩu độ dài 7, 8, 9 và 127, 128, 129 ký tự.
  - Số tiền nạp 49.999, 50.000, 50.001 nếu min = 50.000.

- **Decision Table / Logic Based Testing:**  
  Áp dụng cho các hàm xác định trạng thái, chẳng hạn như:
  - Xác định trạng thái yêu cầu rút tiền dựa vào hành động của admin (duyệt, từ chối, chờ).

Việc thiết kế unit test có thể thực hiện trong code thông qua các framework như JUnit/TestNG (Java) hoặc tương đương tuỳ ngôn ngữ. [4]

#### 2.1.2. Danh sách các test case (khung)

Do báo cáo tập trung nhiều hơn vào System/UI test, phần Unit test chỉ trình bày một số ví dụ đại diện, chẳng hạn:

- Hàm `validateEmail(email)`:

  - TC1: email rỗng → trả về lỗi “bắt buộc nhập”.
  - TC2: email không chứa ký tự `@` → trả về lỗi “sai định dạng”.
  - TC3: email đúng định dạng → trả về “hợp lệ”.

- Hàm `validateAmount(amount)` dùng cho nạp/rút:

  - TC1: amount < min → trả về lỗi “dưới mức tối thiểu”.
  - TC2: min ≤ amount ≤ max → “hợp lệ”.
  - TC3: amount > max → trả về lỗi “vượt quá tối đa”.

- Hàm `updateBalanceOnWithdraw(balance, amount)`:
  - TC1: amount > balance → ném lỗi “không đủ số dư”.
  - TC2: amount ≤ balance → trả về `balance - amount`.

Các test case này có thể triển khai bằng JUnit với cấu trúc: Arrange (chuẩn bị input), Act (gọi hàm), Assert (so sánh kết quả với mong đợi). [4][5]

---

### 2.2. Integration Test Case

#### 2.2.1. Phương pháp, kỹ thuật

Kiểm thử tích hợp nhằm đánh giá sự tương tác giữa các module: tài khoản – ví – giao dịch – sản phẩm – đơn hàng – admin. Nhóm em áp dụng: [4][5]

- **Incremental Integration Testing** với hướng **top‑down**:

  - Bắt đầu từ các màn hình/luồng nghiệp vụ ở mức cao (E2E user flow), dần dần mở rộng sang nhiều module liên quan.
  - Ví dụ tích hợp module Đăng nhập với Trang chủ, sau đó với Nạp tiền, Rút tiền, Mua hàng,…

- Một số trường hợp có thể xem như **Big Bang** integration (tích hợp nhiều module sẵn có) khi hệ thống đã được triển khai gần như đầy đủ; nhóm em tập trung vào luồng dữ liệu qua nhiều module hơn là test riêng từng interface.

#### 2.2.2. Danh sách các test case tích hợp (khung)

Một số Integration test tiêu biểu:

- **ITC-01 – Đăng ký → Đăng nhập → Vào Trang chủ**

  - Mục tiêu: kiểm tra liên kết giữa module đăng ký và đăng nhập, đảm bảo user mới tạo có thể đăng nhập ngay.
  - Module: DMRegister, DMLogin, DMHomePage.
  - Dữ liệu: thông tin tài khoản mới.
  - Kết quả mong đợi: đăng ký thành công → đăng nhập → load đúng avatar và số dư mặc định.

- **ITC-02 – Nạp tiền → Cập nhật số dư → Lịch sử nạp**

  - Module: DMRecharge, module ví, DMBalance/Lịch sử biến động.
  - Bước: tạo yêu cầu nạp tiền bằng mệnh giá nhanh, hệ thống confirm.
  - Kết quả mong đợi: số dư ví tăng đúng, lịch sử nạp và lịch sử biến động ghi nhận giao dịch.

- **ITC-03 – Mua sản phẩm → Tạo đơn hàng → Cập nhật số dư người mua/bán**

  - Module: DMHomePage/chi tiết sản phẩm, module đơn hàng, ví người mua, ví người bán, lịch sử mua hàng.
  - Kết quả mong đợi: đơn hàng trạng thái “Hoàn thành”, số dư buyer giảm, seller tăng (hoặc doanh thu ghi nhận), lịch sử mua hiển thị giao dịch mới.

- **ITC-04 – Rút tiền → Yêu cầu rút tiền admin → Cập nhật số dư**
  - Module: DMWithdraw, DMWithdrawRequest (admin), DMBalance.
  - Kết quả mong đợi: tạo yêu cầu rút trạng thái “Đang chờ”, sau khi admin duyệt → số dư giảm, lịch sử biến động cập nhật, trạng thái đổi sang “Đã duyệt”.

---

### 2.3. System Test Case

#### 2.3.1. Phương pháp, kỹ thuật

Kiểm thử hệ thống được thực hiện dưới góc nhìn người dùng cuối (end user), nhằm đánh giá toàn diện hệ thống dựa trên yêu cầu đã đặc tả. Nhóm em tập trung chủ yếu vào: [4][5]

- **Kiểm thử chức năng (Functional System Test):**

  - Thực thi các test case UI/UX chi tiết trong TEST_CASE.MD cho 15 màn hình.
  - Bảo đảm tất cả yêu cầu chức năng đều có ít nhất một test case.

- **Kiểm thử phi chức năng cơ bản:**

  - UI/UX: bố cục, nhãn, thông báo lỗi dễ hiểu, thống nhất.
  - Tính ổn định trên trình duyệt Chrome (không crash, không lỗi script hiển thị).

- **Kỹ thuật sử dụng:**
  - Kiểm thử hộp đen (black‑box) dựa trên đặc tả.
  - Kiểm thử theo kịch bản người dùng (scenario‑based testing): mô phỏng các tình huống sử dụng điển hình (mua hàng, nạp tiền, rút tiền,…).

#### 2.3.2. Danh sách test case hệ thống

Danh sách System test case chính là toàn bộ bộ test trong `TEST_CASE.MD` mà nhóm em đã thiết kế, bao gồm: [3]

- Test case Đăng nhập: TC‑LOGIN‑01 → TC‑LOGIN‑08.
- Test case Đăng ký: TC‑REG‑01 → TC‑REG‑07.
- Test case Trang chủ: TC‑HOME‑01 → TC‑HOME‑06.
- Test case Thông tin cá nhân & ngân hàng: TC‑PROFILE‑01 → TC‑PROFILE‑05.
- Test case Nạp tiền: TC‑DEPOSIT‑01 → TC‑DEPOSIT‑05.
- Test case Rút tiền: TC‑WITH‑01 → TC‑WITH‑04.
- Test case Lịch sử biến động số dư (Admin): TC‑BAL‑01 → TC‑BAL‑03.
- Test case Lịch sử mua hàng: TC‑ORDHIS‑01 → TC‑ORDHIS‑03.
- Test case Shop của tôi: TC‑SHOP‑01 → TC‑SHOP‑02.
- Test case Đăng bán sản phẩm: TC‑PROD‑01 → TC‑PROD‑04.
- Test case Admin (Dashboard, Users, Categories, Products, Orders, Withdraw Requests): TC‑ADM‑… (đã liệt kê tập trung trong mục 11 của TEST_CASE.MD).

Các test case này bao trùm hầu hết yêu cầu chức năng đã nêu ở Chương 1.

---

## CHƯƠNG 3: THỰC THI TEST VÀ BÁO CÁO KẾT QUẢ TEST

### 3.1. Kết quả thực hiện Integration Test

Trong phạm vi bài tập lớn, nhóm em thực thi các Integration test tiêu biểu (ITC‑01 đến ITC‑04). Kết quả tổng hợp (minh hoạ):

| ID     | Mô tả luồng tích hợp                             | Kết quả | Ghi chú ngắn                           |
| ------ | ------------------------------------------------ | ------- | -------------------------------------- |
| ITC-01 | Đăng ký → Đăng nhập → Trang chủ                  | Pass    | User mới đăng ký đăng nhập bình thường |
| ITC-02 | Nạp tiền → Cập nhật số dư → Lịch sử nạp          | Pass    | Số dư và lịch sử khớp với số tiền nạp  |
| ITC-03 | Mua sản phẩm → Tạo đơn hàng → Cập nhật số dư     | Fail    | Phát hiện lỗi BUG‑03 về trạng thái đơn |
| ITC-04 | Rút tiền → Yêu cầu rút → Duyệt rút → Cập nhật ví | Fail    | Phát hiện lỗi BUG‑02 về vượt số dư     |

**Danh sách lỗi tích hợp tiêu biểu:**

- **BUG‑02 – Cho phép tạo yêu cầu rút vượt quá số dư khả dụng**

  - Luồng: ITC‑04 (Rút tiền + Yêu cầu rút tiền admin).
  - Mô tả tái hiện:
    1. Đăng nhập bằng tài khoản có số dư 100.000 VND.
    2. Vào màn Rút tiền, nhập 200.000 VND, nhấn “Tạo yêu cầu rút tiền”.
    3. Hệ thống vẫn cho tạo yêu cầu và hiển thị trong lịch sử rút.
  - Kỳ vọng: hệ thống phải chặn và hiển thị thông báo “Không đủ số dư để rút”.
  - Severity: High – liên quan đến tiền.
  - Status: Open (chưa sửa) / hoặc Fixed (nếu đã xác nhận sửa trong dev).

- **BUG‑03 – Trạng thái đơn hàng không đổi sang “Hoàn thành” sau khi thanh toán**
  - Luồng: ITC‑03 (Mua sản phẩm).
  - Mô tả tái hiện:
    1. User có đủ số dư, mua 1 sản phẩm bất kỳ.
    2. Sau bước thanh toán, số dư đã trừ đúng.
    3. Vào Lịch sử mua hàng và màn Quản lý đơn hàng (Admin) → trạng thái vẫn là “Đang xử lý”.
  - Kỳ vọng: trạng thái phải chuyển sang “Hoàn thành” khi thanh toán thành công.
  - Severity: Medium–High (ảnh hưởng trải nghiệm và đối soát).
  - Status: Open/Fixed tuỳ thời điểm nhóm test.

### 3.2. Kết quả thực hiện System Test

System test được chạy trên toàn bộ bộ test case UI/UX. Nhóm em tổng hợp theo nhóm chức năng như sau (số liệu minh hoạ, nhóm có thể thay bằng số thực tế): [3]

| Nhóm chức năng                          | Số TC | Pass | Fail | Tỉ lệ Pass | Nhận xét                            |
| --------------------------------------- | ----- | ---- | ---- | ---------- | ----------------------------------- |
| Tài khoản (Đăng ký, Đăng nhập, Hồ sơ)   | 20    | 19   | 1    | 95%        | 1 bug nhỏ về thông báo lỗi hiển thị |
| Giao dịch (Nạp tiền, Rút tiền, Lịch sử) | 18    | 16   | 2    | 89%        | 2 bug liên quan ràng buộc số dư     |
| Sản phẩm & Shop                         | 15    | 14   | 1    | 93%        | 1 bug ở phần upload ảnh thumbnail   |
| Admin (Dashboard, Users, Products, …)   | 22    | 21   | 1    | 95%        | 1 bug về filter trạng thái đơn hàng |
| **Tổng cộng**                           | 75    | 70   | 5    | 93%        | Hệ thống tương đối ổn định          |

**Ví dụ một số lỗi system test:**

- **BUG‑01 – Thiếu thông báo khi nhập số tiền nạp dưới mức tối thiểu**

  - Màn: Nạp tiền.
  - Bước: nhập 10.000 VND trong khi min = 50.000 VND, nhấn xác nhận.
  - Thực tế: hệ thống không hiển thị lỗi rõ ràng.
  - Kỳ vọng: hiển thị cảnh báo cụ thể, không cho phép tạo yêu cầu.
  - Severity: Medium.

- **BUG‑04 – Cho phép upload thumbnail định dạng không được hỗ trợ**
  - Màn: Đăng bán sản phẩm.
  - Bước: chọn file `.pdf` làm ảnh thumbnail, nhấn submit.
  - Thực tế: hệ thống không báo lỗi rõ, vẫn nhận file.
  - Kỳ vọng: chỉ chấp nhận JPG/PNG, báo lỗi cho định dạng khác.
  - Severity: Medium.

Nhìn chung, sau khi ghi nhận bug, nhóm em đã phối hợp với phía phát triển để sửa các lỗi quan trọng, sau đó chạy lại (re‑test) và cập nhật trạng thái Pass cho các test case tương ứng.

---

## CHƯƠNG 4: AUTOMATION TEST

### 4.1. Công cụ sử dụng

Trong phạm vi bài tập lớn, nhóm em lựa chọn các công cụ automation sau: [4][5]

- **Selenium WebDriver + TestNG/JUnit (tuỳ ngôn ngữ):**

  - Dùng để tự động hoá một số kịch bản UI lặp lại như đăng nhập, đăng ký, nạp tiền với dữ liệu hợp lệ.
  - Lý do chọn:
    - Hỗ trợ tốt cho ứng dụng web, đa trình duyệt.
    - Cộng đồng lớn, tài liệu phong phú, dễ tra cứu.

- **Postman (tùy chọn, nếu sử dụng API test):**
  - Kiểm thử một số API backend (nếu tài liệu API sẵn có), ví dụ: login API, transaction API.
  - Hỗ trợ tạo collection và chạy tự động theo môi trường.

Môi trường automation:

- Hệ điều hành: Windows 10/11.
- Trình duyệt: Chrome + ChromeDriver tương ứng.
- Ngôn ngữ: Java/Python (tuỳ nhóm) cùng với Selenium + TestNG/JUnit. [4][5]

### 4.2. Kết quả đạt được

Nhóm em xây dựng một số script automation minh hoạ:

1. **Kịch bản “Đăng nhập hợp lệ”**

   - Mở trang login, nhập email và password hợp lệ, nhấn Đăng nhập.
   - Assert: URL chuyển sang trang chủ, header hiển thị tên user.

2. **Kịch bản “Đăng ký thành công”**

   - Tạo chuỗi email ngẫu nhiên chưa tồn tại, điền form đăng ký, nhấn Đăng ký.
   - Assert: hiển thị thông báo thành công hoặc chuyển sang trang Login.

3. **Kịch bản “Nạp tiền với mệnh giá nhanh”**
   - Đăng nhập, vào màn Nạp tiền, click mệnh giá 100.000 VND.
   - Assert: số tiền hiển thị đúng, mã QR được generate (có thể kiểm tra sự xuất hiện của vùng QR).

Lợi ích đạt được:

- Giảm thời gian kiểm thử lại (regression) cho những luồng cơ bản mỗi khi có cập nhật.
- Tăng độ chính xác khi phải lặp lại cùng một chuỗi thao tác với nhiều bộ dữ liệu.

Hạn chế:

- Chưa tự động hoá được các kịch bản phức tạp liên quan đến xác nhận từ cổng thanh toán thật.
- Việc bảo trì script còn thủ công khi giao diện thay đổi.

---

## KẾT LUẬN

### 1. Những nội dung đã đạt được

- Nhóm em đã phân tích đề bài và tài liệu đặc tả để hiểu rõ bối cảnh, yêu cầu của hệ thống DevMartVN, từ đó xác định được 15 màn hình và các module chức năng chính. [1][2]
- Dựa trên đó, nhóm thiết kế bộ test case chi tiết cho từng màn hình (được tổng hợp trong TEST_CASE.MD), bao gồm cả các trường trên giao diện, hành vi, điều kiện ràng buộc và thông điệp lỗi. [3]
- Nhóm đã thực thi test ở mức Integration và System, phát hiện một số lỗi quan trọng liên quan đến giao dịch tài chính và hiển thị trạng thái. Các lỗi này được ghi nhận và đề xuất hướng xử lý.
- Một phần test đã được tự động hoá bằng Selenium để minh hoạ lợi ích của automation trong regression test. [4][5]

### 2. Hạn chế

- Unit test chưa được triển khai đầy đủ trong code, chủ yếu dừng ở mức mô hình hóa trên giấy.
- Chưa thực hiện kiểm thử hiệu năng và bảo mật chuyên sâu; chưa đo đạc khả năng chịu tải với nhiều người dùng đồng thời.
- Automation test mới bao phủ một số luồng cơ bản, chưa áp dụng data‑driven test và chưa tích hợp CI/CD.

### 3. Hướng phát triển

- Bổ sung unit test và automation test cho các hàm nghiệp vụ quan trọng (xử lý tiền, cập nhật trạng thái giao dịch).
- Thực hiện kiểm thử hiệu năng với các công cụ như JMeter, kiểm thử bảo mật cơ bản theo OWASP Top 10. [5]
- Chuẩn hóa bộ test case và báo cáo theo chuẩn ISO/IEC/IEEE 29119 để dễ chuyển giao và mở rộng cho các phiên bản tiếp theo. [5]
- Tích hợp automation test vào pipeline CI/CD để mỗi lần build mới đều có thể chạy regression tự động.

---

## DANH MỤC TÀI LIỆU THAM KHẢO

1. Đề bài môn Kiểm thử phần mềm – “Hệ thống Website Mua Bán Mã Nguồn DevMartVN”, Bộ môn Công nghệ phần mềm, Trường ….
2. Tài liệu phân tích, thiết kế và danh sách màn hình “KIEM-THU-WEBSITE-MUA-BAN-MA-NGUON-DEVMARTVN.COM.xlsx”, Nhóm …, năm ….
3. File “TEST_CASE.MD – Báo cáo Test Case UI/UX Website Mua Bán Mã Nguồn DevMartVN”, Nhóm …, 2025.
4. G. J. Myers, C. Sandler, T. Badgett, _The Art of Software Testing_, 3rd Edition, Wiley, 2011.
5. ISO/IEC/IEEE 29119, _Software and systems engineering – Software testing_, 2013, cùng các tài liệu hướng dẫn kỹ thuật kiểm thử hộp đen và automation test (Selenium, Postman, JUnit, TestNG).
