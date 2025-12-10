# BÁO CÁO TEST CASE UI/UX – WEBSITE MUA BÁN MÃ NGUỒN DEVMARTVN

**Dự án:** DevMartVN – Source Code Marketplace  
**Ngày cập nhật:** 09/12/2025  
**Người thực hiện:** QA Tester

---

## 1. Đăng nhập (dangnhap.jpg)

### 1.1. Định nghĩa hạng mục màn hình

| No. | Tên hạng mục màn hình  | Mô tả                                        | Định dạng | I/O | Bắt buộc | Place Holder    | Min-length | Max-length | Kiểu dữ liệu | Giá trị default | Note                                                                      |
| --- | ---------------------- | -------------------------------------------- | --------- | --- | -------- | --------------- | ---------- | ---------- | ------------ | --------------- | ------------------------------------------------------------------------- |
| 1   | Tên đăng nhập          | Textbox để nhập tên đăng nhập hoặc email     | Textbox   | I   | Y        | "devmartvn"     | 1          | 255        | String       | ""              | Icon: fa-envelope, required, trim() khi submit                            |
| 2   | Mật khẩu               | Textbox để nhập mật khẩu, có nút hiển thị/ẩn | Password  | I   | Y        | "Nhập mật khẩu" | 8          | 128        | String       | ""              | Icon: fa-lock, có nút toggle show/hide password, required                 |
| 3   | Ghi nhớ đăng nhập      | Checkbox để ghi nhớ trạng thái đăng nhập     | Checkbox  | I   | N        | -               | -          | -          | Boolean      | false           | Lưu vào localStorage nếu checked                                          |
| 4   | Nút "Đăng nhập"        | Button submit form đăng nhập                 | Button    | I   | Y        | -               | -          | -          | -            | -               | Disabled khi loading, màu brand-500, hiển thị "Đang xử lý..." khi loading |
| 5   | Link "Quên mật khẩu?"  | Link điều hướng sang màn quên mật khẩu       | Link      | I   | N        | -               | -          | -          | -            | -               | Màu brand-500, hover underline                                            |
| 6   | Nút "Đăng nhập Google" | Button đăng nhập bằng Google OAuth           | Button    | I   | N        | -               | -          | -          | -            | -               | Icon: fab fa-google, màu đỏ, border gray-200                              |
| 7   | Nút "Đăng nhập GitHub" | Button đăng nhập bằng GitHub OAuth           | Button    | I   | N        | -               | -          | -          | -            | -               | Icon: fab fa-github, màu đen, border gray-200                             |
| 8   | Link "Đăng ký ngay"    | Link điều hướng sang màn hình Đăng ký        | Link      | I   | N        | -               | -          | -          | -            | -               | Màu brand-500, hover underline, text: "Chưa có tài khoản? Đăng ký ngay"   |

### 1.2. Test case chính

| ID          | Mục tiêu                     | Tiền điều kiện    | Bước thực hiện                                          | Kết quả mong đợi                                     | Priority |
| ----------- | ---------------------------- | ----------------- | ------------------------------------------------------- | ---------------------------------------------------- | -------- |
| TC-LOGIN-01 | Bắt buộc nhập Email/Username | User đã tồn tại   | Để trống field 1, nhập mật khẩu hợp lệ, click Đăng nhập | Hiển thị message lỗi yêu cầu nhập Email/Username     | High     |
| TC-LOGIN-02 | Email sai định dạng          | -                 | Nhập `abc@devmart` + mật khẩu hợp lệ, click Đăng nhập   | Hiển thị message “Email không đúng định dạng”        | Medium   |
| TC-LOGIN-03 | Bắt buộc nhập Mật khẩu       | -                 | Nhập email hợp lệ, để trống mật khẩu, click Đăng nhập   | Hiển thị message lỗi yêu cầu nhập Mật khẩu           | High     |
| TC-LOGIN-04 | Sai Email/Password           | -                 | Nhập email đúng + mật khẩu sai, click Đăng nhập         | Thông báo “Email hoặc mật khẩu không đúng”           | High     |
| TC-LOGIN-05 | Đăng nhập thành công         | User hợp lệ       | Nhập email + mật khẩu đúng, click Đăng nhập             | Chuyển tới Trang chủ, header hiển thị avatar + số dư | High     |
| TC-LOGIN-06 | Đăng nhập bằng Google        | Cấu hình OAuth OK | Click nút Google, login Google thành công               | Redirect về site, user ở trạng thái đã đăng nhập     | Medium   |
| TC-LOGIN-07 | Đăng nhập bằng GitHub        | Cấu hình OAuth OK | Click nút GitHub, login GitHub thành công               | Redirect về site, user ở trạng thái đã đăng nhập     | Medium   |
| TC-LOGIN-08 | Link Đăng ký                 | -                 | Click “Đăng ký ngay”                                    | Điều hướng sang màn hình Đăng ký                     | Low      |

---

## 2. Đăng ký (Dang-ki.jpg)

### 2.1. Định nghĩa hạng mục màn hình

| No. | Tên hạng mục màn hình   | Mô tả                                    | Định dạng | I/O | Bắt buộc | Place Holder          | Min-length | Max-length | Kiểu dữ liệu | Giá trị default | Note                                                                      |
| --- | ----------------------- | ---------------------------------------- | --------- | --- | -------- | --------------------- | ---------- | ---------- | ------------ | --------------- | ------------------------------------------------------------------------- |
| 1   | Tên người dùng          | Textbox để nhập tên đăng nhập (username) | Textbox   | I   | Y        | "devmartvn"           | 1          | 255        | String       | ""              | Icon: fa-user, required, trim() khi submit, unique                        |
| 2   | Email                   | Textbox để nhập email                    | Textbox   | I   | Y        | "devmartvn@gmail.com" | 1          | 255        | Email        | ""              | Icon: fa-envelope, required, validate email format, unique                |
| 3   | Mật khẩu                | Textbox để nhập mật khẩu                 | Password  | I   | Y        | "Tạo mật khẩu"        | 8          | 128        | String       | ""              | Icon: fa-lock, required, min 8 ký tự, policy mạnh                         |
| 4   | Xác nhận mật khẩu       | Textbox để nhập lại mật khẩu xác nhận    | Password  | I   | Y        | "Nhập lại mật khẩu"   | 8          | 128        | String       | ""              | Icon: fa-lock, required, phải trùng với mật khẩu                          |
| 5   | Họ và tên               | Textbox để nhập họ và tên đầy đủ         | Textbox   | I   | Y        | "DevMartVN"           | 1          | 255        | String       | ""              | Icon: fa-id-card, required, trim() khi submit                             |
| 6   | Số điện thoại           | Textbox để nhập số điện thoại            | Textbox   | I   | Y        | "0123 456 789"        | 9          | 12         | String       | ""              | Icon: fa-phone, required, chỉ nhận số, format VN                          |
| 7   | Nút "Đăng ký tài khoản" | Button submit form đăng ký               | Button    | I   | Y        | -                     | -          | -          | -            | -               | Disabled khi loading, màu brand-500, hiển thị "Đang xử lý..." khi loading |
| 8   | Link "Đăng nhập ngay"   | Link điều hướng sang màn hình Đăng nhập  | Link      | I   | N        | -                     | -          | -          | -            | -               | Màu brand-500, hover underline, text: "Đã có tài khoản? Đăng nhập ngay"   |

### 2.2. Test case

| ID        | Mục tiêu                    | Bước thực hiện                                       | Kết quả mong đợi                                           | Pri    |
| --------- | --------------------------- | ---------------------------------------------------- | ---------------------------------------------------------- | ------ |
| TC-REG-01 | Bắt buộc Họ và tên          | Để trống field 1, nhập các field khác hợp lệ, submit | Báo lỗi “Không được bỏ trống Họ và tên”                    | High   |
| TC-REG-02 | Email sai định dạng         | Nhập email `abc@`                                    | Báo lỗi định dạng email                                    | High   |
| TC-REG-03 | Email đã tồn tại            | Nhập email đã đăng ký, submit                        | Báo lỗi “Email đã tồn tại”                                 | High   |
| TC-REG-04 | Password quá ngắn           | Nhập mật khẩu < 8 ký tự                              | Báo lỗi độ dài mật khẩu                                    | High   |
| TC-REG-05 | Confirm password không khớp | Field 3 = A, Field 4 = B, submit                     | Báo lỗi “Mật khẩu xác nhận không khớp”                     | High   |
| TC-REG-06 | Số điện thoại chứa ký tự    | Nhập “abc123”                                        | Báo lỗi “Số điện thoại không hợp lệ”                       | Medium |
| TC-REG-07 | Đăng ký thành công          | Tất cả field hợp lệ, submit                          | Tạo user mới, hiển thị thông báo thành công / chuyển login | High   |

---

## 3. Trang chủ (Trang-chu.jpg)

### 3.1. Định nghĩa hạng mục màn hình

| No. | Tên hạng mục màn hình  | Mô tả                                                  | Định dạng | I/O | Bắt buộc | Place Holder | Min-length | Max-length | Kiểu dữ liệu | Giá trị default | Note                                          |
| --- | ---------------------- | ------------------------------------------------------ | --------- | --- | -------- | ------------ | ---------- | ---------- | ------------ | --------------- | --------------------------------------------- |
| 1   | Header                 | Logo, thanh tìm kiếm, menu danh mục, Đăng bán, Login   | Object    | O   | -        | -            | -          | -          | Object       | -               | Fixed top, z-index 30, gradient background    |
| 2   | Banner quảng cáo       | Banner chính khuyến mãi (Swiper slider)                | Image     | O   | -        | -            | -          | -          | String (URL) | slide1.jpg      | Swiper slider tự động, delay 3000ms, 3 slides |
| 3   | Danh mục top menu      | Tất cả, Website, Game/Giải trí, Hệ thống Quản lý,...   | Button    | O   | -        | -            | -          | -          | String       | "all"           | Horizontal menu, click filter sản phẩm        |
| 4   | Khối "Top lượt xem"    | Danh sách sản phẩm xem nhiều (sidebar trái)            | Object    | O   | -        | -            | -          | -          | Array        | []              | Hiển thị trong Sidebar component              |
| 5   | Khối "Ưu đãi đặc biệt" | CTA đăng ký / đăng nhập nhanh                          | Object    | O   | -        | -            | -          | -          | Object       | -               | Promotional banner trong Sidebar              |
| 6   | Danh sách sản phẩm     | Card sản phẩm: ảnh, tên, giá, badge miễn phí, thống kê | Object    | O   | -        | -            | -          | -          | Array        | []              | Grid layout responsive, CodeCard component    |
| 7   | Footer                 | Thông tin DevMartVN, hỗ trợ, liên hệ, social           | Object    | O   | -        | -            | -          | -          | Object       | -               | Fixed bottom, links và social icons           |

### 3.2. Test case chính

| ID         | Mục tiêu                  | Bước thực hiện                       | Kết quả mong đợi                                       |
| ---------- | ------------------------- | ------------------------------------ | ------------------------------------------------------ |
| TC-HOME-01 | Load trang chủ            | Truy cập `/`                         | Hiển thị banner, list sản phẩm, sidebar, footer đầy đủ |
| TC-HOME-02 | Tìm kiếm sản phẩm         | Nhập từ khóa trong search bar, Enter | Danh sách sản phẩm lọc theo từ khóa                    |
| TC-HOME-03 | Chọn danh mục từ menu top | Click “Game / Giải trí”              | Chỉ hiển thị sản phẩm thuộc danh mục tương ứng         |
| TC-HOME-04 | Xem chi tiết sản phẩm     | Click vào card sản phẩm              | Điều hướng tới trang chi tiết sản phẩm                 |
| TC-HOME-05 | Nút Đăng bán              | Click “Đăng Bán” khi chưa login      | Điều hướng tới màn Đăng nhập/Đăng ký                   |
| TC-HOME-06 | Sản phẩm miễn phí         | Chọn card được gắn badge “Miễn phí”  | Giá hiển thị = 0 và có label “Miễn phí”                |

---

## 4. Thông tin cá nhân + Thông tin ngân hàng (Thong-tin-ca-nhan.jpg)

### 4.1. Định nghĩa hạng mục màn hình

| No. | Tên hạng mục màn hình | Mô tả                                     | Định dạng | I/O | Bắt buộc | Place Holder                  | Min-length | Max-length | Kiểu dữ liệu | Giá trị default | Note                                                                   |
| --- | --------------------- | ----------------------------------------- | --------- | --- | -------- | ----------------------------- | ---------- | ---------- | ------------ | --------------- | ---------------------------------------------------------------------- |
| 1   | Avatar người dùng     | Hiển thị ảnh đại diện, có nút upload      | Image     | O   | -        | -                             | -          | -          | String (URL) | defaultAvatar   | 24x24 rounded-3xl, có nút camera để upload, max 5MB, accept image/\*   |
| 2   | Họ và tên             | Textbox để nhập họ và tên đầy đủ          | Textbox   | I   | Y        | -                             | 1          | 255        | String       | ""              | Required, trim() khi submit                                            |
| 3   | Tên đăng nhập         | Textbox hiển thị tên đăng nhập (readonly) | Textbox   | O   | Y        | -                             | -          | -          | String       | ""              | Disabled, bg-gray-50, cursor-not-allowed, không cho sửa                |
| 4   | Email                 | Textbox để nhập email                     | Textbox   | I   | Y        | -                             | 1          | 255        | Email        | ""              | Required, validate email format                                        |
| 5   | Số điện thoại         | Textbox để nhập số điện thoại             | Textbox   | I   | Y        | -                             | 9          | 12         | String       | ""              | Required, chỉ nhận số, format VN                                       |
| 6   | Ngân hàng nhận tiền   | Select dropdown danh sách ngân hàng VN    | Select    | I   | Y        | "— Chọn ngân hàng —"          | -          | -          | String       | ""              | Required, load từ API, format: "ShortName - FullName"                  |
| 7   | Số tài khoản          | Textbox để nhập số tài khoản ngân hàng    | Textbox   | I   | Y        | "Nhập chính xác số tài khoản" | 1          | 20         | String       | ""              | Required, chỉ số, max 20 ký tự                                         |
| 8   | Chủ tài khoản         | Textbox để nhập tên chủ tài khoản         | Textbox   | I   | Y        | "Viết IN HOA có dấu"          | 1          | 255        | String       | ""              | Required, viết IN HOA có dấu                                           |
| 9   | Nút "Lưu thay đổi"    | Button submit form cập nhật thông tin     | Button    | I   | Y        | -                             | -          | -          | Boolean      | false           | Disabled khi loading, màu brand-500, hiển thị "Đang lưu..." khi saving |
| 10  | Nút "Đổi mật khẩu"    | Button điều hướng sang trang đổi mật khẩu | Button    | I   | N        | -                             | -          | -          | -            | -               | Màu gray-900, điều hướng tới /profile/change-password                  |

### 4.2. Test case

| ID            | Mục tiêu                      | Bước thực hiện                                       | Kết quả mong đợi                        |
| ------------- | ----------------------------- | ---------------------------------------------------- | --------------------------------------- |
| TC-PROFILE-01 | Load thông tin cá nhân        | Mở trang khi đã đăng nhập                            | Field pre-fill đúng dữ liệu user        |
| TC-PROFILE-02 | Không cho sửa Email, Username | Thử click, gõ vào Email/Tên đăng nhập                | Không sửa được                          |
| TC-PROFILE-03 | Validate Số điện thoại        | Nhập ký tự chữ, click Lưu thay đổi                   | Báo lỗi định dạng SĐT                   |
| TC-PROFILE-04 | Bắt buộc thông tin ngân hàng  | Để trống một trong các field 5–7, click Lưu          | Báo lỗi yêu cầu nhập đầy đủ             |
| TC-PROFILE-05 | Cập nhật thông tin thành công | Sửa Họ tên, SĐT, ngân hàng, số TK, chủ TK, click Lưu | Thông báo thành công, data mới được lưu |

---

## 5. Nạp tiền (Nap-tien.jpg / Nap-Tien.jpg)

### 5.1. Định nghĩa hạng mục màn hình

| No. | Tên hạng mục màn hình          | Mô tả                                                            | Định dạng | I/O | Bắt buộc | Place Holder               | Min-length | Max-length | Kiểu dữ liệu | Giá trị default | Note                                                                                                                                  |
| --- | ------------------------------ | ---------------------------------------------------------------- | --------- | --- | -------- | -------------------------- | ---------- | ---------- | ------------ | --------------- | ------------------------------------------------------------------------------------------------------------------------------------- |
| 1   | Số dư hiện tại                 | Hiển thị số dư của người dùng                                    | Label     | O   | -        | -                          | -          | -          | Number       | 0               | Format VND, hiển thị trong header hoặc card                                                                                           |
| 2   | Các mệnh giá nhanh             | Các nút chọn nhanh số tiền để nạp                                | Button    | I   | N        | -                          | -          | -          | Number       | 100000          | Grid 3 cột, giá trị: 50000, 100000, 200000, 500000, 1000000, 2000000                                                                  |
| 3   | Nhập số tiền khác              | Textbox để nhập số tiền tùy chỉnh                                | Textbox   | I   | N        | "Nhập số tiền muốn nạp..." | -          | -          | Number       | ""              | Chỉ nhận số, min: 50000, tự động format khi nhập                                                                                      |
| 4   | QR VietQR                      | Mã QR theo số tiền và nội dung chuyển khoản                      | Image     | O   | -        | -                          | -          | -          | String (URL) | -               | Tự động cập nhật theo số tiền, URL: https://img.vietqr.io/image/ACB-17059951-compact2.png                                             |
| 5   | Nội dung chuyển khoản          | Hiển thị nội dung chuyển khoản cần nhập                          | Label     | O   | -        | -                          | -          | 255        | String       | -               | Format: "naptien {username} {amount}", có nút sao chép                                                                                |
| 6   | Nút "Xác nhận đã chuyển khoản" | Xác nhận đã thanh toán                                           | Button    | I   | Y        | -                          | -          | -          | Boolean      | false           | Disabled nếu chưa login, hiển thị loading khi đang kiểm tra                                                                           |
| 7   | Lịch sử nạp tiền               | Bảng hiển thị lịch sử: Thời gian, số tiền, số dư sau, trạng thái | Table     | O   | -        | -                          | -          | -          | Array        | []              | Chỉ hiển thị DEPOSIT, có nút refresh, format: Thời gian (dd/mm/yyyy HH:mm), Số tiền (+format VND), Số dư sau, Trạng thái (Thành công) |

### 5.2. Test case

| ID            | Mục tiêu                             | Bước thực hiện                                     | Kết quả mong đợi                                        |
| ------------- | ------------------------------------ | -------------------------------------------------- | ------------------------------------------------------- |
| TC-DEPOSIT-01 | Chọn mệnh giá nhanh                  | Click vào button 100.000 VND                       | Field số tiền / hiển thị QR tương ứng 100.000           |
| TC-DEPOSIT-02 | Nhập số tiền không hợp lệ (dưới min) | Nhập 10.000, click tạo QR / xác nhận               | Báo lỗi “Số tiền nạp tối thiểu …”                       |
| TC-DEPOSIT-03 | Tạo QR theo số tiền nhập tay         | Nhập 300.000, click tạo / focus ra ngoài           | QR hiển thị số tiền 300.000 và nội dung đúng format     |
| TC-DEPOSIT-04 | Xác nhận đã chuyển khoản             | Sau khi nạp thật, click “Xác nhận đã chuyển khoản” | Tạo yêu cầu nạp, lịch sử nạp thêm 1 dòng trạng thái chờ |
| TC-DEPOSIT-05 | Lịch sử nạp tiền                     | Mở tab lịch sử                                     | Hiển thị các giao dịch với trạng thái Thành công/Chờ    |

---

## 6. Rút tiền (Rut-tien.jpg)

### 6.1. Định nghĩa hạng mục màn hình

| No. | Tên hạng mục màn hình              | Mô tả                                                                        | Định dạng | I/O | Bắt buộc | Place Holder            | Min-length | Max-length | Kiểu dữ liệu | Giá trị default | Note                                                                                                                                |
| --- | ---------------------------------- | ---------------------------------------------------------------------------- | --------- | --- | -------- | ----------------------- | ---------- | ---------- | ------------ | --------------- | ----------------------------------------------------------------------------------------------------------------------------------- |
| 1   | Số dư khả dụng                     | Hiển thị số dư hiện tại của người dùng                                       | Label     | O   | -        | -                       | -          | -          | Number       | 0               | Format VND, hiển thị trong card hoặc header                                                                                         |
| 2   | Các mệnh giá nhanh                 | Các nút chọn nhanh số tiền để rút                                            | Button    | I   | N        | -                       | -          | -          | Number       | 100000          | Grid 3 cột, giá trị: 50000, 100000, 200000, 500000, 1000000, 2000000                                                                |
| 3   | Nhập số tiền rút                   | Textbox để nhập số tiền rút tùy chỉnh                                        | Textbox   | I   | Y        | "Nhập số tiền muốn rút" | -          | -          | Number       | ""              | Chỉ nhận số, min: 50000, max: số dư hiện tại                                                                                        |
| 4   | Nút "Tạo yêu cầu rút tiền"         | Button submit tạo yêu cầu rút tiền                                           | Button    | I   | Y        | -                       | -          | -          | Boolean      | false           | Disabled nếu chưa login hoặc thiếu thông tin ngân hàng, hiển thị "Đang xử lý..." khi submitting                                     |
| 5   | Lịch sử rút tiền                   | Bảng hiển thị lịch sử: Mã giao dịch, số tiền, trạng thái, ghi chú, thời gian | Table     | O   | -        | -                       | -          | -          | Array        | []              | Format: Mã (DMVN{id}), Số tiền (-format VND, màu đỏ), Trạng thái (PENDING/APPROVED/REJECTED), Ghi chú, Thời gian (dd/mm/yyyy HH:mm) |
| 6   | Cảnh báo thiếu thông tin ngân hàng | Hiển thị cảnh báo nếu chưa cập nhật thông tin ngân hàng                      | Label     | O   | -        | -                       | -          | -          | Boolean      | false           | Màu vàng, có link điều hướng tới /profile                                                                                           |

### 6.2. Test case

| ID         | Mục tiêu                     | Bước thực hiện                     | Kết quả mong đợi                                     |
| ---------- | ---------------------------- | ---------------------------------- | ---------------------------------------------------- |
| TC-WITH-01 | Rút dưới số tối thiểu        | Nhập 10.000, click Tạo yêu cầu rút | Báo lỗi “Số tiền rút tối thiểu …”                    |
| TC-WITH-02 | Rút vượt số dư               | Số dư 100k, nhập 200k              | Báo lỗi “Không đủ số dư”                             |
| TC-WITH-03 | Rút thành công (tạo yêu cầu) | Nhập số hợp lệ, click Tạo yêu cầu  | Thêm dòng lịch sử trạng thái “Đang xử lý / Đang chờ” |
| TC-WITH-04 | Hiển thị lịch sử rút tiền    | Mở trang khi đã có dữ liệu         | Danh sách hiển thị đúng số tiền, trạng thái          |

---

## 7. Lịch sử biến động số dư (Lich-su-bien-dong-so-du.jpg – Admin)

### 7.1. Định nghĩa hạng mục màn hình

| No. | Tên hạng mục màn hình | Mô tả                                 | Định dạng  | I/O | Bắt buộc | Place Holder | Min-length | Max-length | Kiểu dữ liệu | Giá trị default | Note                                                                     |
| --- | --------------------- | ------------------------------------- | ---------- | --- | -------- | ------------ | ---------- | ---------- | ------------ | --------------- | ------------------------------------------------------------------------ |
| 1   | Tabs filter           | Các tab lọc theo loại giao dịch       | Tabs       | I   | N        | -            | -          | -          | String       | "Tất cả"        | Tabs: Tất cả, Nạp tiền, Rút tiền, Mua hàng, Bán hàng, Hoàn tiền          |
| 2   | Người dùng            | Hiển thị avatar và tên người dùng     | Object     | O   | -        | -            | -          | -          | Object       | -               | Avatar: rounded-full, fallback: chữ cái đầu, tên: username hoặc fullName |
| 3   | Số tiền               | Hiển thị số tiền với dấu + / – và màu | Label      | O   | -        | -            | -          | -          | Number       | 0               | Giao dịch cộng: màu xanh, dấu +; trừ: màu đỏ, dấu –, format VND          |
| 4   | Số dư sau             | Hiển thị số dư sau giao dịch          | Label      | O   | -        | -            | -          | -          | Number       | 0               | Format VND, màu gray                                                     |
| 5   | Nội dung              | Mô tả giao dịch                       | Label      | O   | -        | -            | -          | 500        | String       | -               | Mô tả ngắn gọn về loại giao dịch                                         |
| 6   | Thời gian             | Hiển thị ngày giờ giao dịch           | Label      | O   | -        | -            | -          | -          | Date         | -               | Format dd/mm/yyyy HH:mm                                                  |
| 7   | Pagination            | Phân trang danh sách giao dịch        | Pagination | I   | N        | -            | -          | -          | Number       | 1               | Hiển thị số trang, nút Previous/Next, số items per page                  |

### 7.2. Test case

| ID        | Mục tiêu                   | Bước thực hiện       | Kết quả mong đợi                             |
| --------- | -------------------------- | -------------------- | -------------------------------------------- |
| TC-BAL-01 | Filter theo loại giao dịch | Chọn tab “Nạp tiền”  | Chỉ hiển thị giao dịch loại Nạp tiền         |
| TC-BAL-02 | Màu và dấu số tiền         | Quan sát cột Số tiền | Giao dịch cộng: màu xanh, tiền +; trừ: đỏ, – |
| TC-BAL-03 | Phân trang                 | Click trang 2        | Dữ liệu trang 2 hiển thị đúng                |

---

## 8. Lịch sử mua hàng (Lich-su-mua-hang.jpg – User)

### 8.1. Định nghĩa hạng mục màn hình

| No. | Tên hạng mục màn hình   | Mô tả                                      | Định dạng | I/O | Bắt buộc | Place Holder | Min-length | Max-length | Kiểu dữ liệu | Giá trị default | Note                                                                                   |
| --- | ----------------------- | ------------------------------------------ | --------- | --- | -------- | ------------ | ---------- | ---------- | ------------ | --------------- | -------------------------------------------------------------------------------------- |
| 1   | Mã giao dịch            | Hiển thị mã đơn hàng                       | Label     | O   | -        | -            | -          | -          | Number       | -               | Format: #{orderId}, font-mono                                                          |
| 2   | Tên sản phẩm            | Hiển thị tên sản phẩm đã mua               | Label     | O   | -        | -            | 1          | 255        | String       | -               | Có thể click để xem chi tiết, font-semibold                                            |
| 3   | Thời gian               | Hiển thị ngày giờ mua hàng                 | Label     | O   | -        | -            | -          | -          | Date         | -               | Format: dd/mm/yyyy HH:mm, màu gray-500                                                 |
| 4   | Giá                     | Hiển thị giá đã thanh toán                 | Label     | O   | -        | -            | -          | -          | Number       | 0               | Format VND, màu gray-500                                                               |
| 5   | Nút "Xem chi tiết"      | Button mở modal chi tiết đơn hàng          | Button    | I   | N        | -            | -          | -          | Boolean      | false           | Màu gray, border, mở modal hiển thị thông tin chi tiết                                 |
| 6   | Nút "Tải xuống"         | Button tải file mã nguồn                   | Button    | I   | N        | -            | -          | -          | Boolean      | false           | Màu brand-500, mở link download trong tab mới                                          |
| 7   | Modal chi tiết đơn hàng | Modal hiển thị thông tin chi tiết đơn hàng | Modal     | O   | -        | -            | -          | -          | Object       | null            | Hiển thị: Sản phẩm, Giá mua, Ngày mua, Người bán, Mô tả ngắn, có nút Tải xuống và Đóng |

### 8.2. Test case

| ID           | Mục tiêu                 | Bước thực hiện                   | Kết quả mong đợi                                |
| ------------ | ------------------------ | -------------------------------- | ----------------------------------------------- |
| TC-ORDHIS-01 | Xem danh sách đơn đã mua | Mở màn Lịch sử mua hàng          | Hiển thị đầy đủ giao dịch của user              |
| TC-ORDHIS-02 | Xem chi tiết đơn hàng    | Click “Xem chi tiết” trên 1 dòng | Điều hướng sang màn chi tiết đơn hàng           |
| TC-ORDHIS-03 | Tải lại source           | Click “Tải xuống”                | Bắt đầu tải file nguồn tương ứng (nếu quyền OK) |

---

## 9. Shop của tôi (Shop-cua-toi.jpg – Seller)

### 9.1. Định nghĩa hạng mục màn hình

| No. | Tên hạng mục màn hình     | Mô tả                                          | Định dạng | I/O | Bắt buộc | Place Holder | Min-length | Max-length | Kiểu dữ liệu | Giá trị default | Note                                                                             |
| --- | ------------------------- | ---------------------------------------------- | --------- | --- | -------- | ------------ | ---------- | ---------- | ------------ | --------------- | -------------------------------------------------------------------------------- |
| 1   | Avatar seller             | Hiển thị ảnh đại diện người bán                | Image     | O   | -        | -            | -          | -          | String (URL) | defaultAvatar   | 24x24 rounded-3xl, fallback: defaultAvatar                                       |
| 2   | Tên seller                | Hiển thị tên người bán                         | Label     | O   | -        | -            | 1          | 255        | String       | -               | Font size: text-3xl, bold, màu gray-900                                          |
| 3   | Username                  | Hiển thị username người bán                    | Label     | O   | -        | -            | 1          | 255        | String       | -               | Font size: text-sm, màu gray-500                                                 |
| 4   | Ngày tham gia             | Hiển thị ngày tham gia                         | Label     | O   | -        | -            | -          | -          | Date         | -               | Format: "Tham gia từ dd/mm/yyyy", màu gray-500                                   |
| 5   | Nút "Liên hệ"             | Button hiển thị thông tin liên hệ              | Button    | I   | N        | -            | -          | -          | Boolean      | false           | Màu brand-500, mở modal hiển thị: Tên, Email, Số điện thoại                      |
| 6   | Nút "Theo dõi"            | Button theo dõi người bán                      | Button    | I   | N        | -            | -          | -          | Boolean      | false           | Border gray-200, hiển thị thông báo "Chức năng đang phát triển"                  |
| 7   | Danh sách sản phẩm        | Grid hiển thị các sản phẩm của seller          | Grid      | O   | -        | -            | -          | -          | Array        | []              | Grid 3 cột (desktop), 2 cột (tablet), 1 cột (mobile), sử dụng CodeCard component |
| 8   | Badge trạng thái sản phẩm | Hiển thị trạng thái sản phẩm (nếu là chủ shop) | Badge     | O   | -        | -            | -          | -          | String       | -               | APPROVED: xanh, PENDING: vàng, REJECTED: đỏ, hiển thị ở góc trên trái card       |
| 9   | Nút "Chỉnh sửa"           | Button chỉnh sửa sản phẩm (nếu là chủ shop)    | Button    | I   | N        | -            | -          | -          | Boolean      | false           | Icon edit, màu blue-600, điều hướng tới /products/edit/{id}                      |
| 10  | Nút "Xóa"                 | Button xóa sản phẩm (nếu là chủ shop)          | Button    | I   | N        | -            | -          | -          | Boolean      | false           | Icon delete, màu red-600, có confirm dialog trước khi xóa                        |

### 9.2. Test case

| ID         | Mục tiêu                  | Bước thực hiện                   | Kết quả mong đợi                      |
| ---------- | ------------------------- | -------------------------------- | ------------------------------------- |
| TC-SHOP-01 | Xem shop người bán        | Click tên người bán ở 1 sản phẩm | Điều hướng tới trang shop tương ứng   |
| TC-SHOP-02 | Danh sách sản phẩm seller | Quan sát danh sách               | Chỉ hiển thị sản phẩm thuộc seller đó |

---

## 10. Đăng bán sản phẩm (Dang-ban-san-pham.jpg)

### 10.1. Định nghĩa hạng mục màn hình

| No. | Tên hạng mục màn hình   | Mô tả                              | Định dạng | I/O | Bắt buộc | Place Holder                                         | Min-length | Max-length | Kiểu dữ liệu  | Giá trị default | Note                                                                              |
| --- | ----------------------- | ---------------------------------- | --------- | --- | -------- | ---------------------------------------------------- | ---------- | ---------- | ------------- | --------------- | --------------------------------------------------------------------------------- |
| 1   | Tên sản phẩm            | Textbox để nhập tên sản phẩm       | Textbox   | I   | Y        | "VD: Website bán hàng thương mại điện tử Full Stack" | 1          | 255        | String        | ""              | Required, trim() khi submit                                                       |
| 2   | Danh mục                | Select dropdown danh sách danh mục | Select    | I   | Y        | "-- Chọn danh mục --"                                | -          | -          | Number        | ""              | Required, load từ API, options: Website, Game, Mobile, Desktop, Plugin, API, etc. |
| 3   | Giá bán                 | Textbox để nhập giá bán (VNĐ)      | Textbox   | I   | Y        | "500000"                                             | -          | -          | Number        | ""              | Required, type="number", min="0", step="1000", nếu = 0 hoặc rỗng → miễn phí       |
| 4   | Mô tả chi tiết          | Rich text editor (CKEditor)        | Editor    | I   | Y        | -                                                    | -          | -          | String (HTML) | ""              | Required, CKEditor với toolbar đầy đủ, minHeight: 500px, hỗ trợ upload image      |
| 5   | Link file mã nguồn      | Textbox để nhập URL file mã nguồn  | Textbox   | I   | N        | "https://drive.google.com/..."                       | -          | 500        | String (URL)  | ""              | Type="url", có thể là Google Drive, Dropbox hoặc link tải trực tiếp               |
| 6   | Link demo               | Textbox để nhập URL demo           | Textbox   | I   | N        | "https://demo.example.com"                           | -          | 500        | String (URL)  | ""              | Type="url", mở trong tab mới                                                      |
| 7   | Ảnh thumbnail           | Upload file ảnh thumbnail          | Upload    | I   | Y        | -                                                    | -          | -          | File          | null            | Accept="image/\*", max size: 10MB, format: JPG/PNG/GIF/WEBP, có preview           |
| 8   | Nút "Gửi yêu cầu duyệt" | Button submit form đăng sản phẩm   | Button    | I   | Y        | -                                                    | -          | -          | Boolean       | false           | Disabled khi loading, màu brand-500, hiển thị "Đang xử lý..." khi loading         |
| 9   | Nút "Xóa thông tin"     | Button reset form                  | Button    | I   | N        | -                                                    | -          | -          | Boolean       | false           | Border gray-300, reset tất cả field về giá trị default                            |

### 10.2. Test case

| ID         | Mục tiêu                      | Bước thực hiện                              | Kết quả mong đợi                                          |
| ---------- | ----------------------------- | ------------------------------------------- | --------------------------------------------------------- |
| TC-PROD-01 | Bắt buộc Tên, Danh mục, Mô tả | Để trống 1 trong 3 field, click Gửi yêu cầu | Báo lỗi bắt buộc                                          |
| TC-PROD-02 | Upload ảnh sai định dạng      | Chọn file `.pdf` làm thumbnail              | Báo lỗi định dạng                                         |
| TC-PROD-03 | Sản phẩm miễn phí             | Đặt Giá = 0 hoặc rỗng, submit               | Sản phẩm tạo với trạng thái “Miễn phí”                    |
| TC-PROD-04 | Gửi yêu cầu duyệt thành công  | Tất cả field hợp lệ                         | Tạo sản phẩm trạng thái “Chờ duyệt”, hiển thị trong admin |

---

## 11. Admin – Thống kê, người dùng, danh mục, sản phẩm, đơn hàng, yêu cầu rút tiền

Các màn hình admin (Thong-ke-tong-quan.jpg, Quan-ly-nguoi-dung.jpg, Quan-ly-danh-muc.jpg, Quan-ly-san-pham.jpg, Quan-ly-don-hang.jpg, Yeu-cau-rut-tien.jpg) dùng chung cấu trúc:

### 11.1. Định nghĩa hạng mục màn hình

| No. | Tên hạng mục màn hình   | Mô tả                                            | Định dạng  | I/O | Bắt buộc | Place Holder  | Min-length | Max-length | Kiểu dữ liệu | Giá trị default | Note                                                                                                                                      |
| --- | ----------------------- | ------------------------------------------------ | ---------- | --- | -------- | ------------- | ---------- | ---------- | ------------ | --------------- | ----------------------------------------------------------------------------------------------------------------------------------------- |
| 1   | Thanh sidebar           | Menu điều hướng các màn hình admin               | Sidebar    | O   | -        | -             | -          | -          | Object       | -               | Menu: Thống kê, Quản lý người dùng, Quản lý sản phẩm, Quản lý danh mục, Quản lý đơn hàng, Yêu cầu rút tiền, Lịch sử giao dịch, Audit logs |
| 2   | Ô tìm kiếm              | Textbox tìm kiếm theo từ khóa                    | Textbox    | I   | N        | "Tìm kiếm..." | 1          | 255        | String       | ""              | Search theo tên/email/sản phẩm/mã đơn tùy màn, có nút search hoặc Enter để submit                                                         |
| 3   | Bảng danh sách          | Bảng hiển thị danh sách dữ liệu                  | Table      | O   | -        | -             | -          | -          | Array        | []              | Cột: ID, thông tin chính, trạng thái, thao tác, có sorting và filtering                                                                   |
| 4   | Cột ID                  | Hiển thị ID của record                           | Label      | O   | -        | -             | -          | -          | Number       | -               | Font-mono, có thể click để xem chi tiết                                                                                                   |
| 5   | Cột thông tin chính     | Hiển thị thông tin chính (tên, email, etc.)      | Label      | O   | -        | -             | 1          | 255        | String       | -               | Tùy màn hình: tên user, tên sản phẩm, tên danh mục, etc.                                                                                  |
| 6   | Cột trạng thái          | Hiển thị trạng thái với badge màu                | Badge      | O   | -        | -             | -          | -          | String       | -               | Màu sắc tùy trạng thái: APPROVED (xanh), PENDING (vàng), REJECTED (đỏ), ACTIVE (xanh), INACTIVE (xám)                                     |
| 7   | Nút "Sửa"               | Button chỉnh sửa record                          | Button     | I   | N        | -             | -          | -          | Boolean      | false           | Icon edit, màu blue, điều hướng tới trang edit                                                                                            |
| 8   | Nút "Xóa"               | Button xóa record                                | Button     | I   | N        | -             | -          | -          | Boolean      | false           | Icon delete, màu red, có confirm dialog trước khi xóa                                                                                     |
| 9   | Nút "Chi tiết"          | Button xem chi tiết record                       | Button     | I   | N        | -             | -          | -          | Boolean      | false           | Màu gray, mở modal hoặc điều hướng tới trang chi tiết                                                                                     |
| 10  | Nút "Duyệt" / "Từ chối" | Button duyệt hoặc từ chối (với yêu cầu rút tiền) | Button     | I   | N        | -             | -          | -          | Boolean      | false           | Duyệt: màu green, Từ chối: màu red, có confirm dialog                                                                                     |
| 11  | Pagination              | Phân trang danh sách                             | Pagination | I   | N        | -             | -          | -          | Number       | 1               | Hiển thị số trang, nút Previous/Next, số items per page (10, 20, 50, 100)                                                                 |
| 12  | Tabs filter             | Tabs lọc theo trạng thái (với quản lý sản phẩm)  | Tabs       | I   | N        | -             | -          | -          | String       | "Tất cả"        | Tabs: Tất cả, Chờ duyệt, Đã duyệt, Từ chối                                                                                                |

### 11.2. Một số test case mẫu

| ID             | Màn hình           | Mục tiêu                 | Bước thực hiện                                       | Kết quả mong đợi                                   |
| -------------- | ------------------ | ------------------------ | ---------------------------------------------------- | -------------------------------------------------- |
| TC-ADM-DASH-01 | Thống kê tổng quan | Load dữ liệu mặc định    | Mở dashboard admin                                   | Card doanh thu, người dùng, đơn hàng hiển thị đúng |
| TC-ADM-USER-01 | Quản lý người dùng | Tìm kiếm theo email      | Nhập email vào ô search, Enter                       | Bảng chỉ hiển thị user khớp                        |
| TC-ADM-USER-02 | Quản lý người dùng | Xóa user                 | Click Xóa trên 1 dòng, xác nhận                      | User bị ẩn/xóa khỏi danh sách                      |
| TC-ADM-CAT-01  | Quản lý danh mục   | Thêm danh mục mới        | Click “Thêm danh mục”, nhập tên, lưu                 | Bảng tăng thêm 1 dòng danh mục                     |
| TC-ADM-PROD-01 | Quản lý sản phẩm   | Lọc sản phẩm “Chờ duyệt” | Click tab “Chờ duyệt”                                | Chỉ hiển thị sản phẩm trạng thái chờ duyệt         |
| TC-ADM-ORD-01  | Quản lý đơn hàng   | Xem chi tiết đơn hàng    | Click “Chi tiết”                                     | Hiển thị trang chi tiết đơn                        |
| TC-ADM-WREQ-01 | Yêu cầu rút tiền   | Duyệt yêu cầu rút        | Chọn 1 yêu cầu “Đang chờ”, chọn hành động “Đã duyệt” | Trạng thái đổi sang Đã duyệt, số dư user cập nhật  |

---

## 12. Trang chủ - Danh sách sản phẩm (HomePage)

### 12.1. Định nghĩa hạng mục màn hình

| No. | Tên hạng mục màn hình | Mô tả                                                                                                                                                                    | Định dạng | I/O | Bắt buộc | Place Holder | Min-length | Max-length | Kiểu dữ liệu  | Giá trị default | Note                                                                                  |
| --- | --------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | --------- | --- | -------- | ------------ | ---------- | ---------- | ------------- | --------------- | ------------------------------------------------------------------------------------- |
| 1   | Số dư hiện tại        | Hiển thị số dư của người dùng (nếu đã đăng nhập)                                                                                                                         | Label     | O   | -        | -            | -          | -          | Number        | 0               | Hiển thị trong header, format VND                                                     |
| 2   | Các mệnh giá nhanh    | Các nút chọn nhanh danh mục sản phẩm                                                                                                                                     | Button    | O   | -        | -            | -          | -          | String        | "all"           | Hiển thị trong Sidebar, danh mục: Tất cả, Website, Game, Mobile, Desktop, Plugin, API |
| 3   | List sản phẩm         | 1. Hiển thị thông tin list sản phẩm theo danh mục đã chọn<br>2. Hiển thị mặc định 20 sản phẩm, có phân trang<br>3. Thứ tự hiển thị theo thứ tự từ API                    | Object    | O   | -        | -            | -          | -          | Array         | []              | Grid layout responsive: 3 cột (desktop), 2 cột (tablet), 1 cột (mobile)               |
| 4   | Image quảng cáo       | Hiển thị image banner quảng cáo (slide 1)                                                                                                                                | Image     | O   | -        | -            | -          | -          | String (URL)  | slide1.jpg      | Swiper slider tự động, delay 3000ms                                                   |
| 5   | Image quảng cáo       | Hiển thị image banner quảng cáo (slide 2)                                                                                                                                | Image     | O   | -        | -            | -          | -          | String (URL)  | slide2.jpg      | Swiper slider tự động, delay 3000ms                                                   |
| 6   | Image quảng cáo       | Hiển thị image banner quảng cáo (slide 3)                                                                                                                                | Image     | O   | -        | -            | -          | -          | String (URL)  | slide3.jpg      | Swiper slider tự động, delay 3000ms                                                   |
| 7   | Tên và image sản phẩm | 1. Hiển thị image sản phẩm<br>2. Hiển thị tên sản phẩm, hiển thị tối đa 2 dòng, những kí tự còn lại hiển thị dạng ...<br>3. Click di chuyển vào màn hình detail sản phẩm | Label     | O   | -        | -            | 1          | 255        | String        | -               | Trong CodeCard component, line-clamp-2                                                |
| 8   | Giá gốc sản phẩm      | 1. Hiển thị thông tin giá gốc của sản phẩm<br>2. Format hiển thị gạch ngang giá gốc sản phẩm (nếu có)                                                                    | Label     | O   | -        | -            | -          | -          | Number        | 0               | Hiển thị line-through, màu gray-400                                                   |
| 9   | Giá sản phẩm          | 1. Hiển thị giá hiện tại của sản phẩm<br>2. Nếu giá = 0 hoặc null, hiển thị "MIỄN PHÍ"                                                                                   | Label     | O   | -        | -            | -          | -          | Number/String | 0               | Màu brand-500, format VND nếu có giá                                                  |
| 10  | Icon đánh giá sao     | Hiển thị mặc định 5 sao cho tất cả các sản phẩm                                                                                                                          | Label     | O   | -        | -            | -          | -          | Number        | 5               | Màu vàng (text-yellow-400), hiển thị 5 sao                                            |

### 12.2. Test case chính

| ID               | Mục tiêu                        | Tiền điều kiện    | Bước thực hiện                       | Kết quả mong đợi                                              | Priority |
| ---------------- | ------------------------------- | ----------------- | ------------------------------------ | ------------------------------------------------------------- | -------- |
| TC-HOME-FLASH-01 | Hiển thị số dư khi đã đăng nhập | User đã đăng nhập | Truy cập trang chủ                   | Header hiển thị số dư của user                                | High     |
| TC-HOME-FLASH-02 | Chọn danh mục từ sidebar        | -                 | Click vào một danh mục trong sidebar | Danh sách sản phẩm lọc theo danh mục đã chọn                  | High     |
| TC-HOME-FLASH-03 | Hiển thị banner quảng cáo       | -                 | Truy cập trang chủ                   | Banner slider tự động chuyển slide sau 3 giây                 | Medium   |
| TC-HOME-FLASH-04 | Hiển thị danh sách sản phẩm     | -                 | Truy cập trang chủ                   | Hiển thị grid 3 cột (desktop), 2 cột (tablet), 1 cột (mobile) | High     |
| TC-HOME-FLASH-05 | Tên sản phẩm quá dài            | -                 | Xem sản phẩm có tên dài              | Tên sản phẩm hiển thị tối đa 2 dòng, còn lại hiển thị ...     | Medium   |
| TC-HOME-FLASH-06 | Click vào sản phẩm              | -                 | Click vào card sản phẩm              | Điều hướng tới trang chi tiết sản phẩm                        | High     |
| TC-HOME-FLASH-07 | Sản phẩm miễn phí               | -                 | Xem sản phẩm có giá = 0              | Hiển thị "MIỄN PHÍ" thay vì giá                               | Medium   |
| TC-HOME-FLASH-08 | Hiển thị đánh giá sao           | -                 | Xem bất kỳ sản phẩm nào              | Hiển thị 5 sao màu vàng                                       | Low      |
| TC-HOME-FLASH-09 | Phân trang sản phẩm             | Có > 20 sản phẩm  | Scroll xuống cuối trang              | Hiển thị nút phân trang, click chuyển trang                   | High     |
| TC-HOME-FLASH-10 | Tìm kiếm sản phẩm               | -                 | Nhập từ khóa vào search bar, Enter   | Danh sách sản phẩm lọc theo từ khóa                           | High     |

---

## 13. Nạp tiền (WalletTopupPage)

### 13.1. Định nghĩa hạng mục màn hình

| No. | Tên hạng mục màn hình          | Mô tả                                                            | Định dạng | I/O | Bắt buộc | Place Holder               | Min-length | Max-length | Kiểu dữ liệu | Giá trị default | Note                                                                                                                                  |
| --- | ------------------------------ | ---------------------------------------------------------------- | --------- | --- | -------- | -------------------------- | ---------- | ---------- | ------------ | --------------- | ------------------------------------------------------------------------------------------------------------------------------------- |
| 1   | Số dư hiện tại                 | Hiển thị số dư của người dùng                                    | Label     | O   | -        | -                          | -          | -          | Number       | 0               | Format VND, hiển thị trong header hoặc card                                                                                           |
| 2   | Các mệnh giá nhanh             | Các nút chọn nhanh số tiền để nạp: 50k, 100k, 200k, 500k, 1M, 2M | Button    | I   | N        | -                          | -          | -          | Number       | 100000          | Grid 3 cột, giá trị: 50000, 100000, 200000, 500000, 1000000, 2000000                                                                  |
| 3   | Nhập số tiền khác              | Textbox để nhập số tiền tùy chỉnh                                | Textbox   | I   | N        | "Nhập số tiền muốn nạp..." | -          | -          | Number       | ""              | Chỉ nhận số, min: 50000, tự động format khi nhập                                                                                      |
| 4   | QR VietQR                      | Mã QR theo số tiền và nội dung chuyển khoản                      | Image     | O   | -        | -                          | -          | -          | String (URL) | -               | Tự động cập nhật theo số tiền, URL: https://img.vietqr.io/image/ACB-17059951-compact2.png                                             |
| 5   | Nội dung chuyển khoản          | Hiển thị nội dung chuyển khoản cần nhập                          | Label     | O   | -        | -                          | -          | 255        | String       | -               | Format: "naptien {username} {amount}", có nút sao chép                                                                                |
| 6   | Nút "Xác nhận đã chuyển khoản" | Xác nhận đã thanh toán                                           | Button    | I   | Y        | -                          | -          | -          | Boolean      | false           | Disabled nếu chưa login, hiển thị loading khi đang kiểm tra                                                                           |
| 7   | Lịch sử nạp tiền               | Bảng hiển thị lịch sử: Thời gian, số tiền, số dư sau, trạng thái | Table     | O   | -        | -                          | -          | -          | Array        | []              | Chỉ hiển thị DEPOSIT, có nút refresh, format: Thời gian (dd/mm/yyyy HH:mm), Số tiền (+format VND), Số dư sau, Trạng thái (Thành công) |

### 13.2. Test case chính

| ID          | Mục tiêu                             | Tiền điều kiện                     | Bước thực hiện                                 | Kết quả mong đợi                                           | Priority |
| ----------- | ------------------------------------ | ---------------------------------- | ---------------------------------------------- | ---------------------------------------------------------- | -------- |
| TC-TOPUP-01 | Hiển thị số dư hiện tại              | User đã đăng nhập                  | Truy cập trang nạp tiền                        | Hiển thị số dư của user, format VND                        | High     |
| TC-TOPUP-02 | Chọn mệnh giá nhanh                  | -                                  | Click vào button 100.000 VND                   | Field số tiền và QR code cập nhật theo 100.000             | High     |
| TC-TOPUP-03 | Nhập số tiền không hợp lệ (dưới min) | -                                  | Nhập 10.000, click xác nhận                    | Báo lỗi "Số tiền nạp tối thiểu 50.000đ"                    | High     |
| TC-TOPUP-04 | Nhập số tiền tùy chỉnh               | -                                  | Nhập 300.000 vào textbox                       | QR code và nội dung chuyển khoản cập nhật theo 300.000     | High     |
| TC-TOPUP-05 | QR code tự động cập nhật             | -                                  | Thay đổi số tiền (chọn mệnh giá hoặc nhập tay) | QR code tự động cập nhật với số tiền mới                   | High     |
| TC-TOPUP-06 | Nội dung chuyển khoản đúng format    | User đã đăng nhập                  | Chọn số tiền bất kỳ                            | Hiển thị "naptien {username} {số tiền}"                    | High     |
| TC-TOPUP-07 | Xác nhận đã chuyển khoản             | User đã đăng nhập, đã chuyển khoản | Click "Xác nhận đã chuyển khoản"               | Hệ thống kiểm tra và cập nhật số dư nếu có giao dịch       | High     |
| TC-TOPUP-08 | Hiển thị lịch sử nạp tiền            | User đã đăng nhập, có lịch sử      | Truy cập trang nạp tiền                        | Bảng hiển thị các giao dịch nạp tiền với đầy đủ thông tin  | High     |
| TC-TOPUP-09 | Chưa đăng nhập                       | User chưa đăng nhập                | Truy cập trang nạp tiền                        | Hiển thị cảnh báo yêu cầu đăng nhập, nút xác nhận disabled | High     |
| TC-TOPUP-10 | Sao chép nội dung chuyển khoản       | -                                  | Click nút "Sao chép" bên cạnh nội dung         | Nội dung được sao chép vào clipboard, hiển thị thông báo   | Medium   |

---

## 14. Chi tiết sản phẩm (ProductDetailPage)

### 14.1. Định nghĩa hạng mục màn hình

| No. | Tên hạng mục màn hình | Mô tả                                   | Định dạng | I/O | Bắt buộc | Place Holder | Min-length | Max-length | Kiểu dữ liệu  | Giá trị default                        | Note                                                                    |
| --- | --------------------- | --------------------------------------- | --------- | --- | -------- | ------------ | ---------- | ---------- | ------------- | -------------------------------------- | ----------------------------------------------------------------------- |
| 1   | Tên sản phẩm          | Hiển thị tên đầy đủ của sản phẩm        | Label     | O   | -        | -            | 1          | 255        | String        | -                                      | Font size: text-2xl md:text-3xl, bold, màu gray-900                     |
| 2   | Image sản phẩm        | Hiển thị image sản phẩm trong gallery   | Image     | O   | -        | -            | -          | -          | String (URL)  | slide1.jpg                             | Swiper slider với pagination, fallback: /images/logo.png                |
| 3   | Giá sản phẩm          | Hiển thị giá bán của sản phẩm           | Label     | O   | -        | -            | -          | -          | Number/String | 0                                      | Nếu = 0 hiển thị "MIỄN PHÍ", format VND nếu có giá, màu brand-500       |
| 4   | Lượt xem              | Hiển thị số lượt xem sản phẩm           | Label     | O   | -        | -            | -          | -          | Number        | 0                                      | Format số, sử dụng hàm getFakeViewCount()                               |
| 5   | Ngày tạo              | Hiển thị ngày tạo sản phẩm              | Label     | O   | -        | -            | -          | -          | Date          | -                                      | Format dd/mm/yyyy, hiển thị "Đang cập nhật" nếu không có                |
| 6   | Mô tả chi tiết        | Hiển thị mô tả chi tiết sản phẩm (HTML) | HTML      | O   | -        | -            | -          | -          | String (HTML) | "<p>Sản phẩm đang cập nhật mô tả.</p>" | Render HTML với class prose, strip HTML tags nếu cần                    |
| 7   | Link demo             | Hiển thị link demo sản phẩm (nếu có)    | Link      | O   | -        | -            | -          | 500        | String (URL)  | -                                      | Mở tab mới (target="\_blank", rel="noreferrer"), màu brand-500          |
| 8   | Thông tin người bán   | Hiển thị avatar, tên người bán          | Object    | O   | -        | -            | -          | -          | Object        | -                                      | Avatar: 14x14 rounded-2xl, fallback: chữ cái đầu, có nút "Xem shop"     |
| 9   | Nút "Mua ngay"        | Button để mua sản phẩm                  | Button    | I   | Y        | -            | -          | -          | Boolean       | false                                  | Yêu cầu đăng nhập, hiển thị confirm dialog, màu brand-500               |
| 10  | Icon đánh giá sao     | Hiển thị đánh giá sao (mặc định 5 sao)  | Label     | O   | -        | -            | -          | -          | Number        | 5                                      | Màu vàng (text-yellow-400), hiển thị 5 sao, có thể hiển thị số đánh giá |

### 14.2. Test case chính

| ID                | Mục tiêu                        | Tiền điều kiện                          | Bước thực hiện                           | Kết quả mong đợi                                                    | Priority |
| ----------------- | ------------------------------- | --------------------------------------- | ---------------------------------------- | ------------------------------------------------------------------- | -------- |
| TC-PROD-DETAIL-01 | Hiển thị thông tin sản phẩm     | -                                       | Truy cập trang chi tiết sản phẩm         | Hiển thị đầy đủ tên, giá, mô tả, hình ảnh                           | High     |
| TC-PROD-DETAIL-02 | Gallery hình ảnh                | Sản phẩm có nhiều hình                  | Xem gallery                              | Swiper slider cho phép xem nhiều hình, có pagination                | Medium   |
| TC-PROD-DETAIL-03 | Sản phẩm miễn phí               | Sản phẩm có giá = 0                     | Xem chi tiết sản phẩm miễn phí           | Hiển thị "MIỄN PHÍ" thay vì giá                                     | Medium   |
| TC-PROD-DETAIL-04 | Mô tả HTML                      | Sản phẩm có mô tả HTML                  | Xem mô tả                                | Render đúng HTML, hiển thị format đẹp                               | Medium   |
| TC-PROD-DETAIL-05 | Link demo                       | Sản phẩm có link demo                   | Click vào link demo                      | Mở link trong tab mới                                               | Low      |
| TC-PROD-DETAIL-06 | Thông tin người bán             | -                                       | Xem phần người bán                       | Hiển thị avatar (hoặc chữ cái đầu), tên người bán                   | High     |
| TC-PROD-DETAIL-07 | Nút "Xem shop"                  | -                                       | Click "Xem shop"                         | Điều hướng tới trang shop của người bán                             | Medium   |
| TC-PROD-DETAIL-08 | Mua sản phẩm khi chưa đăng nhập | User chưa đăng nhập                     | Click "Mua ngay"                         | Hiển thị thông báo yêu cầu đăng nhập, có nút chuyển tới trang login | High     |
| TC-PROD-DETAIL-09 | Mua sản phẩm khi đã đăng nhập   | User đã đăng nhập, có đủ số dư          | Click "Mua ngay", xác nhận               | Mua thành công, số dư trừ đi, hiển thị thông báo thành công         | High     |
| TC-PROD-DETAIL-10 | Mua sản phẩm không đủ số dư     | User đã đăng nhập, số dư < giá sản phẩm | Click "Mua ngay"                         | Hiển thị thông báo lỗi "Không đủ số dư"                             | High     |
| TC-PROD-DETAIL-11 | Hiển thị lượt xem               | -                                       | Xem chi tiết sản phẩm                    | Hiển thị số lượt xem (có thể là fake count)                         | Low      |
| TC-PROD-DETAIL-12 | Sản phẩm không tồn tại          | -                                       | Truy cập URL với productId không tồn tại | Hiển thị thông báo "Không tìm thấy sản phẩm", có nút quay lại       | High     |

---

**Kết thúc file**
