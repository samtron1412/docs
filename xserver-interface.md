Giao diện đồ họa X Server trên Linux


Hệ thống XFree86 còn được gọi là X Window hay X ra đời nhằm cung cấp cho các hệ thống Unix và Linux một giao diện đồ họa dễ sử dụng hơn so với giao diện text trước đó.

Đối với những người dùng Windows và Macintosh khi chuyển sang sử dụng Linux họ đánh giá Linux có dễ sử dụng hay không là ở giao diện đồ họa (X).

Cấu trúc của hệ thống X Window
Hệ thống X Window được thiết kế với cấu trúc Client – Server.

Các ứng dụng X có thể chạy trực tiếp trên máy trạm nội bộ của người dùng hoặc chạy từ một máy chủ từ xa qua môi trường mạng.

Client và X Server giao tiếp với nhau trực tiếp hoặc giao tiếp từ xa qua giao thức X.

Module lớn nhất của hệ thống X Window được gọi là X Server. Module này có khả năng hiển thị giao diện đồ họa các ứng dụng chạy trên hệ thống của người dùng.

X Server nhận các giá trị đầu vào như chuột, bàn phím sau đó hiển thị hình ảnh ra màn hình. Các phần mềm chạy trên máy trạm nội bộ của người dùng (clients) sẽ được điều khiển và được giám sát bởi X Server.

Hệ thống X cũng có chức năng cho phép các ứng dụng chạy trên một máy tính A có thể hiển thị giao diện đồ họa trên một máy tính B khác. Máy tính B sẽ đóng vai trò làm X Server và các ứng dụng trên máy tính A đóng vai trò làm Client. Với chức năng này chúng ta có thể quản trị các máy chủ Linux/Unix từ xa với giao diện đồ họa qua môi trường mạng.

Hầu hết chúng ta đều coi các máy trạm chúng ta đang sử dụng là các Client. Điều này là không đúng vì trong hệ thống X Window các máy trạm của chúng ta sẽ được coi là các Server. Các X Server sẽ hiển thị giao diện đồ họa trên các máy trạm. Các Client (các ứng dụng chạy trên máy trạm) sẽ kết nối nội bộ hoặc kết nối từ xa qua môi trường mạng đến X Server để hiển thị giao diện đồ họa.

Cài đặt X
Cách đơn giản nhất để cài đặt X là cài đặt ngay trong quá trình cài đặt chính của các bản phân phối Linux. Mặc định khi chúng ta cài đặt các bản phân phối Linux (Ubuntu, Fedora, CentOS…) các gói cài đặt X sẽ tự động được cài đặt và tự động được cấu hình.

Chúng ta cũng có thể cài đặt các gói X sau khi cài đặt xong hệ điều hành. Với bản phân phối Redhat và dựa trên Redhat, chúng ta cài đặt các gói X định dạng rpm trong đĩa DVD cài đặt hoặc trên Internet. Với bản phân phối Debian và dựa trên Debian, chúng ta có thể cài đặt X với công cụ quản lý gói apt-get với câu lệnh sau :

# sudo apt-get install task-x-window-system-core
hoặc
# sudo apt-get install task-x-window-system

Cộng cụ apt-get sẽ tự động download các gói cần thiết và cài đặt các gói này. Sau đó chúng ta có thể phải cấu hình bằng tay một số thông số của X.

Đối với những người mới sử dụng Linux việc cài đặt X rất phức tạp và mất thời gian nên chúng ta thường cài đặt tự động X trong quá trình cài các bản phân phối Linux.

Các phiên bản XFree86
Có 2 phiên bản chính của XFree86 đang được sử dụng hiện nay đó là XFree v3 và XFree v4. Một số bản phân phối Linux vẫn tiếp tục sử dụng XFree v3 trong khi đó các bản phân phối Linux khác đã chuyển sang sử dụng XFree v4.

Với XFree v3, X Server được tách biệt hoàn toàn với chipset của card màn hình. Tùy theo các chipset card màn hình (ATI, NVIDIA, S3...) của hệ thống mà chúng ta cài đặt đúng X Server phù hợp với các chipset đó.

Nếu chúng ta cài đặt X Server trong quá trình cài đặt các bản phân phối Linux, chương trình cài đặt sẽ tự động nhận chipset card màn hình của hệ thống và cài đặt đúng X Server phù hợp. Nếu chúng ta cài đặt X Server sau khi cài đặt các bản phân phối Linux, chúng ta phải tiến hành cài đặt bằng tay chính xác X Server phù hợp với card màn hình.

Ví dụ để cài đặt X Server cho chipset S3 trên hệ thống Redhat, chúng ta sẽ cài đặt gói S3-3.3.6-33.i386.rpm.

Với XFree v4, việc cài đặt X Server trở nên dễ dàng hơn. Thay vì phải cài đặt chính xác X Server tương ứng với chipset card màn hình, chúng ta chỉ cần cài đặt X Server chính và sau đó xác định sử dụng driver nào để phù hợp với chipset card màn hình trong file cấu hình của X. Tuy nhiên phiên bản XFree v4 hiện tại không hỗ trợ đầy đủ tất cả các chipset mà XFree v3 hỗ trợ.

Cấu hình X
File cấu hình chính của X Window là /etc/X11/XF86Config. Với hệ thống Redhat file cấu hình của X là /etc/X11/xorg.conf.

Việc cấu hình bằng tay X rất phức tạp đối với những người mới sử dụng Linux. Nhưng chúng ta cùng tìm hiểu qua cấu trúc các thành phần trong file cấu hình để có thể khắc phục một số lỗi nhỏ như không nhận driver card màn hình …

File cấu hình của X được chia ra thành nhiều mục nhỏ với cú pháp như sau :

Section “Tên Section”
Các câu lệnh cấu hình cho Section
Endsection

Một số tên Section được định nghĩa trong file cấu hình X :
Files
ServerFlags
Keyboard
Pointer
Monitor
Device
Screen

Ví dụ mục cấu hình cho Pointer (chuột máy tính)
Section “Pointer”
Protocol “IMPS/2”
Device “/dev/mouse”
ZAxisMapping 4 5
Endsection

Trong đó :
Protocol <tên protocol> : xác định giao thức chuột sử dụng
Device <đường dẫn đến device > : xác định thiết bị sử dụng để giao tiếp với chuột. Trong ví dụ là file /dev/mouse.
ZAxisMapping N M : thông số cầu hình cho con lăn chuột.
… Và một số thông tin cấu hình khác.

Ví dụ mục cấu hình cho Device (xác định một hoặc nhiều card màn hình được sử dụng)
Section “Device”
Indentifier “Nvidia TNT2”
VendorName “Nvidia”
BoardName “TNT2”
Chipset “svga”
Endsection

Trong đó :
Indentifier : Xác định tên card màn hình. Trong ví dụ là card Nvidia TNT2.
VendorName : Thông tin mở rộng xác định tên của hãng sản xuất card màn hình (Nvidia).
BoardName : Thông tin mở rộng xác định model của card màn hình (TNT2).
Chipset : Thông tin mở rộng xác định loại chipset trên model của card màn hình.
… Và một số thông tin cấu hình khác.

