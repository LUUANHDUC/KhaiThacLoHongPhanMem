# Hướng Dẫn Xây Dựng Môi Trường Khai Thác Lỗ Hổng CVE Trên Wordpress

Hướng dẫn này giúp triển khai môi trường nhằm khai thác thành công ba lỗ hổng CVE lần lượt là CVE-2023-2546, CVE-2023-3460, CVE-2023-4596 tồn tại trên các Plugin WP User Switch 1.0.2, Ultimate Member 2.6.5, Forminator 1.24.6 nằm trên CMS Wordpress.

## Mô Hình Triển Khai

![Mô_Hình_Hệ_Thống](https://github.com/LUUANHDUC/KhaiThacLoHongPhanMem/assets/125422094/36dae73a-ceba-4e2a-8e51-977307209b97)
## Cấu Hình Máy Attacker

### Windows 10 trên VMware

  #### Hướng Dẫn Cài Đặt

* [Link Download Windows 10 dành cho Vmware](https:/developer.microsoft.com/en-us/wind/downloads/virtual-machines/)

* Video hướng dẫn cài đặt 

[![Video Title](https://img.youtube.com/vi/v0Af4UIFg_8/0.jpg)](https://www.youtube.com/watch?v=v0Af4UIFg_8)

### Cài Đặt Burp Suite Community Edition (Windows 64-bit)

  #### Hướng Dẫn Cài Đặt

- [Link Tải Burp Suite Community Edition (Windows 64-bit) Version 2023.10.3.6](https://portswigger.net/burp/communitydownload)

- [Hướng dẫn cài đặt](https://portswigger.net/burp/documentation/desktop/getting-started/download-and-install)

- Video hướng dẫn cài đặt và cấu hình chặn bắt Request trên BurpSuite

[![Alt text](https://img.youtube.com/vi/-ozGijESmTY/0.jpg)](https://www.youtube.com/watch?v=-ozGijESmTY&list=PLaoi7ADVdlKf9DnFJvCUB2yDg07Cunz07)
## Cấu Hình Máy Victim

### Kali Linux trên VMware

  #### Hướng Dẫn Cài Đặt

* [Link Download Kali Linux Version 2023.3 dành cho Vmware](https://www.kali.org/get-kali/#kali-installer-images)

* [Hướng dẫn cài đặt](https://www.kali.org/docs/virtualization/install-vmware-guest-vm/)
### Cấu Hình Và Cài Đặt CMS Wordpress Trên Kali
  _Trong hướng dẫn này chúng tôi sẽ hướng dẫn 2 cách (Với dòng lệnh và XAMPP) cài đặt CMS Wordpress trên Localhost dựa trên nền tảng Web Server là Apache, Database Server là MySQL hoặc MariaDB và Language là PHP._

#### Hướng Dẫn Cài Đặt Với Dòng Lệnh  
  _Tất cả các câu lệnh dưới đều thực hiện trên Terminal máy Kali và thực hiện dưới quyền người dùng Root._
  
  * _<Tên_CSDL>: Thay bằng tên của cơ sở dữ liệu mà bạn muốn tạo_

  * _<Tên_người_dùng>: Thay bằng tên của người dùng bạn muốn tạo_
  
  * _<Mật_khẩu_người_dùng>: Thay bằng mật khẩu mà bạn muốn sử dụng cho người dùng muốn tạo_

##### Kiểm tra PHP
  Trước khi cài đặt, bạn cần kiểm tra trên máy đã cài đặt PHP hay chưa bằng câu lệnh sau:
  
    php --version
    
  Nếu máy bạn đã cài đặt PHP nó sẽ cung cấp cho bạn version của PHP
    
  Nếu chưa cài đặt bạn có thể cài đặt PHP bằng câu lệnh sau:

    sudo apt update
    sudo apt install php

  ##### Bước 1: Cấu Hình MySQL
    sudo mysql
    CREATE DATABASE <Tên_CSDL>;
    CREATE USER '<Tên_người_dùng>'@'localhost>' IDENTIFIED BY '<Mật_khẩu_người_dùng>';
    GRANT ALL PRIVILEGES ON <Tên_CSDL>.* TO '<Tên_người_dùng>'@'localhost';
    FLUSH PRIVILEGES;
    EXIT;
    
  ##### Bước 2: Tải và Cấu Hình Wordpress
    cd /tmp
    wget https://wordpress.org/latest.tar.gz
    tar -xvzf latest.tar.gz
    sudo mv wordpress /var/www/html/

  ##### Bước 3: Chuyển đến thư mục WordPress và tạo một bản sao của tệp cấu hình mẫu
    cd /var/www/html/wordpress
    cp wp-config-sample.php wp-config.php

  ##### Bước 4: Sửa tệp cấu hình để phản ánh cơ sở dữ liệu và người dùng bạn đã tạo trước
    sudo nano wp-config.php

  ##### Bước 5: Chỉnh sửa các dòng sau
  _Ta sẽ thay các giá trị trong nháy đơn bằng các giá trị đã tạo ở Bước 1_
  
    define('DB_NAME', '<Tên_CSDL>');
    define('DB_USER', '<Tên_người_dùng>');
    define('DB_PASSWORD', '<Mật_khẩu_người_dùng>');

  ##### Bước 6: Phân quyền và Khởi động lại Apache
    sudo chown -R www-data:www-data /var/www/html/wordpress
    sudo service apache2 restart
    
  ##### Bước 7: Hoàn tất cài đặt thông qua Giao diện Web

Mở trình duyệt và truy cập địa chỉ http://localhost/wordpress. Tiếp
theo, bạn sẽ thấy trang cài đặt WordPress thông qua giao diện web. Nhập thông
tin tài khoản mà bạn đã cấu hình và hoàn tất quá trình cài đặt.

#### Hướng Dẫn Cài Đặt Wordpress Với XAMPP

* [Link Download XAMPP cho Linux (64-bit) ](https://www.apachefriends.org/download.html)

* [Link Download Wordpress cho Linux Version 6.4.1](https://wordpress.org/download/)

* Video hướng dẫn cài đặt Wordpress trên Linux sử dụng XAMPP

[![Video hướng dẫn cài đặt Wordpress trên Linux sử dụng XAMPP](https://img.youtube.com/vi/N_xNkYv3SWc/0.jpg)](https://www.youtube.com/watch?v=N_xNkYv3SWc)

### Cấu Hình Và Cài Đặt Plugin Trên Wordpress
_Các bạn hãy Download các Plugin về máy với link tải bên dưới, mỗi Plugin sẽ sử dụng để triển khai và khai thác một CVE đã nêu_

* [Link Download Plugin WP User Switch 1.0.2](https://downloads.wordpress.org/plugin/wp-user-switch.1.0.2.zip)

* [Link Download Plugin Ultimate Member 2.6.5](https://downloads.wordpress.org/plugin/ultimate-member.2.6.5.zip)

* [Link Download Plugin Forminator 1.24.6](https://downloads.wordpress.org/plugin/forminator.1.24.6.zip)

#### Hướng Dẫn Import một Plugin vào CMS Wordpress
_Đây là quá trình cài đặt một Plugin vào Wordpress sau khi đã tải về_

 ##### Bước 1: Giải nén tập tin Plugin đã tải về
    tar - xvzf forminator.1.24.6.tar.gz
    
  ##### Bước 2: Di chuyển vào thư mục plugin của WordPress
    mv forminator /var/www/html/wordpress/wp-content/plugins/

  ##### Bước 3: Vô trang quản trị, kích hoạt plugin
  
  Tại Menu trái trong trang quản trị Wordpress của admin:
  
    1. Chọn vào mục Plugins -> Installed Plugins 
    2. Tìm tên của các Plugin mà bạn muốn Active -> chọn Active
    3. Nếu Plugin được Active thành công sẽ hiển thị Deactive (để dừng hoạt động của Plugin đó).

Với Plugin phiên bản mới nhất, ở trang quản trị plugin, bấm cập nhật là hệ thống tự tải và cài đặt phiên bản mới nhất cho Plugin đó.
 
