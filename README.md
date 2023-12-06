# Hướng Dẫn Xây Dựng Môi Trường Khai Thác Lỗ Hổng CVE Trên Wordpress
## Cấu Hình Máy Attacker

### Windows 10 trên VMware

  #### Hướng Dẫn Cài Đặt

* [Link Download Windows 10 dành cho Vmware](https:/developer.microsoft.com/en-us/wind/downloads/virtual-machines/)

* [Video hướng dẫn cài đặt](https://www.youtube.com/watch?v=v0Af4UIFg_8)
### Cài Đặt Burp Suite Community Edition (Windows 64-bit)

  #### Hướng Dẫn Cài Đặt

- [Link Tải Burp Suite Community Edition (Windows 64-bit) Version 2023.10.3.6](https://portswigger.net/burp/communitydownload)

- [Hướng dẫn cài đặt](https://portswigger.net/burp/documentation/desktop/getting-started/download-and-install)

## Cấu Hình Máy Victim

### Kali Linux trên VMware

  #### Hướng Dẫn Cài Đặt

* [Link Download Kali Linux Version 2023.3 dành cho Vmware](https://www.kali.org/get-kali/#kali-installer-images)

* [Hướng dẫn cài đặt](https://www.kali.org/docs/virtualization/install-vmware-guest-vm/)
### Cấu Hình Và Cài Đặt CMS Wordpress Trên Kali

# _NOTE:_ 
Trong hướng dẫn này chúng tôi sẽ hướng dẫn 2 cách cài đặt CMS Wordpress trên Local dựa trên nền tảng Web Server là Apache, Database Server là MySQL/MariaDB và PHP.

  #### Hướng Dẫn Cài Đặt Với Dòng Lệnh 

# _NOTE:_ 
Tất cả các câu lệnh dưới đều thực hiện trên Terminal máy Kali và thực hiện dưới quyền người dùng Root.
  
  ##### Bước 1:
    sudo mysql
    CREATE DATABASE wordpress;
    CREATE USER 'wordpressuser'@'localhost' IDENTIFIED BY 'your_password';
    GRANT ALL PRIVILEGES ON wordpress.* TO 'wordpressuser'@'localhost';
    FLUSH PRIVILEGES;
    EXIT;

  ##### Bước 2:

  #### Hướng Dẫn Cài Đặt Wordpress Với XAMPP

* [Link Download XAMPP cho Linux (64-bit) ](https://www.apachefriends.org/download.html)

* [Link Download Wordpress cho Linux Version 6.4.1](https://wordpress.org/download/)

* [Video hướng dẫn cài đặt Wordpress trên Linux sử dụng XAMPP](https://www.youtube.com/watch?v=N_xNkYv3SWc)

