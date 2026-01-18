# Windows Registry 
Windows Registry là một cơ sở dữ liệu phân tầng lưu trữ những cài đặt cấp thấp của hệ điều hành Microsoft Windows và các ứng dụng chọn sử dụng registry, được sử dụng từ phiên bản Windows 95 cho tới hiện nay.Trước phiên bản Windows 95, thì Windows sẽ lưu trữ các thông tin cấu hình bên trong các file (`.ini`).The registry hỗ trợ truy xuất tốc độ cao cho nhân hệ điều hành(Kernel), các thiết bị drivers, dịch vụ, Security Account Manager (SAM), và ứng dụng người dùng. Windows Registry hay là The registry chứa những thông tin, cài đặt, tùy chọn và các giá trị khác của chương trình và phần cứng được tải xuống của tất cả các phiên bản của Microsoft Windows. Ví dụ: một chương trình được tải xuống thì nó sẽ tạo ra một key mới và cái khóa này sẽ chứa các thông tin về vị trí lưu trữ của chương trình này, phiên bản của chương trình, cách mà chương trình hoạt động,.. tất cả sẽ nằm trong Windows Registry.

### 1. Structure of the Registry 
The registry chứa hai thành phần cơ bản là `key` và `value`. `Registry keys` là đối tượng có thể chứa giống như một folder, `Registry value` là một đối tượng không thể chứa giống như một file. `Keys` có thể chứa các subkey và value bên trong. Các khóa được tham chiếu với cú pháp tương tự như tên đường dẫn của Windows, sử dụng giấu gạch chéo ngược. Trong `Windows Registry` có 5 hives chính là: 

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
|REG_DWORD (số nguyên 32 bit)| là kiểu số nguyên 32 bit - 4 byte có thể hiễn thị ở dạng Decimal, Hexadecimal hoặc binary|
|REG_QWORD (số nguyên 64 bit)| Một số nguyên 64 bit (có thể là endian lớn hoặc endian nhỏ hoặc không xác định|
|REG_BINARY (dữ liệu nhị phân)| các giá trị 0 hoặc 1, dùng cho cài đặt không phải văn bản hoặc số như màu sắc, biểu tượng|

### 2. Khái niệm "Hive"

`Windows Registry` là tập hợp của nhiều tập tin riêng biệt gọi là "hives". Mỗi "hives" có thể chứa các key, subkey và value, "hives" có thể chứa 1 phần quan trọng của hệ thống hoặc các thông tin cấu hình của người dùng. Được lưu trữ bên trong 1 tệp riêng biệt trên ổ đĩa

#### Sự khác biệt của Registry_hive và Registry_key nằm ở khái niệm của nó Registry_hive là thư mục đầu tiên của registry và nó có chứa registry_key, còn registry_key nó nằm bên trong registry_hive, chứa các registry_subkey và các giá trị registry.

Hầu hết các tệp hỗ trợ cho hives đều nằm trong thư mục `%SYSTEMROOT%\System32\Config`. Những files này được cập nhật mỗi lần người dùng đăng nhập vào. Phần mở rộng tên tệp của các tệp trong các thư mục này hoặc trong một số trường hợp bị thiếu phần mở rộng, cho biết loại dữ liệu mà chúng chứa. Dưới đây là một bảng các phần mở rộng và dữ liệu mà chúng chứa:

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

# Common Artifact in Windows Registry

## System information and system account 
### 1. OS version, Hostname
Là một giá trị registry chứa những thông tin cấu hình chi tiết về hệ điều hành hiện tại và phần mềm tải xuống. OS version nằm ở `SOFTWARE\Microsoft\Windows NT\CurrentVersion`

<img width="1041" height="539" alt="image" src="https://github.com/user-attachments/assets/0404f210-c563-4ff8-9f16-8a0ea2b81be4" />

**Computer Name** : `SYSTEM\CurrentControlSet\Control\ComputerName\ComputerName `

<img width="1025" height="127" alt="image" src="https://github.com/user-attachments/assets/2fce7ebd-20b9-4191-9d5e-4268beb7234f" />

### 2. Current Control Set
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
- `Default`: Chứa giá trị DWORD 32 bit thứ tự ControlSet mà hệ thống sử dụng làm CurrentControlSet cho lần hoạt động tiếp theo.
- `Failed`: Giá trị DWORD cho biết ControlSet nào đã thất bại trong lần khởi động gần nhất, để Windows có thể quay trở lại cái cấu hình khởi động thành công gần nhất.
- `Last Know Good`: Giá trị DWORD cho biết số thứ tự của Control Set tốt nhất được biết đến (thường là cấu hình thành công cuối cùng).

### 3. Timezone information
Việc nắm được các khung thời gian trong máy sẽ giúp cho chúng ta hiểu được trình tự các sự kiện xảy ra. Timezone có thể được tìm thấy tại: `SYSTEM\CurrentControlSet\Control\TimeZoneInformation`

<img width="1181" height="287" alt="image" src="https://github.com/user-attachments/assets/206afe8d-d88a-4b9c-a4f0-6a48fc5aa801" />

### 4. Network Interface and Past Network
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
| Địa chỉ IP | Địa chỉ ip có thể được thu thập bên trong "IPAddress" hoặc "DHCPIPAddress" dựa vào nó được gán tĩnh hay động |
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
- **ProfileGUID**: Được sử dụng để liên kết dữ liệu trong khóa này với khóa Cấu hình được đề cập trước đó.
- **DNS suffix** liên quan đến mạng đang kết nối.
- Cổng mặc định của địa chỉ MAC.


### 5. AutoStart Programs

**Autostart** là thuật ngữ đề cập tới những phần mềm có khả năng tự động chạy mà không cần người dùng phải chạy nó. Phần mềm này bao gồm các drivers và các dịch vụ bắt đầu khi một máy được khởi động lên. Các ứng dụng, tiện ích, hoặc thậm chí là các lệnh shell được khởi chạy khi người dùng đăng nhập vào, các browser extention tự động tải khi người dùng mở một ứng dụng trình duyệt chẳng hạn như thế.

Trước khi đi sâu vào các khóa registry startup thì em đã tìm hiểu một chút về quá trình một máy windows boot lên sau đó các key registry startup của registry hoạt động:

**System boot**

- Đây là quá trình diễn ra sau khi Kernel được nạp vào và quản lí tiến trình hoạt động, lúc này nó sẽ sinh ra một tiến trình (smss.exe - Session Manager Subsystem) được tạo ra để quản lí các Session, khi đó một registry key sẽ được khởi tạo bên trong registry là `bootExecute` sẽ thực thi các mục bên trong nó để hoàn tất quá trình khởi động hệ thống.

**Winlogon Initialization (khởi tạo)**

- Là quá trình mà nó dựng nên một môi trường đăng nhập bền vững và an toàn cho người dùng bằng cách thiết lập một đăng kí tới với SAS - (Secure Attention Sequence), việc nó thực hiện đăng kí SAS là để độc quyền lắng nghe tổ hợp phím (CTRL + ALT + Delete). Vậy thì SAS nó sẽ hoạt động nó như nào? SAS nó là một ngắt cứng được Windows Kernel lập trình để ngăn chặn một ứng dụng thứ 3 có thể chiếm quyền hoặc thay đổi hành vi, liên quan đến quá trình khởi tạo winlogon thì nó sẽ ngăn chặn việc một phần mềm độc hại có khả năng chiếm quyền hoặc tạo ra một giao diện fake để lấy mật khẩu người dùng. Sau đó tiến trình `winlogon.exe` sẽ xử lí các phiên đăng nhập tương tác với người dùng.

**User logon**

- Sau khi người dùng xác thực xong. Explorer.exe sẽ tiến hành đọc và xử lí các khóa Autostart như (Run - RunOnce), mà nó đã được thiết lập từ trước đó trong khóa Startup, và cuối cùng là bắt đầu thực thi.


Ở đây em sẽ tìm hiểu kĩ về một số các registry startup key bên trong một máy ở trong registry:

<img width="2553" height="891" alt="image" src="https://github.com/user-attachments/assets/63df2954-f949-4aeb-a9bd-0584120364fd" />

`NTUSER.DAT\Software\Microsoft\Windows\CurrentVersion\Run`:   Key Run này chạy bên trong Hive NTUSER.DAT nó sẽ tự động chạy các chương trình được lưu bên trong key Run này mỗi khi mà người dùng đăng nhập vào.

<img width="2517" height="930" alt="image" src="https://github.com/user-attachments/assets/20fcd323-9b50-45fe-941b-fb28c46f05c7" />

`NTUSER.DAT\Software\Microsoft\Windows\CurrentVersion\RunOnce`:  khóa này cho phép thực thi các chương trình 1 lần khi người dùng đăng nhập vào, và sau đó nó sẽ bị xóa đi trong registry để tránh quá trình thực thi lại lệnh như vòng lặp.

<img width="1985" height="1131" alt="image" src="https://github.com/user-attachments/assets/a58485c0-292e-4899-b9a1-44d5f78785e9" />

`SOFTWARE\Microsoft\Windows\CurrentVersion\RunOnce`: Khóa này nó sẽ bao gồm một tập lệnh hoặc chương trình được Windows thực thi sau khi máy được khởi động, hoặc sau khi hoàn thành một tác vụ nào đó. Sau đó nó sẽ bị tự động xóa đi trong registry để tránh việc thực thi lại.

`SOFTWARE\Microsoft\Windows\CurrentVersion\policies\Explorer\Run`: Khóa này sẽ thực thi các chính sách (policies) để buộc các ứng dụng phải chạy, thường được sử dụng bởi administrator để triển khai các phần mềm hoặc kiểm soát ứng dụng đảm bảo dịch vụ quan trọng luôn hoạt động. Khóa này sẽ thực hiện với tất cả các users đã đăng nhập vào máy, khi khởi động máy lên.

<img width="1504" height="1110" alt="image" src="https://github.com/user-attachments/assets/99c41874-b3c1-4170-af17-a2d78e668c87" />

`SOFTWARE\Microsoft\Windows\CurrentVersion\Run` : Khóa này sẽ giống như khóa trong Hive NTUSER.DAT nó sẽ thực thi chương trình hoặc tập lệnh mỗi khi máy được đăng nhập hoặc khởi động nhưng nó sẽ áp dụng với tất cả các user đăng nhập vào máy chứ không phải mỗi user như hive NTUSER.DAT. 


### 6. SAM hive and user Infomation

SAM hive trong Windows registry là một phần cơ sở dữ liệu quan trọng nó lưu trữ những thông tin tài khoản của người dùng và mật khẩu (mã băm), nó cần thiết cho quá trình xác thực.

Những thông tin này nằm ở: `SAM\Domains\Account\Users`

<img width="1179" height="445" alt="image" src="https://github.com/user-attachments/assets/d06a876d-d662-45f4-ac11-feda94ac7f98" />

Những thông tin trong hình bao gồm mã định danh (RID) của người dùng, số lần mà user đăng nhập, lần đăng nhập gần nhất, lần đăng nhập thất bại gần nhất, lần cuối thay đổi mật khẩu, chính sách mật khẩu, passwd hint và bất cứ group nào mà người dùng là một phần.

Có 1 điểm quan trọng khác là hive này khi chúng ta thử sử dụng regedit.exe trên máy để mở thì sẽ không thấy gì cả.

<img width="1179" height="445" alt="image" src="https://github.com/user-attachments/assets/e60b7861-e0aa-47cf-b33d-5aa48f409093" />

Lý do nằm ở hive này chứa những thông tin rất quan trọng là tải khoản và mật khẩu của người dùng, nên quyền administrator cũng không thể xem được, nó chỉ được thiết lập cho những user có quyền SYSTEM tương đương với root. Nhưng trong windows thì lại không có option đưa quyền lên mức SYSTEM.

Nhưng ở đây có 1 tricks em đọc được từ blogs: https://cylab.be/blog/310/install-sysinternals

- Đầu tiên chúng ta cần tải nó xuống thông qua blogs kia.

- Sau đó thực hiện mở cmd bằng administrator.

- Trong cmd, dùng lệnh `psexec -sid Regedit.exe` psexec - là từ công cụ vừa được tải về **Sysinternals**

- Lần này nó sẽ hiện ra tất cả những thông tin bên trong hive.

<img width="952" height="709" alt="image" src="https://github.com/user-attachments/assets/cd4ee655-e46c-4071-97ab-43fbec7dddfe" />



## Usage or knowledge of files/folders

### 1. Recent files

Recent files (các file gần đây) là một tính năng của hệ điều hành windows, nó lưu trữ những file hoặc folder được sử dụng gần đây cho mỗi người dùng. Chẳng hạn như khi ta sử dụng File Explorer ở thư mục home nó sẽ list ra cho ta một danh sách những file gần đây mà chúng ta đã mở hoặc truy cập. Mỗi khi mở một files thì Windows sẽ tạo ra một file `.lnk` tương ứng và đưa nó vào mục `Recent files`.

Registry key `RecentDocs` là một khóa bên trong Windows Registry, nó theo dõi những hoạt động mở files và folders gần đây của người dùng, `RecentDocs` chứa những nhiều những subkeys gắn với những file extention, trong mỗi subkeys này nó sẽ chứa nhiều giá trị bên trong, được đánh số làm tên giá trị, và mỗi giá trị chứa những dữ liệu nhị phân, giá trị tên **MRUListEX (Most Recently Used list Extended)** để quản lí thứ tự các files được mở gần đây.

<img width="1183" height="429" alt="image" src="https://github.com/user-attachments/assets/b2cfffe8-62c8-432b-b140-5bf6fb157354" />


 **MRUListEx** trong khóa registry `RecentDocs` là những giá trị nhị phân mà nó theo dõi thứ tự gần đây nhất của những file hoặc folder được người dùng mở. Nó đóng vai trò là **Index (bảng chỉ mục)** để xác định thứ tự thời gian truy cập của các mục dữ liệu trong một khóa MRU. **MRUListEx** này nó sẽ chứa những con số (IDs), các con số này thường được bắt đầu bằng tên của các Value nằm trong keys `RecentDocs`.

 **MRUListEx** nó sẽ lưu các chuỗi hex này thành một cụm 4 byte một, và byte đầu của nó sẽ là tên của Value, cách nó sắp xếp thứ tự là sẽ dùng byte đầu của 4 byte đầu để xác định tên giá trị và cũng là files được mở gần đây nhất, và cứ nối tiếp như vậy 4 byte tiếp theo.

 `07 00 00 00 06 00 00 00 05 00 00 00 04 00 00 00 03 00 00 00 01 00 00 00 00 00 00 00 02 00 00 00 FF FF FF FF`

- Lấy ví dụ trong ảnh trên thì ta sẽ có:
 - 4 byte đầu là:  `07 00 00 00`, ID = 7 (đây là file mới nhất)
 - 4 byte tiếp theo: `06 00 00 00` ID = 6 (đây là file mới nhì)
 - tương tự thế .....

### 2. Office Recent files

Tương tự như `Recent Docs` thì `Office Recent Files` cũng sẽ theo dõi các files cụ thể nằm trong Microsoft Office được mở gần đâ từ người dùng. 

`HKCU\Software\Microsoft\Office\<VERSION>\Word`

Với mỗi version thì những file lưu trữ bên trong chương trình của Microsoft Office sẽ khác nhau ví dụ ở đây là file `Word`, bên trong key này `Word` này nó sẽ chứa những sub-keys quan trọng cho quá trình truy cập nhanh chóng:

- File MRU: các files được mở gần đây.

- Place MRU: vị trí mà các files được mở hoặc lưu gần đây.

- User MRU: chứa các tài khoản mà người dùng sử dụng để đăng nhập gần đây.

### 3. ShellBags

Shellbags được đề cập đến là một tập hợp những registry key và các key dữ liệu của Windows, dùng để duy trì việc ghi nhớ những tùy chọn hiển thị File Explorer và Windows Open/Save dialogs của người dùng. Giúp hệ điều hành Windows ghi nhớ và khôi phục cách hiển thị các thư mục của người dùng theo tùy chọn của họ. Ví dụ như:
 - Windows location/size.
 - Hiển thị cột.
 - Sắp xếp cột.
 - Icon size.

`ShellBags` có thể chứa đựng rất nhiều những thông tin trong những folders mà người đã truy cập vào. Tuy nhiên, bởi vì những thông tin chi tiết chính xác về cách mà `shellbags` hoạt động không được công bố rộng rãi, nó có thể sẽ khó trong việc hiểu tường tận về dữ liệu. Chúng ta nên sử dụng những cái artifacts khác để xác minh lại những dữ liệu đã tìm được và kiểm tra với những kịch bản cụ thể để đảm bảo mình hiểu được nó và làm sao nó nằm ở đó.

Những keys information từ ShellBags:
| Info | Notes |
|--- | --- |
|Toàn bộ đường dẫn đến thư muc | Kể cả cho những thư mục đã bị xóa |
| Người dùng nào đã truy cập vào folders | Dựa vào registry hive (SAM hive)
| Chỉnh sửa, truy cập và tạo ra timestamps cho folders đã được truy cập | Nó được ghi lại cho lần đầu folders được đưa vào Shellbags |
| Lần đầu và lần cuối người dùng truy cập vào thư mục | Dựa vào lần gần nhất được ghi lại của registry key và có thể được sử dụng trong 1 số trường hợp để suy ra first và last time accesss vào thư mục |

**How ShellBags work?/ More Detailed Breakdown**

**ShellBags** hoạt động dựa trên 2 thành phần là `BagMRU` (Cấu trúc cây) và `Bags`/`Nodeslot` (Dữ liệu cấu hình)

Giờ em sẽ đi sâu vào từng thành phân tương ứng là registry key `BagMRU` và `Bags/Nodeslot`, sau đó sẽ đi vào cách hoạt động

`BagMRU` là một registry key nó lưu trữ cấu trúc phân cấp của các thư mục người dùng đã truy cập theo dạng cây, nó chứa đường dẫn đầy đủ tới thư mục đã được truy cập, cùng với tất cả thông tin timestamp.

<img width="373" height="208" alt="image" src="https://github.com/user-attachments/assets/7a34a5f7-f10a-4cf2-b900-229737a5ce20" />

Mỗi khóa/khóa con được đánh số dưới `BagMRU` chứa các giá trị sau:

- Mỗi thư mục đại diện bởi 1 thư mục con được đánh số (0, 1, 2,...)
 
- `MRUListEx` MRU list hiển thị thứ tự của các thư mục được truy cập.
 
- `Nodeslot` là một giá trị số được liên kết với các mục của thư mục trong `BagMRU`, đến với các cài đặt hiển thị cụ thể (như độ lớn nhỏ của icon, sắp xếp cột, xóa cột trong các Open/Save dialog - File Explorer).

<img width="686" height="176" alt="image" src="https://github.com/user-attachments/assets/0089c696-6ba2-4c5a-8c36-437f6aabd2c0" />

`Bags` cũng là một registry key nó lưu trữ những cài đặt cấu hình hiển thị cho từng thư mục cụ thể.

<img width="1030" height="372" alt="image" src="https://github.com/user-attachments/assets/b34c9284-7e20-48a6-99d2-6acca4d9c3e3" />

Mỗi keys được đánh số bên dưới `Bags` có thể chứa những dữ liệu sau:

- Tên của khóa con (subkey name) được đánh số (1, 2, 3,..) tương ứng với giá trị `NodeSlot` từ `BagMRU` subkeys.
 
- Keys bên dưới các subkeys được đánh số đại diện cho nơi mà các tùy chọn được áp dụng.
 
 - Chúng ta sẽ có 2 giá trị. Giá trị "Shell" đại diện cho tùy chọn được áp dụng cho File Explorer, còn giá trị "comdlg" đại diện cho tùy chọn áp dụng vào Windows Open/Save dialog.
 
- Các khóa con bên dưới `Shell` hoặc là `comdlg` chứa các tùy chọn cụ thể.

**How Shellbags Work**

Như đã nói thì `Shellbags` hoạt động dựa trên 2 thành phần `BagMRU` và `Bags`. Lấy ví dụ về khi mở 1 thư mục `C:\Users\LOQ\Goals`:

- Lúc này `BagMRU` sẽ đóng vai trò là duyệt qua từng thu mục, để tìm ra thư mục đại diện có `NodeSlot` là `Goals`

- Sau đó thì tại `NodeSlot` bên trong thư mục "Goals" đó nó sẽ đọc giá trị DWORD được lưu trữ.

- Nó sẽ đi duyệt qua các keys của `Bags` và tìm đến keys có cùng giá trị với `NodeSlot` được đặt ở tên subkeys.

- Cuối cùng là nó sẽ dùng những tùy chọn đã được set từ trước sử dụng cho thư mục `Goals` được mở


### 4. Open/Save and LastVisited Dialog MRU:

Khi mà chúng ta thực hiện tải một file hoặc một thư mục về máy, thì lúc này trên màn hình sẽ hiện ra dialog box và sẽ hỏi chúng ta muốn lưu file hoặc folder đó ở đâu. Khi chúng ta thực hiện tải về thư mục ở vị trí cụ thể đã chọn trong máy tính, thì Windows sẽ ghi nhớ lại điều này để lần sau khi tải về 1 file nó sẽ giúp chúng ta thực hiện thao tác lưu tiện hơn.

Điều này tương đương với việc chúng ta có thể tìm ra được một files được người dùng mở gần đây nhất thông qua cái cơ chế `LastVisited` này. Vị trí chúng ta có thể tìm được keys này bên trong Registry Explorer là

`NTUSER.DAT\Software\Microsoft\Windows\CurrentVersion\Explorer\ComDlg32\LastVisitedPidlMRU`

<img width="1181" height="131" alt="image" src="https://github.com/user-attachments/assets/e43a8e0e-bcf4-401f-bbb8-dc98d9b05916" />

#### 5. Windows Explorer Address/Search Bars:

**Windows Explorer Address/Search Bars** có thể cho chúng ta biết được files hoặc folder mà người dùng sử dụng gần đây bằng cách hiển thị nó bên trong **Quick Access** và lưu trữ lịch sử tìm kiếm bên trong Windows Registry, chúng ta có thể tìm được thông tin đó ở vị trí:

<img width="1195" height="149" alt="image" src="https://github.com/user-attachments/assets/eba549db-3a08-4758-96b5-dbe3a1b000d4" />

 - `NTUSER.DAT\Software\Microsoft\Windows\CurrentVersion\Explorer\TypedPaths`  : Để theo dõi trực được trực tiếp các đường dẫn mà người dùng đã nhập vào trong thanh tìm kiếm của File Explorer.


 - `NTUSER.DAT\Software\Microsoft\Windows\CurrentVersion\Explorer\WordWheelQuery`  : Dùng để lưu trữ những thuật ngữ mà người dùng đã tìm kiếm trong File Explorer, chứa những dữ liệu nhị phân cho từng truy vấn và sủ dược 1 giá trị `MRUListEx` để theo dõi thứ tự của từng thuật ngữ người dùng tìm. 



## Evidence of Execution

### 1. UserAssits

UserAssist nó là một đặc trưng bên trong Windows cho phép theo dõi việc sử của những file được thực thi và những chương trình hoặc ứng dụng được khởi chạy bởi người dùng. Những dữ liệu được lưu trữ bên trong Windows Registry và có thể đóng 1 vai trò quan trọng trong việc tái cấu trúc timeline hoạt động của người dùng. 

Chúng ta có thể tìm được các dữ liệu được lưu bên trong 1 hive UserAssist ở vị trí:

`Software\Microsoft\Windows\CurrentVersion\Explorer\UserAssist`

Mỗi mục bên trong UserAssist được mã hóa theo thuật toán [ROT13](https://vi.wikipedia.org/wiki/ROT13), và [Magnet Axiom automatically](https://www.magnetforensics.com/products/magnet-axiom/) decodes những thông tin này để có thể dễ nhìn hơn. Những dữ liệu đã được giải mã bao gồm:

 - Đường dẫn của Ứng dụng.
 - Run count (Số lần chạy)
 - Last execution timestamp.
 - Focus time.
 - Focus count.

**Trong các phiên bản Microsoft Windows 10/11:** đã thực hiện thêm vào 1 cơ chế theo dõi chi tiết các ứng dụng **Universal Windows Platform - UWP** (là các ứng dụng chạy được nhiều nền tảng của Microsoft Store). Các nhà phân tích hiện nay không chỉ có thể xác định những ứng dụng nào được chạy, mà còn có thể xem được các hoạt động của người dùng bên trong các ứng dụng **UWP**

**Có một lưu ý rất quan trọng**: 

- Chúng ta đôi khi sẽ nhầm lẫn một file đã được người dùng chạy thông qua shortcut file `.lnk`. Trong thực tế **Windows** có thể tạo hoặc cập nhật thông tin của file `.lnk` ngay cả khi người dùng không chạy nó. Có thể khiến những người phân tích có thể xác định nhầm những file đã được người dùng thực thi, và mốc thời gian của các file không được thực thi trong thực tế đó dẫn đến tạo ra một timeline các hoạt động người dùng không chính xác.

 - **Nguyên nhân**: là khi chúng ta mở một folder có chứa các file `lnk` hoặc nhấp chuột phải vào nó thì hệ thống của Windows cũng sẽ ghi nhận lại là người dùng có `interaction` với nó.

 - **Giải pháp** trong UserAssist có một registry value là **Focus time**, giá trị này nó sẽ tính toán và ghi lại khoảng thời gian mà chương trình được user thật sự bật lên, hiện trên màn hình của người dùng , thao tác trong bao lâu.

- Trong các thông tin hoạt động của người dùng được lưu bên trong **Focus time** cũng có các lưu ý khác:

 - Nếu người dùng mở một ứng dụng nào đó lên và đi khỏi đó, thì lúc đó ứng dụng bị treo (AFK) vẫn được ghi nhận trong **Focus time**. Nên khi phân tích, người dùng có thể mở một ứng dụng khá lâu nhưng không có nghĩa là họ tương tác lên đó liên tục.

 - Nếu người dùng click vào một file shortcut, nó sẽ vẫn được ghi lại trong registry mặc dù là có thể file bị crash hoặc bị Windows Antivirus chặn.

 - Hoặc đôi khi là các tiến trình tự động của Windows, như là shell preloading hoặc khi Windows làm mới các shortcut, có thể tạo ra các bản ghi UserAssist mà không cần hoạt động người dùng.

**Forensic interpretation guidance:**
- Khi giá trị của `focus time` khác 0 thì nó là một bằng chứng cho thấy rằng chương trình đã thực sự chạy và cửa sổ chương trình đã hiện trên màn hình người dùng. Và chúng ta có thể kết hợp nó với các artifact khác để có thể xác định chính xác nhất.
  
 - `Amcache`: xác nhận file thực thi (.exe) có tồn tại và đã được hệ thống ghi nhận.

 - `Prefetch`: xác nhận thời gian lần cuối và tần suất mà chương trình được chạy.
    
 - `SRUM`: cung cấp chính giá trị `focus time` và lượng dữ liệu mạng cùng với/CPU đã tiêu thụ.
- Khi `Focus time` = 0 và `Run count` != 0 có thể là 1 trường hợp khá nhạy cảm và dễ gây hiểu lầm.
  
  - Khi `Run count > 0` cho thấy rằng người dùng đã cố gắng mở nó file này lên, hoặc đã có những double click mở nó lên khiến cho số lần chạy trong `UserAssist` hoặc `Prefetch` tăng lên.

  - Khi `Focus time = 0`: Nhưng hệ thống không ghi nhận bất cứ khoảng thời gian nào file đó được "chạy thành công"

 - Nguyên nhân có thể nằm ở việc: file bị **crash ngay sau khi mở**, **bị chặn bởi Antivirus** hoặc là **bị chặn từ UAC** khi không cho phép quyền.


### 2. ShimCache (Application Compatibility Cache)

**ShimCache** là một tính năng của Windows nó được thiết kế để có thể cung cấp những tương thích ngược đối với các ứng dụng hoặc phần mềm đã cũ có thể chạy trong phiên bản mới của hệ điều hành Microsoft Windows. Các thông tin mà ShimCache thu thập được, lưu trữ bên trong memory và được ghi vào disk khi mà hệ thống được khởi động lai hoặc tắt nguồn. Các mục thông thường đều sẽ được thêm vào Cache nếu nó đã được thực thi hoặc đã hiển thị bên trong File Explorer.

**Location of SimCahce**

ShimCache được lưu trữ bên trong SYSTEM hive:

`SYSTEM\CurrentControlSet\Control\Session Manager\AppCompatCache`

**Những dữ liệu được ShimCache thu thập**

<img width="1570" height="608" alt="image" src="https://github.com/user-attachments/assets/ad2521e1-6066-4a42-8358-28b9d62764ca" />

- **Toàn bộ đường dẫn đến với file được thực thi:** Chỉ đến nơi mà file nó nằm trên ổ đĩa.

- **Last modified timestamp**: Lần chỉnh sửa timestamp của file. Nó có thể được sử dung để tạo một timeline các hoạt động khi mà file còn tồn tại trên hệ thống.

- **Số các mục của Cache**:  Vị trí của Cache. Thông thường thì trong mục **AppCompatCache** các đường dẫn đến các file thực thi sẽ được nằm ở bên trong tab `AppCompatCache`, ở đây thì số thứ tự các số càng nhỏ thì tương đương với các file này càng gần đây được sử dụng hơn. Nó có thể giúp xác định được các files mà mình quan tâm.

**ShimCache Artifacts Forensics**

<img width="1858" height="956" alt="image" src="https://github.com/user-attachments/assets/0d3717b3-e488-4fbf-9a5f-16f4224ace4a" />

Ở đây các mục trong artifacts này sẽ được chia theo các mức độ tùy theo vào màu của các ticks bên trái.

   `Màu xanh tương đương với các kiến thức phổ biến của ShimCache mà nhiều người được biết.`

   `Màu vàng là những artifacts có thể dễ gây nhầm lẫn.`

   `Màu đỏ là các artifacts hầu như bị hiểu sai nhiều nhất`

- **1. Cung cấp sự tương thích ngược với các phần mềm cũ hơn được chạy trong phiên bản mới hơn của Windows**. Nó thực hiện việc thêm các thuộc tính cụ thể để có thể thực thi cụ thể các phần mềm hay ứng dụng trên hệ điều hành Windows.

- **2. ShimCache lưu trữ các tên file, đường dẫn và timestamp của các file đã được thực thi sẽ được ghi lại**. **TimeStamp** ở đây tức là thời gian mà files đó **được chỉnh sửa gần đây nhất**, chứ không phải là thời gian mà file được attacker thêm vào hệ thống, hay là thời gian mà chương trình đó được thực thi trong hệ thống. Nó không ghi lại những thông tin trong lịch sử như số lần chạy, người dùng hoặc tham số.

- **3. Windows 7/8/8.1 có một giá trị đó là *execution flag* mà có thể chỉ định nếu một chương trình đã được chạy**. Đó là trong các phiên bản cũ hơn, còn trong Windows 10 chúng ta không thể dùng **ShimCache** để có thể chứng minh rằng là một file hoặc một chương trình nó đã được thực thi trên hệ thống.

- **4. Files được hiển thị trong Windows Explorer có thể quyết định được cái được thêm vào ShimCache**. Giả sử khi bạn tạo ra 10 files `.exe` được đánh số từ file `1.exe` tới `10.exe`. Bạn đặt nó vào hệ thống và điều hướng nó đến 1 thư mục. Lúc này Windows Registry chỉnh sửa kích thước thư mục tối đa là 5 files, thì lúc này ShimCache chỉ có thể chứa 5 files, nhưng nếu bạn chỉnh tối đa là 7 files, thi se có thêm 2 files được thêm vào **ShimCache**, đó gọi là cơ chế **Khoảng cách gần ở vị trí bộ đệm có thể được sử dụng để tìm các tệp khác có thể được đặt cùng vào 1 thời điểm**.

- **5.  Thay đổi tên hoặc điều hướng 1 file di có thể dẫn đến no bị `re-shimmed (tái tạo lại bộ nhớ đệm)`**. Khi chúng ta thực hiện thay đổi tên của 1 file, thì chúng ta không đang chỉnh sửa vào nội dung của nó mà đang chỉnh sửa metadata của file, nên lúc này ShimCache sẽ không ghi nhận sự thay đổi, trong 1 số trường hợp file `text.txt` bị đổi tên thành `text2.txt` nếu nó có cùng 1 timestamp và chính xác thì có thể đó là cùng 1 file.

- **6. ShimCache chỉ ghi nhận tối đa là 1024 entries**. Và có một sự thật ShimCache lưu trữ hoàn toàn 64 bit timestamp, tức là nếu có 2 files có cùng timestamp chính xác với mức độ chi tiết 64 bit giống nhau, thì chắc chắn đó là cùng 1 file với nhau.

- **7. Hầu hết các công cụ thu thập dữ liệu từ ShimCache như [AppCompatCacheParser ](https://github.com/EricZimmerman/AppCompatCacheParser.git) sẽ output ra các dữ liệu được thêm gần đây nhất từ trên top xuống**.

- **8. ShimCache chỉ được ghi vào disk khi reboot hoặc là shutdown**. 


### 3. AmCache (Application Activity Cache)

`Amcache` là một phần của Windows **Application Compatibility Framework (AppCompat)** giúp đảm bảo rằng các chương trình được chạy mượt mà hơn trên hệ thống bởi ghi lại các thông tin về chương trình thực thi .` AmCache` là một artifact chứa và theo dõi các metadata liên quan đến các chương trình được thực thi và được tải xuống trên Windows, đường dẫn tới tệp thực thi, tên tệp, và mã hash của file execution, last modification time. Thực tế thì `ShimCache` và `AmCache` nó có thể được xem là khá tương đồng với nhau về mặt dữ liệu nó lưu trữ: **Các tệp đã được thực thi và tải xuống trên hệ thống**, nhưng đối với `AmCache` thì nó sẽ chứa những dữ liệu chi tiết hơn, về siêu dữ liệu thời gian tệp thực thi, thời gian tệp được tải xuống,...

**Location of AmCache**

`C:\Windows\AppCompat\Programs\Amcache.hve`

<img width="2164" height="1036" alt="image" src="https://github.com/user-attachments/assets/59c63770-31b0-4fce-8dca-67ca87dc1f91" />


**The Amcahce artifacts**:

<img width="1600" height="358" alt="image" src="https://github.com/user-attachments/assets/a3800afe-7635-42bc-b0a9-0372b0587524" />

AmCache là một trong những tính năng vô cùng hữu ích của Windows và chứa chi tiết các artifact có sẳn cho các nhà điều tra trên hệ thống Windows hiện nay. Bên trong nó chứa rất nhiều thông tin siêu dữ liệu về các tệp thực thi và các file Dlls đã tương tác với hệ thống, cùng với việc ghi lại những keys siêu dữ liệu có thể giúp cho các nhà phân tích tạo ra được **timeline** truy xuất ra hoạt động của người dùng. Khác với ShimCache chỉ thu thập các metadata khi một hệ thống đã tắt nguồn, đối với AmCache thu thập dữ liệu trực tiếp khi một file đã được thực thi trên hệ thống, giúp cho AmCache trở nên đáng tin cậy hơn. Các artifact quan trọng:
 - Lưu trữ siêu dữ liệu toàn diện cho `PE - Portable Excecution là một chuẩn format cho thực thi như DLLs, drivers, ".exe" và một số các chương trình khác` files như là file size, SHA1, và header PE info như CompanyName, FileVersion,...
  
 - SHA1 hash của file đó, để đảm bảo tính duy nhất của file, khi ta nghi ngờ nó là một file độc hại, ta có thể kiểm tra những file khác có cùng hash với nó không, nếu có nó có thể được đổi tên để che dấu đi sự chú ý của người điều tra. Hoặc có thể kiểm tra 1 file ngay cả khi nó đã bị xóa.

 - Thời gian lần đầu tiên mà file được thực thi có thể xác định thông qua registry value sau `The Last Write time` được lưu trữ bên trong `AmCache.hve\Root\File{Volume GUID}\key`, đồng thời cũng lưu trữ một giá trị `File Creation Time`, "thời gian tạo file" trên ổ cứng trong một số trường hợp cũng có thể coi là thời gian file dược tải xuống hoàn tất. Còn thực tế thì AmCache không lưu dữ liệu trực tiếp về thời gian file được tải xuống và thực thi, nó chỉ lưu trữ gián tiếp qua 2 giá trị `The last write time` và `File Creation Time`

 - Bằng cách duyệt qua các `Amcache.hve\Root\File{Volume GUID}\key` trong các công cụ như Registry Explorer, chúng ta có thể xác định được ổ đĩa nơi mà file được thực thi từ việc sử dụng Volume GUID được tìm thấy bên dưới `System\MountedDevices`

**Ý nghĩa của các mã hash SHA-1 trong Forensics**

Một trong những tính năng mạnh mẽ và cực kì quan trọng trong quá trình thu thập dữ liệu đó là khả năng ghi lại các mã băm SHA-1 của `AmCache` của các tệp thực thi (executables) và thư viện liên kết động (DLLs). Mã băm là một chuỗi duy nhất, từ việc dùng các thuật toán để băm ra các giá trị từ nội dung của một file, thuật toán SHA-1 tạo ra 1 chuỗi giá trị băm dài 160-bit được dùng để xác minh tính toàn vẹn của file đó. Mã hash SHA-1 được thu thập bởi AmCache có thể được dùng:

- **Xác minh tính toàn vẹn của tệp**: Mã băm SHA-1 cho phép các nhà phân tích thực hiện so sánh **mã băm được thu thập trong AmCache** và **mã băm của chính file nằm trên disk**, để xác minh tính toàn vẹn của file đó.

- **Nhận diện các biến thể mã độc**: Các author của 1 con malware họ thường tạo ra các phiên bản hơi khác nhau của nó, để tránh sự phát hiện của chương trình AntiVirus của Windows:
  
  - Các phiên bản của những con malware có thể khác nhau, kích thước khác nhau, tên khác nhau, thậm chí nội dung trong mã nguồn có thể sửa đổi nhỏ trong mã nguồn, nhưng khi tạo một mã hash thì chúng chỉ có 1 giá trị duy nhất từ nội dung bên trong, có thể xác định rằng chúng là 1.
  - Chúng ta có thể lấy mã hash SHA-1 từ AmCache và tìm kiếm trên các nguồn hoặc cơ sở dữ liệu như (VirusTotal) để xác định chính xác biến thể mã độc và mức độ nghiêm trọng.

- **Đối chiếu chéo giữa các hệ thống**: 1 cuộc tấn công có thể xảy ra trong nhiều hệ thống, việc sử dụng mã hash SHA-1 từ AmCache, giúp những người điều tra có thể tìm kiếm cho các hệ thống khác mà có thể đã gặp phải cùng 1 tệp, mặc dù tên đã được thay đổi hoặc nằm trong 1 thư mục khác. Tệp hash cho phép đội điều tra có thể theo dõi các luồng của 1 malware hoặc phần mềm trái phép trong hệ thống.

- **Corroborating evidence**: Là phần quan trọng nhất chính là sự liên kết các artifact với nhau tạo ra một bằng chứng xác thực hoàn toàn. Lấy ví dụ nếu tìm được 1 tệp bên trong Prefetch biết được thời gian thực thi của file trong đây, Event logs hoặc trong network traffic và mã hash được tìm thấy cũng match với với cái được ghi lại trong AmCache, điều đó chứng minh rằng file đã được thực thi tại cùng thời điểm nó được ghi lại trong cùng các artifact khác. The multi-artifact corroboration tạo nên 1 **timeline** và cung cấp bức tranh toàn cảnh cho người điều tra
   

### 4. BAM/DAM

**Background Activity Monitor (BAM)** sẽ giữ chức năng là theo dõi các hoạt động trong nền của ứng dụng người dùng đang sử dụng hoặc của máy và **Desktop Activity Monitor (DAM)** là một phần của Microsoft Windows giúp tối ưu hóa năng lượng tiêu thụ cho thiết bị.

 - **Background Activity Monitor (BAM)**:
   - lưu trữ đường dẫn đầy đủ đến file được thực thi và thời gian lần gần nhất mà nó được thực thi.
   - Được thiết kế để chạy các hoạt động nền giúp cải thiện tuổi thọ pin và giúp hệ thống hoạt động hiệu quả hơn.
   - Các mục được lưu trong **BAM** sẽ bị xóa sau 7 ngày mà chương trinh đó không hoạt động


 - **Desktop Activity Monitor (DAM)**:
   - Có các chức năng tương tự như BAM nhưng tập chung vào ứng dụng desktop/
   - Chủ yếu được tìm thấy ở các thiết bị sử dụng `Modern Standby`, một tính năng cho phép quản lí năng lượng giúp hạn chế các hoạt động của các ứng dụng trên desktop khi màn hình tắt.
   - Ít xuất hiện trên các PC desktop nhưng vẫn xuất hiện ở vài hệ thống.


**Location of BAM/DAM**

BAM/DAM được lưu trữ bên trong mỗi user:

`SYSTEM\CurrentControlSet\Services\bam\UserSettings\{SID}`

`SYSTEM\CurrentControlSet\Services\dam\UserSettings\{SID}`

<img width="1295" height="350" alt="image" src="https://github.com/user-attachments/assets/853cfc0b-64a1-4a8f-be6a-fa1b88a3b480" />

Mỗi dữ liệu của người dùng được lưu trữ bên trong một **Security Identifer (SID)** duy nhất, nên chúng ta cần phải xác định đúng người dùng cần điều tra, có thể sử dụng lệnh `whoami /user` để xác định SID của người dùng hiện tại đang sử dụng máy và `wmic useraccount get name,sid` để liệt kê tất cả người dùng gồm tên, quyền, sid:

<img width="1200" height="600" alt="image" src="https://github.com/user-attachments/assets/31f18cdf-24d5-435f-8554-4d5616515fa5" />


<img width="1200" height="600" alt="image" src="https://github.com/user-attachments/assets/552c64ff-050e-4656-bb1f-483ea16d89a5" />


**BAM/DAM lưu trữ***

Mỗi BAM/DAM đều chứa:

- **Đường dân đầy đủ của tệp thực thi** - nơi chính xác mà chương trình đã được chạy.

- **Thời gian cuối cùng mà tệp thực thi** - A 64-bit Windows FILETIME timestamp, hiển thị khi mà chương trình chạy lần cuối.

- **Dữ liệu cụ thể - người dùng** - Mỗi mục trong BAM/DAM đều được gắn với người dùng cá nhân, xác định bởi SID của họ

**BAM/DAM aritfact in forensics**

- Mỗi khi người dùng xóa một ứng dụng, BAM có thể vẫn chứa bản ghi của ứng dụng được thực thi trong khoảng 7 ngày.

- Nếu malware đã được chạy trên hệ thống, **BAM/DAM** có thể cung cấp các bằng chứng về **khi nào** nó được thực thi và thực thi **ở đâu**.

- Những người phân tích có thể xác định được chương trình nào mà người dùng nào tương tác với, khi họ sử dụng và liệu có ứng dụng nào trái phép được đã thực thi.

- BAM timestamp có thể thay đổi trong vài phút, dùng dữ liệu BAM tham chiếu chéo `(cross-reference)` BAM với:
  - `Prefetch`: khi nào file được thực thi và số lần nó được thực thi.
  - `UserAssist`: Nó được chạy trong bao lâu, và số lần nó được mở.
  - `ShimCache & AmCache`: mã hash SHA-1 của file thực thi, thời gian lần đầu file được thực thi, lần gần nhất mà file được thi được liệt kê trong Registry Explorer.
 
  **Các hạn chế của BAM/DAM**

  - **Các mục trong BAM/DAM không lưu trữ vĩnh viễn** - nó sẽ bị xóa sau 7 ngày kể từ lần gần nhất nó hoạt động.

  - Nó **không ghi lại các thực thi của USB/Network** - Các chương trình được thực thi từ các `removable drivers` hoặc `network share` sẽ không được logged trong BAM.
 
  - **Timestamp có thể hơi khác** - thời gian thực thi trong `BAM` có thể sẽ hơi khác vài phút với thực tế trong chương trình khởi chạy.
 
  The **BAM & DAM** registry key cung cấp một cách nhanh chóng để theo dõi các ứng dụng đã được thực thi gần đây trên hệ thống Windows. Mặc dù mỗi mục chỉ tồn tại 7 ngày trước khi nó bị xóa vì file không hoạt động, nhưng nó vẫn sẽ cung cấp một cái nhìn sâu sắc và một dấu vết về các hoạt động người dùng, malware infections(nhiễm) và Forensics Investigation.



## External Devices / USB device forensics

Khi thực hiện phân tích pháp y một hệ thống hoặc 1 máy, log các thiết bị USB là một nguồn chứng cứ rất có giá trị. Khi thực hiện giám định, chúng ta cũng cần xác định xem nếu có thiết bị rời nào kết nối vào hệ thống thì USB artifact cung cấp dấu vết cho nhiều hoạt động.

**USB artifact** sẽ cung cấp cho chúng ta:

- Thiết bị nào đã được kết nối vào máy.

- Số serial của thiết bị đó, tên thiết bị và nhà sản xuất của nó

- Timestamp mà nó được kết nối và ngắt kết nổi vào máy tính, tần suất và số lần usb đó được sử dụng trong hệ thống.

- Cung cấp GUID của thiết bị để thực hiện dùng trong so sánh với các artifact khác.

-  Đặc biệt nó còn cung cấp cho chúng ta loại thiệt bị external được kết nối vào máy tính là gì (HID usb, storage usb,..)

  Giả sử, nếu như những thông tin nhạy cảm của một công ty đã bị tuồng ra ngoài từ 1 hệ thống, USB device logs có thể tiết lộ sự hiện diện của 1 thiết bị external storage có thể đã sao chép toàn bộ dữ liệu đó. Hoặc như một con malware đã được nhận biết thông qua một thiết bị USB, thì log của thiết bị kết nối vào hệ thống đó có thể giúp truy vết ra cái nguồn sự lây nhiễm.

  **Location of USB**

- `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Enum\USB` keys lưu trữ tất cả các thông tin về các thiết bị được kết nối qua cổng usb bao gồm: chuột, bàn phím, dây sạc.
   - Quản lí drivers và thông tin nhận dạng phần cứng cấp thấp.
     
   - `VID_xxxx&PID_xxxx`(Vendor ID và Product ID)
     
   - Một số các nội dung:
     - `Device Paramaters`: Chứa các thông tin cấu hình drivers cơ bản
    
     - `Service`: Tên dịch vụ drivers. (ví dụ `usbccgp`: cho thiết bị tổng hợp, `hidusb`: cho bàn phím, chuột,.., `usbtor` cho thiết bị lưu trữ)
    
     - `ClassGUID`: Định danh loại thiết bị (GUID của Human Interface Device - HID,...)
    
     - `ContainerID`: ID duy nhất để nhóm các chức năng của cùng một thiết bị vật lý lại với nhau.
    
- `SYSTEM\CurrentControlSet\Enum\USBSTOR` keys này chứa các thông tin cho các thiết bị thuộc [Mass Storage Device (MSC](https://thietbinas.com/mass-storage-la-gi). Chứa các thông tin chi tiết hơ để hệ điều hành nhận biết thiết bị đó là một ổ đĩa.
  - Quản lý các thiết bị lưu trữ (USB Flash, ổ cứng ngoài).
 
  - `Disk&Ven_xxxx&Prod_xxxx`
 
  - Một số nội dung bên trong:
    - `FriendlyName`: tên dễ đọc cho thiết bị đó.
   
    - `SerialNumber`: số sê ri duy nhất của thiết bị.
   
    - `ParentIdPrefix`: Một chuỗi ID được dùng để liên kết với các artifact khác trong registry.
   
**First/Last time connect/disconnect**

`SYSTEM\CurrentControlSet\Enum\USBSTOR\Ven_Prod_Version\USBSerial#\Properties\{83da6326-97a6-4088-9453-a19231573b29}\####` với mỗi thiết bị usb sẽ chứa subkey `xxxx` chứa thời gian khác nhau

|Value | information |
| --- | --- |
| 0064 | first connected |
| 0066 | last connected |
| 0067 | last time removed |

<img width="915" height="119" alt="image" src="https://github.com/user-attachments/assets/44ead5bb-b5ad-4fe3-a7ef-bd6c8711ec2c" />

Lần đầu tiên kết nối: 2022-06-15 05:44:05

<img width="909" height="111" alt="image" src="https://github.com/user-attachments/assets/af8873bd-8246-488f-a979-ba02d4fb7d5a" />

Lần cuối cùng kết nối:  2022-06-16 05:44:05

<img width="818" height="127" alt="image" src="https://github.com/user-attachments/assets/4755fbb7-5952-4275-9513-44f6f6080a20" />

Lần cuối cùng bị rút ra:  2022-06-16 05-49-02

**USB device Volume Name**

Bên trong keys `MountDevices`, bạn có thể lấy được tên ổ đĩa đó:

`HKLM\SYSTEM\MountedDevices`:

<img width="1389" height="275" alt="image" src="https://github.com/user-attachments/assets/fffe323a-315b-4ea0-b52b-3067b430ff05" />

Chúng ta có thể dựa vào đây để biết được thiết bị usb đó liên kết với ổ đĩa nào, và tìm được serial number, (ví dụ: thiết bị `usb`: USB key JetFlash Transcend 16GDB&Rev_100 & `số seri`:"37DXYQWK7W33HB5M")

`HKLM\SOFTWARE\Microsoft\Windows Portable Devices\Devices` Vào keys này để xác định chắc chắn lại thiết bị và ổ đĩa.

<img width="1604" height="621" alt="image" src="https://github.com/user-attachments/assets/e5f814b5-cd73-47f2-b7dc-6c30e78fd980" />

---

# Common Artifact in Windows 

<img width="838" height="484" alt="image" src="https://github.com/user-attachments/assets/3f9ca032-a160-4952-90c5-623daa8eb3b5" />

## Event logs

Trong hệ điều hành Windows, the event log lưu trữ rất nhiều những thông tin hữu ích về system, users, activity và application. Mục đích chính của event logs đó chính là cung cấp các thông tin cho người dùng quản trị và người dùng về thông báo các lỗi hệ thống, các đăng nhập thành công, thất bại, thiết bị nào được kết nối, users nào đã đăng nhập,...  Cấu trúc của event logs gồm 5 cấp độ (infomation, warning, error, critical and success/failure audit). Trong phân tích pháp y, thì các nguồn thông tin này có giá trị vô cùng lớn, trong bối cảnh của một cuộc tấn công.

### Location/Type of event logs

`C:\Windows\​System32\​winevt\​Logs` . Các file `evtx` là các file chứa các logs. Trong Windows thì có các logs chính là:
  1. **System logs**: theo dõi và ghi lại các sự kiện liên quan đến các phân đoạn của hệ điều hành. Nó bao gồm các thông tin về thay đổi phần cứng, device drivers, thay đổi hệ thống và các hoạt động khác liên quan đến hệ thống và thiết bị.

  2. **Security logs**: Ghi lại các sự kiện kết nối tới việc đăng nhập và đăng xuất trên thiết bị. Chính sách kiểm toán của hệ thống cho sự kiện cụ thể. Logs security là 1 nguồn rất có giá trị cho những người phân tích điều tra về các hoạt động trái phép trong hệ thống.

  3. **Application logs**: Ghi lại các sự kiện liên quan đến các ứng dụng được tải xuống trên hệ thống, các thông tin về các ứng dụng bị lỗi, các lỗi trước được ghi nhận trước khi sập hệ thống.

  4. **Directory Service Events**: Các thay đổi trong Active Directory và các hoạt động được ghi lại trong logs, chủ yếu nằm trên Domain controller.

  5. **DNS Event Logs**: DNS servers sử dụng logs này để ghi lại các sự kiện trong miền.

Thêm vào đó trong một số logs sẽ có thêm mức độ của từng sự kiện, đi sâu vào đó:

|Event type | Level ID  | Description |
| --- | --- | --- |
| Error | 40 |  Sự kiện chỉ ra có vấn đề như là mất dữ liệu hoặc mất đi các chức năng. Ví dụ: Một dịch vụ thất bại để loads sau khi khởi động xong |
| Warning | 50 | Sự kiện cung cấp các vấn đề có thể xảy ra, mặc dù nó không response là 1 lỗi thực tế, warning chỉ ra có 1 thành phần hoặc ứng dụng không ở trạng thái lý tưởng và có thể sẽ xảy ra lỗi nghiêm trọng ở hành động tiếp theo |
| Infomation | 80 | Sự kiện được mô tả là đã hoạt động thành công của một ứng dụng, drivers hoặc dịch vụ. |
| Critical | 30 | Sự kiện đòi hỏi cần tập chung vào nó ngay lập tức của quản trị viên hệ thống. Chúng thường ảnh hưởng đến toàn bộ hệ thống hoặc ứng dụng. Cũng có thể là chỉ ra một ứng dụng hoặc hệ thống đã không còn phản hồi.
| Success Audit | not | Sự kiện ghi lại các kiểm tra bảo mật được truy cập đã thành công. Ví dụ như khi một người dùng đăng nhập thành công.|
| Failure Audit | not | Sự kiện ghi lại các kiểm tra bảo mật được truy cập đã không thành công.|

### Event id
Trong phân tích các log trong event log, nó sẽ có các event id dùng để mô tả rằng sự kiện đó biểu thị cho hành động như thế nào trong hệ thống. Nó giúp cho chúng ta xác định và lọc ra các sự kiện đơn giản hơn.

| Event ID | Event Description |
| --- | --- |
| 1006 | Antimalware engine tìm thấy malware hoặc có thêm [Pottentially Unwanted Program (PUP)](https://www.kaspersky.com/resource-center/definitions/what-is-pup-pua)||
| 1007 | Nền tảng antimalware thực hiện hành động bảo vệ hệ thống từ malware hoặc potentially unwanted program (PUP) |
| 1015 | Nền tảng antimalware đã phát hiện ra các hành vi đáng nghi |
| 1016 | Nền tảng antimalware xác định được malware hoặc **PUP** |
| 1017 | Nền tảng antimalware thực hiện hành động bảo vệ hệ thống từ malware hoặc **PUP**|
| 1100 | Dịch vụ ghi nhật kí sự kiện đã ngừng hoạt động | 
| 1102 | Nhật kí kiểm tra đã bị xóa |
| 4624 | Một tài khoảng vừa được đăng nhập thành công |
| 4625 | Một tài khoảng đã đăng nhập thất bại |
| 4634 | Một tài khoảng vừa đăng xuất |
| 4648 | Một người dùng đang cố gắng chạy 1 ứng dụng chương trình với đặc quyền "RUNAS" |
| 4620 | Một tài khoảng người dùng vừa được tạo thành công |
| 4722 | Một tài khoảng đươc bật thành công |
| 4723 | Một nổ lực để thay đổi mật khẩu 1 tài khoảng |
| 4724 | Một nổ lực để reset mật khẩu |

### Prefetch

Prefetch là 1 file được tạo ra từ Windows mỗi khi một ứng dụng được chạy từ 1 vị trị cụ thể trong máy lần đầu tiên, nó giúp Windows có thể tối ưu hiệu năng khi startup và hiệu suất của hệ thống. Prefetch là một artifact rất giá trị cho quá trình phân tích ứng dụng, nó cung cấp các dữ liệu về lịch sử những ứng dụng đã được chạy trên hệ thống.

**Location of Prefetch**

`C:\Windows\Prefetch\*.pf`

<img width="1344" height="812" alt="image" src="https://github.com/user-attachments/assets/068e6cdd-6252-4ece-8eef-f2669f4fb273" />

**Artifacts of Prefetch file**

Prefetch chứa những dữ liệu như:
 - **File name**: tên của file đã thực thi.

 - **Timestamp**: Các thông tin về thời gian mà file được thực thi.

 - **Run count**: Số lần mà tệp thực thi đã được chạy.

 - **File and Directory path**: Chứa các chi tiết về file và đường dẫn đã được truy cập tới tệp thực thi.

Khi một chương trình đã bị xóa,`prefetch file` có thể vẫn sẽ tồn tại trên hệ thống để cung cấp các chứng cứ về sự thực thi đó.

`Prefetch file` chứa các chi tiết về số lần mà file được chạy được chạy, chi tiết về ổ đĩa, cả về các thông tin chi tiết của timestamp khi mà lần đầu và lần cuối nó được chạy. Trong phiên bản Windows 8+, thì trong prefetch chứa tối đa 8 timestamp khi ứng dụng được chạy lần đầu tiên.

Vị trí của nơi một file được thực thi cũng rất quan trọng. Khi 1 tiến trình của hệ thống Windows hợp lệ nó sẽ chạy trong các nơi như `%SYSTEM32%` hoặc là `C:\Program File`. Trong quá trình tấn công malware, kẻ tấn công nếu không leo quyền thì sẽ không thể đặt nó trong các thư mục hệ thống đó được, nên sẽ đặt ở các file `temp` tạm, đây là manh mối rất quan trọng để nhận biết 1 file đáng nghi đặt tên giả dạng thành file chương trình hệ thống. Trong `Prefetch` nó có lưu đường dẫn của mỗi nơi file được thực thi.


<img width="1006" height="493" alt="image" src="https://github.com/user-attachments/assets/c5903883-0a24-4b8a-9f2e-a6be9fc9212c" />

**Tools for Prefetch**

Eric Zicmerman có phát triển 1 công cụ `Prefetch Parse` [PECmd.exe](https://download.ericzimmermanstools.com/net9/PECmd.zip) để có thể phân tích các `Prefetch` file và trích xuất dữ liệu.
```
t0b1ra@tobiraNduy:/mnt/d/Eric-Zic_tools/PECmd$ ./PECmd.exe -h
Description:
  PECmd version 1.5.1.0

  Author: Eric Zimmerman (saericzimmerman@gmail.com)
  https://github.com/EricZimmerman/PECmd

  Examples: PECmd.exe -f "C:\Temp\CALC.EXE-3FBEF7FD.pf"
            PECmd.exe -f "C:\Temp\CALC.EXE-3FBEF7FD.pf" --json "D:\jsonOutput"
            PECmd.exe -d "C:\Temp" -k "system32, fonts"
            PECmd.exe -d "C:\Temp" --csv "c:\temp" --csvf foo.csv --json c:\temp\json
            PECmd.exe -d "C:\Windows\Prefetch"

            Short options (single letter) are prefixed with a single dash. Long commands are prefixed with two dashes

Usage:
  PECmd [options]

Options:
  -f <f>           File to process. Either this or -d is required
  -d <d>           Directory to recursively process. Either this or -f is required
  -k <k>           Comma separated list of keywords to highlight in output. By default, 'temp' and 'tmp' are
                   highlighted. Any additional keywords will be added to these
  -o <o>           When specified, save prefetch file bytes to the given path. Useful to look at decompressed Win10
                   files
  -q               Do not dump full details about each file processed. Speeds up processing when using --json or --csv
                   [default: False]
  --json <json>    Directory to save JSON formatted results to. Be sure to include the full path in double quotes
  --jsonf <jsonf>  File name to save JSON formatted results to. When present, overrides default name
  --csv <csv>      Directory to save CSV formatted results to. Be sure to include the full path in double quotes
  --csvf <csvf>    File name to save CSV formatted results to. When present, overrides default name
  --html <html>    Directory to save xhtml formatted results to. Be sure to include the full path in double quotes
  --dt <dt>        The custom date/time format to use when displaying time stamps. See https://goo.gl/CNVq0k for
                   options [default: yyyy-MM-dd HH:mm:ss]
  --mp             When true, display higher precision for timestamps [default: False]
  --vss            Process all Volume Shadow Copies that exist on drive specified by -f or -d [default: False]
  --dedupe         Deduplicate -f or -d & VSCs based on SHA-1. First file found wins [default: False]
  --debug          Show debug information during processing [default: False]
  --trace          Show trace information during processing [default: False]
  --version        Show version information
  -?, -h, --help   Show help and usage information

```
Để phân tích 1 file `.pf` và nó vào 1 file `.csv` ta dùng lệnh:

`PECmd.exe -f <path-to-Prefetch-files> --csv <path-to-save-csv>`

Để phân tích cả 1 folder chứa các file `.pf` thì ta dùng lệnh:

`PECmd.exe -d <path-to-Prefetch-directory> --csv <path-to-save-csv>`

### File LNK

Files `.lnk` là artifact khá quan trọng trong quá trình giám định pháp y đối với một hệ thống. Shortcut files liên kết với các ứng dụng hoặc các file thông thường được tìm thấy ở mục desktop của user hoặc trên toàn hệ thống, thường là các file có phần extention file là `.lnk`. File `.LNK` có thể được tạo bởi người dùng và cũng có thể được và cũng có thể được tạo tự động từ hệ điều hành Microsoft Windows. Mỗi file có những giá trị riêng và ý nghĩa của nó. Windows tạo ra các file `.lnk` này mục đích là cho sự tiện lợi người dùng có thể truy cập nhanh chóng tới các file mình thường xuyên sử dụng, và cũng là một artifact giá trị trong quá trình phân tích các hoạt động đáng nghi.

**Location of LNK file**

- `C:\Users\%USERNAME%\Recent`

- `C:\Users\%USERNAME%\AppData\Roaming\Microsoft\Windows\Recent`

- `C:\Users\%USERNAME%\Roaming\Office\Recent`

- `C:\Users\%USERNAME%\Desktop`


**LNK artifact in Windows Forensics**

LNK file giúp cho các nhà phân tích có thể tìm kiếm các file không còn tồn tại trên hệ thống mà họ đang kiểm tra. Các tệp có thể đã bị xóa, hay được lưu trữ trên USB hoặc mạng chia sẽ , mặc dù tệp có thể không còn tồn tại ở đó nhưng tệp gốc của nó vẫn tồn tại và trỏ đến file `.lnk` đó, và nó thường sẽ được lưu trữ bên trong thư mục `%AppData%\Microsoft\Windows\Recent`, giúp cho nó trở thành 1 bằng chứng cho thấy rằng file này đã từng tồn tại trên hệ thống, mặc dù đã bị xóa, di chuyển đi. 

LNK file thông thường chứa các thông tin:

- Đường dẫn gốc của một file.

- Timestamp của file gốc, không chỉ là khoảng thời gian cho file `.lnk` mà còn là mốc thời gian cho file gốc của nó, như thời gian file được tạo, thời gian sửa đổi, thời gian truy cập cuối cùng nằm trong siêu dữ liệu của chính nó.
> Ở đây có 1 cách gọi cho 3 mốc thời gian chính thường rất quan trọng là `Created time (C)`, `Modified time (M)`, `Accessed time (A)` có thể nói tắt là `MAC time` 

- Thông tin về ổ đĩa và hệ thống nơi mà file `lnk` đó được lưu trữ. Nó bao gồm tên ổ đĩa, số sê-ri, tên NetBIOS, và địa chỉ MAC của host nơi mà liên kết được lưu trữ.

- Thông tin chi tiết về mạng nếu nó được lưu trữ bên trên `network share` hoặc `remote computer`.

- Kích thước của file được liên kết.

**Analyzed lnk artifact**

Có một công cụ dùng để phân tích các file `lnk` được phát triển bởi **Eric Zimmerman** gọi là [LECmd](https://github.com/EricZimmerman/LECmd). Chúng ta có thể sử dụng công cụ này để trích xuất đường dẫn đầy đủ của file gốc, MAC time, các metadata khác của file lnk gốc và file lnk.

```
t0b1ra@tobiraNduy:/mnt/d/Eric-Zic_tools/LECmd$ ./LECmd.exe -h
Description:
  LECmd version 1.5.1.0

  Author: Eric Zimmerman (saericzimmerman@gmail.com)
  https://github.com/EricZimmerman/LECmd

  Examples: LECmd.exe -f "C:\Temp\foobar.lnk"
            LECmd.exe -f "C:\Temp\somelink.lnk" --json "D:\jsonOutput" --pretty
            LECmd.exe -d "C:\Temp" --csv "c:\temp" --html c:\temp --xml c:\temp\xml -q
            LECmd.exe -f "C:\Temp\some other link.lnk" --nid --neb
            LECmd.exe -d "C:\Temp" --all

            Short options (single letter) are prefixed with a single dash. Long commands are prefixed with two dashes


Usage:
  LECmd [options]

Options:
  -f <f>          File to process. Either this or -d is required
  -d <d>          Directory to recursively process. Either this or -f is required
  -r              Only process lnk files pointing to removable drives [default: False]
  -q              Only show the filename being processed vs all output. Useful to speed up exporting to json and/or csv
                  [default: False]
  --all           Process all files in directory vs. only files matching *.lnk [default: False]
  --csv <csv>     Directory to save CSV formatted results to. Be sure to include the full path in double quotes
  --csvf <csvf>   File name to save CSV formatted results to. When present, overrides default name
  --xml <xml>     Directory to save XML formatted results to. Be sure to include the full path in double quotes
  --html <html>   Directory to save xhtml formatted results to. Be sure to include the full path in double quotes
  --json <json>   Directory to save json representation to. Use --pretty for a more human readable layout
  --pretty        When exporting to json, use a more human readable layout [default: False]
  --nid           Suppress Target ID list details from being displayed [default: False]
  --neb           Suppress Extra blocks information from being displayed [default: False]
  --dt <dt>       The custom date/time format to use when displaying time stamps. See https://goo.gl/CNVq0k for options
                  [default: yyyy-MM-dd HH:mm:ss]
  --mp            Display higher precision for time stamps [default: False]
  --debug         Show debug information during processing [default: False]
  --trace         Show trace information during processing [default: False]
  --cp <cp>       Code page to parse strings [default: 1252]
  --version       Show version information
  -?, -h, --help  Show help and usage information


t0b1ra@tobiraNduy:/mnt/d/Eric-Zic_tools/LECmd$
```
Để phân tích 1 file `.lnk` và nó vào 1 file `.csv` ta dùng lệnh:

`LECmd.exe -f <path-to-Prefetch-files> --csv <path-to-save-csv>`

Để phân tích cả 1 folder chứa các file `.lnk` thì ta dùng lệnh:

`LECmd.exe -d <path-to-Prefetch-directory> --csv <path-to-save-csv>`

### OST/PST file

Cả 2 đều là định dạng tệp tin cơ sở dữ liệu được Microsoft Outlook sử dụng để lưu trữ email, danh bạ, lịch, tác vụ và các dữ liệu khác cụ bộ trên máy tính. Tuy nhiên , mục đích sử dụng và cơ chế hoạt động nó khác nhau.

|       | OST (.ost) Office Storage Table | PST (.pst) Personal Storage Table |
| ---   | --- | --- |
| Chức năng | Được sử dụng cho các tài khoảng `IMAP`, `Microsoft 365`. Nó đóng vai trò là một bản sao lưu bộ đệm (cache) cục bộ của dữ liệu trên server | Được sử dụng chủ yếu cho các tài khoản email POP3( nơi email được tải về máy tính cục bộ và bị xóa hoàn toàn khỏi server) hoặc dùng để lưu trữ và sao lưu dữ liệu thủ công |
| Đặc điểm | Tệp OST được gắn chặt với cấu hình phần cứng và tài khoản Outlook cụ thể đã tạo ra nó. Không thể sao chép tệp `.ost` từ máy này sang máy khác. | Tệp `.pst` hoạt động độc lập Có thể sao chép từ máy này sang máy khác và mở được bằng Outlook |
| Vị trí lưu trữ | `C:\Users\[User]\AppData\Local\Microsoft\Outlook` | `C:\Users\[User]\Documents\Outlook Files` - `C:\Users\[User]\AppData\Local\Microsoft\Outlook`|

**Artifact OST/PST file**

- **Email header**
  - Xác định địa chỉ IP nguồn (Sender IP) để truy vết.
 
  - Phân tích lộ trình email (Received lines) để phát hiện giả mạo (spoofing).
 
  - Thông tin về Message ID và thời gian gửi/nhận thực tế.
 
- **Nội dung Email**: Chứa nội dung của email.

- **Tệp đính kèm**: Có thể là đường dẫn, chứa mã độc cho các cuộc tấn công phishing, các tệp có thể chạy ngay sau khi mở (.docm, .xlsm, .pptm).

- **Metadata**:
  - `Timestamp`: thời gian được tạo, thời gian sửa đổi, thời gian gửi/nhận.
 
  - `Status`: Trạng thái của file.
 
 Công cụ thường sử dụng để xem các file `.ost` hoặc `.pst`: [Kernel OST Viewer](https://www.nucleustechnologies.com/ost-viewer.html).

 <img width="3623" height="2023" alt="image" src="https://github.com/user-attachments/assets/fe023557-065f-4e5c-9bc1-153e5b72ed0f" />

 ### EML file

 File EML thực chất là một file văn bản thuần túy (Plain Text) tuân theo chuẩn MIME. Các file `.eml` có thể mở bằng bất cứ công cụ nào như là `notepad` hoặc là `Text Editor`.

 #### Artifact in EML file

 - **Header Artifact**:
   - `Recevied`: Cho biết lộ trình email đi qua các Mail Server. Ip server của kẻ tấn công( hoặc người gửi) nằm ở bên dưới của file.
  
   - `Return-Path`: Địa chỉ email thực sự sẽ nhận thông báo lỗi nếu gửi thất bại, giúp xác nhận nếu email được gửi thất bại
  
   - `Message-id`: Mã định danh duy nhất của email. 
  
   - `X-Mailer / User-Agent`: Cho chúng ta biết ứng dụng gửi mail là gì ví dụ (Outlook, Thunderbird,..)
  
 - **Body Artifact**:
   - `URLs/Links`: Kẻ tấn công thường che giấu link độc hại bằng HTML.
  
   - `HTLM Obfustication`: Mã HTLM bị làm rối, chèn các kí tự khó đọc, để có thể che giấu các hành vi đáng nghi.
  
 - **Attachment Artifacts**
   - Trong 1 file `.eml` thì các tệp đính kèm này chính là khối dữ liệu `base64` ở cuối file.

