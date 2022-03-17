# Threads

## ``Thread`` là gì ???
  1 Threand ( 1 luồng ) về cơ bản là chuối các lệnh chạy song song với các luồng khác. Mỗi chương trình được làm ít nhất từ  1 ``Thread``: hàm ``main()``. Chương trình chỉ sử dụng ``main Thread`` là đơn luồng, nếu bạn thêm 1 hoặc nhiều luồng ( Thread ) chúng sẽ trờ thành đa luồng ( multi-threaded )
  Tóm lại, Thread ( luồng ) là cách để thực hiện nhiều công việc cùng lúc. Ví dụ,  để hiển thị ảnh động và react với đầu vào của người dùng trong khi load âm thanh hoặc hình ảnh. Thread cũng được sử dụng rộng rãi trong Network programming, để chờ nhận dữ liệu trong khi tiếp tục cập nhâp và vẽ ứng dụng. 
  
## SFML threads or std::thread ?
  Trong phiên bản 2011 của C++, Thư viện chuẩn trong C++ có cấp class về phân luồng. Tại thời điểm SFML được viết, C++11 vẫn chưa được viết và không có cách tiêu chuẩn để tạo luồng. Khi SFML 2.0 được phát hành, vẫn có rất nhiều vẫn không hỗ trợ cái này.
    Nếu bạn sử dụng trình biển dịch có hỗ trợ thread thì nó là <thread> header, `` quên đi thread của SFML và sử dụng nó sẽ tốt hơn nhiều. `` Nhưng nếu bạn sử dụng trình biên dịch trước năm 2011 thì dùng `` thread của SFML là giải pháp tốt nhất. ``

  
## Creating thread with SFML
  Class có khả năng tạo ra  thread trong SFML là sf::thread và đây là cách nó hoạt động:
  
    #include <SFML/System.hpp>
    #include <iostream>

    void func()
    {
        // hàm này sẽ chạy khi có lệnh `` thread.launch() `` được gọi.

        for (int i = 0; i < 10; ++i)
            std::cout << "I'm thread number one" << std::endl;
    }

    int main()
    {
        // tạo ra thread với func() là dữ liệu vào
        sf::Thread thread(&func);

        // run it
        thread.launch();

        // the main thread continues to run...

        for (int i = 0; i < 10; ++i)
            std::cout << "I'm the main thread" << std::endl;

        return 0;
    }
  
  
  Trong code này, cả 2 hàm `` main() `` và `` func() `` đều chạy song song với nhau sau khi lệnh `` thread.lauch() `` được gọi. Kết quả là test của 2 function trộn lẫn vào nhau trong màn hình console. 
  
  ![image](https://user-images.githubusercontent.com/91585606/158830063-0faf6909-5489-431b-b88d-20576aecb782.png)

  Điểm đầu vào của thread ( the entry point of the thread ), tức là function sẽ được chạy khi thread bắt đầu, sẽ được chuyển tới sf::thread, sf::thread sẽ cố gắng linh hoạt và chấp nhận nhiều điểm nhập: non-member function or member function, có hoặc hông có đối số, function,... Xem ví dụ để rõ hơn:
  
  - No-member function với 1 đối số
  
    void func(int x)
    {
    }

    sf::Thread thread(&func, 5);
  
