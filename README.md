# SFML- Cài đặt và chạy chương trình đầu tiên với thư viện đồ họa SFML

## Table of Contents
- [0.Sơ lược về SFML](#1.Tải-bản-pre-built-SFML)
- [1.Tải bản pre-built SFML](#tải-bản-pre-built-SFML)
- [2.Tìm hiểu về các thư mục trong bản pre-built](#tìm-hiểu-về-thư-mục-trong-pre-built)
- [3.Cài đặt SFML vào project](cài-đặt-SFML-vao-project)



1. Tải bản pre-built SFML

Để tải thì các bạn lên trang chủ của SFML.

![ckukgdu0am_sfml-homepage (1)](https://user-images.githubusercontent.com/91585606/156887354-7b5f637a-1738-40fd-9e8a-5ae714bd835c.png)


Trang chủ:  https://www.sfml-dev.org/
Tại trang chủ thì các bạn chọn Download.

![image](https://user-images.githubusercontent.com/91585606/156887384-00b531b7-c3ae-4910-91dc-2f8dd4463958.png)

Hiện tại thì phiên bản mới nhất của SFML là 2.5.1, ta chọn vào SFML 2.5.1.

![image](https://user-images.githubusercontent.com/91585606/156887404-458c184b-8f8a-4736-8ea9-d6f99caa8771.png)

Tại đây, các bạn sẽ thấy các bản pre-built cho các phiên bản của Visual Studio. Các bản này phân ra làm 2 loại: 32bit và 64bit. Nếu bạn chọn bản 32bit thì khi build ra chương trình có thể chạy trên cả windows 32bit và 64bit. Còn bạn chọn 64bit thì khi build ra chương trình chỉ chạy được trên windows 64bit.

![image](https://user-images.githubusercontent.com/91585606/156887419-571389df-c081-4777-a052-936bc82ba219.png)

Ở đây mình sẽ tải bản cho Visual Studio 2017 64bit nhé!

2. Tìm hiểu các thư mục trong bản pre-built

Sau khi tải về, các bạn tiến hành giải nén sẽ được như hình. Ta chỉ quan tâm các thư mục bin, include, lib.

![image](https://user-images.githubusercontent.com/91585606/156887434-39838358-141b-45d2-b05f-7eba5b9bd791.png)

Thư mục include là thư mục chứa các file header của SFML. Khi code các bạn phải include chúng thì mới có thể dùng được SFML.

![image](https://user-images.githubusercontent.com/91585606/156887438-f21b5302-fe6b-40f2-8c9f-0563a23f6643.png)

Thư mục lib là thư mục chứa các file .lib. Cái này mình chả biết giải thích sao 😀 nhưng nôm na là phải có để các bạn có thể build ra file .exe. Nếu không sẽ bị lỗi.

![image](https://user-images.githubusercontent.com/91585606/156887449-0325c8b9-34a9-4078-843b-4c831b8f0be9.png)

Thư mục bin là thư mục chứa các file .dll (dynamic linker library). Cần thiết cho chương trình khi build ở dạng dynamic linker.

![image](https://user-images.githubusercontent.com/91585606/156887455-f620cd9e-8de8-4f60-a2e0-c4d03d8365f7.png)

Trong thư mục examples là các chương trình demo của SFML, bạn có thể vào để thử. Nếu lúc chạy có bị thiếu file .dll thì cứ vào thư mục bin mà tìm.

![image](https://user-images.githubusercontent.com/91585606/156887460-c9f7ba6e-acef-4725-938f-06193797681d.png)

3. Cài đặt SFML vào project
3.1. Tạo project trên Visual Studio

Các bạn tạo cho mình một Empty project. Ở đây mình sẽ đặt tên là SFML-Tutorial.

![image](https://user-images.githubusercontent.com/91585606/156887505-16af5905-ed83-4673-b05c-015ca430a79f.png)

![image](https://user-images.githubusercontent.com/91585606/156887511-168edafb-0721-4942-83e5-add798fce0d3.png)

Rồi các bạn add file Main.cpp vào project.

![image](https://user-images.githubusercontent.com/91585606/156887512-7942aefb-9fe6-4b00-8e05-0212a17216ed.png)

Lúc nãy nếu các bạn tải bản SFML cho windows 64bit thì chỉnh project ở dạng x64 (bạn nào tải 32bit thì thôi).
Tập tin đính kèm:
3.2. Cấu hình project

Các bạn chọn chuột phải vào tên project sau đó chọn Property.

![image](https://user-images.githubusercontent.com/91585606/156887522-45521fcd-2a5b-4b87-83bb-fe485c29a4b3.png)

Sau khi mở, các bạn chọn đến mục C++ ---> General ---> Additional Include Directories ---> Edit.

![image](https://user-images.githubusercontent.com/91585606/156887531-7a52c865-06f8-4066-b955-d373b08285e0.png)

Tại đây, các bạn chọn đến thư mục include trong thư mục SFML đã tải về (trong ảnh gif mình chỉ làm bên Debug, bên Release các bạn làm tương tự, do mình lười thôi 😀).

![image](https://user-images.githubusercontent.com/91585606/156887536-7a2218d7-749d-4333-ac9e-6ffa0df887eb.png)

Tiếp theo các bạn chọn đến mục Linker ---> General ---> Additional Library Directories ---> Edit.

![image](https://user-images.githubusercontent.com/91585606/156887563-84e0414e-f1c9-4025-8203-23f5921b6ad9.png)

Tại đây, các bạn chọn đến thư mục lib trong thư mục SFML đã tải về (trong ảnh gif mình chỉ làm bên Debug, bên Release các bạn làm tương tự, lí do như trên 😀).

![image](https://user-images.githubusercontent.com/91585606/156887569-b5661e93-7aa1-4be4-87ac-9453db1ef0c7.png)

Sau đó các bạn đến mục Linker ---> Input ---> Additional Dependencies ---> Edit.

![image](https://user-images.githubusercontent.com/91585606/156887579-11350044-9a82-4d78-b743-c8bd7a036077.png)

Ở bước này sẽ có sự khác nhau giữa Release và Debug nên mình sẽ chia ra 2 phần.
Ở Debug, các bạn gõ như sau (gõ như thế là đã cài đủ 5 module của SFML, copy paste mỗi cái cái rồi enter rồi tiếp tục các khác)
sfml-graphics-d.lib
sfml-audio-d.lib
sfml-network-d.lib
sfml-window-d.lib
sfml-system-d.lib

![image](https://user-images.githubusercontent.com/91585606/156887585-945ccde7-49bd-4eef-bd4e-b0a9532efb50.png)

Ở Release, các bạn gõ như sau:
sfml-graphics.lib
sfml-audio.lib
sfml-network.lib
sfml-window.lib
sfml-system.lib

![image](https://user-images.githubusercontent.com/91585606/156887595-33bfb659-6f67-49de-83d8-df156422fc94.png)

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

![image](https://user-images.githubusercontent.com/91585606/156887605-794b8921-0acd-460c-8ddd-c8633d5696db.png)

Như thế là đã thành công. Bây giờ các bạn hãy vào đường dẫn mà nó hiển thị trong Output để tìm file exe đã build.
Tuy nhiên lúc này, nếu các bạn mở lên thì sẽ bị lỗi thiếu các file dll.

![image](https://user-images.githubusercontent.com/91585606/156887615-cddaa0b6-1b0a-49d2-80f6-db3ff0cc2630.png)

Để khắc phục, các bạn vào thư mục bin của SFML để tìm các file dll bị thiếu và paste vào. Sau đó hãy run lần nữa để thử lại.

![image](https://user-images.githubusercontent.com/91585606/156887630-ea014610-1cd1-4084-9ab1-34a061012120.png)

Đó là các cài đặt SFML cho project Visual Studio ở dạng dynamic linker. Ở dạng dynamic linker thì chương trình của các bạn sẽ phải cần các file dll để chạy. Nếu các bạn không thích sự phiền hà đó thì có thể cài đặt ở dạng static. Lúc này thì chương trình của các bạn sẽ không cần các file dll của SFML (vẫn cần file openal32.dll) nhưng chương trình của các bạn sẽ nặng hơn rất nhiều .

4. Cài đặt SFML dạng static linker

Các bước thì vẫn giống như trên. Chỉ có thêm 1 bước và khác bước add các file lib tại mục Additional Dependencies.
Các bạn mở chọn C++ ---> Preprocessor --> Preprocessor Definitions ---> Edit

![image](https://user-images.githubusercontent.com/91585606/156887651-05bc3baf-0c9a-488a-b045-3a56848d9331.png)

Các bạn gõ thêm dòng SFML_STATIC (làm cả Debug lẫn Release nhé).

![image](https://user-images.githubusercontent.com/91585606/156887669-1ffac1e1-029a-4055-bfe0-424c6b794f13.png)

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

