Host Discovery

Là bước xác định xem các máy nào đang sống trong một mạng trước khi scan sâu hơn.
------------------------------------
Network Mapping 

Là quá trình thu thập thông tin để biết:
    Có những host nào trong mạng
    Các host đó nằm ở đâu
    Chúng liên kết như thế nào
    Dịch vụ và vai trò của từng host
    Mạng có chia VLAN không? Có firewall ở đâu?

Ngắn gọn: Network Mapping = Xây bản đồ tổng thể của mạng cần pentest.

Công cụ: nmap

| Thành phần        | Ý nghĩa                         |
| ----------------- | ------------------------------- |
| Host Discovery    | Tìm host sống                   |
| Port Scan         | Tìm port mở                     |
| Service Detection | Biết dịch vụ/phiên bản          |
| OS Detection      | Đoán hệ điều hành               |
| Traceroute        | Tìm đường đi mạng               |
| Mapping           | Vẽ lại sơ đồ mạng (network map) |

-----------------------------------
3 Bước Thiết lập Kết nối TCP
Quá trình bắt tay diễn ra tuần tự qua ba gói tin chính:

Bước 1: SYN (Synchronize) – Yêu cầu Kết nối
    Máy Khách (Client) muốn kết nối với Máy Chủ.
    Nó gửi một gói tin SYN (Synchronize) đến cổng của Máy Chủ.
    Gói tin này có cờ SYN được bật.
    Nó chứa một Số Thứ tự Ban đầu (Initial Sequence Number - ISN) ngẫu nhiên của Máy Khách.
→ Mục đích: Máy Khách thông báo cho Máy Chủ biết nó muốn bắt đầu một kết nối và đưa ra số thứ tự đầu tiên mà nó sẽ sử dụng để theo dõi dữ liệu.

Bước 2: SYN-ACK (Synchronize-Acknowledge) – Chấp nhận và Phản hồi
    Máy Chủ (Server) nhận được gói SYN.
    Nếu cổng đang mở và Máy Chủ sẵn sàng chấp nhận kết nối, nó sẽ gửi lại một gói tin SYN-ACK.
    Gói tin này có cả cờ SYN và cờ ACK (Acknowledge) được bật.
    Cờ SYN chứa ISN ngẫu nhiên của Máy Chủ.
    Cờ ACK chứa số thứ tự tiếp theo mà Máy Chủ mong đợi từ Máy Khách (thường là ISN của Máy Khách + 1).
→ Mục đích: Máy Chủ xác nhận đã nhận được yêu cầu (ACK), và đồng thời, yêu cầu Máy Khách xác nhận số thứ tự của mình (SYN).

Bước 3: ACK (Acknowledge) – Hoàn tất Thiết lập
    Máy Khách nhận được gói SYN-ACK.
    Nó gửi lại gói tin ACK cuối cùng để hoàn tất quá trình bắt tay.
    Gói tin này chỉ có cờ ACK được bật.
    Nó chứa số thứ tự tiếp theo mà Máy Khách mong đợi từ Máy Chủ (thường là ISN của Máy Chủ + 1).
→ Mục đích: Máy Khách xác nhận đã nhận được phản hồi của Máy Chủ.
-----------------------------------
Host Discovery Techniques

Là các kỹ thuật dùng để biết máy nào đang sống trong mạng

Tool: nmap

Kỹ thuật 1: ICMP Ping (ICMP Echo Request)
    Gửi lệnh "ping" xem có host nào trả lời không.
    Ưu điểm:
        Nhanh
    Nhược điểm:
        Thường bị chặn bởi firewall
Kỹ thuật 2: ARP Scan
    ARP - Address Resolution Protocol: Giao thức phân giải địa chỉ
        ARP là giao thức sử dụng để tìm địa chỉ MAC từ địa chỉ IP (MAC -> Media Access Control - định danh duy nhất vĩnh viễn với mỗi thiết bị có kết nối mạng, dùng để đảm bảo dữ liệu đến đúng thiết bị đích)
    Trong cùng một mạng cục bộ (LAN), gửi ARP request để khám phá các host đang hoạt động.
    Ưu điểm:
        Chuẩn nhất, nhanh.
            Không giống như Ping Scan (sử dụng giao thức ICMP, Lớp 3), các gói tin ARP Request hoạt động ở Lớp 2 (Data Link Layer) và thường không thể bị tường lửa chặn trên các máy chủ trong cùng một LAN, khiến nó trở nên rất đáng tin cậy.
    Nhược điểm:
        Chỉ dùng được trong mạng LAN.
Kỹ thuật 3: TCP SYN Ping
    Lợi dụng giai đoạn đầu tiên của quá trình thiết lập kết nối TCP ba bước (Three-Way Handshake) để kiểm tra trạng thái của máy chủ.
    Gửi SYN đến một số port phổ biến (ví dụ: cổng 80-http, 443-https, 22-ssh), nếu nhận lại được SYN/ACK. Nếu nhận được:
        Phản hồi SYN/ACK -> cổng đó đang mở (Open) và máy chủ đang hoạt động (Alive).
        Phản hồi RST (Reset) -> cổng đó đang đóng (Closed) nhưng máy chủ đang hoạt động.
        Không có phản hồi hoặc nhận được lỗi ICMP (như Host Unreachable) -> máy chủ có thể không hoạt động hoặc đang bị chặn bởi tường lửa.
    Ưu điểm:
        Gói tin TCP SYN thường được phép đi qua tường lửa
        Tạo ra ít dấu vết trong log của máy chủ hơn do kỹ thuật này không hoàn thành quá trình bắt tay 3 bước 
        Cho phép người dùng lựa chọn cổng mục tiêu
    Nhược điểm:
        Mặc dù SYN Scan được gọi là "Stealth Scan" (Quét lén lút) so với Full Connect Scan (-sT) vì nó không hoàn thành bắt tay ba bước, nhưng các Hệ thống Phát hiện Xâm nhập (IDS) và Hệ thống Ngăn chặn Xâm nhập (IPS) hiện đại đã được cấu hình để dễ dàng phát hiện chuỗi SYN-SYN/ACK-RST bất thường.
            Việc gửi hàng loạt gói SYN mà không có gói ACK hoàn tất kết nối là một hành vi bất thường rõ rệt trong lưu lượng mạng, thường được coi là dấu hiệu của việc quét cổng ác ý.
        Khó phân biệt giữa Cổng đóng và Cổng được Lọc (Filtered)
            Trong một số trường hợp, nếu tường lửa chặn gói tin phản hồi SYN/ACK (khi cổng mở) hoặc chặn gói tin RST (khi cổng đóng), máy quét sẽ không nhận được bất kỳ phản hồi nào.
Kỹ thuật 4: TCP ACK Ping
    Nó khác biệt với TCP SYN Ping (đã đề cập trước đó) vì mục đích chính của nó không phải là xác định trạng thái cổng (mở/đóng) mà là để kiểm tra sự hiện diện của tường lửa.
    Gửi gói ACK → nếu nhận RST → host sống.
    Ưu điểm
        Rất tốt để bypass firewall vì nhiều firewall chỉ filter SYN.
        Tạo ít nghi ngờ hơn SYN.
    Nhược điểm
        Nếu firewall drop ACK vô hướng → sẽ không hiệu quả.
        Không xác định port mở, chỉ biết host sống.
    


    

