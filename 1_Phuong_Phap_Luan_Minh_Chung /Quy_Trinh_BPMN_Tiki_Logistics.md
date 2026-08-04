# MÔ TẢ CHI TIẾT LUỒNG QUY TRÌNH NGHIỆP VỤ BPMN

## 1. Quy trình Tiếp nhận & Phân loại đơn hàng tự động (Core Process)
Đơn vị thực hiện (Pool): Trung tâm Phân loại Tiki Logistics.
1. Phân làn (Pool & Lanes)
- **Lane 1: Nhân viên Bãi nhập (Receiving Staff)**  
- **Lane 2: Hệ thống Tự động & WMS (Automated System & WMS)** 
- **Lane 3: Nhân viên Xuất kho (Dispatch Staff)**

2. Luồng chi tiết

**Giai đoạn 1: Tiếp nhận & Kiểm tra đầu vào (Inbound & Check-in)**
- **Start Event:** Xe tải chở hàng đến và hạ hàng tại bãi tiếp nhận. 
- **Task 1.1 (Nhân viên Bãi nhập):** Dỡ hàng và kiểm tra ngoại quan kiện hàng. 
- **XOR 1:** Ngoại quan nguyên vẹn?
  - *KHÔNG (Móp/Rách):* **Task 1.2:** Lập biên bản từ chối nhận hàng => **End Event 1:** Trả hàng về Nhà bán hàng.
  - *CÓ:* Chuyển sang Task tiếp theo.
- **Task 1.3 (Nhân viên Bãi nhập):** Quét mã vạch bằng máy PDA.
- **XOR 2:** Mã vạch hợp lệ / Đọc được?
  - *KHÔNG (Lỗi/Mờ):* **Task 1.4:** Chuyển ra Khu vực Rework dán lại tem $\rightarrow$ Quét lại $\rightarrow$ (Quay lại nối vào Task 1.5).  
  - *CÓ:* **Task 1.5:** Đưa kiện hàng lên băng chuyền tự động luồng chính.

**Giai đoạn 2: Đo đạc, Đọc mã & Tách luồng song song (Sorting & Data Sync)**
- **Task 2.1 (Hệ thống Tự động):** Cảm biến DWS đo tự động kích thước và trọng lượng.
- **XOR 3:** Kiện hàng bị Quá khổ (Oversize)?
  - *CÓ:* **Task 2.2:** Tách sang băng chuyền phụ / Xe nâng chở hàng cồng kềnh $\rightarrow$ *(Bỏ qua băng chuyền phân loại, nối thẳng tới Bước gom hàng cồng kềnh ở Bãi xuất)*.
  - *KHÔNG:* Tiếp tục di chuyển trên băng chuyền chính.
- **Task 2.3 (Hệ thống Tự động):** Camera quang học đọc mã vùng giao hàng.
- **XOR 4:** Đọc thành công mã vùng?
  - *KHÔNG (No-read):* **Task 2.4:** Băng chuyền gạt hàng ra máng Reject $\rightarrow$ Nhân viên nhập mã thủ công $\rightarrow$ *(Quay lại băng chuyền chính)*.
  - *CÓ:* **Task 2.5:** Hệ thống phân tích tuyến đường đích.
    
**Giai đoạn 3: Phân nhánh xử lý song song (AND Split)**
- **Gateway 5 (AND Split - Song song):** Tách thành 2 nhánh chạy đồng thời:
  - **NHÁNH 1: Xử lý Dữ liệu WMS**
    - **Task 1A:** Gửi API đồng bộ trạng thái kiện hàng lên WMS.
    - **XOR 6:** Kết nối API WMS thành công?
      - *Thất bại:* **Task 1B:** Lưu log & Retry (tối đa 3 lần).
        - *Gửi lại thành công:* Chuyển tới **AND Join**.
        - *Vẫn thất bại:* Cảnh báo lỗi IT + **Tín hiệu chặn gạt hàng (Hold Signal)** gửi sang Nhánh 2 $\rightarrow$ Đẩy kiện hàng ra khu vực Rework IT.
      - *Thành công:* Chuyển trực tiếp tới **Gateway 8 (AND Join)**.
  - **NHÁNH 2: Phân loại Vật lý Băng chuyền**
    - **Task 2A:** Băng chuyền di chuyển kiện hàng đến vị trí máng trượt (Chute) đích.
    - **XOR 7:** Cảm biến kiểm tra máng trượt có bị ĐẦY (Full)?
      - *CÓ (Đầy):* Cho kiện hàng xoay vòng (Recirculation).
        - *Số vòng =< 2:* Chờ máng trống và thử lại ở XOR 7.
        - *Số vòng > 2:* **Task 2B:** Đẩy ra máng xả tràn (Overflow Chute) $\rightarrow$ Nhân viên xả tràn phân loại thủ công / Nối lại băng chuyền.    
      - *KHÔNG (Trống) AND Không có tín hiệu chặn lỗi WMS:* **Task 2C:** Tay gạt tự động đẩy kiện hàng xuống máng trượt.  
    - Chuyển trực tiếp tới **Gateway 8 (AND Join)**. 
- **Gateway 8 (AND Join - Hợp nhất):** Xác nhận CẢ HAI điều kiện: Kiện hàng đã xuống máng **VÀ** Dữ liệu WMS đã đồng bộ thành công.
  
**Giai đoạn 4: Thu gom & Bàn giao Xuất kho (Dispatch & Outbound)**
- **Task 3.1 (Nhân viên Xuất kho):** Thu gom hàng từ máng trượt, đóng vào túi chuyên dụng (Bag) và niêm phong.
- **Task 3.2 (Nhân viên Xuất kho):** Dùng máy PDA quét Cross-check mã túi hàng với Lịch trình xe tải.
- **XOR 9:** Mã túi khớp với lịch trình xe?
  - *KHÔNG (Sai tuyến):* **Task 3.3:** Chuyển sang Khu vực xử lý sai lệch định tuyến (Kiểm tra lại hệ thống/Chuyển về máng đúng) $\rightarrow$ *(End Event phụ: Chờ xử lý)*.
  - *CÓ:* Chuyển sang bước bàn giao.
- **Task 3.4 (Nhân viên Xuất kho):** Xếp túi hàng/Pallet vào khu vực chờ tải của xe chặng cuối (Last-mile Truck).
- **End Event Final:** Kiện hàng sẵn sàng bàn giao cho xe chặng cuối xuất kho.


## 2. Quy trình IT Helpdesk Hỗ trợ Hạ tầng & Thiết bị Kho (Support Process)
1. Phân làn (Pool & Lanes)
- **Tên quy trình:** Quy trình IT Helpdesk Hỗ trợ Hạ tầng & Thiết bị Kho (Warehouse IT Infrastructure & Device Support Process).
- **Mã quy trình:** SUP-IT-02.
- **Đơn vị thực hiện (Pool):** Hệ thống Hỗ trợ Kỹ thuật CNTT Tiki (Tiki IT Support System).
- **Các phân làn (Lanes):**
  - **Nhân viên vận hành kho (Warehouse Operator / User):** Người phát sinh sự cố, phối hợp kiểm tra và nghiệm thu.
  - **Bộ phận Helpdesk Tuyến 1 (Tier 1 Support):** Tiếp nhận, phân loại, hỗ trợ cấu hình/sửa chữa từ xa và điều phối.
  - **Đội ngũ Kỹ thuật Chuyên sâu Tuyến 2 (Tier 2 Advanced Support):** Xử lý phần cứng, lỗi phần mềm nâng cao, làm việc với nhà cung cấp (Vendor) hoặc thực hiện thủ tục thanh lý/thay mới.
- **Đối tượng khách hàng nội bộ:** Nhân viên các bộ phận Nhập hàng (Inbound), Soạn hàng (Picking), Đóng gói (Packing), Xuất hàng (Outbound) tại bãi kho.
- **Kết quả đầu ra (Outputs):**
  - **Thành công:** Thiết bị (PDA/Máy in tem) phục hồi hoạt động hoàn toàn; Phiếu yêu cầu được đóng.
  - **Thất bại 1 (Hủy):** Người dùng tự hủy phiếu do thao tác nhầm.
  - **Thất bại 2 (Thanh lý):** Thiết bị hỏng nặng không thể sửa chữa, chuyển thủ tục thanh lý/thay thế mới.

2. Luồng chi tiết
**Sự kiện bắt đầu (Start Event):** Nhân viên kho phát hiện sự cố thiết bị PDA không quét được mã hoặc máy in tem bị kẹt/mất kết nối và tạo Ticket trên ứng dụng IT Support.
**Hoạt động 1 (Tuyến 1):** Hệ thống ghi nhận Ticket. Nhân viên Helpdesk Tuyến 1 tiếp nhận và phân tích thông tin mô tả lỗi.
**Gateway 1 (Exclusive Gateway - XOR 1): Phân loại tính hợp lệ của Ticket.**
- *Nhánh 1 (Lỗi thao tác nhầm):* Tuyến 1 nhắc nhở/hướng dẫn nhanh, User xác nhận và hủy ticket. Luồng kết thúc tại **[Sự kiện kết thúc thất bại 1: Hủy Ticket do lỗi thao tác]**.
- *Nhánh 2 (Lỗi thiết bị thực tế):* Luồng tiếp tục chuyển sang Gateway 2.
**Gateway 2 (Exclusive Gateway - XOR 2): Phân loại mức độ sự cố.**
- *Nhánh 1 (Lỗi cấu hình phần mềm/Wifi nhẹ):* Chuyển sang Hoạt động 2.
- *Nhánh 2 (Lỗi phần cứng/Phần mềm hệ thống nặng):* Chuyển tiếp (Escalate) phiếu cho Đội Kỹ thuật Tuyến 2 (Đi đến Hoạt động 3).
**Hoạt động 2 (Tuyến 1):** Kỹ thuật viên Tuyến 1 truy cập từ xa (Remote) hoặc gọi điện hướng dẫn User xử lý sự cố cấu hình mạng/ứng dụng cơ bản.
**Gateway 3 (Exclusive Gateway - XOR 3): Kiểm tra kết quả xử lý của Tuyến 1.**
- *Nhánh 1 (Xử lý thành công):* Chuyển thẳng đến bước nghiệm thu của User (Hoạt động 6).
- *Nhánh 2 (Không thành công / Phát hiện lỗi sâu hơn):* Chuyển tiếp (Escalate) lên Tuyến 2 (Đi đến Hoạt động 3).
**Hoạt động 3 (Tuyến 2):** Kỹ thuật viên Tuyến 2 di chuyển trực tiếp (On-site) đến vị trí bãi kho để kiểm tra tình trạng vật lý của thiết bị.
**Gateway 4 (Exclusive Gateway - XOR 4): Xác định nguyên nhân gốc rễ tại bãi kho.**
- *Nhánh 1 (Lỗi phần mềm chuyên sâu - OS/Firmware/App):* Chuyển sang Hoạt động 4.
- *Nhánh 2 (Lỗi hỏng hóc phần cứng):* Chuyển sang Gateway 5.
**Hoạt động 4 (Tuyến 2):** Cài đặt lại Firmware, flash ROM PDA hoặc cấu hình lại Print Server cho máy in. Sau khi hoàn tất cài đặt, luồng chuyển thẳng đến bước nghiệm thu (Hoạt động 6).
**Gateway 5 (Exclusive Gateway - XOR 5): Kiểm tra tình trạng kho linh kiện thay thế.**
- *Nhánh 1 (Có sẵn linh kiện dự phòng):* Chuyển sang Hoạt động 5.
- *Nhánh 2 (Hết linh kiện hoặc lỗi vi mạch phức tạp):* Chuyển sang Hoạt động 5.1.
**Hoạt động 5 (Tuyến 2):** Tiến hành thay thế linh kiện hỏng (đầu in máy in, pin/màn hình PDA) trực tiếp tại chỗ. Sau đó luồng chuyển đến Gateway 6.
**Hoạt động 5.1 (Tuyến 2):** Thực hiện quy trình đóng gói và gửi thiết bị cho Nhà cung cấp (Vendor) để bảo hành hoặc sửa chữa chuyên sâu. Chờ Vendor phản hồi. Sau đó luồng chuyển đến Gateway 6.
**Gateway 6 (Exclusive Gateway - XOR 6): Đánh giá khả năng phục hồi của thiết bị (Sau khi tự sửa hoặc Vendor trả về).**
- *Nhánh 1 (Thiết bị sửa thành công, hoạt động tốt):* Chuyển sang Hoạt động 6 để nghiệm thu.
- *Nhánh 2 (Thiết bị hỏng hoàn toàn / Chi phí sửa chữa vượt quá giới hạn):* Đề xuất thanh lý và cấp thiết bị mới dự phòng cho kho. Luồng kết thúc tại **[Sự kiện kết thúc thất bại 2: Cấp mới & Thanh lý thiết bị hỏng]**.
**Hoạt động 6 (User & Tuyến 1):** Nhân viên kho trực tiếp thao tác thử nghiệm thiết bị sau sửa chữa và xác nhận hoàn thành (Resolve) trên hệ thống.
**Gateway 7 (Exclusive Gateway - XOR 7): Phân nhánh dựa trên Đánh giá mức độ hài lòng (CSAT) của người dùng.**
- *Nhánh 1 (Người dùng đánh giá từ 3 sao trở lên - Hài lòng/Chấp nhận được):* Luồng đi thẳng đến bước đóng phiếu (Gateway 8).
- *Nhánh 2 (Người dùng đánh giá dưới 3 sao - Không hài lòng):* Luồng chuyển sang Hoạt động 7.
**Hoạt động 7 (Hệ thống):** Tự động tạo một Ticket kiểm tra chất lượng (QA Ticket) để quản lý điều tra nguyên nhân không hài lòng, phục vụ cải tiến dịch vụ. Sau khi QA Ticket được tạo, luồng tiếp tục đi đến Gateway 8.
**Gateway 8 (Parallel Gateway - AND Split): Khởi chạy thủ tục hoàn tất đóng phiếu.** Hệ thống tách làm 2 nhánh thực hiện đồng thời:
- *Hoạt động 8A (Hệ thống):* Cập nhật nhật ký lịch sử sửa chữa thiết bị vào cơ sở dữ liệu Asset Management.
- *Hoạt động 8B (Hệ thống):* Tự động xuất báo cáo và gửi Email thông báo hoàn tất sự cố cho Quản lý kho.
**Gateway 9 (Parallel Gateway - AND Join): Điểm hội tụ hệ thống.** Chờ cả hai Hoạt động 8A và 8B hoàn tất để gộp luồng lại thành một.
**Sự kiện kết thúc (End Event):** Phiếu hỗ trợ chính thức được đóng trên hệ thống (Closed Successful). Quy trình hoàn tất.
