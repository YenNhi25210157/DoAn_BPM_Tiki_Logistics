# BỘ CÂU HỎI PHỎNG VẤN & KỊCH BẢN WORKSHOP - TIKI LOGISTICS

---

## 1. Bộ câu hỏi phỏng vấn thu thập dữ liệu & Đáp án khảo sát

### A. Khối câu hỏi cấu trúc (Structured Questions)

* **1. Quy trình tiếp nhận và xử lý phân loại hàng hóa tại kho TikiNow Logistics hiện được tiêu chuẩn hóa qua bao nhiêu công đoạn cố định?**
  * **Đáp án:** 4 công đoạn cố định: Dỡ hàng & Nhận diện (Inbound) -> Phân loại & Dán tem -> Kiểm đếm (Inspection) -> Lưu kho/Chờ xuất (Staging).

* **2. Thời gian định mức kỹ thuật cho máy quét tự động xử lý và nhận diện một mã đơn hàng là bao nhiêu giây?**
  * **Đáp án:** 1.5 - 2.0 giây/mã.

* **3. Hệ thống phần mềm Quản lý Kho hàng (WMS) có cơ chế tự động ghi nhận vị trí lưu kho ngay sau khi quét mã kiểm kê hay không?**
  * **Đáp án:** Có. Hệ thống WMS tự động ghi nhận vị trí ô/kệ (Bin/Rack) ngay khi thiết bị PDA quét mã QR/mã vạch hàng hóa.

* **4. Nhân viên trực ca vận hành kho xuất biên bản giao nhận ca làm việc qua biểu mẫu điện tử nào?**
  * **Đáp án:** Form điện tử **"E-Handover Logistics"** tích hợp trên hệ thống WMS nội bộ.

* **5. Tỷ lệ phát sinh lỗi phân loại nhầm tuyến giao hàng trong tổng lượng đơn vận hành hàng tháng bình quân là bao nhiêu?**
  * **Đáp án:** 0.8% - 1.2% trên tổng lượng đơn vận hành hàng tháng.

---

### B. Khối câu hỏi phi cấu trúc (Unstructured Questions)

* **1. Những vướng mắc lớn nhất trong khâu bàn giao dữ liệu giữa bộ phận phân loại kho tổng và đội ngũ giao hàng chặng cuối (Last-Mile Delivery) là gì?**
  * **Đáp án:** Sai lệch thời gian đồng bộ dữ liệu giữa WMS và app tài xế; thiếu sót thông tin ghi chú giao hàng (như hẹn giờ, giao giờ hành chính); trễ hạn bàn giao ca vào các khung giờ cao điểm (Peak Hours).

* **2. Phương án xử lý kỹ thuật của điều phối viên khi thiết bị định vị và ứng dụng cầm tay của tài xế bị gián đoạn kết nối mạng?**
  * **Đáp án:** Tài xế chuyển sang chế độ **Offline Mode** trên ứng dụng (lưu dữ liệu tạm thời vào bộ nhớ cục bộ). Khi có kết nối, ứng dụng tự động đồng bộ (Auto-sync) về server; trường hợp lỗi phần cứng/hệ thống sẽ gọi tổng đài điều phối hỗ trợ thủ công.

* **3. Cần áp dụng các giải pháp tổ chức nào nhằm giảm thiểu việc kiểm tra xác minh thủ công tại khu vực cửa xuất hàng?**
  * **Đáp án:** Tích hợp công nghệ **RFID** hoặc cổng quét mã vạch tự động (Barcode Gate) tại cửa xuất kho; áp dụng cơ chế xác thực tự động bằng mã QR thay cho ký nhận biên bản giấy.

* **4. Đánh giá tính khả thi và rào cản vận hành khi triển khai hệ thống băng chuyền tự động hóa toàn phần tại trung tâm phân loại?**
  * **Đáp án:** 
    * *Tính khả thi:* Cao, hỗ trợ giảm tới 40% chi phí nhân công phân loại và tăng tốc độ xử lý hàng.
    * *Rào cản:* Chi phí đầu tư ban đầu (CAPEX) lớn, rủi ro tắc nghẽn cục bộ khi xử lý hàng quá khổ/dễ vỡ, và phát sinh thời gian dừng ca để bảo trì thiết bị.

* **5. Các phản hồi chưa hài lòng của người mua về thời gian hoàn thành dịch vụ giao hàng nhanh 2 giờ thường xuất phát từ khâu nào?**
  * **Đáp án:** Thường xuất phát từ khâu **"Pick & Pack" (Nhặt hàng & Đóng gói)** trong kho bị trễ ca, hoặc do nghẽn điều phối tài xế (Last-mile assignment) vào giờ cao điểm.

---

### C. Khối câu hỏi phân tích định tính (Qualitative Questions)

* **1. Công đoạn nào trong luồng di chuyển kiện hàng tại kho có nguy cơ tạo ra nút thắt cổ chai (bottleneck) cao nhất?**
  * **Đáp án:** Khu vực **Phân loại thủ công (Sorting Area)** và **Kiểm tra/Bàn giao xuất kho (Outbound Handover)**.

* **2. Các trường dữ liệu nào trên phiếu giao hàng hiện tại bị lặp lại, gây tốn thời gian xử lý của nhân viên?**
  * **Đáp án:** Thông tin Địa chỉ người nhận, Mã đơn hàng, và Mã vận đơn bị in lặp lại ở cả phiếu dán trên kiện lẫn biên bản bàn giao.

* **3. Nhân viên kiểm kê kho có bắt buộc phải nhập lại mã hàng thủ công sau khi đã quét bằng thiết bị cầm tay PDA không?**
  * **Đáp án:** Không. Chỉ cần quét mã PDA, trừ trường hợp mã vạch bị mờ, rách hoặc tem bị lỗi thì mới nhập tay (Manual Entry).

* **4. Khâu đối soát tiền thu hộ (COD) vào cuối ca gặp khó khăn gì nếu tài xế bàn giao ca trễ so với khung giờ quy định?**
  * **Đáp án:** Bị lệch sổ sách kế toán cuối ngày, tài xế phải đợi đối soát sang ca sau, gây nguy cơ thất thoát hoặc chênh lệch tiền mặt tồn quỹ.

* **5. Quy định phân loại riêng cho nhóm hàng hóa dễ vỡ và hàng quá khổ hiện đã được thực hiện triệt để tại bãi dỡ hàng chưa?**
  * **Đáp án:** Chưa triệt để. Hàng dễ vỡ vẫn còn tình trạng bị xếp chung bãi dỡ hàng trong các khung giờ nhận hàng dồn dập.

* **6. Có xuất hiện các thao tác phê duyệt trùng lặp giữa bộ phận Hỗ trợ kỹ thuật Tuyến 1 (Helpdesk) và Tuyến 2 (Chuyên sâu) không?**
  * **Đáp án:** Có. Đôi khi Helpdesk Tuyến 1 giải quyết xong sự cố nhưng vẫn chuyển Ticket sang Tuyến 2 để "xác nhận lại", gây lãng phí thời gian xử lý.

* **7. Tài xế giao hàng gặp những trở ngại gì khi kiểm tra giấy tờ xác thực của người nhận đối với các đơn hàng giá trị cao?**
  * **Đáp án:** Khách hàng không muốn cung cấp CCCD/mã OTP, thời gian chờ khách ra nhận hàng lâu, ứng dụng kiểm tra thông tin đôi khi bị giật lag.

* **8. Công tác chuẩn bị và dọn dẹp mặt bằng trước ca phân loại hàng hóa có thể rút gọn qua những giải pháp nào?**
  * **Đáp án:** Chuẩn bị trước pallet/xe đẩy theo phân vùng từ cuối ca trước; áp dụng tiêu chuẩn **5S** và phân công checklist vệ sinh mặt bằng cố định 15 phút trước khi giao ca.

* **9. Nguyên nhân dẫn đến việc các phiếu yêu cầu hỗ trợ thiết bị quét mã vạch (ticket IT) bị chuyển giao lòng vòng giữa các bộ phận?**
  * **Đáp án:** Thiếu quy trình phân loại lỗi ban đầu (Triaging); nhân viên báo lỗi chung chung ("máy hỏng") khiến IT L1 chuyển nhầm cho bộ phận phần mềm thay vì kỹ thuật phần cứng.

* **10. Nội dung chương trình đào tạo nhân viên kho mới đã bám sát thực tế khối lượng công việc trong các kỳ cao điểm mua sắm chưa?**
  * **Đáp án:** Chưa bám sát. Bài đào tạo thiên về lý thuyết quy trình chuẩn, thiếu các kịch bản xử lý sự cố thực tế khi lượng đơn tăng đột biến (Peak season).

---

### D. Khối câu hỏi phân tích định lượng (Quantitative Questions)

* **1. Thời gian xử lý trung bình một kiện hàng tính từ thời điểm hạ hàng khỏi xe tải đến khi sẵn sàng xuất kho là bao nhiêu phút?**
  * **Đáp án:** 25 - 35 phút/kiện hàng.

* **2. Tỷ lệ kiện hàng gặp lỗi dán tem, rách nhãn mã vạch phải đưa vào khu vực xử lý lại (Rework Area) chiếm bao nhiêu %?**
  * **Đáp án:** 3.5% - 5.0% tổng lượng tem nhãn.

* **3. Thời gian trung bình để đội IT Helpdesk khắc phục xong sự cố phần cứng của máy quét cầm tay PDA là bao nhiêu phút?**
  * **Đáp án:** 45 phút/sự cố.

* **4. Tổng chi phí nhân công tính toán cho một lượt kiểm kê kho định kỳ toàn phần là bao nhiêu VNĐ?**
  * **Đáp án:** 15.000.000 - 20.000.000 VNĐ/lượt (quy mô kho trung bình).

* **5. Mức độ chênh lệch trung bình giữa số liệu hàng hóa thực tế kiểm đếm và chỉ số trên hệ thống WMS là bao nhiêu %?**
  * **Đáp án:** 0.15% - 0.3%.

* **6. Thời gian tài xế xe tải phải chờ đợi tại bãi dỡ hàng trước khi được xếp ca nhập kho là bao nhiêu phút?**
  * **Đáp án:** 15 - 25 phút/xe.

* **7. Chi phí vận hành bình quân để hoàn thành một đơn hàng chặng cuối (Last-Mile) là bao nhiêu VNĐ?**
  * **Đáp án:** 12.000 - 18.000 VNĐ/đơn hàng.

* **8. Tỷ lệ đơn hàng TikiNow 2 giờ hoàn thành đúng thời gian cam kết đạt bao nhiêu % trên tổng lượng đơn?**
  * **Đáp án:** 92% - 94% (Mục tiêu cam kết quy chuẩn: >96%).

* **9. Khối lượng phiếu sự cố thiết bị kho hàng gửi về bộ phận IT Helpdesk trung bình trong một tuần là bao nhiêu?**
  * **Đáp án:** 35 - 50 ticket/tuần.

* **10. Tỷ lệ đơn hàng bị chuyển hoàn do không liên lạc được với người nhận chiếm bao nhiêu % tổng đơn phát đi?**
  * **Đáp án:** 4.5% - 6.0% tổng đơn phát đi.

---

> **Lưu ý ghi chú:** 
> *Dữ liệu định lượng và thông tin vận hành trong tài liệu này được tổng hợp qua phương pháp phỏng vấn chuyên gia & giả định theo tiêu chuẩn vận hành (Benchmark) thực tế của ngành E-commerce Logistics.*
