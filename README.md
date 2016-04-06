# tcpdump
##I. Khái niệm
- Tcpdump là phần mềm bắt gói tin trong mạng, làm việc trên hầu hết các phiên bản hệ điều hành unix/linux.

##II. Cấu trúc
###1. Câu lệnh
tcpdump [ -AbdDefhHIJKlLnNOpqStuUvxX# ] [ -B buffer_size ] [ -c count ] 

         [ -C file_size ] [ -G rotate_seconds ] [ -F file ] 

         [ -i interface ] [ -j tstamp_type ] [ -m module ] [ -M secret ] 

         [ --number ] [ -Q in|out|inout ] 
         [ -r file ] [ -V file ] [ -s snaplen ] [ -T type ] [ -w file ] 

         [ -W filecount ] 

         [ -E spi@ipaddr algo:secret,... ] 

         [ -y datalinktype ] [ -z postrotate-command ] [ -Z user ] 
         [ --time-stamp-precision=tstamp_precision ] 
         [ --immediate-mode ] [ --version ] 
         [ expression ] 
###2. Một số tùy chọn
| Tùy chọn | Mô tả |
|----------|-------|
| -A | Hiển thị các gói tin dưới dạng mã ACSII |
| -b | In số AS trong các gói tin BGP trong ký hiệu ASDOT hơn là ký hiệu ASPLAIN |
| -B size | Cài đặt buffer_size |
| -c | Thoát sau khi nhận được số lượng gói tin |
| -D | Liệt kê ra tất cả các interface đang hiện hữu trên máy có thể capture được |
| -e | Thay thế hiển thị địa chỉ IP của người gửi và người nhận bằng địa chỉ MAC |
| -i | Bắt gói tin từ một giao diện ethernet cụ thể |
| -q | Hiển thị ít thông tin hơn |
| -n | Không phân giải từ địa chỉ IP sang hostname|
| -L | Hiển thị danh sách các datalink type mà interface hỗ trợ |
| -N | Không in các quality domain name ra màn hình |
| -s | Định nghĩa snaplength (kích thước) gói tin sẽ lưu lại, sử dụng 0 để mặc định |
| -v | Tăng số lượng thông tin về gói tin có thể nhận được, thậm chí có thể tăng thêm với option –vv hoặc –vvv |
| -t | Bỏ qua thời gian bắt được gói tin khi hiển thị |
| -tt | Thời gian hiển thị trên mỗi dòng lệnh sẽ không được format theo dạng chuẩn |
| -ttt | Thời gian hiển thị chính là thời gian chênh lệnh giữa thời gian tcpdump bắt được gói tin của gói tin và gói tin đến trước |
| -tttt | Hiển thị thêm ngày vào mỗi dòng lệnh |
| -ttttt | Thời gian hiển thị trên mỗi dòng chính là thời gian chênh lệch giữa thời gian tcpdump bắt được gói tin của gói tin hiện tại và gói tin đầu tiên |
| -x | Hiển thị dữ liệu của gói tin capture dưới dạng mã Hex |
| -xx | Tương tự option –x tuy nhiên sẽ chuyển đổi cả Ethernet header |
| -X | Hiển thị dữ liệu của gói tin dưới dạng mã Hex và ASCII |
| -y | Lựa chọn datalinktype khi bắt các gói tin |

##III. Một số bộ lọc cơ bản
- dst A: Khi sử dụng option này, tcpdump sẽ chỉ capture các gói tin có địa chỉ đích là “A”, có thể sử dụng kèm với từ khóa net để chỉ định một dãy mạng cụ thể. Ví dụ: tcpdump dst net 192.168.1.0/24.
- Tương tự như option dst, nhưng thay vì capture các gói tin có địa chỉ đích cụ thể thì nó sẽ capture các gói tin có địa chỉ nguồn như quy định.
- host A: Khi sử dụng option này, tcpdump sẽ chỉ capture các gói tin có địa chỉ nguồn hoặc địa chỉ đích là “A”.
- port / port range: Khi sử dụng option này, tcpdump sẽ chỉ capture các gói tin có địa chỉ port được chỉ định rõ, hoặc nằm trong khoảng range định trước. Có thể sử dụng kèm với option dst hoặc src.
- less: Khi sử dụng từ khóa này, tcpdump sẽ lọc (filter) các gói tin có dung lượng nhỏ hơn giá trị chỉ định.
- greater: Khi sử dụng từ khóa này, tcpdump sẽ lọc (filter) các gói tin có dung lượng  cao hơn giá trị chỉ định.
- (ether | ip) broadcast: Capture các gói tin ip broadcast hoặc ethernet broadcast.
- (ether | ip | ip6) multicast: Capture các gói tin ethernet, ip , ipv6 multicast.
- Ngoài ra, tcpdump còn có thể capture các gói tin theo các protocol như : udp, tcp, icmp, ipv6  (chỉ cần gõ trực tiếp các từ khóa vào là được). Ví dụ: tcpdump icmp

##IV.Một số kết hợp trong tcpdump
- AND: Sử dụng từ khóa and hoặc &&.
- OR: Sử dụng từ khóa or hoặc ||.
- EXCEPT: sử dụng từ khóa not hoặc !.
- Ngoài ra để gom nhóm các điều kiện ta có thể dùng cặp từ khóa ‘’.  Ví dụ: tcpdump –i eth0 ‘dst host 192.168.1.1 or 192.168.1.10 or 192.168.1.11’

##V. Một số ví dụ
###1. Bắt số lượng N gói tin từ một giao diện ethernet cụ thể

<img src="http://i.imgur.com/FSzTeT4.png">

###2. Hiển thị các gói tin được bắt trong hệ ASCII thông qua tcpdump -A

<img src="http://i.imgur.com/l2INvED.png">

###3. Bắt gói tin và ghi vào một file thông qua tcpdump -w

<img src="http://i.imgur.com/voaSrJF.png">

###4. Đọc các gói tin từ một file thông qua tcpdump -r

<img src="http://i.imgur.com/Mdbi2Ph.png">

###5. Chỉ nhận những gói tin trong với một kiểu giao thức cụ thể

<img src="http://i.imgur.com/gupzz6D.png">

###6. Nhận các gói tin trên một cổng cụ thể thông qua tcpdump port

<img src="http://i.imgur.com/1jcEcSz.png">

###7. *Lưu ý: Trong lệnh tcpdump bạn có thể kết hợp các tùy chọn và sử dụng điều kiện “and”, “or” hoặc “not” để lọc các gói tin.*

##VI. Tham khảo
- http://www.tcpdump.org/manpages/tcpdump.1.html#lbAD
- http://www.thegeekstuff.com/2010/08/tcpdump-command-examples/
- https://vinahost.vn/ac/knowledgebase/248/TCPDUMP-va-cac-th-thut-s-dng.html
