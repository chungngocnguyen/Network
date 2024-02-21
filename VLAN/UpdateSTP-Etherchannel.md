# Etherchannel: 
## Thuật toán Hash:
+ Là hàm chuyển đổi 1 giá trị sang giá trị khác
+ với 1 đầu vào ngẫu nhiên, hashing tạo ra 1 giá trị tương ứng
+ Đầu vào khác nhau xuất ra các giá trị khác nhau


## Thuật toán hash trong etherchannel
+ SW lựa chọn đường link để forward frame dựa vào kết quả thuật toán hash
+ Input: Địa chỉ IP nguồn, đích; địa chỉ MAC nguồn, đích; có thể sử dụng cổng TCP/UDP.
+ Output: THuật toán hash tính toán ra các giá trị nhị phân, giá trị chọn ra 1 kết nối trong bundle để chọn ra kết nối thành viên nào sẽ mang frame đó. 
+ Nếu chỉ có source hoặc destination được hash (IP, MAC, port number): sử dụng 1 hoặc nhiều bits thấp của giá trị hash để lựa chọn link trong etherchannel
+ Cả source và destination được hash, sw thực hiện phép toán XOR trên 1 hoặc nhiều bit thấp để làm index.
![](https://thegioimang.vn/dien-dan/attachments/upload_2017-8-22_9-38-59-jpeg.56/)

Load balancing:
![](https://thegioimang.vn/dien-dan/attachments/upload_2017-8-22_9-39-7-jpeg.57/)


# Spanning tree protocol
## Hậu quả của Loop:
### Broadcast storm:
![](https://tailamblog.files.wordpress.com/2017/08/513.png)
Như hình trên:
	    1. Máy A muốn gửi dữ liệu cho máy B sẽ dùng ARP request để tìm địa chỉ MAC máy B.
    	Khi đó SW sẽ gửi các request ra tất cả các port (trừ port 1) để sang sw2 và sw3
	    2. Sw2 cũng gửi ARP request ra tất cả các port, có gói đi đến đích là máy B, 1 gói 		tới máy C và 1 gói đi tới SW3
	    3. SW3 sẽ trung gian gửi dữ liệu ra tất cả các port trừ port 3, gói tin sẽ quay trở lại SW1 tạo ra vòng lặp dữ liệu vô tận.
###  MAC Address Table Instability-Bảng địa chỉ MAC không ổn định và thay đổi liên tục: 
SW khi gửi thông tin đi nó cũng cập nhật MAC và Port gửi đi vào bảng định tuyến. Khi có vô hạn vòng lặp, các gói được gửi liên tục qua nhiều con đường khác nhau dẫn đế thông tin bảng MAC phải cập nhật liên tục

### Quá trình thực hiện: 
### 1. Bình bầu root bridge:
+ SW có priority nhỏ nhất làm root (Bridge priority + MAC )
### 2. Xác định Root Port :
+ Xác định đường đi ngắn nhất đến Root Bridge
+ Dựa vào số cost, cost nhỏ nhất thì port sẽ là root port, cost = nhau thì xét MAC nhỏ nhất
+ Thay đổi băng thông thì cost thay đổi nên vẫn xác định được Root port 
![](https://tailamblog.files.wordpress.com/2017/08/79.png?w=616)
### 3. Xác định Deginated port:
+ SW là root bridge thì các port đều là DP
+ 1 kết nối: 1 đầu là RP, đầu còn lại là DP
+ Các sw còn lại chưa xác định thì port tạo đường đi ngắn nhất là DP. Bằng cost thì so sánh bảng MAC
![](https://www.upsieutoc.com/images/2020/07/16/107947814_375950156921034_4609593664093057223_n.jpg)
