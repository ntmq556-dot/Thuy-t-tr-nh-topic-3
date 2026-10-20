# THÀNH VIÊN 3: NGUYỄN MINH HIẾU
## ĐẶC TẢ USE CASE 02 (HỦY ĐƠN HÀNG) VÀ BẢNG LIÊN KẾT YÊU CẦU

---

## 1. Tổng quan Use Case 02: Hủy đơn hàng (Cancel Order)

* **Tên Use Case:** UC02 – Hủy đơn hàng
* **Mục tiêu người dùng (User Goal):** Cho phép người dùng dừng giao dịch đơn hàng đã khởi tạo, giải quyết các rủi ro nghiệp vụ liên quan đến quyền lợi tài chính (hoàn tiền) và cập nhật lại trạng thái tồn kho của hệ thống.
* **Ranh giới hệ thống (System Boundary):** Thuộc Hệ thống Bán hàng Online (E-commerce Platform).
* **Danh sách Tác nhân (Actors) liên quan:**
  * **Tác nhân chính (Primary Actor):** 
    * Khách hàng (Customer): Khởi tạo yêu cầu hủy đơn hàng đã đặt.
    * Nhân viên / Quản trị viên (Staff / Admin): Tiếp nhận, kiểm tra và phê duyệt/xử lý yêu cầu hủy đơn.
  * **Tác nhân phụ (Secondary Actor - Hệ thống bên ngoài):** 
    * Hệ thống thanh toán (Payment Gateway - VNPay/Momo/Thẻ ngân hàng): Tiếp nhận yêu cầu và xử lý giao dịch hoàn tiền tự động.
    * Đơn vị vận chuyển (Shipping Partner - GHTK/GHN/Viettel Post): Tiếp nhận thông báo hủy đơn khi đơn đã trong luồng giao vận và thực hiện chuyển hoàn.

---

## 2. Tiền điều kiện & Hậu điều kiện (Preconditions & Postconditions)

* **Tiền điều kiện (Preconditions):**
  1. Đơn hàng tồn tại hợp lệ trên Hệ thống Bán hàng Online.
  2. Người dùng đã đăng nhập vào hệ thống với tài khoản hợp lệ (Khách hàng sở hữu đơn hàng hoặc Nhân viên/Admin có thẩm quyền).
* **Hậu điều kiện (Postconditions):**
  1. Trạng thái đơn hàng trên hệ thống được cập nhật thành **"Đã hủy"**.
  2. Kích hoạt Use Case bổ trợ: **Cập nhật tồn kho** (Số lượng sản phẩm trong đơn hủy được tự động cộng trả lại vào kho).
  3. Kích hoạt Use Case bổ trợ: **Xử lý hoàn tiền** (Nếu đơn hàng đã hoàn tất thanh toán trước đó).
  4. Hệ thống phát thông báo/email xác nhận hủy đơn thành công gửi tới Khách hàng.

---

## 3. Luồng sự kiện (Flow of Events)

### 3.1. Luồng sự kiện chính (Basic Flow / Main Success Scenario)
*(Kịch bản hủy đơn hàng thành công trước khi bàn giao cho Đơn vị vận chuyển)*

1. Khách hàng (hoặc Nhân viên) truy cập danh sách đơn hàng và chọn đơn hàng cần hủy.
2. Người dùng nhấn nút "Yêu cầu hủy đơn".
3. Hệ thống kiểm tra trạng thái đơn hàng (Xác nhận đơn hàng chưa bàn giao cho Đơn vị vận chuyển).
4. Hệ thống hiển thị biểu mẫu yêu cầu lý do hủy đơn.
5. Người dùng chọn/nhập lý do hủy (ví dụ: Đổi ý, Thay đổi địa chỉ, Đặt nhầm sản phẩm...) và bấm xác nhận.
6. Hệ thống chuyển trạng thái đơn hàng thành **"Đã hủy"**.
7. Hệ thống tự động kích hoạt Use Case bổ trợ **Cập nhật tồn kho** để cộng trả số lượng sản phẩm về lại kho hàng.
8. Hệ thống hiển thị thông báo "Hủy đơn hàng thành công" và gửi email xác nhận cho Khách hàng.

### 3.2. Các luồng thay thế (Alternate Flows)

* **A1: Hủy đơn hàng đã thanh toán thành công (Kích hoạt Xử lý hoàn tiền)**
  * Tại Bước 6 của luồng chính, hệ thống phát hiện đơn hàng đã được thanh toán qua Cổng thanh toán (UC03).
  * Hệ thống tự động kích hoạt Use Case bổ trợ **Xử lý hoàn tiền**, gửi lệnh hoàn tiền sang Cổng thanh toán (VNPay/Momo/Thẻ ngân hàng).
  * Cổng thanh toán xử lý và trả về phản hồi giao dịch hoàn tiền "Thành công".
  * Hệ thống cập nhật trạng thái đơn hàng thành **"Đã hủy - Đã hoàn tiền"** và tiếp tục Bước 7 của luồng chính.

* **A2: Đơn hàng đã bàn giao cho Đơn vị vận chuyển**
  * Tại Bước 3 của luồng chính, hệ thống kiểm tra thấy đơn hàng đang ở trạng thái "Đã bàn giao vận chuyển".
  * Hệ thống gửi yêu cầu hủy đơn tự động qua API kết nối với **Đơn vị vận chuyển (GHTK/GHN/Viettel Post)**.
  * Đơn vị vận chuyển xác nhận yêu cầu, cập nhật trạng thái đơn thành "Hủy giao - Chuyển hoàn" và trả phản hồi về hệ thống.
  * Hệ thống ghi nhận phản hồi và tiếp tục chuyển sang Bước 6 để xử lý hoàn tiền/kho.

### 3.3. Các luồng ngoại lệ (Exception Flows)

* **E1: Đơn hàng đã giao thành công (Không đủ điều kiện hủy)**
  * Tại Bước 3 của luồng chính, hệ thống phát hiện đơn hàng đã ở trạng thái "Đã giao hàng thành công".
  * Hệ thống từ chối yêu cầu hủy đơn và hiển thị thông báo: *"Đơn hàng đã giao thành công, không thể hủy đơn. Vui lòng sử dụng chức năng Yêu cầu Trả hàng / Hoàn tiền"*.

* **E2: Mất kết nối API với Cổng thanh toán hoặc Đơn vị vận chuyển (Timeout / Lỗi mạng)**
  * Tại luồng A1 hoặc A2, hệ thống không nhận được phản hồi từ hệ thống đối tác bên ngoài sau 60 giây.
  * Hệ thống cập nhật trạng thái đơn hàng thành **"Đã hủy - Chờ đối soát thủ công"**.
  * Hệ thống tự động tạo cảnh báo lên màn hình quản trị của Nhân viên/Admin để xử lý liên hệ đối soát thủ công.
