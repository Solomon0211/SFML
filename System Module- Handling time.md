# Handling time
## Time trong SFML
  Không giống như thư viện khác mà ở đó thời gian được tính bằng miliseconds, hay phần thập phân của giây, SFML không áp đặt bất kì đơn vị hoặc kiểu cụ thế cho các giá trị thời gian, thay vào đó nó để lại lựa chọn này cho người dùng thông qua 1 lớp linh hoạt sf::Time. Tất cả các Class hoặc functions đều sử dụng lớp này.
  sf::Time đại diện cho 1 khoảng thời gian ( có thể hiểu khoảng thời gian trôi qua giữa 2 sự kiện ). Nó không thể hiện theo kiểu date-time là năm/tháng/ngày/giờ/phút/giây mà nó chỉ là 1 giá trị đại cho khoảng thời gian đó và diễn giải nó phụ thuộc vào ngữ cảnh nơi nó được sử.
 
 
## Chuyển đổi thời gian
  Giá trị sf::Time có thể xây dựng từ seconds, milisecond, microseconds.
  
    sf::Time t1 = sf::microseconds(10000);
    sf::Time t2 = sf::milliseconds(10);
    sf::Time t3 = sf::seconds(0.01f);
  
  Note:: 3 thời điểm đều bằng nhau
  
  Và có thể chuyển đổi ngược trờ về bằng cách :
  
    sf::Time time = ...;

    sf::Int64 usec = time.asMicroseconds();
    sf::Int32 msec = time.asMilliseconds();
    float     sec  = time.asSeconds();



## Làm việc với các giá trị thời gian

  sf::Time là chỉ 1 lượng thời gian nên nó có thể thực hiện các phép toán là +, -, *, /, so sánh... Thời gian cũng có số âm.

    sf::Time t1 = ...;
    sf::Time t2 = t1 * 2;
    sf::Time t3 = t1 + t2;
    sf::Time t4 = -t3;

    bool b1 = (t1 == t2);
    bool b2 = (t3 > t4);

## Đo thời gian

  Đây là cách làm thể nào để vận dụng SFML để đo thời gian trôi qua. Và hầu hết mỗi program đều cần tính thời gian trôi qua ( measuring the time elapsed ).

SFML có 1 cách đơn giản để đo thời gian là sf::Clock. Nó chỉ có 2 functions: ``**getElepsedTime**`` để lấy thời gian kể từ khi đồng hồ bắt đầu, và ``restart`` để bắt đầu lại đồng hồ. 

    sf::Clock clock; // starts the clock
    ...
    sf::Time elapsed1 = clock.getElapsedTime();
    std::cout << elapsed1.asSeconds() << std::endl;
    clock.restart();
    ...
    sf::Time elapsed2 = clock.getElapsedTime();
    std::cout << elapsed2.asSeconds() << std::endl;
    
    
Note: ``restart`` cũng trả về giá trị thời gian trôi qua, vì vậy để tránh 1 số lỗi nhỏ có thể xảy ra thì bạn phải gọi ``getElapsedTime``1 cách rõ ràng trước khi ``restart`` .Chỗ này mình cũng chả pit dích s cho sát nghĩa nữa bạn nào giỏi tiếng anh thì dịch nha @@ Note that restart also returns the elapsed time, so that you can avoid the slight gap that would exist if you had to call getElapsedTime explicitly before restart.

  Dưới dây là ví dụ sử dụng thời gian trôi mỗi lần lặp lại của vòng lặp trò chơi để update the game logic.

    sf::Clock clock;
    while (window.isOpen())
    {
        sf::Time elapsed = clock.restart();
        updateGame(elapsed);
        ...
    }



`` Đây là bài viết mang ý kiến cá nhân mình hiểu được nên có sai sót gì các bạn cứ comment để mình sữa lại nhaa <3``
[link bài viết gốc ở đây](https://www.sfml-dev.org/tutorials/2.5/system-time.php)


