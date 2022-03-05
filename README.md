# SFML- Cài đặt và chạy chương trình đầu tiên với thư viện đồ họa SFML

## Table of Contents
- [0.Sơ lược về SFML](#1.Tải-bản-pre-built-SFML)
- [1.Tải bản pre-built SFML](#tải-bản-pre-built-SFML)
- [2.Tìm hiểu về các thư mục trong bản pre-built](#tìm-hiểu-về-thư-mục-trong-pre-built)
- [3.Cài đặt SFML vào project](cài-đặt



1. Tải bản pre-built SFML

Để tải thì các bạn lên trang chủ của SFML.

Tập tin đính kèm:

Trang chủ:  https://www.sfml-dev.org/
Tại trang chủ thì các bạn chọn Download.

Tập tin đính kèm:

Hiện tại thì phiên bản mới nhất của SFML là 2.5.1, ta chọn vào SFML 2.5.1.

Tập tin đính kèm:

Tại đây, các bạn sẽ thấy các bản pre-built cho các phiên bản của Visual Studio. Các bản này phân ra làm 2 loại: 32bit và 64bit. Nếu bạn chọn bản 32bit thì khi build ra chương trình có thể chạy trên cả windows 32bit và 64bit. Còn bạn chọn 64bit thì khi build ra chương trình chỉ chạy được trên windows 64bit.

Tập tin đính kèm:

Ở đây mình sẽ tải bản cho Visual Studio 2017 64bit nhé!

2. Tìm hiểu các thư mục trong bản pre-built

Sau khi tải về, các bạn tiến hành giải nén sẽ được như hình. Ta chỉ quan tâm các thư mục bin, include, lib.

Tập tin đính kèm:

Thư mục include là thư mục chứa các file header của SFML. Khi code các bạn phải include chúng thì mới có thể dùng được SFML.

Tập tin đính kèm:

Thư mục lib là thư mục chứa các file .lib. Cái này mình chả biết giải thích sao 😀 nhưng nôm na là phải có để các bạn có thể build ra file .exe. Nếu không sẽ bị lỗi.

Tập tin đính kèm:

Thư mục bin là thư mục chứa các file .dll (dynamic linker library). Cần thiết cho chương trình khi build ở dạng dynamic linker.

Tập tin đính kèm:

Trong thư mục examples là các chương trình demo của SFML, bạn có thể vào để thử. Nếu lúc chạy có bị thiếu file .dll thì cứ vào thư mục bin mà tìm.

Tập tin đính kèm:

3. Cài đặt SFML vào project
3.1. Tạo project trên Visual Studio

Các bạn tạo cho mình một Empty project. Ở đây mình sẽ đặt tên là SFML-Tutorial.

Tập tin đính kèm:

Tập tin đính kèm:

Rồi các bạn add file Main.cpp vào project.

Tập tin đính kèm:

Lúc nãy nếu các bạn tải bản SFML cho windows 64bit thì chỉnh project ở dạng x64 (bạn nào tải 32bit thì thôi).
Tập tin đính kèm:
3.2. Cấu hình project

Các bạn chọn chuột phải vào tên project sau đó chọn Property.

Tập tin đính kèm:

Sau khi mở, các bạn chọn đến mục C++ ---> General ---> Additional Include Directories ---> Edit.

Tập tin đính kèm:

Tại đây, các bạn chọn đến thư mục include trong thư mục SFML đã tải về (trong ảnh gif mình chỉ làm bên Debug, bên Release các bạn làm tương tự, do mình lười thôi 😀).

Tập tin đính kèm:

Tiếp theo các bạn chọn đến mục Linker ---> General ---> Additional Library Directories ---> Edit.

Tập tin đính kèm:

Tại đây, các bạn chọn đến thư mục lib trong thư mục SFML đã tải về (trong ảnh gif mình chỉ làm bên Debug, bên Release các bạn làm tương tự, lí do như trên 😀).

Tập tin đính kèm:

Sau đó các bạn đến mục Linker ---> Input ---> Additional Dependencies ---> Edit.

Tập tin đính kèm:

Ở bước này sẽ có sự khác nhau giữa Release và Debug nên mình sẽ chia ra 2 phần.
Ở Debug, các bạn gõ như sau (gõ như thế là đã cài đủ 5 module của SFML, copy paste mỗi cái cái rồi enter rồi tiếp tục các khác)
sfml-graphics-d.lib
sfml-audio-d.lib
sfml-network-d.lib
sfml-window-d.lib
sfml-system-d.lib

Tập tin đính kèm:

Ở Release, các bạn gõ như sau:
sfml-graphics.lib
sfml-audio.lib
sfml-network.lib
sfml-window.lib
sfml-system.lib

Tập tin đính kèm:

Sau đó các bạn nháy OK để hoàn tất các quá trình.

3.3. Test thử

Thế là OK. Bây giờ các bạn copy đoạn code bên dưới để test.
#include <SFML/Graphics.hpp>
 
int main()
{
    sf::RenderWindow window(sf::VideoMode(900, 500), "SFML-Tutorial", sf::Style::Close);
    window.setFramerateLimit(60);
 
    sf::RectangleShape rectang(sf::Vector2f(400, 220));
 
    rectang.setPosition(250, 140);
    rectang.setFillColor(sf::Color::Yellow);
 
    while (window.isOpen())
    {
        sf::Event event;
        while (window.pollEvent(event))
        {
            if (event.type == sf::Event::EventType::Closed)
            {
                window.close();
            }
        }
 
        window.clear();
 
        window.draw(rectang);
 
        window.display();
    }
 
    return 0;
}

Sau đó các bạn hãy build.

Tập tin đính kèm:

Như thế là đã thành công. Bây giờ các bạn hãy vào đường dẫn mà nó hiển thị trong Output để tìm file exe đã build.
Tuy nhiên lúc này, nếu các bạn mở lên thì sẽ bị lỗi thiếu các file dll.

Tập tin đính kèm:

Để khắc phục, các bạn vào thư mục bin của SFML để tìm các file dll bị thiếu và paste vào. Sau đó hãy run lần nữa để thử lại.

Tập tin đính kèm:

Đó là các cài đặt SFML cho project Visual Studio ở dạng dynamic linker. Ở dạng dynamic linker thì chương trình của các bạn sẽ phải cần các file dll để chạy. Nếu các bạn không thích sự phiền hà đó thì có thể cài đặt ở dạng static. Lúc này thì chương trình của các bạn sẽ không cần các file dll của SFML (vẫn cần file openal32.dll) nhưng chương trình của các bạn sẽ nặng hơn rất nhiều .

4. Cài đặt SFML dạng static linker

Các bước thì vẫn giống như trên. Chỉ có thêm 1 bước và khác bước add các file lib tại mục Additional Dependencies.
Các bạn mở chọn C++ ---> Preprocessor --> Preprocessor Definitions ---> Edit

Tập tin đính kèm:

Các bạn gõ thêm dòng SFML_STATIC (làm cả Debug lẫn Release nhé).

Tập tin đính kèm:

Ở Debug, các bạn thêm như sau. Chú ý là phải đúng thứ tự.
sfml-graphics-s-d.lib
sfml-window-s-d.lib
sfml-audio-s-d.lib
sfml-network-s-d.lib
sfml-system-s-d.lib
opengl32.lib
freetype.lib
winmm.lib
gdi32.lib
openal32.lib
flac.lib
vorbisenc.lib
vorbisfile.lib
vorbis.lib
ogg.lib
ws2_32.lib

Ở Release, các bạn thêm như sau. Chú ý như trên .
sfml-graphics-s-d.lib
sfml-window-s-d.lib
sfml-audio-s-d.lib
sfml-network-s-d.lib
sfml-system-s-d.lib
opengl32.lib
freetype.lib
winmm.lib
gdi32.lib
openal32.lib
flac.lib
vorbisenc.lib
vorbisfile.lib
vorbis.lib
ogg.lib
ws2_32.lib

Sau đó các bạn nhấn OK để hoàn tất, rồi run và tận hưởng 😀
OK, bài viết đến đây là hết rồi. Mình sẽ viết về cài đặt SFML cho Codeblocks trên Windows vào Phần 2.
Các bạn cứ bình luận để bày tỏ ý kiến về bài viết cho mình nhé!! Bye 😀

