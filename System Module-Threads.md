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

 - Member function
   
    class MyClass
    {
    public:

        void func()
        {
        }
    };

    MyClass object;
    sf::Thread thread(&MyClass::func, &object);
  
  
- Functor (function-object):
  
    struct MyFunctor
    {
        void operator()()
        {
        }
    };

    sf::Thread thread(MyFunctor());
  
  - Ví dụ cuối cùng đó là sử dụng functors, lầ ví dụ tốt nhất vì nó có thể chấp nhận bất kì loại functor nào và do đó làm cho sf::thread tương thích với nhiều loại hàm không hỗ trợ trực tiếp. Nó khá đặc biệt với C++11 lambdas hoặc std::blind.
  
    // with lambdas
    sf::Thread thread([](){
        std::cout << "I am in thread!" << std::endl;
    });
  

    // with std::bind
    void func(std::string, int, double)
    {
    }

    sf::Thread thread(std::bind(&func, "hello", 24, 0.5));
  
  
  Nếu bạn muốn sử dụng sf::thread bên trong class, đừng quên rằng không có hàm tạo mặc định. Vì vậy, bạn có thể khỏi tạo nó trực tiếp trong danh sách khởi tạo (Initialize List) của hàm khởi tạo. 
  
    class ClassWithThread
    {
    public:

        ClassWithThread()
        : m_thread(&ClassWithThread::f, this)
        {
        }

    private:

        void f()
        {
            ...
        }

        sf::Thread m_thread;
    };
  
  
  Nếu bạn cần xây dựng cá thể sf::thread sau khi xây dựng owner object. Bạn cũng có thể trì hoãn bằng cách xây dựng nó bằng cách phân bố động nó trên heap.
  
  
  ## Starting threads
  
  Khi bạn tạo 1 sf::thread, bạn phải sử dụng nó với `` lauch() `` funtion.
  
    sf::Thread thread(&func);
    thread.launch();
  
  Khi gọi lauch() funtion, có nghĩa là bạn đã chuyển hàm tạo vào 1 luồng mới và trả về ngạy lập tức để luồng đang gọi có thể tiếp tục chạy. 
  
  
  ## Stopping threads
  
  Thread tự động dừng khi điểm đầu vào ( entry funtions ) return . Nếu bạn muốn chờ 1 luồng kết thúc theo khi luồng khác kết thúc, bạn có thể gọi wait() function. 
  
  
    sf::Thread thread(&func);

    // start the thread
    thread.launch();

    ...

    // block execution until the thread is finished
    thread.wait();
  
  
  `` wait() funtion `` cũng được gọi ngầm bởi hàm huy của sf::thread, do đó một chuỗi không thể vẫn tồn tại (và ngoài tầm kiểm soát) sau khi cá thể chủ sở hữu sf :: Thread bị hủy. Hãy ghi nhớ điều này khi bạn quản lý chủ đề của mình (xem phần cuối cùng của hướng dẫn này).
  
  ## Pausing threads 
  
  Không có chức năng nào trong sf :: Thread cho phép một luồng khác tạm dừng nó, cách duy nhất để tạm dừng một luồng là thực hiện nó từ mã mà nó chạy. Nói cách khác, bạn chỉ có thể tạm dừng luồng hiện tại. Để làm như vậy, bạn có thể gọi hàm sf :: sleep:
  

    void func ()

    {

    ...

    sf :: sleep (sf :: mili giây (10));

    ...

    }

sf :: sleep có một đối số, đó là thời gian để ngủ. Khoảng thời gian này có thể được cung cấp với bất kỳ đơn vị / độ chính xác nào, như đã thấy trong hướng dẫn thời gian.

Lưu ý rằng bạn có thể đặt bất kỳ luồng nào ở chế độ ngủ bằng chức năng này, ngay cả chức năng chính.

sf :: sleep là cách hiệu quả nhất để tạm dừng một luồng: miễn là luồng ngủ, nó yêu cầu CPU bằng không. Việc tạm dừng dựa trên hoạt động chờ đợi, chẳng hạn như các vòng lặp trong khi trống, sẽ tiêu tốn 100% CPU chỉ để ... không làm gì cả. Tuy nhiên, hãy nhớ rằng thời lượng ngủ chỉ là một gợi ý, tùy thuộc vào hệ điều hành mà nó sẽ chính xác hơn hoặc ít hơn. Vì vậy, đừng dựa vào nó để
  
  
  ## Protecting shared data
  
  Tất cả các luồng trong một chương trình dùng chung một bộ nhớ, chúng có quyền truy cập vào tất cả các biến trong phạm vi mà chúng đang ở. Điều đó rất tiện lợi nhưng cũng nguy hiểm: vì các luồng chạy song song, có nghĩa là một biến hoặc hàm có thể được sử dụng đồng thời từ một số chủ đề cùng một lúc. Nếu hoạt động không an toàn theo luồng, nó có thể dẫn đến hành vi không xác định (tức là nó có thể bị hỏng hoặc làm hỏng dữ liệu).

Một số công cụ lập trình tồn tại để giúp bạn bảo vệ dữ liệu được chia sẻ và làm cho chuỗi mã của bạn an toàn, những công cụ này được gọi là nguyên thủy đồng bộ hóa. Những cái phổ biến là mutexes, semaphores, biến điều kiện và khóa quay. Chúng đều là các biến thể của cùng một khái niệm: chúng bảo vệ một đoạn mã bằng cách chỉ cho phép một số luồng nhất định truy cập vào nó trong khi chặn các luồng khác.

Nguyên thủy cơ bản nhất (và được sử dụng) là mutex. Mutex là viết tắt của "MUTual EXclusion": nó đảm bảo rằng chỉ một luồng duy nhất có thể chạy mã mà nó bảo vệ. Hãy xem cách họ có thể mang lại một số trật tự cho ví dụ trên:
   
    #include <SFML/System.hpp>
    #include <iostream>

    sf::Mutex mutex;

    void func()
    {
        mutex.lock();

        for (int i = 0; i < 10; ++i)
            std::cout << "I'm thread number one" << std::endl;

        mutex.unlock();
    }

    int main()
    {
        sf::Thread thread(&func);
        thread.launch();

        mutex.lock();

        for (int i = 0; i < 10; ++i)
            std::cout << "I'm the main thread" << std::endl;

        mutex.unlock();

        return 0;
    }
  
  
  Mã này sử dụng tài nguyên được chia sẻ (std :: cout) và như chúng ta đã thấy, nó tạo ra các kết quả không mong muốn - mọi thứ được trộn lẫn trong bảng điều khiển. Để đảm bảo rằng các dòng hoàn chỉnh được in đúng cách thay vì bị trộn ngẫu nhiên, chúng tôi bảo vệ vùng tương ứng của mã bằng mutex.

Luồng đầu tiên đạt đến dòng mutex.lock () thành công để khóa mutex, trực tiếp có quyền truy cập vào mã theo sau và in văn bản của nó. Khi luồng khác đạt đến dòng mutex.lock () của nó, mutex đã bị khóa và do đó luồng được đưa vào trạng thái ngủ (như sf :: sleep, không có thời gian CPU nào bị tiêu tốn bởi luồng đang ngủ). Khi luồng đầu tiên cuối cùng mở khóa mutex, luồng thứ hai được đánh thức và được phép khóa mutex cũng như in khối văn bản của nó. Điều này dẫn đến các dòng văn bản xuất hiện tuần tự trong bảng điều khiển thay vì bị trộn lẫn.
  
  
  ![image](https://user-images.githubusercontent.com/91585606/158834275-3ba950b3-014c-440a-b01e-98abc9f98171.png)

  
  Mutexes không phải là nguyên thủy duy nhất mà bạn có thể sử dụng để bảo vệ các biến được chia sẻ của mình, nhưng nó phải là đủ cho hầu hết các trường hợp. Tuy nhiên, nếu ứng dụng của bạn thực hiện những việc phức tạp với các luồng và bạn cảm thấy như vậy là chưa đủ, đừng ngần ngại tìm kiếm một thư viện phân luồng thực sự, với nhiều tính năng hơn.
  
  ## Protecting mutexes

Đừng lo lắng: mutexes đã an toàn theo luồng, không cần phải bảo vệ chúng. Nhưng chúng không phải là ngoại lệ an toàn! Điều gì xảy ra nếu một ngoại lệ được ném ra trong khi mutex bị khóa? Nó không bao giờ có cơ hội được mở khóa và vẫn bị khóa mãi mãi. Tất cả các chuỗi cố gắng khóa nó trong tương lai sẽ chặn vĩnh viễn và trong một số trường hợp, toàn bộ ứng dụng của bạn có thể bị đóng băng. Kết quả khá tệ.

Để đảm bảo rằng mutexes luôn được mở khóa trong môi trường có thể đưa ra các ngoại lệ, SFML cung cấp một lớp RAII để bọc chúng: sf :: Lock. Nó khóa một mutex trong hàm tạo của nó và mở khóa nó trong trình hủy của nó. Đơn giản và hiệu quả.

    sf :: Mutex mutex;

    void func ()

    {

    sf :: Khóa khóa (mutex); // mutex.lock ()

    functionThatMightThrowAnException (); // mutex.unlock () nếu hàm này ném

    } // mutex.unlock ()

Lưu ý rằng sf :: Lock cũng có thể hữu ích trong một hàm có nhiều câu lệnh trả về.

    sf :: Mutex mutex;

    bool func ()

    {

    sf :: Khóa khóa (mutex); // mutex.lock ()

    if (! image1.loadFromFile ("..."))

    trả về sai; // mutex.unlock ()

    if (! image2.loadFromFile ("..."))

    trả về sai; // mutex.unlock ()

    if (! image3.loadFromFile ("..."))

    trả về sai; // mutex.unlock ()

    trả về true;

    } // mutex.unlock ()

  ## Common mistakes

Một điều mà các lập trình viên thường bỏ qua là một luồng không thể tồn tại nếu không có cá thể sf :: Thread tương ứng của nó.

Đoạn mã sau đây thường thấy trên các diễn đàn:

    void startThread ()

    {

    sf :: Chuỗi chủ đề (& funcToRunInThread);

    thread.launch ();

    }

    int main ()

    {

    startThread ();

    // ...

    trả về 0;

    }

Các lập trình viên viết loại mã này mong đợi hàm startThread () bắt đầu một luồng sẽ tự tồn tại và bị hủy khi hàm luồng kết thúc. Đây không phải là những gì xảy ra. Hàm luồng xuất hiện để chặn luồng chính, như thể luồng đó không hoạt động.

Nguyên nhân của việc này là gì? Cá thể sf :: Thread là cục bộ của hàm startThread () và do đó sẽ bị hủy ngay lập tức khi hàm trả về. Hàm hủy của sf :: Thread được gọi, gọi hàm wait () như chúng ta đã học ở trên, và kết quả là luồng chính sẽ chặn và đợi hàm luồng kết thúc thay vì tiếp tục chạy song song.

Vì vậy, đừng quên: Bạn phải quản lý cá thể sf :: Thread của mình để nó tồn tại miễn là hàm luồng được cho là chạy.
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  

