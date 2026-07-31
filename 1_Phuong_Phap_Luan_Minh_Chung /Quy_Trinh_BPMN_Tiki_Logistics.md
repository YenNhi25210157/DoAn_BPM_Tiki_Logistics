# MÔ TẢ CHI TIẾT LUỒNG QUY TRÌNH NGHIỆP VỤ BPMN

## 1. Quy trình Tiếp nhận & Phân loại đơn hàng tự động (Core Process)

* **Đơn vị thực hiện (Pool):** Trung tâm Phân loại Tiki Logistics (Tiki Warehouse & Sorting Center).
* **Các phân làn (Lanes):** Nhân viên tiếp nhận Bãi nhập (Receiving Staff), Hệ thống Phân loại Băng tải Tự động (Automated Sorting System), Nhân viên Đóng gói & Xuất kho (Dispatch Staff).
* **Luồng tiến trình chi tiết:**
  1. *Sự kiện bắt đầu (Start Event):* Xe vận chuyển từ Nhà bán hàng (Merchant) hạ hàng tại bãi tiếp nhận.
  2. *Hoạt động 1 (Task):* Nhân viên bãi dỡ hàng và sử dụng máy quét PDA để ghi nhận nhập kho (Scan In).
  3. *Cổng kiểm tra (Exclusive Gateway - XOR):* Kiểm tra chất lượng và tính hợp lệ của tem nhãn mã vạch.
     * Nếu tem nhãn hỏng/lỗi: Chuyển hàng về Khu vực xử lý ngoại lệ (Rework Area) để dán lại tem.
     * Nếu tem nhãn hợp lệ: Đưa hàng lên hệ thống băng chuyền tự động.
  4. *Hoạt động 2 (Task):* Cảm biến tự động đo kích thước, trọng lượng và máy quét quang học đọc mã vùng giao hàng.
  5. *Cổng song song (Parallel Gateway - AND):* Tách luồng xử lý thành hai nhánh đồng thời:
     * Nhánh 1: Đồng bộ trạng thái kiện hàng 'Đã phân loại' lên phần mềm WMS.
     * Nhánh 2: Điều khiển tay gạt tự động gạt kiện hàng vào đúng máng chia theo khu vực giao hàng chặng cuối (Hub).
  6. *Sự kiện kết thúc (End Event):* Kiện hàng được đóng vào túi chuyên dụng, sẵn sàng bàn giao cho tài xế chặng cuối.

## 2. Quy trình IT Helpdesk Hỗ trợ Hạ tầng & Thiết bị Kho (Support Process)

* **Đơn vị thực hiện (Pool):** Bộ phận Kỹ thuật CNTT Tiki (Tiki IT Support System).
* **Các phân làn (Lanes):** Nhân viên vận hành kho (User), Bộ phận Helpdesk Tuyến 1 (Tier 1 Support), Đội ngũ Kỹ thuật Chuyên sâu Tuyến 2 (Tier 2 Advanced Support).
* **Luồng tiến trình chi tiết:**
  1. *Sự kiện bắt đầu (Start Event):* Nhân viên kho gửi phiếu yêu cầu hỗ trợ (Ticket) khi thiết bị quét PDA hoặc máy in tem gặp sự cố.
  2. *Hoạt động 1 (Task):* IT Helpdesk Tuyến 1 tiếp nhận phiếu, phân tích thông tin mô tả lỗi.
  3. *Cổng kiểm tra (Exclusive Gateway - XOR):* Phân loại mức độ phức tạp của sự cố.
     * Đối với lỗi cấu hình nhẹ (kết nối wifi, phần mềm): Kỹ thuật viên Tuyến 1 xử lý từ xa, hướng dẫn nhân viên và đóng phiếu trong vòng 15 phút.
     * Đối với lỗi hỏng hóc phần cứng hoặc lỗi hệ thống nghiêm trọng: Chuyển tiếp phiếu yêu cầu lên Đội Kỹ thuật Tuyến 2.
  4. *Hoạt động 2 (Task):* Kỹ thuật viên Tuyến 2 trực tiếp đến khu vực bãi kho kiểm tra, thay thế linh kiện hoặc sửa lỗi phần mềm chuyên sâu.
  5. *Sự kiện kết thúc (End Event):* Thiết bị được khôi phục hoạt động, nhân viên kho kiểm tra xác nhận và ghi nhận mức độ hài lòng trên hệ thống.
