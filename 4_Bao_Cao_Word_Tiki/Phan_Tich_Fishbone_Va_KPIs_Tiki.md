# BÁO CÁO PHÂN TÍCH NGUYÊN NHÂN GỐC RỄ VÀ CHỈ SỐ CHẤT LƯỢNG (KPIS) - TIKI LOGISTICS

## 1. Phân tích nguyên nhân gốc rễ nút thắt vận hành (Sơ đồ Xương cá - Fishbone)

**Vấn đề cốt lõi:** Tỷ lệ chậm trễ thời gian cam kết giao hàng 2 giờ (TikiNow) và phát sinh tỷ lệ hủy đơn tại trung tâm phân loại.

* **Con người (Man):**
  * Nhân viên bãi dỡ hàng thao tác kiểm tra thủ công đối với các kiện hàng quá khổ, dễ gây ra sai sót vào khung giờ cao điểm.
  * Lực lượng tài xế chặng cuối (Last-Mile) chưa được tập huấn kỹ về quy trình xác thực chứng từ đối với các đơn hàng giá trị cao.
* **Quy trình (Process):**
  * Sự thiếu đồng bộ giữa ca kiểm kê kho và ca giao hàng khiến thời gian chờ bàn giao bãi xuất bị kéo dài.
  * Các bước xử lý sự cố thiết bị (ticket IT) phải trải qua bước duyệt trung gian không cần thiết giữa Helpdesk Tuyến 1 và Tuyến 2.
* **Công nghệ & Thiết bị (Technology & Machine):**
  * Mạng kết nối không dây (Wifi) tại một số khu vực ngách trong kho bãi chập chờn, ảnh hưởng đến tốc độ truyền dữ liệu của máy quét PDA.
  * Độ trễ đồng bộ dữ liệu giữa phần mềm WMS và ứng dụng di động của tài xế dao động khoảng 2 phút.
* **Môi trường & Mặt bằng (Environment):**
  * Mặt bằng khu vực phân loại thủ công bị hạn chế không gian vào ca cao điểm mua sắm, gây ra hiện tượng ùn tắc cục bộ.

---

## 2. Bảng chỉ số đo lường chất lượng vận hành (KPIs)

| Chỉ số chất lượng (KPI) | Hiện trạng đo lường | Mục tiêu tối ưu (To-Be) | Phương án cải tiến kỹ thuật |
| :--- | :---: | :---: | :--- |
| Tỷ lệ lỗi dán tem / nhãn mã vạch rách | 4.2% | < 1.0% | Tích hợp máy in nhãn tự động tại đầu băng chuyền tiếp nhận. |
| Tỷ lệ trễ hạn xử lý ticket IT Tuyến 2 | 11.5% | < 3.0% | Chuẩn hóa bộ cẩm nang xử lý sự cố (Knowledge Base) cho Helpdesk Tuyến 1. |
| Tỷ lệ chênh lệch tồn kho thực tế - WMS | 2.8% | < 0.5% | Bổ sung quy trình kiểm kê quét mã vạch tự động định kỳ theo ca. |
| Tỷ lệ giao hàng đúng cam kết TikiNow 2h | 88.5% | > 97.0% | Tối ưu hóa thuật toán tự động chia máng hàng theo vùng giao cho tài xế. |
