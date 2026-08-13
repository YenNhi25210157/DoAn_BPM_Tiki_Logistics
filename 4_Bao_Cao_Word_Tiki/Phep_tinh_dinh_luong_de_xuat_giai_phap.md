# BÁO CÁO PHÂN TÍCH VÀ CẢI TIẾN QUY TRÌNH LOGISTICS (TIKI LOGISTICS)

---

## 1. PHÂN TÍCH ĐỊNH LƯỢNG MÔ HÌNH HIỆN TẠI (AS-IS)

### 1.1. Thời gian (Time)
* **Thời gian xử lý thực (VA):** 
  $$\text{VA} = \text{Hạ hàng (2 phút)} + \text{Quét tự động (0.5 phút)} + \text{Đóng bao (3 phút)} = 5.5 \text{ phút}$$
* **Thời gian chờ / thao tác thừa (NVA + BVA):** 
  $$\text{NVA + BVA} = \text{Quét tay PDA (1.5 phút)} + \text{Đồng bộ trễ (2 phút)} = 3.5 \text{ phút}$$
* **Thời gian chu kỳ (Cycle Time - CT):** 
  $$\text{CT}_{\text{As-Is}} = 5.5 + 3.5 = 9 \text{ phút}$$
* **Hiệu suất thời gian (Cycle Time Efficiency - CTE):** 
  $$\text{CTE}_{\text{As-Is}} = \left(\frac{5.5}{9}\right) \times 100\% = 61.1\% \quad (\text{Cần cải thiện})$$

### 1.2. Chi phí (Cost)
* **Mức lương nhân viên kho trung bình:** $30,000\text{ VNĐ/giờ}$.
* **Thời gian tiêu tốn cho mỗi đơn hàng:** $9\text{ phút}$.
* **Chi phí nhân sự trực tiếp / đơn hàng:** 
  $$\text{Chi phí}_{\text{As-Is}} = \left(\frac{9}{60}\right) \times 30,000 = 4,500\text{ VNĐ/đơn}$$

### 1.3. Chất lượng (Quality)
* **Tỷ lệ lỗi quét nhầm mã vạch PDA:** $4.2\%$ *(Mục tiêu sau cải tiến $< 1\%$)*.
* **Tỷ lệ tắc nghẽn băng chuyền do hàng quá khổ:** $2.1\%$.

---

## 2. DỰ PHÓNG ĐỊNH LƯỢNG MÔ HÌNH TƯƠNG LAI (TO-BE)

Khi áp dụng **Camera AI** tự động đọc mã/kích thước và **Cổng Self-service**, quy trình loại bỏ hoàn toàn việc quét tay PDA và độ trễ đồng bộ.

### 2.1. Thời gian (Time)
* **Thời gian xử lý thực (VA):** 
  $$\text{VA}_{\text{To-Be}} = \text{Hạ hàng (2 phút)} + \text{Quét Camera AI (0.1 phút)} + \text{Đóng bao (2.5 phút)} = 4.6 \text{ phút}$$
* **Thời gian chờ / thao tác thừa (NVA + BVA):** 
  $$\text{NVA + BVA}_{\text{To-Be}} = \text{Xử lý tại Cổng Self-service (0.4 phút)} = 0.4 \text{ phút}$$
  *(Eliminate hoàn toàn quét PDA 1.5 phút và đồng bộ trễ 2 phút)*
* **Thời gian chu kỳ (Cycle Time - CT):** 
  $$\text{CT}_{\text{To-Be}} = 4.6 + 0.4 = 5 \text{ phút} \quad (\text{Giảm 44.4\% so với As-Is})$$
* **Hiệu suất thời gian (CTE):** 
  $$\text{CTE}_{\text{To-Be}} = \left(\frac{4.6}{5}\right) \times 100\% = 92\% \quad (\text{Tăng từ 61.1\% lên 92\%})$$

### 2.2. Chi phí (Cost)
* **Thời gian tiêu tốn cho mỗi đơn hàng:** $5\text{ phút}$.
* **Chi phí nhân sự trực tiếp / đơn hàng:** 
  $$\text{Chi phí}_{\text{To-Be}} = \left(\frac{5}{60}\right) \times 30,000 = 2,500\text{ VNĐ/đơn}$$
  *(Tiết kiệm $2,000\text{ VNĐ/đơn}$, cắt giảm $44.4\%$ chi phí nhân sự)*

### 2.3. Chất lượng (Quality)
* **Tỷ lệ lỗi quét nhầm mã vạch:** Giảm từ $4.2\%$ xuống $< 0.5\%$.
* **Tỷ lệ tắc nghẽn băng chuyền:** Giảm từ $2.1\%$ xuống $< 0.2\%$ nhờ phân loại kích thước chủ động.

---

## 3. BẢNG SO SÁNH HIỆU QUẢ VẬN HÀNH (AS-IS vs. TO-BE)

| Tiêu chí phân tích | Mô hình As-Is | Mô hình To-Be | Mức độ cải thiện |
| :--- | :--- | :--- | :--- |
| **Cycle Time (CT)** | 9 phút | 5 phút | **Giảm 44.4%** |
| **Hiệu suất CTE** | 61.1% | 92.0% | **Tăng 30.9%** |
| **Chi phí nhân sự / đơn** | 4,500 VNĐ | 2,500 VNĐ | **Tiết kiệm 2,000 VNĐ (-44.4%)** |
| **Tỷ lệ lỗi quét mã** | 4.2% | < 0.5% | **Giảm > 3.7%** |
| **Tắc nghẽn băng chuyền** | 2.1% | < 0.2% | **Khắc phục gần như hoàn toàn** |

---

## 4. ĐỀ XUẤT GIẢI PHÁP CẢI TIẾN TỚI MÔ HÌNH TO-BE

### 4.1. Ứng dụng Camera AI (Đọc mã vạch đa góc & Phân loại thể tích)
* **Cơ chế hoạt động:** Lắp đặt hệ thống Camera AI băng chuyền cố định ngay tại điểm tiếp nhận hàng.
* **Tác động lên quy trình BPMN:**
  * Tự động quét barcode/QR code và đo kích thước 3D (dài x rộng x cao) của kiện hàng trong vòng **$\le 6$ giây ($0.1$ phút)** khi kiện hàng di chuyển qua.
  * Loại bỏ thao tác thủ công `Quét tay PDA` ($1.5$ phút).
  * Giảm tỷ lệ lỗi quét nhầm từ $4.2\%$ xuống $< 0.5\%$.
  * Tự động phát hiện và cảnh báo các kiện hàng quá khổ trước khi đi vào hệ thống phân loại chính, giải quyết triệt để sự cố `Tắc nghẽn băng chuyền` ($2.1\%$).

### 4.2. Ứng dụng Cổng Self-service (Tự phục vụ tiếp nhận hàng)
* **Cơ chế hoạt động:** Trang bị các Kiosk Self-service tại khu vực nhập hàng cho tài xế/đối tác vận chuyển.
* **Tác động lên quy trình BPMN:**
  * Tài xế chủ động quét mã xác nhận chuyến hàng tại Kiosk Self-service.
  * Dữ liệu giao nhận được đẩy tự động trực tiếp qua API tới hệ thống WMS/TMS của Tiki Logistics theo thời gian thực (Real-time integration).
  * Loại bỏ hoàn toàn nút thắt chai `Đồng bộ trễ` ($2$ phút), rút ngắn thời gian xác nhận xuống còn $0.4$ phút.

### 4.3. Đánh giá tổng thể hiệu quả dự án
1. **Năng suất vận hành:** Khả năng xử lý đơn hàng tại Trung tâm phân loại (Sortation Center) tăng thêm khoảng **$1.8$ lần**.
2. **Chi phí vận hành (OpEx):** Cắt giảm trực tiếp $2,000$ VNĐ/đơn hàng. Với sản lượng hàng trăm ngàn đơn/ngày, Tiki Logistics sẽ tối ưu hóa chi phí vận hành ở quy mô rất lớn.
3. **Mô hình BPMN To-Be:** Luồng công việc mượt mà, tự động hóa cao, giảm sự phụ thuộc vào lao động thủ công và nâng cao độ chính xác của dữ liệu hệ thống.