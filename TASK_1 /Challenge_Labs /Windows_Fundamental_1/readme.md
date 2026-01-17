### TASK 1: Windows Editions


<img width="778" height="179" alt="image" src="https://github.com/user-attachments/assets/6f25b04a-43dc-4b72-839f-809d81ef4238" />

Câu này em lên mạng tìm thì em thấy họ ghi là Bitlocker, bởi vì 

<img width="1230" height="961" alt="image" src="https://github.com/user-attachments/assets/07e42fce-e8a9-4f03-8d9e-df7f4430e1dd" />

### TASK2

**1. Which selection will hide/disable the Search box?**

<img width="759" height="110" alt="image" src="https://github.com/user-attachments/assets/fcf7a63e-acd8-47d6-9cde-135e7819e66e" />

Đây là một cách có thể được dùng để tắt hiển thị 1 số file. Trong đó cách này có thể được các attacker dùng để ẩn di các file trong phần File Explorer nếu chúng ta không cẩn thận mà không bật phần `Hidden Items` lên.

<img width="542" height="440" alt="image" src="https://github.com/user-attachments/assets/0f08ce98-36a8-4f00-b7ef-e0253ad5d507" />

**2. Which selection will hide/disable the Task View button?**

<img width="763" height="124" alt="image" src="https://github.com/user-attachments/assets/30915875-479d-40d4-8cdf-2f854c0be15f" />

<img width="358" height="476" alt="image" src="https://github.com/user-attachments/assets/f5e97b95-3f05-412f-9926-a0cd02c394b7" />

Có thể bật hoặc tắt thanh taskbar bên dưới

**3. Besides Clock and Network, what other icon is visible in the Notification Area?**

<img width="762" height="124" alt="image" src="https://github.com/user-attachments/assets/b7575e31-ffcc-4940-a90f-663a0513f553" />
**Action Center** nó gắn với 4 nút truy cập nhanh của người dùng thường là (Wifi, Bluetooth, Sound,...)

### TASK 4: The File System

<img width="769" height="137" alt="image" src="https://github.com/user-attachments/assets/1a192372-6201-4915-87c6-99f69812b599" />

Giới thiệu qua một chút về `FAT16/FAT32` và `NTFS`

**FAT(File Allocation Table)** là một bảng phân bổ tệp tin, là một danh sách liên kết (linked list) của tất cả các cluster, Nó chứa trạng thái của cluster và con trỏ đến cluster tiếp theo của chuỗi.

Bên trong của **FAT** một cấu trúc của hệ thống tệp **FAT**: hệ thống tệp FAT hỗ trợ các Cấu trúc dữ liệu sau:

- **Cluster** : Là đơn vị lưu trữ cơ bản của hệ thống tệp FAT. Mỗi tệp được lưu trên thiết bị lưu trữ có thể được coi là một nhóm các cluster chứa các bit thông tin.

- **Directory(Thư mục) một thư mục chứa thông tin về nhận dạng tệp, chẳng hạn như tên tệp, cluster bắt đầu, các metadata.

- **FAT16,FAT32**: cấc con số như là 12, 16, 32 là các bit được dùng để đặt địa chỉ định danh cho các cluster.
  - **FAT16**: là hệ thống phổ biến thời MS-DOS và Windows 95. Hạn chế lớn là dung lượng phân vùng tối đa chỉ có  2GB hoặc (4GB). Ngày nay rất ít dùng.
 
  - **FAT32**: tương thích tốt. Cắm USB FAT32 vào Windows, MAC, Linux, loa, TV đều có thể dùng được. Nhưng nó cũng có nhược điểm là không thể lưu trữ tập tin nào lớn hơn 4GB.

**NTFS (New Technology File System)**: là một hệ thống tệp chính được sử dụng cho các phiên bản Microsoft và Windows Server. Hệ điều hành của một máy tính tạo ra và duy trì những hệ thống tệp trên ổ lưu trữ hoặc thiết bị. Hệ thống tệp tổ chức các dữ liệu vào bên trong các files. Điều khiển cách dữ liệu được đặt tên, lưu trữ khôi phục và cập nhật. Bên trong **NTFS** có một số tính năng mới như:

  - Journaling ( Ghi nhật ký hệ thống)

  - Access Control Lists(ACLS- Danh sách kiểm soát truy cập)

  - Volume Shadow Copy(Bản sao bóng phân vùng)

  - Alternate Data Stream( (ADS - luồng dữ liệu thay thế)

  - **$MFT, $MFTmirr, $LogFile, $UsnJrnl (Các tệp siêu dữ liệu)**

### TASK 5: The Windows\System32 Folders

<img width="761" height="120" alt="image" src="https://github.com/user-attachments/assets/5996f761-8e6c-4b58-a058-000518a7cf39" />

Biến môi trường hệ thống lưu trữ những thông tin về môi trường của hệ điều hành. Những thông tin này bao gồm các chi tiết như là đường dẫn hệ điều hành, số các tiến trình được sử dụng cho hệ điều hành, và nơi lưu trữ trong các folders temporary.

### TASK 6:User Accounts, Profiles, and Permissions

Có 2 loại users account thông thường trong Windows đó là **Standard users** và **Administrator**. Và trong đó việc quản lý các người dùng trong máy rất quan trọng, vì những attacker có thể từ việc dựa vào việc leo quyền trong một máy và thực hiện tạo nên một người dùng khác với quyền cao để duy trì đăng nhập và kiểm soát hệ thống máy tính.

Trong đó lệnh run `lusrmgr.msc` dùng để quản lý tất cả người dùng **administrator** và **standard user**. Với điều kiện là bạn có quyền admin để kiểm soát trong miền.

<img width="941" height="780" alt="image" src="https://github.com/user-attachments/assets/777ff88f-af9f-4945-b4a6-b2babd1c0d03" />

**What is the name of the other user account?**

<img width="767" height="779" alt="image" src="https://github.com/user-attachments/assets/e3747053-0069-417b-956b-5cbfaa1a0d1d" />

<img width="876" height="141" alt="image" src="https://github.com/user-attachments/assets/e952709b-9941-4922-84bc-34368106c510" />

**What groups is this user a member of?**

<img width="515" height="658" alt="image" src="https://github.com/user-attachments/assets/f20bb1ea-7de9-4d95-987c-a60bd282d434" />

<img width="880" height="146" alt="image" src="https://github.com/user-attachments/assets/359da91e-a77f-446f-826c-524f8762d7b4" />

**What built-in account is for guest access to the computer?**

<img width="535" height="124" alt="image" src="https://github.com/user-attachments/assets/afe5bfff-9b9b-46f8-acb0-f8ace9da54e9" />

<img width="887" height="106" alt="image" src="https://github.com/user-attachments/assets/58af171a-b357-41d2-8b25-2a18022c019d" />

**What is the account description?**

`window$Fun1!` được ghi trong phần description của user tryhackme

<img width="883" height="134" alt="image" src="https://github.com/user-attachments/assets/b1d186bf-7411-49ab-87da-a2ba693a0db5" />


### TASK 7: User Account Control

Trong task này chúng ta học về **User Account Control (UAC)** là một phần khóa bên trong Windows Security. **UAC** giảm thiếu các rủi ro từ malware bằng cách giới hạn các quyền có khả năng của các mã độc hại cho việc thực thi nâng quyền administrator

Khi một người dùng thông thường hoặc 1 người dùng quyền administrator đăng nhập vào một hệ thống, thì Windows sẽ cung cấp cho chúng ta các token riêng cho những người dùng đó một quyền 

Để thực hiện kiểm tra quyền mà của các người dùng có thể tương tác lên file hoặc folder, chúng ta nhấn vào file hoặc folder vô phần `properties` và xem quyền của từng người dùng. 

<img width="444" height="590" alt="image" src="https://github.com/user-attachments/assets/b9eaab44-e3b7-4a8b-a9c9-58888a0325fb" />

<img width="122" height="111" alt="image" src="https://github.com/user-attachments/assets/5e297522-abc6-48fd-b3b2-49923b638cef" />

Một ứng dụng có cái khiên sẽ yêu cầu một quyền cao trong máy để có thể tải.

<img width="896" height="123" alt="image" src="https://github.com/user-attachments/assets/fc8eb8cc-a757-4f24-aafd-4ef5a89a1d40" />

### TASK 8: Settings and the Control Panel

**Control Panel** là một phần của Microsoft Windows nó cung cấp khả năng để xem và thay đổi cac cài đặt hệ thống. Nó bao gồm các thiết lập [applets](https://glints.com/vn/blog/java-applet-la-gi/) bao gồm thêm vào và remove các phần cứng và phần mềm, điều khiển tài khoản người dùng, thay đổi tùy chọn [accessibility](https://en.wikipedia.org/wiki/Computer_accessibility) và truy cập vào cài đặt mạng.

**Settings** trung tâm trung tâm để quản lý các khía cạnh khác nhau của PC của bạn. Nó cung cấp một giao diện đơn giản để tùy chỉnh và điều khiển thiết bị Windows của bạn, đảm bảo trải nghiệm cá nhân hóa và hiệu quả hơn.

<img width="772" height="157" alt="image" src="https://github.com/user-attachments/assets/d69f7cc9-e110-420d-b31b-2a3204108cb4" />

<img width="865" height="480" alt="image" src="https://github.com/user-attachments/assets/92bb6e1f-d7b8-478b-bf6d-761b79ac7bdc" />

### TASK 9: Task Manager

The Task Manager cung cấp các thông tin về các ứng dụng và chương trình được chạy hiện tại trên hệ thống. Một số thông tin khác cũng có sẳn, như là Lượng **CPU** và **RAM** được sử dụng, nó nằm bên trong **Performance**.

<img width="1867" height="961" alt="image" src="https://github.com/user-attachments/assets/065453bc-1b48-497d-b36c-feb780da9e74" />

<img width="760" height="130" alt="image" src="https://github.com/user-attachments/assets/0532a147-8d58-4685-9a95-e2bcaef495dd" />
