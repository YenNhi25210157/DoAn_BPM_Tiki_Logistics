# MÔ TẢ CHI TIẾT LUỒNG QUY TRÌNH NGHIỆP VỤ BPMN

## 1. Quy trình Tiếp nhận & Phân loại đơn hàng tự động (Core Process)
Đơn vị thực hiện (Pool): Trung tâm Phân loại Tiki Logistics.
1. Phân làn
•	Làn 1: Nhân viên bãi nhập
•	Làn 2: Hệ thống tự động & WMS
•	Làn 3: Nhân viên xuất kho 
2. Luồng chi tiết
Giai đoạn 1: Tiếp nhận & Kiểm tra đầu vào (Inbound & Check-in)
•	Start Event: Xe tải chở hàng đến và hạ hàng tại bãi tiếp nhận.
•	Task 1.1 (Nhân viên Bãi nhập): Dỡ hàng và kiểm tra ngoại quan kiện hàng.
•	XOR 1: Ngoại quan nguyên vẹn?
o	KHÔNG (Móp/Rách): Task 1.2: Lập biên bản từ chối nhận hàng -> End Event 1: Trả hàng về Nhà bán hàng.
o	CÓ: Chuyển sang Task tiếp theo.
•	Task 1.3 (Nhân viên Bãi nhập): Quét mã vạch bằng máy PDA.
•	XOR 2: Mã vạch hợp lệ / Đọc được?
o	KHÔNG (Lỗi/Mờ): Task 1.4: Chuyển ra Khu vực Rework dán lại tem -> Quét lại -> (Quay lại nối vào Task 1.5).
o	CÓ: Task 1.5: Đưa kiện hàng lên băng chuyền tự động luồng chính.
Giai đoạn 2: Đo đạc, Đọc mã & Tách luồng song song (Sorting & Data Sync)
•	Task 2.1 (Hệ thống Tự động): Cảm biến DWS đo tự động kích thước và trọng lượng.
•	XOR 3: Kiện hàng bị Quá khổ (Oversize)?
o	CÓ: Task 2.2: Tách sang băng chuyền phụ / Xe nâng chở hàng cồng kềnh -> (Bỏ qua băng chuyền phân loại, nối thẳng tới Bước gom hàng cồng kềnh ở Bãi xuất).
o	KHÔNG: Tiếp tục di chuyển trên băng chuyền chính.
•	Task 2.3 (Hệ thống Tự động): Camera quang học đọc mã vùng giao hàng.
•	XOR 4: Đọc thành công mã vùng?
o	KHÔNG (No-read): Task 2.4: Băng chuyền gạt hàng ra máng Reject -> Nhân viên nhập mã thủ công -> (Quay lại băng chuyền chính).
o	CÓ: Task 2.5: Hệ thống phân tích tuyến đường đích.
Giai đoạn 3: Phân nhánh xử lý song song (AND Split)
•	Gateway 5 (AND Split - Song song): Tách thành 2 nhánh chạy đồng thời:
o	NHÁNH 1: Xử lý Dữ liệu WMS
	Task 1A: Gửi API đồng bộ trạng thái kiện hàng lên WMS.
	XOR 6: Kết nối API WMS thành công?
	Thất bại: Task 1B: Lưu log & Retry (tối đa 3 lần).
	Gửi lại thành công: Chuyển tới AND Join.
	Vẫn thất bại: Cảnh báo lỗi IT + Tín hiệu chặn gạt hàng (Hold Signal) gửi sang Nhánh 2 -> Đẩy kiện hàng ra khu vực Rework IT.
	Thành công: Chuyển trực tiếp tới Gateway 8 (AND Join).
o	NHÁNH 2: Phân loại Vật lý Băng chuyền
	Task 2A: Băng chuyền di chuyển kiện hàng đến vị trí máng trượt (Chute) đích.
	XOR 7: Cảm biến kiểm tra máng trượt có bị ĐẦY (Full)?
	CÓ (Đầy): Cho kiện hàng xoay vòng (Recirculation).
	Số vòng nhỏ hơn hoặc bằng 2: Chờ máng trống và thử lại ở XOR 7.
	Số vòng lớn hơn 2: Task 2B: Đẩy ra máng xả tràn (Overflow Chute) -> Nhân viên xả tràn phân loại thủ công / Nối lại băng chuyền.
	KHÔNG (Trống) AND Không có tín hiệu chặn lỗi WMS: Task 2C: Tay gạt tự động đẩy kiện hàng xuống máng trượt.
	Chuyển trực tiếp tới Gateway 8 (AND Join).
•	Gateway 8 (AND Join - Hợp nhất): Xác nhận CẢ HAI điều kiện: Kiện hàng đã xuống máng VÀ Dữ liệu WMS đã đồng bộ thành công.
Giai đoạn 4: Thu gom & Bàn giao Xuất kho (Dispatch & Outbound)
•	Task 3.1 (Nhân viên Xuất kho): Thu gom hàng từ máng trượt, đóng vào túi chuyên dụng (Bag) và niêm phong.
•	Task 3.2 (Nhân viên Xuất kho): Dùng máy PDA quét Cross-check mã túi hàng với Lịch trình xe tải.
•	XOR 9: Mã túi khớp với lịch trình xe?
o	KHÔNG (Sai tuyến): Task 3.3: Chuyển sang Khu vực xử lý sai lệch định tuyến (Kiểm tra lại hệ thống/Chuyển về máng đúng) -> (End Event phụ: Chờ xử lý).
o	CÓ: Chuyển sang bước bàn giao.
•	Task 3.4 (Nhân viên Xuất kho): Xếp túi hàng/Pallet vào khu vực chờ tải của xe chặng cuối (Last-mile Truck).
•	End Event Final: Kiện hàng sẵn sàng bàn giao cho xe chặng cuối xuất kho.


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
