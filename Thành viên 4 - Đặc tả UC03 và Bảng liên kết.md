# THÀNH VIÊN 4: PHẠM CÔNG CHÁNH
## ĐẶC TẢ USE CASE 03 (XÁC NHẬN THANH TOÁN) VÀ BẢNG LIÊN KẾT YÊU CẦU

---

### 1. ĐẶC TẢ UC03 – XÁC NHẬN THANH TOÁN

**Mô tả:** Xử lý quá trình nhận tiền từ khách hàng, xác thực thông tin giao dịch qua các nền tảng (Tiền mặt, QR Code, Thẻ POS) và cập nhật trạng thái đơn hàng thành đã thanh toán.
**Actor:** 
- **Chính (Primary):** Nhân viên bán hàng
- **Phụ (Secondary):** Cổng thanh toán (Ngân hàng / Ví điện tử / Máy POS)

#### 1.1. Tiền điều kiện và Hậu điều kiện
* **Tiền điều kiện:**
  - Đơn hàng đã được tạo thành công với tổng số tiền cần thanh toán hợp lệ.
  - Các thiết bị ngoại vi (máy POS) và kết nối mạng hoạt động bình thường.
* **Hậu điều kiện:**
  - Trạng thái đơn hàng được cập nhật thành "Đã thanh toán".
  - Hệ thống ghi nhận doanh thu vào ca làm việc của nhân viên.
  - Hóa đơn tài chính được xuất và gửi cho khách hàng.

#### 1.2. Luồng sự kiện chính (Main Flow - Thanh toán qua mã QR Ví điện tử)
1. Hệ thống hiển thị tổng số tiền cần thanh toán của đơn hàng.
2. Nhân viên xác nhận với khách hàng và chọn phương thức thanh toán là quét mã QR.
3. Hệ thống tạo và hiển thị mã QR động chứa thông tin đơn hàng và số tiền.
4. Khách hàng sử dụng ứng dụng ngân hàng/ví điện tử để quét mã và xác nhận chuyển tiền.
5. Hệ thống gửi yêu cầu kiểm tra trạng thái giao dịch đến Cổng thanh toán.
6. Cổng thanh toán xử lý và trả về kết quả "Thành công".
7. Hệ thống cập nhật trạng thái đơn hàng thành "Đã thanh toán".
8. Hệ thống phát lệnh in hóa đơn cứng và thông báo giao dịch hoàn tất.

#### 1.3. Luồng thay thế (Alternate Flows)
* **Luồng thay thế 1: Thanh toán bằng Tiền mặt**
  - Tại Bước 2, khách hàng chọn thanh toán tiền mặt.
  - Nhân viên nhận tiền từ khách và nhập số tiền khách đưa vào hệ thống.
  - Hệ thống tính toán số tiền cần thối lại (nếu có) và hiển thị lên màn hình.
  - Nhân viên trả lại tiền thừa cho khách và bấm nút xác nhận hoàn thành.
  - Hệ thống chuyển thẳng sang Bước 7 của luồng chính.

* **Luồng thay thế 2: Thanh toán bằng Thẻ ngân hàng qua máy POS**
  - Tại Bước 2, khách hàng chọn quẹt thẻ POS.
  - Hệ thống đẩy dữ liệu số tiền sang máy POS kết nối.
  - Khách hàng quẹt thẻ/nhập mã PIN. Máy POS truyền tín hiệu "Thành công" lại cho hệ thống.
  - Hệ thống tiếp tục thực hiện Bước 7 của luồng chính.

#### 1.4. Luồng ngoại lệ / Tình huống thất bại (Exception Flows)
* **Ngoại lệ 1: Giao dịch bị từ chối (Sai PIN, tài khoản không đủ số dư)**
  - Cổng thanh toán trả về thông báo lỗi "Giao dịch thất bại".
  - Hệ thống phát âm thanh cảnh báo và hiển thị lý do thất bại.
  - Nhân viên yêu cầu khách hàng đổi phương thức thanh toán khác hoặc thử lại.
* **Ngoại lệ 2: Mất kết nối mạng / Hết thời gian chờ (Timeout)**
  - Hệ thống không nhận được phản hồi từ Cổng thanh toán sau 60 giây.
  - Hệ thống báo lỗi hết thời gian kết nối.
  - Nhân viên kiểm tra biến động số dư trên điện thoại/máy POS. Nếu chưa trừ tiền thì tạo lại lệnh; nếu đã trừ tiền thì thực hiện đối soát thủ công với Quản lý.

---

### 2. BẢNG LIÊN KẾT YÊU CẦU – USE CASE (REQUIREMENT TRACING MATRIX)

Bảng này đối chiếu các Yêu cầu chức năng (Functional Requirements - FR) với Use Case tương ứng để đảm bảo tính đầy đủ và bao phủ của hệ thống:

| Mã Yêu cầu (FR) | Tên Yêu cầu chức năng | Use Case tương ứng | Người chịu trách nhiệm đặc tả |
| :--- | :--- | :--- | :--- |
| **FR01** | Cho phép quét mã vạch và thêm sản phẩm vào đơn | UC01 – Đặt hàng | Nguyễn Lê Uyên |
| **FR02** | Tính tổng tiền tạm tính và áp dụng mã giảm giá | UC01 – Đặt hàng | Nguyễn Lê Uyên |
| **FR03** | Tiếp nhận và xử lý yêu cầu hủy đơn hàng | UC02 – Hủy đơn hàng | Nguyễn Minh Hiếu |
| **FR04** | Kiểm tra điều kiện hủy đơn (chưa giao vận chuyển) | UC02 – Hủy đơn hàng | Nguyễn Minh Hiếu |
| **FR05** | Hỗ trợ đa dạng phương thức thanh toán (Tiền mặt, QR, POS) | UC03 – Xác nhận thanh toán | Phạm Công Chánh |
| **FR06** | Xác thực giao dịch thanh toán tự động qua Cổng thanh toán | UC03 – Xác nhận thanh toán | Phạm Công Chánh |
| **FR07** | Xử lý các ngoại lệ thanh toán (Timeout, Thất bại) | UC03 – Xác nhận thanh toán | Phạm Công Chánh |
| **FR08** | In hóa đơn và cập nhật trạng thái đơn hàng | UC03 – Xác nhận thanh toán | Phạm Công Chánh |
