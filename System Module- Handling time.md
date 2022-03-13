# Handling time
## Time trong SFML
  Không giống như thư viện khác mà ở đó thời gian được tính bằng miliseconds, hay phần thập phân của giây, SFML không áp đặt bất kì đơn vị hoặc kiểu cụ thế cho các giá trị thời gian, thay vào đó nó để lại lựa chọn này cho người dùng thông qua 1 lớp linh hoạt sf::Time. Tất cả các Class hoặc functions đều sử dụng lớp này.
  sf::Time đại diện cho 1 khoảng thời gian ( có thể hiểu khoảng thời gian trôi qua giữa 2 sự kiện ). Nó không thể hiện theo kiểu date-time là năm/tháng/ngày/giờ/phút/giây mà nó chỉ là 1 giá trị đại cho khoảng thời gian đó và diễn giải nó phụ thuộc vào ngữ cảnh nơi nó được sử.
 
 
## Chuyển đổi thời gian
  Giá trị sf::Time có thể xây dựng từ seconds, milisecond, microseconds.
  ![image](https://user-images.githubusercontent.com/91585606/158044951-3e89140a-1f4f-427a-8cef-f65ad1a29e27.png)
  Note:: 3 thời điểm đều bằng nhau
  
  Và có thể chuyển đổi ngược trờ về bằng cách :
  
  ![image](https://user-images.githubusercontent.com/91585606/158044983-51b332e7-bdaa-4eed-b821-ee2d51443f2e.png)



## Làm việc với các giá trị thời gian

  sf::Time là chỉ 1 lượng thời gian nên nó có thể thực hiện các phép toán là +, -, *, /, so sánh... Thời gian cũng có số âm.
![image](https://user-images.githubusercontent.com/91585606/158045026-a976993a-2257-481b-ab78-ff2854d7251d.png)

## Đo thời gian

  Đây là cách làm thể nào để vận dụng SFML để đo thời gian trôi qua. Và hầu hết mỗi program đều cần tính thời gian trôi qua ( measuring the time elapsed ).

SFML có 1 cách đơn giản để đo thời gian là sf::Clock. Nó chỉ có 2 functions: ``sdfasdfd``
