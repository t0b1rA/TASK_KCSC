# Inside Lab 

<img width="792" height="742" alt="image" src="https://github.com/user-attachments/assets/bdd58a3d-918e-4b8d-be1f-5fca1757a0bd" />

Link đề: [Inside_lab](https://cyberdefenders.org/blueteam-ctf-challenges/insider/)

Ở chall này phần description nói cho chúng ta rằng sau khi bắt đầu làm việc ở `TAAUSAI`, thì Karen đang bắt đầu những hành động bất hợp pháp bên trong, và với tư cách là 1 nhân viên SOC analysts chúng ta được cung cấp một disk image của OS Linux, và bắt đầu phân tích. 

Đề bài cung cấp cho mình 1 file `.ad1` thì vẫn tiếp tục dùng FTK imager để phân tích chính. 

### 1. Which Linux distribution is being used on this machine?

<img width="3139" height="1129" alt="image" src="https://github.com/user-attachments/assets/75363f0f-d590-4e9c-9913-a25d59cbc142" />

Khi em vào thư mục `boot` của hệ thống trong FTK imager thì em thấy ở đây có các file cấu hình `Kali Linux` nên bản phân phối Linux dùng cho máy trên chắc chắn là `Kali Linux`.

<img width="639" height="225" alt="image" src="https://github.com/user-attachments/assets/6d21143b-ac2b-4744-a468-70d1e5812fa5" />

### 2. What is the MD5 hash of the Apache access.log file?

Chúng ta có được file access.log của `/apache2` nằm bên trong thư mục root `/var` với đường dẫn đầy đủ là `/var/log/apache2/access.log`, và mã MD5 hash sẽ được cung cấp ở ô Properties bên dưới của ứng dụng FTK Imager.

<img width="2621" height="1863" alt="image" src="https://github.com/user-attachments/assets/2f1c3078-31fc-4c61-9566-004dcd98de54" />

Mã MD5 hash: `d41d8cd98f00b204e9800998ecf8427e`

<img width="649" height="202" alt="image" src="https://github.com/user-attachments/assets/5f92a7e3-be9c-4362-b62d-566cec0c68bb" />

### 3. It is suspected that a credential dumping tool was downloaded. What is the name of the downloaded file?

Vì câu hỏi nhắc đến 1 suspicios tools đã được *download*, thì chắc chắn nó sẽ nằm bên trong thư mục `downloads` của thư mục `/root` user.

<img width="2549" height="1047" alt="image" src="https://github.com/user-attachments/assets/14a9e226-6584-49aa-b328-0ef49c99ae67" />

Công cụ Karen sử dụng là `mimikatz`, một công cụ chuyên dùng để bẻ khóa mật khẩu của người dùng login thông qua 1 mã hash đánh cắp được. 

### 4. A super-secret file was created. What is the absolute path to this file?

Sau 1 lúc tìm kiếm, mình nghĩ rằng Karen sẽ phải sử dụng 1 lệnh nào đó để tạo ra file (bằng `touch` chẳng hạn) và để vô thư mục super-secret gì đó của cô ấy, hoặc là để tạo nên 1 thư mục (bằng `mkdir` giả sử), thì mình sẽ check thử bên trong `bash_history` xem có manh mối gì không.

path: `/root/bash_history`

<img width="3134" height="1930" alt="image" src="https://github.com/user-attachments/assets/96e92ce5-9d7f-45e2-8336-7bbdb4e1e990" />

Bên trong đây chúng ta thấy được Karen đã sử dụng 1 logic dùng lệnh khá ảo ;)), cô ấy dùng lệnh `touch` chỉ để tạo ra 1 file trống để cố gắng viết `snky` và chuyển hướng nó vào bên trong file `SuperSecretFile.txt`, kết quả là không có gì cả.

Nhưng mà chunsg ta vẫn có được file bí mật mà đề nhắc đến với đường dẫn đầy đủ là: `/root/Desktop/SuperSecretFile.txt`.

<img width="627" height="232" alt="image" src="https://github.com/user-attachments/assets/f4e7b05c-3607-4a87-8068-9d3f20a6f053" />

### 5. What program used the file didyouthinkwedmakeiteasy.jpg during its execution?
mình tiếp tục tìm kiếm chương trình đã sử file `.jpg`, thì chắc kiểu gì Karen cũng sẽ sử dụng 1 lệnh gì đó để mở file, hoặc là phân tích file, nên có thể nó sẽ được ghi lại bên trong `bash_history`. Mình lướt xuống 1 tí thì thấy:

<img width="2080" height="1400" alt="image" src="https://github.com/user-attachments/assets/76d1d1a7-9410-48ba-81c6-6b04be86b542" />

Lệnh sử dụng cho file `.jpg` là `binwalk`.

<img width="616" height="233" alt="image" src="https://github.com/user-attachments/assets/1b64bf07-7d30-40f6-b06b-21f1421e7b8a" />

### 6. What is the third goal from the checklist Karen created?

Khi chúng ta vào thư mục `/root/Desktop` chúng ta sẽ thấy 1 file khác ngoài thư mục mimikatz, là file checklist,, ở đây Karen ghi lại những mục tiêu của mình.

<img width="2753" height="1115" alt="image" src="https://github.com/user-attachments/assets/273588ae-391a-472e-9cc8-47c34b00b2c5" />

- Đầu tiên là lấy lòng tin của Bob.
- Tiếp theo là học cách hack =))).
- Cuối cùng là profit - kiếm lời

### 7. How many times was Apache run?

Để biết được bao nhiêu lần apache được run trong hệ thống, chúng ta sẽ dựa vào mỗi file `access.log và error.log` được ghi lại trong hệ thống và lưu trữ bên trong `/apache2`, nhưng khi mình vào check thử các log trong thư mục này, đều trống, và không có những file log cũ, mình nghĩ có thể là `/apache2` chưa từng được chạy, cùng với hint 1 cũng nói thế, nên mình nghĩ số lần chạy là `0`.

<img width="437" height="225" alt="image" src="https://github.com/user-attachments/assets/7817956a-396c-4580-b735-05ac965555da" />

<img width="617" height="209" alt="image" src="https://github.com/user-attachments/assets/074f4ed6-4598-40ad-863f-1d065db76284" />

### 8. This machine was used to launch an attack on another. Which file contains the evidence for this?

Ở trong thư mục `/root` của user, khi chúng ta tìm kĩ ở phần bên dưới, chúng ta có thể thấy được, 1 tấm hình có vẽ như là đang ở máy Windows của `Bob`, ở trên chúng ta còn thấy được 1 khung call video, có thể như Karen đang kêu `Bob` hãy thực thi 1 file khá đáng nghi là `aylmao.exe`. Và file chứa manh mối đó là file ảnh `irZLAohL.jpeg`.

<img width="626" height="448" alt="image" src="https://github.com/user-attachments/assets/db2f1f6d-9336-4e7c-ae96-6c1f6d55d6a5" />

### 9. It is believed that Karen was taunting a fellow computer expert through a bash script within the Documents directory. Who was the expert that Karen was taunting?

Trong câu hỏi có nhắc đến Karen đã chế nhạo 1 chuyên gia máy tính khác, bên trong thư mục Documents của cô ấy. Dựa theo hint này, mình sẽ check thử các file bên trong thư mục `myfirsthack` thử xem.

Và đây là 1 file script mà mình tìm được, Karen đang in ra đường dẫn hiện tại của cô ấy, những kết nối với cổng network `80`. Và dòng cuối đã nhắc đến 1 người tên là `Young`.

<img width="2530" height="1164" alt="image" src="https://github.com/user-attachments/assets/964e084f-77ef-433d-9fa8-8467d87b838b" />

<img width="634" height="264" alt="image" src="https://github.com/user-attachments/assets/89571cd4-0bc2-4940-8885-ba3f58a24211" />

### 10. A user executed the su command to gain root access multiple times at 11:26. Who was the user?

Để xem được một người dùng đã thực thi lệnh `su` để lấy được quyền truy cập `root`, thì chúng ta phải check qua `auth.log`. Chúng ta cũng càn biết được bên trong file `auth.log` này chứa gì bên trong:

- Đầu tiên là nó ghi lại những phiên đăng nhập thành công và thất bại đối với hệ thống Linux này.
  - Đăng nhập thành công: Ai đã đăng nhập, lúc mấy giờ, qua phương thức (mật khẩu, ssh,..).
  - Đăng nhập thất bại: Ghi lại những lần người dùng nhập sai mật khẩu.
 
- Sử dụng quyền quản trị (root):
  - Mỗi khi chúng ta dùng lệnh `sudo`, hệ thống đều sẽ ghi lại vào file `auth.log`:
    - Ai là người thực thi lệnh.
   
    - Lệnh được thực thi ở mục nào.
   
    - Nội dung của chính xác của lệnh đó là gì.

- Hoạt động của SSH (remote Desktop)

- Thay đổi tài khoản và nhóm
  - Tạo người dùng mới (useradd)
 
  - Thay đổi mật khẩu (passwd).
 
  - Thêm người dùng vào nhóm `sudoers` - những người dùng có quyền dùng lệnh sudo.
 
Sau khi biết được thêm những thông tin rồi, thì mình bắt đầu kiểm tra file `auth.log` trước, Mình lướt 1 lúc khá sâu bên dưới thì thấy có 1 lệnh su được sử dụng cho 1 người dùng khác được ghi tại đây, đúng vào mốc thời gian `11:26`:

<img width="2015" height="404" alt="image" src="https://github.com/user-attachments/assets/8c7edcd3-271b-47f3-868e-f27d26eff5ff" />

Chúng ta có thể thấy được hệ thống đã ghi lại là đã có một lệnh su được sử dụng bởi người dùng root thực hiện chuyển đổi tài khoản với 1 user tên là `posstges`, và lúc này user này hoàn toàn có toàn bộ quyền của 1 `root` user
, nói thêm thì user `postges` là 1 tài khoản mặc định của cơ sở dữ liệu PostgreSQL, có lẽ 1 user đang muốn thực hiện hành động bất hợp pháp ở đây.

```
Mar 20 11:26:22 KarenHacker su[4060]: + ??? root:postgres
```

Lúc này chúng ta thấy user `postgres` đã có quyền root và được log ghi lại tại đây.

<img width="606" height="231" alt="image" src="https://github.com/user-attachments/assets/c7df07f1-7ec0-481e-a9fa-24e1fd2eb3ba" />

### 11. Based on the bash history, what is the current working directory?

Ở đây chúng ta tiếp tục dựa vào file `bash_history` để giải quyết câu hỏi cuối cùng này, thư mục cuối cùng hiện được sử dụng bởi Karen cho phiên làm việc của cô ấy:

<img width="1783" height="868" alt="image" src="https://github.com/user-attachments/assets/c0f23fff-153b-44b5-9b87-1bc9a7826488" />

Ở đây chúng ta nhìn vào dòng `cd ../Documents/myfirsthack/`, đây là lần chuyển hướng cuối cùng của Karen, chứng tỏ đây là phiên làm việc cuối cùng của Karen, đường dẫn đầy đủ đến file này là:
```
/root/Documents/myfirsthack`
```
<img width="2486" height="1076" alt="image" src="https://github.com/user-attachments/assets/d1e47275-c84b-44ea-b270-ea87b81f211a" />

<img width="635" height="245" alt="image" src="https://github.com/user-attachments/assets/c6f0cdd3-d42f-45fc-94c0-3b183ed09725" />

Đây là 1 challenge giúp mình có thể cải thiện thêm về kiến thức của các file log bên trong linux, đồng thời biết được vị trí và khoanh vùng vào những thư mục quan trọng cần chú ý tới.
