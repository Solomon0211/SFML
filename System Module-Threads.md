# Threads

## ``Thread`` là gì ???
  1 Threand ( 1 luồng ) về cơ bản là chuối các lệnh chạy song song với các luồng khác. Mỗi chương trình được làm ít nhất từ  1 ``Thread``: hàm ``main()``. Chương trình chỉ sử dụng ``main Thread`` là đơn luồng, nếu bạn thêm 1 hoặc nhiều luồng ( Thread ) chúng sẽ trờ thành đa luồng ( multi-threaded )
  Tóm lại, Thread ( luồng ) là cách để thực hiện nhiều công việc cùng lúc. Ví dụ,  để hiển thị ảnh động và react với đầu vào của người dùng trong khi load âm thanh hoặc hình ảnh. Thread cũng được sử dụng rộng rãi trong Network programming, để chờ nhận dữ liệu trong khi tiếp tục cập nhâp và vẽ ứng dụng. 
  
## SFML threads or std::thread ?
  Trong phiên bản 2011 của C++, Thư viện chuẩn trong C++ có cấp class về phân luồng. Tại thời điểm SFML được viết, C++11 vẫn chưa được viết và không có cách tiêu chuẩn để tạo luồng. Khi SFML 2.0 được phát hành, vẫn có rất nhiều vẫn không hỗ trợ cái này.
    Nếu bạn sử dụng trình biển dịch có hỗ trợ thread thì nó là <thread> header, quên đi ``thread`` của SFML và ``sử dụng nó sẽ tốt hơn nhiều``. 
