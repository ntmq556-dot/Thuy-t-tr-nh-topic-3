# TÀI LIỆU ĐẶC TẢ YÊU CẦU PHẦN MỀM (SRS)
## HỆ THỐNG BÁN HÀNG ONLINE (E-COMMERCE PLATFORM)
**Tiêu chuẩn áp dụng:** ISO/IEC/IEEE 29148:2018  
**Phiên bản:** 1.0  
**Ngày lập:** 22/10/2026  

---

## 1. GIỚI THIỆU (INTRODUCTION)

### 1.1 Mục đích (Purpose)
Tài liệu này xác định các yêu cầu chức năng, tác nhân, ranh giới hệ thống và đặc tả chi tiết các Use Case cho **Hệ thống Bán hàng Online (E-commerce Platform)**. Tài liệu làm cơ sở cho đội ngũ phát triển, kiểm thử (QA/QC) và các bên liên quan (Stakeholders) triển khai và nghiệm thu hệ thống.

### 1.2 Phạm vi hệ thống (System Scope)
* **Tên hệ thống:** Hệ thống Bán hàng Online (E-commerce Platform).
* **Ranh giới & Phạm vi:**
  * **Chức năng nội bộ:** Quản lý quy trình từ xem/tìm kiếm sản phẩm, đặt hàng, xử lý thanh toán, cập nhật trạng thái đơn hàng đến tiếp nhận và xử lý hủy đơn hàng (hoàn tiền, cập nhật kho).
  * **Tương tác ngoại vi:** Tích hợp với người dùng cuối (*Khách hàng, Nhân viên/Admin*) và hệ thống đối tác bên ngoài (*Cổng thanh toán, Đơn vị vận chuyển*) thông qua API.

### 1.3 Thuật ngữ & Tóm tắt (Definitions and Abbreviations)
* **SRS:** Software Requirements Specification (Đặc tả yêu cầu phần mềm).
* **FR:** Functional Requirement (Yêu cầu chức năng).
* **UC:** Use Case (Kịch bản sử dụng).
* **POS:** Point of Sale (Máy chấp nhận thanh toán thẻ/điểm bán hàng).
* **COD:** Cash on Delivery (Thanh toán khi nhận hàng).
* **RTM:** Requirements Traceability Matrix (Bảng liên kết vết yêu cầu).

---

## 2. MÔ TẢ TỔNG QUAN (OVERALL DESCRIPTION)

### 2.1 Bối cảnh hệ thống (System Context)
Hệ thống đóng vai trò làm trung gian kết nối giữa Khách hàng mua sắm, Nhân viên vận hành nội bộ và các bên đối tác tài chính / logistics thứ ba.

### 2.2 Tác nhân hệ thống (System Actors)

#### A. Tác nhân chính (Primary Actors - Con người)
1. **Khách hàng (Customer):**
   * **Vai trò:** Người tiêu dùng thực hiện mua sắm trên nền tảng.
   * **Mục tiêu:** Tìm kiếm, xem sản phẩm, thực hiện đặt hàng, tiến hành thanh toán và yêu cầu hủy đơn khi có nhu cầu.
2. **Nhân viên / Quản trị viên (Staff / Admin):**
   * **Vai trò:** Người quản lý, vận hành và xử lý nghiệp vụ đơn hàng.
   * **Mục tiêu:** Kiểm tra và xác nhận đơn hàng, duyệt/xử lý yêu cầu hủy đơn, cập nhật trạng thái đơn hàng, bàn giao vận chuyển và xác nhận thanh toán.

#### B. Tác nhân phụ (Secondary Actors - Hệ thống bên ngoài)
1. **Hệ thống thanh toán (Payment Gateway - VNPay/Momo/Thẻ ngân hàng):**
   * **Vai trò:** Đối tác thanh toán tài chính tự động.
   * **Mục tiêu:** Tiếp nhận giao dịch thanh toán/hoàn tiền, xác thực tài khoản và trả về kết quả trạng thái.
2. **Đơn vị vận chuyển (Shipping Partner - GHTK/GHN/Viettel Post):**
   * **Vai trò:** Đối tác hậu cần logistics.
   * **Mục tiêu:** Tiếp nhận thông tin giao đơn, nhận thông báo hủy giao/chuyển hoàn và cập nhật trạng thái vận chuyển theo thời gian thực.

### 2.3 Phân định Mục tiêu người dùng vs. Thao tác UI (User Goals vs. UI Interactions)
Theo quy chuẩn 29148 & UML:
* **Mục tiêu người dùng (Use Cases độc lập):** Đặt hàng, Xác nhận thanh toán, Hủy đơn hàng, Tìm kiếm & Xem sản phẩm, Cập nhật trạng thái đơn hàng.
* **Thao tác giao diện UI/UX (Không phải Use Case):** Bấm nút "Thêm vào giỏ hàng", Nhập ô tìm kiếm, Đăng nhập/Đăng xuất, Bấm "Xác nhận".

---

## 3. DANH SÁCH YÊU CẦU CHỨC NĂNG (FUNCTIONAL REQUIREMENTS)

| Mã Yêu cầu | Tên Yêu cầu Chức năng | Mức độ ưu tiên | Use Case Liên kết |
| :--- | :--- | :--- | :--- |
| **FR01** | Cho phép quét mã vạch và thêm sản phẩm vào đơn | High | UC01 – Đặt hàng |
| **FR02** | Tính tổng tiền tạm tính và áp dụng mã giảm giá | High | UC01 – Đặt hàng |
| **FR03** | Tiếp nhận và xử lý yêu cầu hủy đơn hàng | High | UC02 – Hủy đơn hàng |
| **FR04** | Kiểm tra điều kiện hủy đơn (chưa giao vận chuyển) | High | UC02 – Hủy đơn hàng |
| **FR05** | Hỗ trợ đa dạng phương thức thanh toán (Tiền mặt, QR, POS) | High | UC03 – Xác nhận thanh toán |
| **FR06** | Xác thực giao dịch thanh toán tự động qua Cổng thanh toán | High | UC03 – Xác nhận thanh toán |
| **FR07** | Xử lý các ngoại lệ thanh toán (Timeout, Thất bại) | Medium | UC03 – Xác nhận thanh toán |
| **FR08** | In hóa đơn và cập nhật trạng thái đơn hàng | High | UC03 – Xác nhận thanh toán |

---

## 4. ĐẶC TẢ CHI TIẾT CÁC USE CASE (USE CASE SPECIFICATIONS)

---

### 4.1 Use Case UC01: Đặt hàng (Place Order)

* **Mã Use Case:** UC01
* **Tên Use Case:** Đặt hàng (Place Order)
* **Tác nhân chính (Primary Actor):** Khách hàng (Customer)
* **Tác nhân phụ (Secondary Actor):** Hệ thống thanh toán (Payment Gateway / Third-party)
* **Mô tả (Description):** Cho phép Khách hàng chọn sản phẩm từ giỏ hàng, nhập/xác nhận thông tin giao hàng, chọn phương thức thanh toán và hoàn tất khởi tạo đơn hàng mới.
* **Tiền điều kiện (Preconditions):**
  1. Khách hàng đã đăng nhập (hoặc hệ thống cho phép đặt hàng với tư cách khách vãng lai).
  2. Giỏ hàng có ít nhất 01 sản phẩm hợp lệ.
* **Hậu điều kiện (Postconditions):**
  1. Đơn hàng mới được lưu thành công với trạng thái ban đầu (*Chờ xác nhận / Chờ thanh toán*).
  2. Tồn kho sản phẩm được tự động trừ bớt.
  3. Giỏ hàng hiện tại của Khách hàng được xóa sạch.
  4. Thông báo/Email xác nhận đơn hàng gửi tới Khách hàng.

#### Luồng sự kiện (Flow of Events):

##### Luồng chính (Basic Flow / Main Success Scenario):
1. Khách hàng truy cập Giỏ hàng và chọn "Tiến hành Đặt hàng".
2. Hệ thống kiểm tra số lượng tồn kho và tính khả dụng của sản phẩm.
3. Hệ thống hiển thị màn hình Thanh toán/Xác nhận đơn hàng (sản phẩm, đơn giá, địa chỉ mặc định, phương thức vận chuyển và thanh toán).
4. Khách hàng chọn/nhập địa chỉ nhận hàng và thông tin liên hệ.
5. Khách hàng chọn đơn vị vận chuyển và phương thức thanh toán (COD, Chuyển khoản, Ví điện tử,...).
6. Khách hàng áp dụng mã giảm giá / khuyến mãi (nếu có).
7. Hệ thống tính toán tổng chi phí ($\text{Tổng} = \text{Tiền hàng} + \text{Phí vận chuyển} - \text{Khuyến mãi}$).
8. Khách hàng nhấn nút "Đặt hàng".
9. Hệ thống khởi tạo đơn hàng, cập nhật tồn kho, làm sạch giỏ hàng và hiển thị màn hình "Đặt hàng thành công" kèm Mã đơn hàng (Order ID).

##### Các luồng thay thế (Alternative Flows):
* **A1: Thay đổi địa chỉ / thông tin giao hàng:**
  * Tại Bước 4, Khách hàng chọn "Thêm địa chỉ mới" hoặc chỉnh sửa địa chỉ.
  * Hệ thống lưu thông tin và tái tính toán phí vận chuyển ở Bước 7.
* **A2: Thanh toán trực tuyến (Ví điện tử / Thẻ / QR Code):**
  * Tại Bước 5, Khách hàng chọn thanh toán trực tuyến.
  * Sau Bước 8, Hệ thống chuyển hướng sang Cổng thanh toán.
  * Khách hàng giao dịch thành công; Cổng thanh toán phản hồi "Thành công".
  * Hệ thống thực hiện Bước 9 với trạng thái đơn là **"Đã thanh toán"**.

##### Các luồng ngoại lệ (Exception Flows):
* **E1: Sản phẩm hết hàng hoặc không đủ số lượng tồn:**
  * Tại Bước 2, Hệ thống phát hiện sản phẩm vượt quá tồn kho.
  * Hệ thống báo lỗi, đánh dấu sản phẩm thiếu hụt và yêu cầu cập nhật giỏ hàng.
* **E2: Thanh toán trực tuyến thất bại:**
  * Tại Luồng A2, giao dịch bị từ chối hoặc hết thời gian chờ (timeout).
  * Cổng thanh toán phản hồi lỗi; Hệ thống lưu đơn ở trạng thái *Chờ thanh toán / Bị hủy do lỗi thanh toán* và cho phép "Thử lại thanh toán".
* **E3: Mã giảm giá không hợp lệ / Hết hạn:**
  * Tại Bước 6, mã giảm giá không thỏa mãn điều kiện.
  * Hệ thống báo "Mã không hợp lệ" và giữ nguyên tổng tiền ban đầu.

---

### 4.2 Use Case UC02: Hủy đơn hàng (Cancel Order)

* **Mã Use Case:** UC02
* **Tên Use Case:** Hủy đơn hàng (Cancel Order)
* **Tác nhân chính (Primary Actor):** Khách hàng (Customer), Nhân viên / Quản trị viên (Staff / Admin)
* **Tác nhân phụ (Secondary Actor):** Hệ thống thanh toán (Payment Gateway), Đơn vị vận chuyển (Shipping Partner)
* **Mô tả (Description):** Cho phép hủy đơn hàng đã khởi tạo, giải quyết hoàn tiền tài chính và cập nhật trả lại tồn kho.
* **Tiền điều kiện (Preconditions):**
  1. Đơn hàng tồn tại hợp lệ trong hệ thống.
  2. Người dùng đã đăng nhập tài khoản có thẩm quyền (chủ đơn hàng hoặc Staff/Admin).
* **Hậu điều kiện (Postconditions):**
  1. Trạng thái đơn chuyển thành **"Đã hủy"**.
  2. Tự động kích hoạt Use Case bổ trợ *Cập nhật tồn kho* (cộng trả lại sản phẩm).
  3. Kích hoạt Use Case bổ trợ *Xử lý hoàn tiền* (nếu đã thanh toán).
  4. Phát email/thông báo xác nhận hủy đơn thành công.

#### Luồng sự kiện (Flow of Events):

##### Luồng chính (Basic Flow - Hủy đơn chưa bàn giao vận chuyển):
1. Người dùng truy cập danh sách đơn hàng và chọn đơn cần hủy.
2. Chọn "Yêu cầu hủy đơn".
3. Hệ thống kiểm tra trạng thái (đơn chưa bàn giao cho Đơn vị vận chuyển).
4. Hệ thống hiển thị biểu mẫu nhập lý do hủy đơn.
5. Người dùng chọn/nhập lý do hủy và xác nhận.
6. Hệ thống chuyển trạng thái đơn hàng thành **"Đã hủy"**.
7. Hệ thống tự động kích hoạt UC *Cập nhật tồn kho* để cộng lại số lượng vào kho.
8. Hiển thị thông báo "Hủy đơn hàng thành công" và gửi email xác nhận.

##### Các luồng thay thế (Alternative Flows):
* **A1: Hủy đơn hàng đã thanh toán thành công (Kích hoạt Hoàn tiền):**
  * Tại Bước 6, hệ thống nhận diện đơn đã thanh toán thành công trước đó.
  * Hệ thống tự động kích hoạt UC *Xử lý hoàn tiền*, gửi lệnh hoàn tiền sang Cổng thanh toán.
  * Cổng thanh toán xử lý và phản hồi "Thành công".
  * Trạng thái đơn cập nhật thành **"Đã hủy - Đã hoàn tiền"**, tiếp tục Bước 7 luồng chính.
* **A2: Đơn hàng đã bàn giao cho Đơn vị vận chuyển:**
  * Tại Bước 3, đơn hàng đang ở trạng thái "Đã bàn giao vận chuyển".
  * Hệ thống gửi yêu cầu hủy giao tự động qua API tới Đơn vị vận chuyển.
  * Đơn vị vận chuyển xác nhận, chuyển trạng thái "Hủy giao - Chuyển hoàn".
  * Hệ thống ghi nhận phản hồi và chuyển sang Bước 6.

##### Các luồng ngoại lệ (Exception Flows):
* **E1: Đơn hàng đã giao thành công (Không đủ điều kiện hủy):**
  * Tại Bước 3, đơn hàng đã ở trạng thái "Đã giao hàng thành công".
  * Hệ thống từ chối yêu cầu hủy và thông báo: *"Đơn hàng đã giao thành công, không thể hủy đơn. Vui lòng sử dụng chức năng Yêu cầu Trả hàng / Hoàn tiền"*.
* **E2: Mất kết nối API bên thứ ba (Timeout / Lỗi mạng):**
  * Tại luồng A1 hoặc A2, không nhận được phản hồi kết nối sau 60 giây.
  * Hệ thống đổi trạng thái thành **"Đã hủy - Chờ đối soát thủ công"**.
  * Tạo cảnh báo lên hệ thống quản trị để Nhân viên/Admin đối soát thủ công.

---

### 4.3 Use Case UC03: Xác nhận thanh toán (Confirm Payment)

* **Mã Use Case:** UC03
* **Tên Use Case:** Xác nhận thanh toán (Confirm Payment)
* **Tác nhân chính (Primary Actor):** Nhân viên bán hàng (Staff)
* **Tác nhân phụ (Secondary Actor):** Cổng thanh toán (Ngân hàng / Ví điện tử / Máy POS)
* **Mô tả (Description):** Tiếp nhận thanh toán, xác thực giao dịch đa kênh (Tiền mặt, QR, POS) và chuyển trạng thái đơn hàng thành đã thanh toán.
* **Tiền điều kiện (Preconditions):**
  1. Đơn hàng được khởi tạo hợp lệ với tổng tiền chính xác.
  2. Thiết bị ngoại vi (máy POS) và kết nối mạng hoạt động bình thường.
* **Hậu điều kiện (Postconditions):**
  1. Đơn hàng cập nhật trạng thái **"Đã thanh toán"**.
  2. Doanh thu ghi nhận vào ca làm việc của Nhân viên.
  3. Xuất và gửi hóa đơn tài chính cho khách.

#### Luồng sự kiện (Flow of Events):

##### Luồng chính (Main Flow - Thanh toán qua mã QR Ví điện tử):
1. Hệ thống hiển thị tổng chi phí cần thanh toán.
2. Nhân viên xác nhận với khách và chọn thanh toán Quét mã QR.
3. Hệ thống tạo và hiển thị mã QR động chứa thông tin đơn hàng và số tiền.
4. Khách hàng dùng ứng dụng Ngân hàng/Ví điện tử quét mã và xác nhận chuyển tiền.
5. Hệ thống gửi yêu cầu xác thực tới Cổng thanh toán.
6. Cổng thanh toán kiểm tra và phản hồi "Thành công".
7. Hệ thống cập nhật trạng thái đơn thành **"Đã thanh toán"**.
8. Hệ thống xuất lệnh in hóa đơn cứng và thông báo hoàn tất.

##### Các luồng thay thế (Alternative Flows):
* **Luồng thay thế 1: Thanh toán Tiền mặt:**
  * Tại Bước 2, chọn thanh toán Tiền mặt.
  * Nhân viên nhận tiền mặt và nhập số tiền khách đưa.
  * Hệ thống tính toán và hiển thị tiền thừa thối lại.
  * Nhân viên thối tiền thừa và bấm xác nhận hoàn tất.
  * Hệ thống chuyển đến Bước 7 luồng chính.
* **Luồng thay thế 2: Thanh toán Thẻ ngân hàng qua máy POS:**
  * Tại Bước 2, chọn thanh toán POS.
  * Hệ thống truyền dữ liệu số tiền sang máy POS.
  * Khách quẹt thẻ/nhập mã PIN; Máy POS gửi tín hiệu "Thành công" về hệ thống.
  * Chuyển đến Bước 7 luồng chính.

##### Các luồng ngoại lệ (Exception Flows):
* **Ngoại lệ 1: Giao dịch bị từ chối (Sai PIN, tài khoản không đủ số dư):**
  * Cổng thanh toán phản hồi "Giao dịch thất bại".
  * Hệ thống báo động âm thanh và hiển thị lý do thất bại.
  * Nhân viên đề nghị khách đổi phương thức thanh toán hoặc thực hiện lại.
* **Ngoại lệ 2: Mất kết nối mạng / Hết thời gian chờ (Timeout):**
  * Không nhận được phản hồi sau 60 giây.
  * Hệ thống báo lỗi hết thời gian kết nối.
  * Nhân viên kiểm tra biến động tài khoản/máy POS: Nếu chưa trừ tiền thì tạo lệnh mới; nếu đã trừ tiền thì đối soát thủ công với Quản lý.

---

## 5. BẢNG LIÊN KẾT VẾT YÊU CẦU (REQUIREMENTS TRACEABILITY MATRIX - RTM)

Bảng RTM bảo đảm tính bao phủ (coverage) giữa Yêu cầu chức năng (FR) và đặc tả Use Case (ISO/IEC/IEEE 29148):

| Mã FR | Tên Yêu cầu Chức năng | Use Case áp dụng | Tác nhân liên quan | Phụ trách đặc tả |
| :--- | :--- | :--- | :--- | :--- |
| **FR01** | Quét mã vạch và thêm sản phẩm vào đơn | UC01 – Đặt hàng | Khách hàng | Nguyễn Lê Uyên |
| **FR02** | Tính tổng tiền tạm tính và áp dụng khuyến mãi | UC01 – Đặt hàng | Khách hàng | Nguyễn Lê Uyên |
| **FR03** | Tiếp nhận và xử lý yêu cầu hủy đơn hàng | UC02 – Hủy đơn hàng | Khách hàng, Staff/Admin | Nguyễn Minh Hiếu |
| **FR04** | Kiểm tra điều kiện hủy đơn (chưa giao vận) | UC02 – Hủy đơn hàng | Khách hàng, Staff/Admin | Nguyễn Minh Hiếu |
| **FR05** | Hỗ trợ phương thức thanh toán đa dạng (Tiền mặt, QR, POS) | UC03 – Xác nhận thanh toán | Nhân viên, Cổng thanh toán | Phạm Công Chánh |
| **FR06** | Tự động xác thực thanh toán qua Cổng thanh toán | UC03 – Xác nhận thanh toán | Cổng thanh toán | Phạm Công Chánh |
| **FR07** | Xử lý ngoại lệ giao dịch (Timeout, Thất bại) | UC03 – Xác nhận thanh toán | Nhân viên, Cổng thanh toán | Phạm Công Chánh |
| **FR08** | In hóa đơn và cập nhật trạng thái đơn | UC03 – Xác nhận thanh toán | Nhân viên | Phạm Công Chánh |