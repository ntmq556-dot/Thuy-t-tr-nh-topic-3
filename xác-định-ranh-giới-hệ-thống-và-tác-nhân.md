# Tài liệu Phân tích & Mô hình hóa Use Case
**Hệ thống:** Hệ thống Bán hàng Online (E-commerce Platform)

---

## 1. Ranh giới hệ thống (System Boundary)

* **Tên hệ thống:** Hệ thống Bán hàng Online (E-commerce Platform).
* **Phạm vi hệ thống:**
  * **Chức năng nội bộ:** Bao gồm các chức năng quản lý từ khâu duyệt sản phẩm, đặt hàng, xử lý thanh toán, cập nhật trạng thái đơn hàng đến quy trình tiếp nhận và xử lý hủy đơn hàng.
  * **Tương tác bên ngoài:** Kết nối và tương tác trực tiếp với người dùng (*Khách hàng, Nhân viên*) và các hệ thống đối tác bên ngoài (*Cổng thanh toán, Đơn vị vận chuyển*).

---

## 2. Danh sách Tác nhân (Actors)

### A. Tác nhân chính (Con người - Trực tiếp sử dụng hệ thống)
1. **Khách hàng (Customer):**
   * **Vai trò:** Người mua sắm sản phẩm trên nền tảng.
   * **Mục tiêu:** Tìm kiếm và xem thông tin sản phẩm, thực hiện đặt hàng, tiến hành thanh toán và yêu cầu hủy đơn hàng khi phát sinh nhu cầu.
2. **Nhân viên / Quản trị viên (Admin / Staff):**
   * **Vai trò:** Người quản lý và vận hành hệ thống bán hàng.
   * **Mục tiêu:** Kiểm tra và xác nhận đơn hàng, duyệt/xử lý yêu cầu hủy đơn của khách hàng, cập nhật trạng thái đơn hàng và chuyển thông tin cho bên vận chuyển.

### B. Tác nhân phụ (Hệ thống bên ngoài - Kết nối tự động)
1. **Hệ thống thanh toán (Payment Gateway - VNPay/Momo/Thẻ ngân hàng):**
   * **Vai trò:** Đối tác tài chính bên ngoài.
   * **Mục tiêu:** Nhận yêu cầu giao dịch, xác thực thông tin tài khoản và trả về kết quả xác nhận thanh toán (thành công hoặc thất bại) cho hệ thống.
2. **Đơn vị vận chuyển (Shipping Partner - GHTK/GHN/Viettel Post):**
   * **Vai trò:** Đối tác logistics bên ngoài.
   * **Mục tiêu:** Nhận thông tin bàn giao đơn hàng, nhận thông báo hủy đơn khi đơn đã trong luồng giao, và trả về trạng thái vận chuyển thời gian thực cho hệ thống.

---

## 3. Phân biệt Mục tiêu người dùng vs. Thao tác giao diện

Để sơ đồ Use Case đạt chuẩn UML và không bị sai bản chất nghiệp vụ, hệ thống phân biệt rõ ràng:

* **Mục tiêu người dùng (Đưa vào sơ đồ Use Case):**
  * **Đặt hàng:** Mua được hàng.
  * **Xác nhận thanh toán:** Hoàn tất nghĩa vụ tài chính.
  * **Hủy đơn hàng:** Dừng giao dịch và giải quyết quyền lợi hoàn tiền/kho.
  * **Tìm kiếm & Xem sản phẩm:** Tra cứu thông tin hàng hóa.
  * **Cập nhật trạng thái đơn hàng:** Theo dõi tiến trình đơn.
* **Thao tác giao diện (KHÔNG đưa vào sơ đồ Use Case):**
  * Bấm nút "Thêm vào giỏ hàng", Nhập ô tìm kiếm, Đăng nhập/Đăng xuất, Bấm nút "Xác nhận". *(Các thao tác này thuộc về thiết kế UI/UX, không phải Use Case độc lập).*

---

## 4. Danh sách các Use Case

### 3 Use Case Cốt lõi (Trọng tâm đề tài)
1. **Đặt hàng:** Cho phép khách hàng khởi tạo đơn hàng và chuyển sang bước thanh toán.
2. **Xác nhận thanh toán:** Xử lý xác nhận giao dịch tài chính cho đơn hàng qua cổng thanh toán hoặc phương thức COD.
3. **Hủy đơn hàng:** Xử lý bài toán hủy đơn (kể cả khi đơn đã bàn giao vận chuyển), giải quyết rủi ro nghiệp vụ và đảm bảo kết quả hệ thống (hoàn tiền, cập nhật kho).

### Các Use Case Bổ trợ
* Tìm kiếm sản phẩm
* Xem sản phẩm
* Cập nhật trạng thái đơn hàng
* Cập nhật tồn kho *(Xử lý sau khi hủy đơn thành công)*
* Xử lý hoàn tiền *(Xử lý sau khi hủy đơn đã thanh toán)*

## Sơ đồ Use Case tổng thể 

<img width="733" height="682" alt="sodotongthe drawio" src="https://github.com/user-attachments/assets/553733d2-283b-43c6-a6ce-00efda4a59a7" />


