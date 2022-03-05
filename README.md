# SFML- Cài đặt và chạy chương trình đầu tiên với thư viện đồ họa SFML

## Table of Contents
- [0.Sơ lược về SFML](#1.Tải bản pre-built SFML)
- [1.Tải bản pre-built SFML](#tải-bản-pre-built-SFML)
- [2.Tìm hiểu về các thư mục trong bản pre-built](#tìm-hiểu-về-thư-mục-trong-pre-built)
- [3.Cài đặt SFML vào project](cài-đặt



## 1.Tải bản pre-built SFML

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

##2.Tìm hiểu các thư mục trong bản pre-built

Sau khi tải về, các bạn tiến hành giải nén sẽ được như hình. Ta chỉ quan tâm các thư mục bin, include, lib.

﻿Tập tin đính kèm:
﻿
Thư mục include là thư mục chứa các file header của SFML. Khi code các bạn phải include chúng thì mới có thể dùng được SFML.

Tập tin đính kèm:

Thư mục lib là thư mục chứa các file .lib. Cái này mình chả biết giải thích sao 😀 nhưng nôm na là phải có để các bạn có thể build ra file .exe. Nếu không sẽ bị lỗi.

Tập tin đính kèm:

Thư mục bin là thư mục chứa các file .dll (dynamic linker library). Cần thiết cho chương trình khi build ở dạng dynamic linker.

Tập tin đính kèm:

Trong thư mục examples là các chương trình demo của SFML, bạn có thể vào để thử. Nếu lúc chạy có bị thiếu file .dll thì cứ vào thư mục bin mà tìm.

Tập tin đính kèm:




