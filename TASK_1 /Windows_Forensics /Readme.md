# Windows Registry 
Windows Registry là một cơ sở dữ liệu phân tầng lưu trữ những cài đặt cấp thấp của hệ điều hành Microsoft Windows và các ứng dụng chọn sử dụng registry, được sử dụng từ phiên bản Windows 95 cho tới hiện nay.Trước phiên bản Windows 95, thì Windows sẽ lưu trữ các thông tin cấu hình bên trong các file (`.ini`).The registry hỗ trợ truy xuất tốc độ cao cho nhân hệ điều hành(Kernel), các thiết bị drivers, dịch vụ, Security Account Manager (SAM), và ứng dụng người dùng. Windows Registry hay là The registry chứa những thông tin, cài đặt, tùy chọn và các giá trị khác của chương trình và phần cứng được tải xuống của tất cả các phiên bản của Microsoft Windows. Ví dụ: một chương trình được tải xuống thì nó sẽ tạo ra một key mới và cái khóa này sẽ chứa các thông tin về vị trí lưu trữ của chương trình này, phiên bản của chương trình, cách mà chương trình hoạt động,.. tất cả sẽ nằm trong Windows Registry.

### 1. Structure of the Registry 
The registry chứa hai thành phần cơ bản là key và value. Registry keys là đối tượng có thể chứa giống như một folder, Registry value là một đối tượng không thể chứa giống như một file. Keys có thể chứa các subkey và value bên trong. Các khóa được tham chiếu với cú pháp tương tự như tên đường dẫn của Windows, sử dụng giấu gạch chéo ngược. Trong Windows Registry có 5 hives chính là: 

- **HKEY_CURRENT_USER (HKCU)**: Chứa những thông tin cấu hình gốc cho người dùng hiện đang đăng nhập. Folder của người dùng, cài đặt control panel được lưu trữ ở đây. Những thông tin này thường liên quan đến hồ sơ người dùng.
 
- **HKEY_USERS (HKU)**: Chứa tất cả những thông tin cấu hình người dùng cụ thể cho tất cả những người dùng đang đăng nhập, và những người khác đã đăng nhập, hay nói cách khác là toàn bộ hồ sơ của những người dùng đã từng đăng nhập trên máy tính đó. **HKCU** là một subkey của **HKU**, vì sao nói vậy? Bởi vì **HKCU** là một nhánh nhỏ là những hồ sơ của người dùng đang hoạt động hiện tại trên máy tính.

- **HKEY_LOCAL_MACHINE (HKLM)**: Chứa những thông tin cấu hình từng phần cho máy tính. Ngoài ra trong hive HKLM còn có 4 main subkey là **HKLM/SAM, HKLM/SECURITY, HKLM/SOFTWARE, HKLM/SYSTEM** em sẽ đi vào nội dung của 4 khóa con chính này của hive HKLM
  - **HKLM/SAM**: Dùng để quản lý tài khoản và mật khẩu cho tất cả các hệ thống miền cục bộ đang chạy. Chứa các cơ sở dữ liệu về người dùng (users), nhóm và mật khẩu(mã băm/hash). Đây là nơi hệ thống tra cứu khi một người dùng đăng nhập, và chỉ có những users có đặc quyền cao mới có thể truy cập được.
  - **HKLM/SECURITY**: Là các chính sách và quyền hạn, chứa các chính sách bảo mật toàn hệ thống và quy định ai có quyền làm gì trong máy tính, thường không hiển thị với tất cả người dùng, trừ những người có quyền quản trị trong hệ thống.
  - **HKLM/SOFTWARE**: Chứa các thiết lập của Windows và các phần mềm đã cài vào máy (Chrome, Office,..). Các cài đặt ở đây áp dụng chung cho tất cả người dùng cho máy tính.
  - **HKLM/SYSTEM**: Là nơi khởi động và vận hành chứa các thông tin cốt lõi để Windows khởi động được, bao gồm cấu hình driver và các dịch vụ nền. Nếu khóa hỏng, máy sẽ không thể boot được.
- **HKEY_CLASSES_ROOT (HKCR)**: Nó là một subkey của **HKLM\SoftWare**. Những thông tin được lưu trữ ở đây đảm bảo các chương trình được mở đúng khi bạn mở một file bằng Windows Explorers. Chứa những thông tin quan trọng cho liên kết các tập tin với các ứng dụng và quản lí COM(Component Object Model), thiết yếu để nói với Windows rằng là cần làm gì với file đó.

- **HKEY_CURRENT_CONFIG (HKCC)**: Chứa những thông tin về hồ sơ phần cứng được sử dụng trong máy tính cục bộ khi thiết bị được mở lên.


Registry Value là các giá trị dữ liệu cụ thể nhỏ nhất được lưu trữ bên trong Windows Registry, nó có thể chứa các cấu hình cài đặt chi tiết cho hệ điều hành, phần cứng, phần mềm.
Một số registry value chính là:

|Kiểu dữ liệu | Mô tả kỹ thuật |
| --- | --- |
|REG_SZ(chuỗi đơn)| Giá trị văn bản đơn giản, có một dòng|
|REG_EXPAND_SZ (chuỗi mở rộng)| Giá trị chuỗi "có thể mở rộng" có thể chứa các biến môi trường, thường được lưu trữ và hiển thị trong `UTF-16LE`, thường được kết thúc bằng ký tự NUL|
|REG_MULTI_SZ (chuỗi nhiều dòng)| Giá trị nhiều chuỗi, là danh sách có thứ tự các chuỗi không trống, thường được lưu trữ và hiển thị bằng Unicode, mỗi chuỗi được kết thúc bằng ký tự null, danh sách thường được kết thúc bằng ký tự null thứ hai|
|REG_DWORD (số nguyên 32 bit)| Thường dùng cho các giá trị boolean (0 cho false - 1 cho true)|
|REG_QWORD (số nguyên 64 bit)| Một số nguyên 64 bit (có thể là endian lớn hoặc endian nhỏ hoặc không xác định|
|REG_BINARY (dữ liệu nhị phân)| các giá trị 0 hoặc 1, dùng cho cài đặt không phải văn bản hoặc số như màu sắc, biểu tượng|

### 2. Khái niệm "Hive"

`Windows Registry` là tập hợp của nhiều tập tin riêng biệt gọi là "hives". Mỗi "hives" có thể chứa các key, subkey và value, "hives" có thể chứa 1 phần quan trọng của hệ thống hoặc các thông tin cấu hình của người dùng. Được lưu trữ bên trong 1 tệp riêng biệt trên ổ đĩa

#### Sự khác biệt của Registry_hive và Registry_key nằm ở khái niệm của nó Registry_hive là thư mục đầu tiên của registry và nó có chứa registry_key, còn registry_key nó nằm bên trong registry_hive, chứa các registry_subkey và các giá trị registry.

Hầu hết các têp hỗ trợ cho hives đều nằm trong thư mục `%SYSTEMROOT%\System32\Config`. Những files này được cập nhật mỗi lần người dùng đăng nhập vào. Phần mở rộng tên tệp của các tệp trong các thư mục này hoặc trong một số trường hợp bị thiếu phần mở rộng, cho biết loại dữ liệu mà chúng chứa. Dưới đây là một bảng các phần mở rộng và dữ liệu mà chúng chứa:

|Phần mở rộng | Mô tả |
|--- | ---|
|none | Một bản sao chép dữ liệu của hive |
|.alt | file `.alt` (alternative) là một bản sao lưu quan trọng dùng để khôi phục dự phòng khi có lỗi hoặc cập nhật hệ thống, giúp bảo vệ toàn vẹn các dữ liệu trong registry, nằm trong hive `HKEY_LOCAL_MACHINE\System`|
|.log | là file transaction log lưu lại các thay đổi trong key và value trước khi đưa vào hive chính|
|.sav | là một bản sao lưu cho hive như SAM, SYSTEM, SECURITY, SOFTWARE được tạo tự động bởi windows để phòng ngừa lỗi, đảm bảo có thể khôi phục cấu hình khi có sự cố xảy ra|


### 3. Accessing registry hives offilne
Vị trí của các keys trong một máy Windows:
- **DEFAULT** (mounted on `HKEY_USERS\DEFAULT`)
- **SAM** (mounted on `HKEY_LOCAL_MACHINE\SAM`)
- **SECURITY** (mounted on `HKEY_LOCAL_MACHINE\Security`)
- **SOFTWARE** (mounted on `HKEY_LOCAL_MACHINE\Software`)
- **SYSTEM** (mounted on `HKEY_LOCAL_MACHINE\SYSTEM`).

#### Hive chứa đựng thông tin của người dùng
Mỗi khi một người dùng khởi động máy tính hoặc đăng nhập vào nó sẽ tạo ra một hive user mới, 2 loại hive người dùng phổ biến là:
- NTUSER.DAT: Nằm tại thư mục gốc của người dùng (C:\Users\<User>). Chứa các cấu hình `desktop`, `RunMRU`, `RecentDocs`. Chứa các thông tin cấu hình cho từng người dùng cụ thể, như màn hình desktop, cài đặt về các chương trình được tải về, và những thông tin hồ sơ người dùng khác.
- USRCLASS.DAT: Nằm tại C:\Users\<User>\AppData\Local\Microsoft\Windows\. Chứa `ShellBags`, `MUICache`. Hive này thường chứa những thông tin về lớp ứng dụng và phần mở rộng tệp.

#### Ampache hive
Windows tạo ra hive này để lưu lại các thông tin quan trọng trên chương trình thường được chạy gần đây trên hệ thống. Nằm ở `C:\Windows\AppCompat\Programs\Amcache.hve`
#### Transaction logs
Registry hoạt động dựa trên cơ chế giao dịch để đảm bảo toàn vẹn dữ liệu. Khi một thay đổi được thực hiện, thì nó không ngay lập tức ghi vào hive chính ngay (Primary file), mà nó sẽ ghi lại vào trong tệp nhật kí giao dịch (Transaction Log). Nhật kí giao dịch với mỗi hive được ghi dưới dạng `.LOG`, nó có cùng tên với registry hive nhưng có thêm phần mở rộng `.LOG`.

Cơ chế: Là các thay đổi nằm trong bộ nhớ(Memory) được đẩy xuống các tệp `.LOG` hoặc (`.LOG1`, `.LOG2` trên hệ thống mới) trước khi hợp nhất với hive chính.

Dirty hive: Một hive được coi là 'bẩn' (dirty) khi có các thay đổi trong registry nhưng nó chưa được ghi vào hive chính, nó sẽ được đánh dấu là "dirty" và cần sử dụng một công cụ của Eric-Zic là công cụ RECmd(https://download.ericzimmermanstools.com/net9/RECmd.zip)
#### Registry Backup
Ngược lại với Transaction log, thì đây là những bản sao lưu của registry hive nằm trong thư mục `C:\Windows\System32\Config`. Những hive này được sao chép vào thư mục `C:\Windows\System32\Config\RegBack` cứ 10 ngày 1 lần, nó sẽ là những thông tin rất quan trọng trong quá trình phân tích các thay đổi dữ liệu gần đây trong registry key.

Dưới đây là một bảng danh sách các hives và các file hỗ trợ:
|Registry hive | File hỗ trợ |
| --- | --- |
|HKEY_CURRENT_CONFIG | System, System.alt, System.log, System.sav|
|HKEY_CURRENT_USER | Ntuser.dat, Ntuser.dat.log |
|HKEY_LOCAL_MACHINE\SAM | Sam, Sam.log, Sam.sav |
|HKEY_LOCAL_MACHINE\Security | Security, Security.log, Security.sav |
|HKEY_LOCAL_MACHIN\Software | Software, Software.log, Software.sav |
|HKEY_LOCAL_MACHINE\System | System, System.alt, System.log, System.sav |
|HKEY_USERS\.DEFAULT | 	Default, Default.log, Default.sav |


---

# Commond Artifact in Windows Forensics

## WindowsForensics1 - Tryhackme

### System information and system account 
#### 1. OS version, Hostname
Là một giá trị registry chứa những thông tin cấu hình chi tiết về hệ điều hành hiện tại và phần mềm tải xuống. OS version nằm ở `SOFTWARE\Microsoft\Windows NT\CurrentVersion`

<img width="1041" height="539" alt="image" src="https://github.com/user-attachments/assets/0404f210-c563-4ff8-9f16-8a0ea2b81be4" />

**Computer Name** : `SYSTEM\CurrentControlSet\Control\ComputerName\ComputerName `

<img width="1025" height="127" alt="image" src="https://github.com/user-attachments/assets/2fce7ebd-20b9-4191-9d5e-4268beb7234f" />

#### 2. Current Control Set
**Current Control set** không phải là một nơi lưu trữ dữ liệu vật lý, mà nó là một Symbolic link (liên kết tượng trưng) hoặc cũng có thể coi là một con trỏ, nó sẽ trỏ hệ thống hoặc ứng dụng đến các khóa Control Set.

**Control Sets** nó là một hives chứa những dữ liệu cấu hình của một máy được sử dụng để điều khiển hệ thống trong quá trình khởi động. Phổ biến, ta có hai Control Sets là ControlSet001 thường được trỏ đến từ con trỏ Current Control Set khi một máy được khởi động thành công, và ControlSet002 sẽ được trỏ đến khi lần khởi động đầu tiên gặp sự cố trục trặc thì ControlSet002 thường sẽ giữ Cấu hình `Last Know good` - một bản sao lưu cài đặt khởi động thành công gần đây nhất, nếu cài đặt hiện tại không thành công.
Vị trí lưu trữ của hai ControlSet:

`SYSTEM\ControlSet001`

`SYSTEM\ControlSet002`

Và chúng ta cũng có thể tìm thấy được ControlSet nào đang được sử dụng hiện tại, và cấu hình `Last Know Good` bằng cách theo giá trị registry sau:

`SYSTEM\Select\Current`

`SYSTEM\Select\LastKnowGood`

<img width="805" height="237" alt="image" src="https://github.com/user-attachments/assets/3b3ccf5d-ad71-4126-aa14-de329d621bf5" />

Subkey `Select` ở đây chứa thông tin của ConTrolSet nào đang được hoạt động (Current), ControlSet nào được dùng mặc định (Default), Control Set nào được dự phòng (last know good) nếu có lỗi boot máy mà nó không hoạt động, và Control Set nào bị lỗi sẽ được lưu bên trong (Failed)

Các giá trị registry chính:

- `Current`: Chứa giá trị DWORD 32 bit thứ tự  ControlSet đang được sử dụng làm CurrentControlSet trong lần khởi động hiện tại.
- `Default`: Chứa giá trị DWORD 32 bit thứ tư ControlSet mà hệ thống sử dụng làm CurrentControlSet cho lần hoạt động tiếp theo.
- `Failed`: Giá trị DWORD cho biết ControlSet nào đã thất bại trong lần khởi động gần nhất, để Windows có thể quay trở lại cái cấu hình khởi động thành công gần nhất.
- `Last Know Good`: Giá trị DWORD cho biết số thứ tự của Control Set tốt nhất được biết đến (thường là cấu hình thành công cuối cùng).

#### 3. Timezone information
Việc nắm được các khung thời gian trong máy sẽ giúp cho chúng ta hiểu được trình tự các sự kiện xảy ra. Timezone có thể được tìm thấy tại: `SYSTEM\CurrentControlSet\Control\TimeZoneInformation`

<img width="1181" height="287" alt="image" src="https://github.com/user-attachments/assets/206afe8d-d88a-4b9c-a4f0-6a48fc5aa801" />

#### 4. Network Interface and Past Network
**Network Interface**: Mỗi giao diện sẽ đại diện cho một subkey định danh(GUID) duy nhất, chứa các giá trị liên quan đến cấu hình TCP/IP của giao diện, khóa này cung cấp các key information chính cho network interface artifact:

- IP cấu hình cho từng giao diện.
- Địa chỉ MAC cho từng giao diện.
- Danh sách tất cả những giao diện đã tải xuống trên hệ thống.

**IP cấu hình cho từng giao diện**

<img width="1091" height="597" alt="image" src="https://github.com/user-attachments/assets/9705c11f-790d-4260-81f4-c5a7810a1010" />

`HKEY_LOCAL_MACHINE\SYSTEM\ControlSet001\Services\Tcpip\Parameters\Interfaces\`

Mỗi một khóa con thì nó sẽ đại diện cho một IP cấu hình dữ liệu cho từng interface. Mỗi cái tên cho các khóa con đại diện cho một GUID được sử dụng để nhận dạng duy nhất cho giao diện đó, và có thể được sử dụng để tương quan với những thông tin của những artifact khác.

**Key data mà mỗi giao diện có thể chứa**:
|Info | Notes |
| --- | --- |
| Cách mà IP được gán tĩnh hay động | "EnableDHCP" với giá trị là 1 có nghĩa là DHCP đã được bật |
| Đia chỉ IP | Địa chỉ ip có thể được thu thập bên trong "IPAddress" hoặc "DHCPIPAddress" dựa vào nó được gán tĩnh hay động |
| Subnet mask | Subnet mask có thể được thu thập bên trong "SubnetMask" hoặc là "DHCPSubnetMask" dựa vào nó được gán tĩnh hay động |
| DNS server | DNS server ip có thể được thu thập trong "NameServer" hoặc là "DHCPNameServer" dựa vào nó được gán tĩnh hay động |

**Địa chỉ MAC cho mỗi giao diện**
Mỗi giao diện trong đó nó sẽ chứa một địa chỉ MAC được lưu trong subkey kernel bên trong các GUID của giao diện đó, mỗi giao diện đều sinh ra địa chỉ MAC riêng biệt vì nó định danh cho phần cứng duy nhất cho mỗi card mạng, và được lưu trữ lại:

`HKEY_LOCAL_MACHINE\SYSTEM\ControlSet001\Control\NetworkSetup2\Interfaces\{INTERFACE_GUID}\Kernel`

<img width="1082" height="703" alt="image" src="https://github.com/user-attachments/assets/556f11ef-be97-49c8-8939-c5eb2638c4b7" />

**Danh sách tất cả các giao diện đã tải xuống trên hệ thống**
Là nơi lưu trữ danh sách của toàn bộ những card mạng từng được cài đặt cho máy tính, cung cấp các thông tin chi tiết về card mạng hiện tại

<img width="1092" height="646" alt="image" src="https://github.com/user-attachments/assets/e02ac741-1584-4d28-9a9f-8e92697bbd86" />

`HKEY_LOCAL_MACHINE\SYSTEM\ControlSet001\Control\Class\{4d36e972-e325-11ce-bfc1-08002be10318}\xxxx`

- Mỗi subkey đều theo một khuôn là XXXX với mỗi số X là các con số biểu thi cho 1 giao diện.
- Nó có rất nhiều những thông tin kỹ thuật chi tiết cho giao diện như (Driver version, driver install date, install timestamp, interface enable,...)

**Connected Networks (các mạng từng được kết nối)**, một số những artifact em tìm hiểu được từ những mạng từng được kết nối:

- Tên của những mạng đã từng được kết nối.
- Lần đầu và lần cuối những mạng này được kết nối.
- Cổng địa chỉ Mac 
- DNS suffix: là phần đuôi tên miền được máy chủ DHCP cấp phát tự động cho máy tính khi nó kết nối vào mạng đó.(airport.wifi: mạng kết nối tại sân bay, localdomain or none: thường là mạng gia đình cấu hình mặc định)

Có 2 vị trí mà chúng ta có thể tìm thấy các artifact này:

**Locate1** : `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\NetworkList\Profiles\`

<img width="1091" height="624" alt="image" src="https://github.com/user-attachments/assets/d1e31fd3-07eb-4167-82b6-22a6c987584d" />

Mỗi subkey nó sẽ đại diện cho những metadata liên quan đến mạng mà hệ thống đã kết nối tại thời điểm đó, các name subkey là các GUID duy nhất để định danh cho các hồ sơ mạng (Network Profile ID) mà máy tính này đã từng kết nối thành công.
Các giá trị registry trong mỗi GUID này mang các ý nghĩa sau:

|Info | Notes |
| --- | --- |
| ProfileName | Các tên mạng được nhận dạng bởi Windows. Trong các trường hợp mạng không dây thì đây là các SSID|
| Description | Là những tên quen thuộc của người dùng, thông thường thì nó giống với ProfileName |
| DateCreated | Là ngày hệ thống lần đầu kết nối vào mạng |
| DateLastConnected | Ngày cuối mà hệ thống kết nối vào mạng |
| Category | Hồ sơ kết nối mạng được dùng khi tham gia vào 1 mạng (0 = public, 1 = private, 2 = domain) |

**Located2** : `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\NetworkList\Profiles\Signatures\*\`

Mỗi subkey bên dưới Managed và Unmanaged sẽ đại diện cho các metadata thêm vào khi tham gia vào một mạng.

`SOFTWARE\Microsoft\Windows NT\CurrentVersion\NetworkList\Signatures\Unmanaged`

`\Unmanaged` là những mạng không thuộc sự kiểm soát của các miền cục bộ như mạng wifi gia đình, mạng công cộng.

`SOFTWARE\Microsoft\Windows NT\CurrentVersion\NetworkList\Signatures\Managed`

`\Managed` chứa thông tin các mạng doanh nghiệp được xác định trong Domain Controller (Active Directory)

<img width="1195" height="231" alt="image" src="https://github.com/user-attachments/assets/bac8c27d-8cbc-47ea-836c-bdccd359df01" />

Các registry key này chứa các mạng trước đây, cùng với lần gần nhất mà chúng được kết nối. Thời gian ghi cuối cùng của registry key nó sẽ trỏ đến cái lần cuối cùng mà những mạng này nó được kết nối.

Các giá trị registry quan trọng trong các subkey:
- ProfileGUID: Được sử dụng để liên kết dữ liệu trong khóa này với khóa Cấu hình được đề cập trước đó.
- DNS suffix liên quan đến mạng đang kết nối.
- Cổng mặc định của địa chỉ MAC.
