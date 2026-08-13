# BẢNG PHÂN TÍCH ĐỊNH LƯỢNG & ĐỀ XUẤT CẢI TIẾN QUY TRÌNH (TO-BE)

## I. QUY TRÌNH 1: TIẾP NHẬN & PHÂN LOẠI ĐƠN HÀNG (ÁP DỤNG CAMERA AI)

### 1. Mô hình So sánh Định lượng (As-Is vs. To-Be)

| Chỉ số | Hiện trạng (As-Is) | Cải tiến (To-Be) | Mức độ Cải thiện |
| :--- | :--- | :--- | :--- |
| **Giá trị tạo ra (VA)** | **5.5 phút**<br>• Hạ hàng: 2.0 phút<br>• Cân đo máy: 0.5 phút<br>• Đóng bao: 3.0 phút | **5.5 phút**<br>• Hạ hàng & Quét Camera AI: 2.0 phút<br>• Cân đo máy: 0.5 phút<br>• Đóng bao: 3.0 phút | Không thay đổi |
| **Lãng phí (BVA + NVA)** | **3.5 phút**<br>• Quét PDA thủ công: 1.5 phút<br>• Trễ đồng bộ WMS: 2.0 phút | **0 phút**<br>• Camera AI tự động nhận diện barcode/OCR khi hạ hàng.<br>• Tự động đẩy dữ liệu thời gian thực lên WMS qua API. | **Giảm 100%** (3.5 phút) |
| **Thời gian chu kỳ (CT)** | **9.0 phút/đơn** | **5.5 phút/đơn** | **Rút ngắn 38.9%** (3.5 phút/đơn) |
| **Hiệu suất thời gian (CTE)**| **61.1%** | **100.0%** | **Tăng 38.9%** (Đạt 100% VA) |
| **Chi phí nhân sự / đơn** | **4.500 VNĐ/đơn**<br>*(9 phút / 60) * 30.000* | **2.750 VNĐ/đơn**<br>*(5.5 phút / 60) * 30.000* | **Tiết kiệm 38.9%** (1.750 VNĐ/đơn) |

### 2. Đề xuất Giải pháp To-Be: Tự động hóa tiếp nhận bằng Camera AI

* **Cơ chế hoạt động:**
  * **Đọc dữ liệu tự động:** Lắp đặt Camera AI tại khu vực hạ hàng. Khi nhân viên hạ hàng, Camera AI tự động quét mã vận đơn/mã thông tin trên thùng hàng mà không cần thao tác bấm PDA thủ công.
  * **Tích hợp WMS trực tiếp:** Camera AI kết nối API trực tiếp với WMS, tự động cập nhật trạng thái đơn hàng ngay lập tức, triệt tiêu độ trễ đồng bộ dữ liệu.
* **Lợi ích đạt được:**
  * Giảm thời gian chu kỳ từ **9 phút xuống 5.5 phút/đơn**.
  * Cứ mỗi **1.000 đơn hàng**, doanh nghiệp tiết kiệm **58.3 giờ làm việc** và **1.750.000 VNĐ** chi phí nhân công.

---

## II. QUY TRÌNH 2: IT HELPDESK HỖ TRỢ THIẾT BỊ (ÁP DỤNG CỔNG SELF-SERVICE)

### 1. Mô hình So sánh Định lượng (As-Is vs. To-Be)

| Chỉ số | Hiện trạng (As-Is) | Cải tiến (To-Be) | Mức độ Cải thiện |
| :--- | :--- | :--- | :--- |
| **Thời gian tiếp nhận & phân loại (NVA)** | **25 phút**<br>• Nhận ticket: 10 phút<br>• Tuyến 1 duyệt/phân loại: 15 phút | **2 phút**<br>• Khai báo sự cố trực tiếp qua Cổng Self-service.<br>• Hệ thống tự động phân loại và định tuyến ticket. | **Giảm 92%** (23 phút) |
| **Thời gian xử lý trực tiếp (VA)** | **45 phút**<br>• Tuyến 2 xuống bãi xử lý | **15 phút**<br>• Cổng Self-service cung cấp hướng dẫn tự khắc phục nhanh (Self-troubleshooting) hoặc định tuyến ưu tiên đến Tuyến 2. | **Giảm 66.7%** (30 phút) |
| **Thời gian chu kỳ (CT)** | **70 phút/sự cố** | **17 phút/sự cố** | **Rút ngắn 75.7%** (53 phút/sự cố) |
| **Hiệu suất thời gian (CTE)**| **64.2%** *(45 / 70)* | **88.2%** *(15 / 17)* | **Tăng 24.0%** |
| **Chi phí gián đoạn (Downtime)** | **58.333 VNĐ/sự cố**<br>*(70 phút / 60) * 50.000* | **14.167 VNĐ/sự cố**<br>*(17 phút / 60) * 50.000* | **Tiết kiệm 75.7%** (44.166 VNĐ/sự cố) |

### 2. Đề xuất Giải pháp To-Be: Tối ưu hóa xử lý sự cố qua Cổng Self-Service

* **Cơ chế hoạt động:**
  * **Tạo yêu cầu & Phân loại tự động:** Nhân viên kho tự truy cập Cổng Self-service (trên điện thoại/Kiosk) để gửi báo lỗi trong 1-2 phút. Hệ thống tự động phân loại đúng bộ phận chuyên trách.
  * **Hỗ trợ tự khắc phục (Self-healing/Troubleshooting):** Cổng cung cấp quy trình hướng dẫn xử lý nhanh các lỗi cơ bản (Reset, kết nối lại Wifi, thay pin), giúp nhân viên tự xử lý ngay tại chỗ mà không cần chờ IT.
* **Lợi ích đạt được:**
  * Rút ngắn thời gian Downtime từ **70 phút xuống 17 phút/sự cố**.
  * Cứ mỗi **100 sự cố**, doanh nghiệp tiết kiệm **4.416.600 VNĐ** chi phí thời gian chết của nhân viên.

---

## III. TỔNG HỢP HIỆU QUẢ CẢI TIẾN (SUMMARY)

* **Quy trình Tiếp nhận & Phân loại (Camera AI):** Rút ngắn **38.9%** thời gian chu kỳ, nâng CTE lên **100%**, tiết kiệm **1.750 VNĐ/đơn**.
* **Quy trình IT Helpdesk (Cổng Self-service):** Rút ngắn **75.7%** thời gian gián đoạn, nâng CTE lên **88.2%**, tiết kiệm **44.166 VNĐ/sự cố**.