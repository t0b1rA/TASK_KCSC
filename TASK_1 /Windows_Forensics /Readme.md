# Windows Registry 
Windows Registry là một cơ sở dữ liệu phân tầng lưu trữ những cài đặt cấp thấp của hệ điều hành Microsoft Windows và các ứng dụng chọn sử dụng registry, được sử dụng từ phiên bản Windows 95 cho tới hiện nay.Trước phiên bản Windows 95, thì Windows sẽ lưu trữ các thông tin cấu hình bên trong các file (`.ini`).The registry hỗ trợ truy xuất tốc độ cao cho nhân hệ điều hành(Kernel), các thiết bị drivers, dịch vụ, Security Account Manager (SAM), và ứng dụng người dùng. Windows Registry hay là The registry chứa những thông tin, cài đặt, tùy chọn và các giá trị khác của chương trình và phần cứng được tải xuống của tất cả các phiên bản của Microsoft Windows. Ví dụ: một chương trình được tải xuống thì nó sẽ tạo ra một subkey mới và cái khóa này sẽ chứa các thông tin về vị trí lưu trữ của chương trình này, phiên bản của chương trình, cách mà chương trình hoạt động,.. tất cả sẽ nằm trong Windows Registry.

Lý do mà Windows sử dụng registry là bởi vì trước đó khi các thông tin cấu hình được lưu trữ trong các file `.ini` thì không chỉ người dùng có thể dễ dàng vô tình xóa đi những file này mà không thể khôi phục lại, còn là việc nó thiếu đi các cấu trúc chuẩn hóa. Windows registry tập trung và chuẩn hóa việc lưu trữ các cấu hình, cấu trúc chuẩn hóa của windows registry chính là dạng cây phân cấp: Root -> Keys -> Subkeys -> Value, việc này giúp cho nó khó có thể vô tình bị xóa đi, có thể sao lưu và khôi phục mà còn được Windows bảo vệ khỏi các cuộc tấn công ( bằng tính năng của Windows - Windows Security).
### 2. Structure of the Registry Key
The registry chứa hai thành phần cơ bản là key và value. Registry keys là đối tượng có thể chứa giống như một folder, Registry value là một đối tượng không thể chứa giống như một file. Keys có thể chứa các subkey và value bên trong. Các khóa được tham chiếu với cú pháp tương tự như tên đường dẫn của Windows, sử dụng giấu gạch chéo ngược. Cấu trúc của Windows Registry bao gồm 5 khóa gốc chính, bê dưới root key `Computer`:
- **HKEY_CURRENT_USER (HKCU)**
- **HKEY_USERS (HKU)**
- **HKEY_LOCAL_MACHINE (HKLM)** 
- **HKEY_CLASSES_ROOT (HKCR)**
- **HKEY_CURRENT_CONFIG (HKCC)**
Registry Value là các giá trị dữ liệu cụ thể nhỏ nhất được lưu trữ bên trong Windows Registry, nó có thể chứa các cấu hình cài đặt chi tiết cho hệ điều hành, phần cứng, phần mềm.
Một số registry value chính là:
- **REG_SZ(chuỗi đơn)**: giá trị văn bản đơn giản, có một dòng.
- **REG_EXPAND_SZ (chuỗi mở rộng)**: Giá trị chuỗi "có thể mở rộng" có thể chứa các biến môi trường, thường được lưu trữ và hiển thị trong `UTF-16LE`, thường được kết thúc bằng ký tự NUL
- **REG_MULTI_SZ (chuỗi nhiều dòng)**: Giá trị nhiều chuỗi, là danh sách có thứ tự các chuỗi không trống, thường được lưu trữ và hiển thị bằng Unicode, mỗi chuỗi được kết thúc bằng ký tự null, danh sách thường được kết thúc bằng ký tự null thứ hai.
- **REG_DWORD (số nguyên 32 bit)**: thường dùng cho các giá trị boolean (0 cho false - 1 cho true).
- **REG_QWORD (số nguyên 64 bit)**: một số nguyên 64 bit (có thể là endian lớn hoặc endian nhỏ hoặc không xác định.
- **REG_BINARY (dữ liệu nhị phân)**: các giá trị 0 hoặc 1, dùng cho cài đặt không phải văn bản hoặc số như màu sắc, biểu tượng.

Để xem được những keys này chúng ta có thể sử dụng tiện ích `regedit.exe`. Để mở registry editor, nhấn Windows R , rồi nhập `regedit.exe`.
Bây giờ chúng ta sẽ tìm hiểu sâu hơn về phần ý nghĩa của từng keys trên sẽ đảm nhận cho cái gì.
- **HKEY_CURRENT_USER (HKCU)**: Chứa những thông tin cấu hình gốc rể cho người dùng hiện đang đăng nhập. Folder của người dùng, cài đặt control panel được lưu trữ ở đây. Những thông tin này thường liên quan đến hồ sơ người dùng.
- **HKEY_USERS (HKU)**: Chứa tất cả những thông tin cấu hình người dùng cụ thể cho tất cả những người dùng đang đăng nhập, và những người khác đã đăng nhập, hay nói cách khác là toàn bộ hồ sơ của những người dùng đã từng đăng nhập trên máy tính đó. **HKCU** là một subkey của **HKU**, vì sao nói vậy? Bởi vì **HKCU** là một nhánh nhỏ là những hồ sơ của người dùng đang hoạt động hiện tại trên máy tính.
- **HKEY_LOCAL_MACHINE (HKLM)**: Chứa những thông tin cấu hình từng phần cho máy tính.
- **HKEY_CLASSES_ROOT (HKCR)**: Nó là một subkey của **HKLM\SoftWare**. Những thông tin được lưu trữ ở đây đảm bảo các chương trình được mở đúng khi bạn mở một file bằng Windows Explorers. Chứa những thông tin quan trọng cho liên kết các tập tin với các ứng dụng và quản lí COM(Component Object Model), thiết yếu để nói với Windows rằng là cần làm gì với file đó.
- **HKEY_CURRENT_CONFIG (HKCC)**: Chứa những thông tin về hồ sơ phần cứng được sử dụng trong máy tính cục bộ khi thiết bị được mở lên.

### 3. Accessing registry hives offilne
Vị trí của các keys trong một máy Windows:
- **DEFAULT** (mounted on `HKEY_USERS\DEFAULT`)
- **SAM** (mounted on `HKEY_LOCAL_MACHINE\SAM`)
- **SECURITY** (mounted on `HKEY_LOCAL_MACHINE\Security`)
- **SOFTWARE** (mounted on `HKEY_LOCAL_MACHINE\Software`)
- **SYSTEM** (mounted on `HKEY_LOCAL_MACHINE\SYSTEM`).
