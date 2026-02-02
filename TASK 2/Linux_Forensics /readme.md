# Chức năng của các lệnh linux cơ bản

### Lệnh ls Listings file and Directory in Linux

Lệnh `ls` giúp liệt kê ra các file và thư mục tại vị trí thư mục hiện tại mà chúng ta đứng, hoặc có thể chỉ định đến một thư mục khác cần được liệt kê

<img width="1033" height="440" alt="image" src="https://github.com/user-attachments/assets/1c569f18-2845-4bb7-89a9-2b65f0a4bba1" />

Đây là một ví dụ cơ bản của `ls`, chúng ta liệt kê ra các thư mục và file tại vị trí mà chúng ta hiện tại đang đứng trong `terminal`. Hoặc chúng ta cũng có thể liệt kê ra được các file và thư mục tại 1 thư mục khác mà chúng ta chỉ định đến bằng lệnh `ls <ten_thu_muc>`, như ví dụ sau:

```
┌──(nhduydeptrai㉿tobi)-[~]
└─$ ls Challenge2 
base64.txt  encode_payload.py  get_modulus.py  InfectedProcess.dmp  malware.exe  payload.txt  Traffic.pcapng

```

### Lệnh cd - Change Directory

Lệnh này có thể được sử dụng cho Windows Command Prompt và cả Linux Terminal, nó giúp cho chúng ta có thể di chuyển từ thư mục đang làm việc hiện tại, đến mốt thư mục khác bằng cách cung cấp cho lệnh `cd` một đường dẫn cụ thể.

- Ví dụ cơ bản nhất cho lệnh `cd` này là: `cd /usr/share/wordlists/` giúp cho người dùng di chuyển đến thư mục `wordlists` trong Linux:
  - Có 1 lưu ý khác là khi sử dụng lệnh `cd`:

    <img width="1114" height="497" alt="image" src="https://github.com/user-attachments/assets/b469ad42-7dd9-488f-8e05-ea989026c0ac" />

    - Khi chúng ta đang di chuyển đến 1 thư mục mà hiện tại nó đang xuất hiện trong thư mục chúng ta đang đứng, thì chúng ta có thể `cd <ten_thu_muc>` để di chuyển ngay tới. Lấy ví dụ như trong hình, mình đang đứng ở ngay thư mục `/home/kali/` và trong thư mục `/home/kali/` có thư mục `Scarlet_CTF`, thì mình có thể đi vào thư mục đó trực tiếp.

    - Nhưng giả sử mình muốn đi tới 1 thư mục khác không nằm trong thư mục `/home/kali/` thì chúng ta không thể nhập mỗi tên thư mục đó ra được, mà phải nhập cả đường dẫn từ gốc để đến được thư mục đó:
   
    <img width="1135" height="589" alt="image" src="https://github.com/user-attachments/assets/4a21bfbc-6147-40a6-a4cf-84a04fd83749" />

    - Như ở đây khi mà mình muốn di chuyển đến thư mục `./VSL_ctf_2026/` thì chúng ta không thể nhập mỗi tên vì nó không nằm trong `/home/kali/`, chúng ta cần nhập đầy đủ đường dẫn của nó.
    
    ```
        ┌──(nhduydeptrai㉿tobi)-[~]
    └─$ cd /mnt/hgfs/kali_linux_real_machine/CTF/VSL_ctf_2026/           
                                                                                                                                                       
    ┌──(nhduydeptrai㉿tobi)-[/mnt/hgfs/kali_linux_real_machine/CTF/VSL_ctf_2026]
    └─$ ls                                       
     accindent   challenge   challenge.zip  'Data stole'   float   notagia
    ```

    - Ngoài ra thì chúng ta cũng có thể di chuyển lùi về thư mục cha của thư mục hiện tại chúng ta đang làm việc bằng lệnh `cd ..`

    ```
    ┌──(nhduydeptrai㉿tobi)-[/mnt/hgfs/kali_linux_real_machine/CTF/VSL_ctf_2026]
    └─$ cd ..                                                 
                                                                                                                                                 
    ┌──(nhduydeptrai㉿tobi)-[/mnt/hgfs/kali_linux_real_machine/CTF]
    └─$ 
    ```

    Hoặc có thể lùi về thư mục gốc ban đầu khi chưa điều hướng tới bất cứ thư mục nào bằng lệnh `cd` thôi
    ```                                                                                                                                                 
    ┌──(nhduydeptrai㉿tobi)-[/mnt/hgfs/kali_linux_real_machine/CTF]
    └─$ cd   
                                                                                                                                                 
    ┌──(nhduydeptrai㉿tobi)-[~]
    └─$ 
    ```
  - Ngoài ra có 1 số option khác có thể ít được sử dụng hơn:
    - `cd /` : Điều hướng người dùng đến với thư mục root trong Kali linux và trở về ổ đĩa hiện tại được chọn trong Windows. Lệnh `cd ~` giúp cho người dùng quay trở về lại thư mục home ban đầu hoặc có thể sử dụng lệnh `cd` 
     
    Linux
    ```                                                                                                                                             
    ┌──(nhduydeptrai㉿tobi)-[~]
    └─$ cd /                                                  
                                                                                                                                              
    ┌──(nhduydeptrai㉿tobi)-[/]
    └─$ ls
    bin   core.403978  etc   initrd.img      lib    lib64       media  opt   root  sbin  srv   sys  usr  vmlinuz
    boot  dev          home  initrd.img.old  lib32  lost+found  mnt    proc  run   snap  swap  tmp  var  vmlinuz.old
    
    ```
    
    Windows
    ```
    PS C:\Users\LOQ> cd /
    PS C:\> ls 
    Directory: C:\
    Mode                 LastWriteTime         Length Name
    ----                 -------------         ------ ----
    d-----        08/12/2025     13:03                $WINDOWS.~BT
    d-----        22/11/2025     07:13                Dev-Cpp
    d-----        09/07/2025     05:05                Drivers
    d-----        08/12/2025     13:26                ESD
    d-----        11/11/2025     01:57                inetpub
    d-----        11/11/2025     21:52                New folder
    d-----        01/12/2025     13:31                ProcLogs
    d-----        23/01/2026     08:43                Program Files
    d-r---        23/01/2026     08:42                Program Files (x86)
    d-----        23/01/2026     08:38                SQL2025
    d-r---        27/11/2025     20:09                Users
    da----        22/01/2026     09:27                Windows
    -a----        04/12/2025     23:40          12288 DumpStack.log
    
    ```

### Lệnh ps (Proccess Status)

Lệnh `ps` cung cấp cho người dùng một bản snapshot về các tiến trình hiện tại đang hoạt động. Nó giúp cho người dùng có thể giám sát và quản lí các tiến trình của hệ thống.

**Syntax** `ps -<option>`
```
┌──(nhduydeptrai㉿tobi)-[~]
└─$ ps                        
    PID TTY          TIME CMD
   1808 pts/0    00:00:01 zsh
  32966 pts/0    00:00:00 ps

```
`zsh` là trình thông dịch dòng lệnh mặc định hiện nay, thay thế cho lệnh bash.
Giải thích qua về output của lệnh `ps`:

- **PID**: ID của tiến trình, một mã định danh duy nhất cho mỗi tiến trình.
- **TTY**: Loại Terminal liên quan đến tiến trình đó.
- **TIME**: Tổng thời gian CPU được dùng bởi tiến trình.
- **CMD**: lệnh chạy tiến trình đó.

### Lệnh xxd

- Chức năng là nó sẽ hiển thị cho chúng ta file đó dưới dạng HEX, nó giúp cho người phân tích có thể xác định chính xác file đó là gì thông qua những giá trị hex và ASCII trong 2 cột output của `xxd`, vì đôi khi một file có thể bị sửa đổi nhỏ bằng cách thay đổi extention để đánh lừa. Có một cách khác là có thể dùng lệnh `file`. Ngoài ra xxd còn rất nhiều những công dụng khác. Chúng ta có thể tìm hiểu thêm tại [xxd_command](https://www.geeksforgeeks.org/linux-unix/xxd-command-in-linux/).

**Syntax**: `xxd <optione> <ten_file>`

<img width="1063" height="702" alt="image" src="https://github.com/user-attachments/assets/79a9c965-4696-414f-bdde-be75f2a2d192" />

Ở đây thì output của `xxd` sẽ được chia thành 3 cột:
- Cột bên trái là địa chỉ của bộ nhớ, cột ở giữa là mã hex, cột bên phải là kí tự ASCII tương ứng với mã hex đó.

### Lệnh strings, grep

Chức năng của lệnh này là giúp người dùng lọc ra các kí tự có thể đọc được trong một file có rất nhiều những kí tự rác không thể đọc được, bởi vì phần lớn các dữ liệu bên trong 1 file nhị phân không phải văn bản thuần túy, mà là các giá trị nhị phân thể hiện qua kí tự, ký hiệu.

**Syntax:** `strings <ten_file>`

<img width="1000" height="535" alt="image" src="https://github.com/user-attachments/assets/8f4d43df-50b7-48f4-8a7e-b845a846ae9e" />

Thông thường khi sử dụng strings, ta có thể kết hợp với 1 lệnh bằng cách sử dụng dấu `pipe (|)` kèm với lệnh `less` - giúp chúng ta có thể cuộn xem nội dung từ từ để không bỏ xót, và `grep` - giúp chúng ta lọc ra các kí tự - nội dung cần tìm trong một chuỗi output, lệnh `grep` thường không đi 1 mình nó.

Output của lệnh `strings <ten_file> | less` 

<img width="1230" height="847" alt="image" src="https://github.com/user-attachments/assets/f3c2f0b3-1f73-49c1-b96d-5550e76496a4" />

Output của lệnh `strings <ten_file> | grep`: 

<img width="989" height="696" alt="image" src="https://github.com/user-attachments/assets/3563f5ec-a033-4bec-b391-65a92168a01e" />

### Lệnh cat

Là lệnh giúp hiển thị nội dung trong 1 file ra màn hình người dùng.

**Syntax:**  `cat /path/to/filename`

Ví dụ: `cat firefox_decrypt.py`

<img width="1968" height="846" alt="image" src="https://github.com/user-attachments/assets/cb2e17b2-5b7a-4645-bdec-18bb504649d5" />

Chúng ta cũng có thể cat một lượt nhiều file bằng cách **syntax**: `cat file1 file2`.

```
                                                                                                                                                      
┌──(nhduydeptrai㉿tobi)-[~]
└─$ cat file1 file2
hello world 1
hello world 2
                               
```

Và chúng ta cũng có thể điều hướng output vào 1 file khác bằng kí hiệu `>`.
> Kí hiệu `>` này là kí hiệu chung và chúng ta cũng có thể sử dụng nó cho mọi lệnh khác nếu muốn lưu output của nó vào 1 file cho mục đích người dùng.
> Ví dụ: `strings file2 > file4`

```
                                                                                                                                                      
┌──(nhduydeptrai㉿tobi)-[~]
└─$ cat file1 file2 > file3
                                                                                                                                                      
┌──(nhduydeptrai㉿tobi)-[~]
└─$ cat file3              
hello world 1
hello world 2
                          
```
### Lệnh find

Lệnh find cho phép người dùng có thể tìm kiếm một file hoặc 1 thư mục dựa trên tên, extention, kích thước, hoặc các điều kiện khác. Nó quét các folder và subfolder được chỉ định để xác định vị trí của file cần tìm.

**Syntax**: `find <path> <options> <file name hoac extentions, size,...>`

Ví vụ: mình muốn tìm một file tên là `flag.png` trong thư mục `CTF` thì chúng ta dùng lệnh sau:

```                                                                                                                                              
┌──(nhduydeptrai㉿tobi)-[~]
└─$ find /mnt/hgfs/kali_linux_real_machine/CTF -name flag.png 
/mnt/hgfs/kali_linux_real_machine/CTF/hcmus_ctf/Pho ren sic/Cropped/flag.png

```

Chúng ta cũng có thể tìm kiếm nhiều file với cùng 1 extention, ví dụ:

```                                                                                                                                                   
┌──(nhduydeptrai㉿tobi)-[~]
└─$ find /mnt/hgfs/kali_linux_real_machine/CTF/UOF_CTF -name *.png  
/mnt/hgfs/kali_linux_real_machine/CTF/UOF_CTF/deda/deda_gui/web/misc/logo.png
/mnt/hgfs/kali_linux_real_machine/CTF/UOF_CTF/deda/deda_gui/web/misc/x-y.png
                                                                                        
```

### Lệnh file 

Lệnh này giúp cho người phân tích có thể xác định nhanh rằng đây là file gì để có thể lựa chọn được phương án phân tích tiếp theo tốt nhất, lựa chọn công cụ phù hợp, hoặc có thể để kiểm tra trong trường hợp file bị đổi tên để đánh lừa. 

Cách lệnh `file` nhận dạng được 1 file đó là file gì hoàn toàn không dựa vào extentions của file, mà nó lệnh sẽ tự động quét các byte đầu tiên của file đó, sau đó so sánh với cơ sở dữ liệu của nó, và nhận định file là file gì.

**Syntax:** `file <ten_file>`

Ví dụ, cụ thể:
```
┌──(nhduydeptrai㉿tobi)-[~/Pico_CTF/St3g0]
└─$ file pico.flag.jpg                                             
pico.flag.jpg: PNG image data, 585 x 172, 8-bit/color RGBA, non-interlaced                                                                         
```
Rõ là chúng ta có thể thấy được đây là một file `jpg` nhưng khi sử dụng lệnh `file` thì thực tế nó là một file `png` bởi vì lệnh `file` sẽ không đọc extentions hiện tại của file mà sẽ quét qua các byte đầu tiên của file `png`. Lệnh `file` thấy các signature byte của `png` như `89 50 4E 47 0D 0A 1A 0A` và các chunk, nó thực hiện so sánh với dữ liệu được lưu trên cơ sở dữ liệu của lệnh `file` và nhận diện được đây là file `.png`


### Lệnh mv, rm

- Lệnh `mv` cho phép người dùng có thể di chuyển các file từ thư mục này sang thư mục khác, hoặc có thể sử dụng để tổi tên của một file
  **Syntax**: `mv file_cu file_moi` or `mv /path/file_cu /path/file_moi`
```
┌──(nhduydeptrai㉿tobi)-[~/Pico_CTF/St3g0]
└─$ mv pico.flag.png pico.flag.jpg 
```

```                                                                                                                                             
┌──(nhduydeptrai㉿tobi)-[~]
└─$ mv pcap1.pcapng /mnt/hgfs/kali_linux_real_machine/CTF/VSL_ctf_2026/Data\ stole 
                                                                                                                                                    
┌──(nhduydeptrai㉿tobi)-[~]
└─$ mv pcap2.pcapng /mnt/hgfs/kali_linux_real_machine/CTF/VSL_ctf_2026/Data\ stole 
                                                                                                    
```

  

- Lệnh `rm` dùng để xóa đi 1 file hoặc 1 thư mục, đặc biệt là lệnh `rm` sẽ xóa trực tiếp file vĩnh viễn mà không để nó vào thùng rác.
**Syntax**: `rm <ten_file/folder>`

```                                                                                                                                                 
┌──(nhduydeptrai㉿tobi)-[~]
└─$ rm docker-compose.yml        
```
Để xóa đi 1 thư mục chúng ta có thể dùng option `-r` của `rm` để thực hiện đệ quy xóa thư mục

<img width="1202" height="208" alt="image" src="https://github.com/user-attachments/assets/300ed67c-3bd7-4d55-806b-6ebe399f0d30" />


### Lệnh echo

Lệnh `echo` có thể dùng để in ra màn hình một chuỗi nào đó từ người dùng.

```
┌──(nhduydeptrai㉿tobi)-[~]
└─$ echo rm -rf /                  
rm -rf /

```
Đây là một cách thường được sử dụng để debug một mã độc nào đó, thay vì chúng ta thực hiện chạy nó trước, bởi vì lệnh `echo` chỉ thực hiện in chứ không thực thi.

Nhưng có một cách để có thể sử dụng lệnh `echo` để thực thi một lệnh, hắn sẽ chèn lệnh đó vào dấu `$()`, lúc này trình thông dịch sẽ tạm dừng `echo` và nó thực thi lệnh bên trong `$()` trước, ví dụ:

```
┌──(nhduydeptrai㉿tobi)-[/mnt/…/kali_linux_real_machine/CTF/VSL_ctf_2026/float]
└─$ echo "toi hien dang o $(pwd)"  
toi hien dang o /mnt/hgfs/kali_linux_real_machine/CTF/VSL_ctf_2026/float

```
Trình thông dịch sẽ thực thi lệnh bên trong `$()` là lệnh `pwd` sẽ thực thi việc in ra toàn bộ đường dẫn hiện tại của người dùng đang "đứng" tại thư mục đó, xong sau đó nó mới ghép chuỗi trước đó vào lệnh `pwd` vừa thực hiện xác định đường dẫn, và in ra màn hình người dùng.

Ngoài việc dùng để in ra 1 chuỗi ra màn hình người dùng, thì lệnh `echo` còn dùng để ghi 1 chuỗi đó vào phần cuối của một file bằng kí hiệu `>>`, hoặc có thể ghi đè nội dung mới vào file bằng kí hiệu `>`, ví dụ:

- `>`  ghi đè nội dung mới vào 1 file (xóa nội dung cũ đi):

```
┌──(nhduydeptrai㉿tobi)-[~]
└─$ cat file_cu                               
noi dung truoc khi dung lenh echo de ghi de`
                                                                                                                                                    
┌──(nhduydeptrai㉿tobi)-[~]
└─$ echo "noi dung sau khi dung lenh echo de ghi de" > file_cu 
                                                                                                                                                    
┌──(nhduydeptrai㉿tobi)-[~]
└─$ cat file_cu 
noi dung sau khi dung lenh echo de ghi de
```

- `>>` ghi nối tiếp nội dung vào 1 file cũ:

```
┌──(nhduydeptrai㉿tobi)-[~]
└─$ cat file_cu 
noi dung sau khi dung lenh echo de ghi de
                                                                                                                                                    
┌──(nhduydeptrai㉿tobi)-[~]
└─$ echo "noi dung ghi noi tiep vao file cu~" >> file_cu      
                                                                                                                                                    
┌──(nhduydeptrai㉿tobi)-[~]
└─$ cat file_cu
noi dung sau khi dung lenh echo de ghi de
noi dung ghi noi tiep vao file cu~

```
Chúng ta thấy đấy, nó sẽ thực hiện ghi vào phần cuối của file cũ từ chuỗi mới.

### Lệnh pwd

Lệnh này sẽ in ra đường dẫn đầy đủ từ (root) cho đến vị trí của người dùng trong folder hiện tại trong terminal.

- Ví dụ:

```                                                                                                                                             
┌──(nhduydeptrai㉿tobi)-[~]
└─$ cd /mnt/hgfs/kali_linux_real_machine/CTF/WANNAGAME_CTF_UIT/Where_is_the_malware/2025-12-05T175919_alexPC/C/Users/alex 
                                                                                                                                                    
┌──(nhduydeptrai㉿tobi)-[/mnt/…/2025-12-05T175919_alexPC/C/Users/alex]
└─$ pwd
/mnt/hgfs/kali_linux_real_machine/CTF/WANNAGAME_CTF_UIT/Where_is_the_malware/2025-12-05T175919_alexPC/C/Users/alex

```

# File System in Linux 

## I. Every file system in Linux

### 1. Ext4 (Extended file system)

**Ext4** (Fourth Extended Filesystem) là hệ thống tệp tiêu chuẩn cho hầu hết các bản phân phối Linux hiện nay. So với các phiên bản tiền nhiệm, Ext4 không chỉ tăng giới hạn lưu trữu mà còn thay đổi hoàn toàn cách quản lý dữ liệu để tối ưu hóa tốc độ và độ tin cậy

#### A. Structure of Ext4

Thay vì sử dụng phương pháp ánh xạ khối truyền thống của **Ext2/3**, thì **Ext4** sử dụng **Extents**.
- Cơ chế: Một extent là một dải các khối dữ liệu liên tiếp nhau trên đĩa cứng. Thay vì liệt kê từng khối, Ext4 chỉ ghi lại theo cách: "*Bắt đầu từ khối 1 và kéo dài đến khối 4*".

- **Cấu trúc cây B+**: Một inode đơn lẻ trong Ext4 có thể chauws tối đa 4 extents. Nếu một tệp quá lớn hoặc bị phân mảnh nhiều, các extents còn lại sẽ được tổ chức theo cấu trúc cây B+ để truy xuất nhanh.

> **Cấu trúc cây B+** là một cấu trúc dữ liệu cây tự cân bằng, chuyên tối ưu hóa các thao tác tìm kiếm, chèn, và xóa trong hệ thống cơ sở dữ liệu và tệp tin

- Giảm thiểu đáng kể metadata, giúp việc truy cập tệp lớn nhanh hơn và giảm tải cho CPU.

#### B. Cơ chế Phân Bổ trì hoãn 

Một trong những tính năng quan trọng nhất giúp cho **Ext4** vượt trội về hiệu suất.

- **Cách hoạt động của cơ chế**: Khi 1 ứng dụng ghi dữ liệu, thay vì ghi lập tức vào ổ đĩa, thì ext4 sẽ giữ nó trong RAM. Hệ thống chỉ quyết định vị trí các khối dữ liệu thực tế trên đĩa khi dữ liệu chuẩn bị được flush xuống ổ cứng.

- Bằng cách chờ đợi thế này thì hệ thống tệp biết được tổng kích thước của tệp và có thể tìm một khoảng trống đủ lớn liên tục để ghi toàn bộ tệp đó 1 lần duy nhất, giảm thiểu tình trạng chia nhỏ ổ đĩa.

#### C. Nhật ký dữ liệu (Journaling) và Checksum

Ext4 sử dụng cơ chế ghi nhật ký để bảo vệ dữ liệu trước các sự cố bị crash đột ngột.

- **Journaling**: Mọi thay đổi về siêu dữ liệu (metadata) đều được ghi vào 1 vùng nhật ký trước khi thực hiện thay đổi thực tế. Nếu máy bị crash đột ngột, hệ thống chỉ cần kiểm tra nhật ký để phục hồi trạng thái ổn định thay vì phải quét cả ổ đĩa để fix từng mục.

- **CheckSUms**: Ext4 là hệ thống tệp đầu tiên thêm mã kiểm tra vào nhật ký. Cơ chế này giúp phát hiện nếu dữ liệu nhật ký bị hỏng trong quá trình ghi, tránh việc hệ thống cố gắng phục hồi dữ liệu từ 1 bản nhật ký lỗi, có thể gây hư tổn thêm.

#### D. Giới hạn và khả năng mở rộng tệp

|Thông số | Giới hạn |
| --- | --- |
| Kích thước hệ thống tệp tối đa | 1 Exbibyte (EB) cực lớn |
| Kích thước tối đa của 1 tệp đơn lẻ | 16 TB |
| Số lượng thư mục con | Không giới hạn |

### 2. XFS (Extended File System)

**XFS** là một hệ thống tệp khác có độ hoàn thiện cao hơn so với **Ext4**, loại hệ thống tệp này được tối ưu hóa để lưu trữ các tệp và phân vùng lớn trên 1 máy chủ duy nhất.

#### Cấu trúc và Cơ chế hoạt động

**Allocation Groups**: XFS chia không gian lưu trữ thành các khu vực có kích thước bằng nhau gọi là *Allocation Groups*. Mỗi nhóm này hoạt động như 1 hệ thống tệp riêng biệt, nó có **Superblock** riêng, tự quản lý cấu trúc và sử dụng không gian của mình.

**Quản lý không gian bằng cây B+**: Sử dụng không gian được kiểm soát nhờ sự hỗ trợ của cấu trúc cây B+, trong đó:

- Một cây ghi lại khối đầu tiên trong vùng không gian trống liên tục.

- Cây còn lại ghi nhận số lượng khối tạo nên vùng trống đó.

**Extents**: Các khối lưu trữ được gán cho tệp bằng phương pháp dựa trên extent, tương tự như Ext4.

**Inode**: Tất cả các tệp và thư mục trong **XFS** đều được đại diện bởi các inode riêng lẻ.

- Việc cấp phát các extent có thể được lưu trực tiếp trong inode, hoặc được theo dõi bởi 1 cây B+ khác liên kết với nó trong trường hợp tệp quá lớn hoặc bị phân nhánh.

- Cũng giống như inode trong hệ thống Ext4, chúng không chứa tên tệp, tên chỉ có sẳn trong các thư mục tương ứng.

**Khả năng phục hồi và độ tin cậy**

**XFS** cũng có cơ chế **Journaling** cho mọi cập nhật liên quan đến metadata. Tất cả các thay đổi được ghi vào nhật ký trước, sau đó các khối dữ liệu thực tế mới được sửa đổi sau.

#### Ưu nhược điểm của XFS

Ưu điểm lớn của XFS là: 

- Có khả năng xử lí các tệp tin lớn như (video 4k, cơ sở dữ liệu) rất tốt do cơ chế Extents và cấu trúc cây B+.

- Hiệu suất xử lí song song tốt nhờ vào các không gian lưu trữ **(Allocation Groups)**, khi nhiều luồng hoặc nhiều proccess muốn ghi dữ liệu vào ổ đĩa -> gây chậm CPU, thay vào đó nó có thể ghi vào các **AG** khác nhau cùng 1 lúc mà không cần chờ đợi lẫn nhau.

- Khả năng mở rộng cực cao

Nhược điểm của XFS:

Một khi mà XFS thực hiện mở rộng kích thước tệp, thì nó không thể shrink tệp lại. Khiến cho việc làm việc với nhiều tệp tin nhỏ sẽ gây ra nhiều rắc rối. 

### 3. Btrfs

**Btrfs (B-tree File System)** là 1 trong những định dạng thế hệ mới phổ biến cho Linux, và rất nhiều nỗ lực đang được thực hiện để đảm bảo tính ổn định của nó. Btrfs được tinh chỉnh để hoạt động được trên nhiều thiết bị. Nó bao hàm các tính năng của 1 *trình quản lý phân vùng logic* (Logical Volume Manager - LVM), có khả năng trải rộng nhiều dữ liệu và thiết bị lưu trữ khác nhau.


#### Cấu trúc dựa trên B-tree

Như tên gọi của nó, Btrfs dựa rất nhiều vào cấu trúc B-tree. Mỗi cây được tạo thành từ các nút trong (internal nodes) và các nút lá (leaves). Một nút trong sẽ trỏ đến 1 nút con hoặc nút lá, trong khi nút lá chứa 1 "mục" mang thông tin cụ thể, Bố cục nó sẽ là:

- **Root B-tree**: Vị trí của nó được lưu trong Superblock và nó chứa các tham chiếu đến tất cả cây B-tree còn lại.

- **Chunk B-tree:** Để quản lý việc ánh xạ từ địa chỉ logic sang địa chỉ vật lý.

- **Device B-tree:** Khác với Chunk B-tree, thì nó liên kết các khối vật lý trên thiết bị phần cứng với phần địa chỉ ảo tương ứng.

- **File system B-tree**: Chịu trách nhiệm cấp phát tệp và thư mục.
  - Tệp nhỏ: Được lưu trữ trực tiếp ngay bên trong các mục `extent` của cây (giúp tiết kiệm không gian và truy xuất nhanh).
 
  - Tệp lớn: Được đặt bên ngoài tại các vùng liên tục gọi là `extent`. Lúc này mục `extent` trong cây sẽ tham chiếu đến tất cả các `extent` đang chứa dữ liệu tệp đó.
 
- Thư mục: Các mục thư mục chứa tên tệp và trỏ đến các "mục inode" tương ứng.

### Cơ chế mới

**1. Tích hợp LVM/RAID**: Nó có thể gộp nhiều ổ cứng lại thành 1 khối lưu trữ mà không cần phần mềm hay phần cứng RAID riêng.

**2. Lưu trữ tệp nhỏ (Inline Data)**: Các tệp rất nhỏ được nhét thẳng vào cấu trúc cây dữ liệu thay vì chiếm 1 khối block riêng biệt trên đĩa, giúp tiết kiệm dung lượng đáng kể.

**3. An toàn dữ liệu (CoW)**: Cơ chế tạo bản sao của 1 khối dữ liệu, thực hiện ghi dữ liệu mới vào chỗ trống khác trên đĩa, sau khi được ghi an toàn thì trỏ bản sao đó đến phần dữ liệu mới được ghi. Giúp loại bỏ nguy cơ hỏng dữ liệu khi bị crash.

### 4. F2FS 

**F2FS** hoạt động dựa trên phương pháp Hệ thống tệp cấu trúc nhập kí (LFS). Nó tính toán đến các đặc thù riêng cho bộ nhớ flash. Thay vì tạo 1 khối dữ liệu lớn nhất để ghi, **F2FS** tập hợp các khối thành các đoạn riêng biệt (tối đa 6 đoạn ) và ghi chúng đồng thời. Giúp tối ưu hóa tốc độ.

#### A. Cấu trúc lưu trữ

F2FS chia không gian lưu trữ theo cấu trúc phân cấp:

- **Segment**: Đơn vị cơ bản có kích thước cố định.

- **Section**: Được tạo thành từ nhiều segment liên tiếp.

- **Zone***: Được tạo thành từ nhiều Sections.

#### B. Quản lý dữ liệu qua các Nodes

- **Inode**: lưu trữ các metadata như tên tệp, kích thước, permission.

- **Direct Node**: Chỉ ra vị trí các khối dữ liệu thực tế.

- **Indirec Node**: Trỏ đến các khối nằm trong các nút khác.

#### C. Các bảng quản lý quan trọng

- **NAT (Node Address Table)**: Bảng chứa địa chỉ vật lý của các nút.

- **SIT (Segment infomation table)**: ghi lại trạng thái sử dụng của tất cả các khối.

- **SSA (Segment Summary Area)**: Xác định khối nào thuộc về nút nào.

- **Main area**: Nơi chứa nội dung dữ liệu thực tế và các nút.

#### Cơ chế tự làm sạch (Garbage Collection)

Khi sắp xếp các phân đoạn trống, F2FS sẽ tự động dọn dẹp trong nền khi hệ thống không hoạt động.
- Thuật toán dọn dẹp: Chọn các "segment victim" để xử lí và tiêu chí dựa vào số lượng khối đã sử dụng (theo SIT) hoặc dựa vào thời gian tuổi thọ của segment đó.


### 5. JFS (Journaled File System) 

#### A. Cấu trúc và tổ chức dữ liệu
Một phân vùng JFS được cấu thành từ các vùng gọi là Allocation Groups, và mỗi nhóm chứa 1 hoặc nhiều FileSets (tập tệp).

- Quản lý tệp: Tất cả các tệp và thư mục được mô tả bởi các inode riêng biệt.

- Dữ liệu: Nội dung dữ liệu thực tế được đại diện bởi 1 hoặc nhiều extents. Tất cả các extents này được lập chỉ mục bởi 1 cấu trúc **cây B+** chuyên dụng.

- Lưu trữ thư mục:
  - Thư mục nhỏ: được lưu trữ ngay bên trong các inode (khác với extent).
 
  - Thư mục lớn: Được tổ chức dưới dạng **cây B+**.
 
#### Quản lý không gian và Nhật ký

Cấu trúc cây B+ cũng đóng vai trò kiểm soát việc sử dụng không gian lưu trữ thông qua 2 cây riêng biệt:

- Một cây lưu trữ địa chỉ khối bắt đầu của các dải trống (free extent).
- Một cây lưu trữ số lượng (kích thước) của các dải trống đó.

**JFS** cũng bao gồm một vùng Nhật ký (Log area) riêng biệt. Bất cứ khi nào có thay đổi về siêu dữ liệu (metadata), hệ thống sẽ ghi vào vùng nhật ký này để đảm bảo tính toàn vẹn.


### 6. ZFS (Zettabyte File System)

**ZFS** nó vừa là hệ thống tệp, vừa là trình quản lý phân vùng (volume manager). Nó gộp tất cả các ổ cứng vật lý vào 1 (Storage Pool - zpool). Từ đây, bạn có thể tạo hàng trăm hệ thống tệp con khác mà không cần quan tâm đến kích thước cố định. Các tệp con này dùng chung dung lượng của vùng lưu trữ. Vùng lưu trữ này còn trống bao nhiêu, thì các tệp con được dùng bấy nhiêu.

#### Cấu trúc và cơ chế của ZFS

**A. Cơ chế toàn vẹn dữ liệu** 
- Khi ghi dữ liệu , ZFS tính toán mã **checksum** cho từng khối dữ liệu và kể cả siêu dữ liệu. Khi đọc lại file, ZFS tính toán lại và so sánh với mã checksum khi dữ liệu được ghi.

- Đặc biệt là khả năng tự sửa lỗi **(Self-healing)**: Nếu ZFS phát hiện checksum không khớp, và bạn đang chay chế độ Mirror hoặc RAID, ZFS sẽ tự động lấy bản sao tốt từ ổ cứng khác đè lên lỗi, và trả về dữ liệu sạch.

**B. RAID-Z**

**ZFS** không dùng RAID phần cứng, nó dùng RAID riêng gọi là RAID-Z.
- **RAID-Z1,2,3:** tương ứng với RAID 5,6 (có thể tìm hiểu sâu về [RAID](https://www.baeldung.com/linux/raid-intro))  nhưng mạnh hơn. Z3 cho phép hỏng cùng lúc 3 ổ cứng nhưng không mất dữ liệu.

**C. ARC (Adaptive Replcacement Cache)**

ZFS sử dụng RAM cực kì tích cực. Nó biến RAM dư thừa của máy chủ thành bộ nhớ đệm (Cache) đọc dữ liệu nhanh hơn. Điều này khiến cho hệ thống tệp ZFS ngốn rất nhiều RAM.

**D. Copy-on-Write (CoW) và Snapshot**

Giống Btrfs, ZFS không ghi đè dữ liệu cũ, nó cho phép:

- **Snapshot** bạn có thể chụp ảnh hệ thống tệp nhanh chóng, dù dữ liệu nặng cả terabyte.

- **Rollback**: Nếu lỡ tay xóa file hoặc bị virus mã hóa, cơ chế CoW sẽ đưa file đó về ngay trạng thái ban đầu mà không cần mất thời gian để giải mã. Tìm hiểu thêm về cơ chế **Snapshot và CoW** ở đây (https://klarasystems.com/articles/basics-of-zfs-snapshot-management/).




## II. Linux File Hierarchy Structure 

Khác với Windows sẽ có cấu trúc file system khác nhiều so với Linux, với Windows sẽ quản lý lưu trữ theo từng phân vùng ổ đĩa riêng biệt và giống như những cái cây độc lập trong 1 khu rừng chúng riêng biệt hoàn toàn với nhau. Đối với Linux, cấu trúc bên trong của file system sẽ theo dạng cấu trúc cây phân cấp, với đỉnh là thư mục gốc duy nhất `/`.

Hầu hết các thư mục dưới đây tồn tại trong tất cả hệ điều hành UNIX và thông thường đều được sử dụng cùng 1 cách, và đây là các thư mục như mặc định bên trong các hệ điều hành Linux.

<img width="708" height="623" alt="image" src="https://github.com/user-attachments/assets/f4d9faeb-4973-440f-b00e-4795aeeb4b55" />

### 1. "/" (Root) 

Nằm ở phần top của mọi bản Linux file system đó chính là thư mục `root`, đại diện bởi dấu gạch `/`. Không có bất kì thư mục nào nằm trên thư mục `root`. Nếu bạn nhìn vào giao diện file system, bạn sẽ có thể thấy được mọi thư mục đều nằm dưới thư mục `root`.

- Mọi file và thư mục đơn lẻ đều bắt đầu từ thư mục root.

- Chỉ có root user mới có quyền modify thư mục root.

- /root là root user's của thư mục home, nó khác hoàn toàn với `/`. Một là `root` của cả hệ thống lưu trữ toàn bộ dữ liệu của hệ điều hành máy tính đó, còn thư mục `/root` chỉ đơn giản là `1 căn phòng ` nhỏ bên trong ngôi nhà lớn `/`, chỉ có user đăng nhập với quyền root `khi terminal thay đổi từ $ -> #`, lúc này người dùng này mới có toàn quyền trong hệ thống, kể cả xóa bỏ hệ thống.

Nếu một user thông thường, muốn tải về 1 file tại thư mục `/`, hoặc muốn tạo or xóa một folder trong đây, đều sẽ bị chặn với thông báo `Permission denied`.

<img width="881" height="637" alt="image" src="https://github.com/user-attachments/assets/f833fed9-650e-4dae-a2f6-bd896515d76d" />

### 2. /bin

Thư mục /bin chứa các command và các file nhị phân cần thiết cho hoạt động của mọi người dùng, bao gồm các lệnh `ls`, `cd`, `ssh`,... Những lệnh này có sẳn đối với mọi người dùng trong hệ thống.

- Chứa các file binary để thực thi các chương trình hay ứng dụng cần thiết cho mỗi người dùng. Nói đơn giản thì những `file binary` bên trong thư mục `/bin` căn bản là giống với file `.exe` trong windows, chỉ có cái khác là nó không có đuôi `.exe` thôi.

- Các lệnh thông dụng của 1 người dùng thường được sử dụng đều lưu trữ trong thư mục này. `/bin` chứa tất cả câu lệnh được sử dụng bởi tất cả người dùng trong hệ thống.

<img width="883" height="619" alt="image" src="https://github.com/user-attachments/assets/263a17ab-8cb4-47bd-9660-6083e0a3aa3a" />

### 3. /boot

Thư mục này là nơi mà chúng ta không nền đi vào nhất, bởi vì nó chứa những file và folder cần thiết cho việc khởi động máy tính lên. Nó bao gồm cấu hình **GRUB** bootloader và những file kernel cần thiết được tải lên trong quá trình khởi động.

<img width="886" height="618" alt="image" src="https://github.com/user-attachments/assets/95724fb9-d6f9-4151-a6df-b0e6ae4d8fc9" />

### 4. /dev

Các file của thiết bị sẽ được lưu trữ bên trong thư mục `/dev`. Những file đặc biệt này hành động giống như giao diện giữa hardware và software. Các file thiết bị có 2 loại: block device (hard drives) và các thiết bị cho người dùng như (bàn phím, tai nghe, chuột, USB,..). Ví dụ trong `/dev` sẽ chứa các phân vùng ổ đĩa như `/dev/sda1`, `/dev/sda2`,...

<img width="883" height="616" alt="image" src="https://github.com/user-attachments/assets/18f1384b-e7d6-4623-8abb-8a112d529dab" />

### 5. /etc

Nó được ghi tắt cho **Editable text configuration**. Thư mục `/etc` chứa các file cấu hình cho system application, users, dịch vụ và các tools hoặc nó chứa các tệp cấu hình cho toàn hệ thống.

- Nó chứa bên trong các shell script để startup và shutdown được sử dụng cho việc bắt đầu/tạm dừng các chương trình cá nhân.

### 6. /home

Đây là thư mục chứa thư mục cá nhân dành riêng dành cho mỗi user, kể cả user thông thường và đây cũng là thư mục cho phép người dùng không có quyền hạn có thể modify bên trong đây. Và mỗi user chỉ thấy được tên thư mục (là tên của user đó) của chính user đó bên trong thư mục home này, đối với những người có quyền cao hơn như là `root`, sẽ có thể thấy được mọi thư mục của những user khác trong thư mục `/home`.

- `/home` là thư mục cho mọi users lưu trữ thư mục riêng của họ bên trong, chứa các files được lưu, cài đặt cá nhân,...

- Example: /home/Nduy, /home/T0b1.

<img width="1302" height="885" alt="image" src="https://github.com/user-attachments/assets/69d369fb-13d7-4343-b3d1-27c807161195" />

<img width="1002" height="863" alt="image" src="https://github.com/user-attachments/assets/f85710c4-ca43-424d-b64c-7e192842c96f" />


### 7. /lib

Ứng dụng yêu cầu các thư viện dùng chung để có thể khởi chạy được, tất cả những thư viện đó được lưu trữ bên trong `/lib`. Bao gồm các thư viện liên kết động cần thiết trong quá trình runtime. Ví dụ, Apache server libraries được lưu trữ ở đây. 

<img width="1313" height="843" alt="image" src="https://github.com/user-attachments/assets/dc2355fc-a6a6-40e3-be6c-cb8d0faf66b6" />

Ví dụ như các thư viện có thể dùng để giải nén `7z`, `dpkg`,...

### 8. /media

Các thiết bị như USBs, CDs và các drivers được gắn bên trong `/media`. Khi bạn mount một USB, hay floopy disk vào máy tính, nó sẽ tự động tạo ra 1 thư mục con về thiết bị này bên trong `/media`, mục đích là chứa các file cấu hình của các thiết bị trên. 

- Thư mục mount tạm thời cho các thiết bị rời.

- Example: /media/cdrom dành cho CD-ROM; /media/floppy dành cho floppy drives.

### 9. /mnt

Khác với thư mục `/media` sẽ tự động tạo ra subfolder bên trong khi các thiết bị rời được cắm vào máy tính, nhưng đối với `/mnt` bạn phải tự động mount thủ công 1 ổ đĩa ngoài được kết nối. Và khi 1 ổ đĩa ngoài được kết nối nó sẽ được lưu trữ bên trong `/mnt`.

<img width="996" height="831" alt="image" src="https://github.com/user-attachments/assets/5d10233f-56b1-41b2-bf66-d66406458313" />

<img width="1146" height="851" alt="image" src="https://github.com/user-attachments/assets/a9bd2f5f-8da0-4914-9add-394dbc512bb6" />

### 10. /opt

Phần mềm và gói của bên thứ 3 không thuộc cài đặt hệ thống mặc định được lưu trữ bên trong `/opt`. Nó bao gồm các tập tin cấu hình và dữ liệu của các ứng dụng đó.

<img width="882" height="626" alt="image" src="https://github.com/user-attachments/assets/5e398ea6-5afc-4c46-b03e-1736ad27355c" />

### 11. /sbin

Khác với `/bin` chứa các tệp binary cho người dùng thông thường trong hệ thống, thì `/sbin` sẽ chứa các file binary cho administrative như iptable, firewall, management tools, route, init. Những file binary này chủ yếu chỉ dành cho administrator của hệ thống và thông thường yêu cầu cần có quyền root để thực thi.

<img width="886" height="626" alt="image" src="https://github.com/user-attachments/assets/39067dba-a0a8-4cd6-8006-7d8e40dba977" />

### 12. /srv

Dữ liệu dành riêng cho trang web được dành riêng cho hệ thống, như là data và scripts dành cho web server, FTB. Những user thông thường hoặc kể cả root đều thấy thư mục này trống, bởi vì nó chỉ xuất hiện các thư mục con khi bạn đang là 1 hệ thống web server hoặc FTB server.

Example: /srv/cvs chứa CVS liên quan đến data.

<img width="1203" height="845" alt="image" src="https://github.com/user-attachments/assets/7cb3a670-d52c-40ae-a908-a6c71ba0a751" />

<img width="1189" height="890" alt="image" src="https://github.com/user-attachments/assets/7cbdf349-1fe4-4fc5-b71b-abf9b1c14d38" />

### 13. /tmp

Thư mục này chứa các file hoặc thư mục được tạo tự động bởi chương trình khi file được thực thi. Các files này sẽ được xóa ngay lập tức sau khi các chương trình kết thúc, hoặc sau khi shutdown or restart.

- Thư mục chứa các file tạm thời được tạo bởi hệ thống hoặc người dùng.

- Files trong thư mục này sẽ bị xóa khi hệ thống tắt.

<img width="1653" height="982" alt="image" src="https://github.com/user-attachments/assets/91d78b18-9c8c-44c5-9450-658b01a6d12a" />

### 14. /usr

Hệ thống phân cấp thư cấp cho việc read-only user data. chứa phần lớn các tiện ích người dùng và ứng dụng.

- Chứa file binary, library dynamic, tài liệu và mã nguồn cho các chương trình.

<img width="1057" height="827" alt="image" src="https://github.com/user-attachments/assets/25317db9-c2d3-4c37-9574-b76199b5125f" />

- /usr/bin chứa các file binary cho user programs. Nếu bạn không thể tìm thấy user binary bên trong /bin, bạn có thể tìm kiếm bên trong /usr/bin.

<img width="1063" height="836" alt="image" src="https://github.com/user-attachments/assets/eb0638f3-aaa1-4f45-aceb-76f04fa7a7eb" />


- /usr/sbin chứa các file binary cho administrator, và cũng tương tự như trên thì nếu như bạn không tìm thấy file binary cho administrator bên trong /sbin, thì có thể tìm kiếm bên trong /usr/sbin.

<img width="1080" height="870" alt="image" src="https://github.com/user-attachments/assets/82fc4e2f-f522-4173-ac9a-1ed0eac211b9" />


- /usr/lib chứa các thư viện động cho /usr/bin và /usr/lib.

<img width="1115" height="846" alt="image" src="https://github.com/user-attachments/assets/fa98d4f8-0386-40da-8e42-8e99a3c2b67a" />


- /usr/local chứa chương trình của người dùng mà tải xuống từ source. Vdu: Khi bạn tải xuống apache từ source, nó sẽ được lưu trữ bên trong /usr/local/apache2.

<img width="1128" height="840" alt="image" src="https://github.com/user-attachments/assets/b267d3fd-4507-4b83-b4a1-23c556a4b0d9" />


- /usr/src chứa Linux kernel source, header-files và tài liệu.

<img width="1126" height="852" alt="image" src="https://github.com/user-attachments/assets/f37735a6-b776-42a2-93e3-27ea8b58e8b8" />

### 15. /proc

Chứa các thông tin chi tiết cho các tiến trình hệ thống. Mỗi tiến trình sẽ được gán với 1 ID duy nhất và đại diện cho thư mục bên trong `/proc`

- Chứa thông tin cho tiến trình hệ thống.

- Đây là 1 hệ thống tệp tin giả chứa thông tin về các tiến trình đang chạy. Ví dụ /proc/{pid} thư mục này chứa thông tin chi tiết cho tiến trình với pid cụ thể đó.

- Cũng là virtual filesystem với các text infomation về tài nguyên hệ thống.

<img width="885" height="608" alt="image" src="https://github.com/user-attachments/assets/f94afbac-3fee-48be-9cfa-1b664fb08b1e" />

### 16. /sys

Bản chất nó không giống như `/dev` - khi mà chứa các tệp thiết bị, đóng vai trò là giao diện thực thi, bản chất của `/dev` là cung cấp cho các ứng dụng một ` lối đi ` để giao tiếp với phần cứng.

Còn đối với `/sys`, là nơi chứa thông tin và cấu trúc, đóng vai trò là giao diện quản lý, nó trình abyf cấu trúc cây cho toàn bộ phần cứng và driver mà nhân Linux đang quản lý. Cho biết tên thiết bị, thuộc hãng ?, đang tiêu thụ điện thế nào,....

/sys là nơi Linux trình bày toàn bộ "bản đồ" phần cứng của máy tính dưới dạng các file văn bản, để người dùng có thể dễ quản lí hơn.

<img width="1081" height="836" alt="image" src="https://github.com/user-attachments/assets/2f817d41-fdcb-4fdb-bd5f-46626142ac9f" />


# Log file in Linux

## File log trong Linux là gì ?

File log là một tập hợp các bản ghi mà Linux duy trì để các quản trị viên theo dõi các sự kiện quan trọng. Các file log này sẽ chứa các thông báo về máy chủ, bao gồm kernel, dịch vụ và ứng dụng đang chạy trên hệ thống. File log cung cấp thời gian chi tiết cho từng sự kiện của hệ điều hành, ứng dụng và hệ thóng Linux, giúp cho người dùng hoặc quản trị viên có thể chẩn đoán và khắc phục sự cố.

Hệ điều hành Linux sẽ lưu tất cả các log file quan trọng bên trong 1 thư mục `/var/log`. Hầu hết các file log bên trong đây sẽ được chia thành 4 loại chính;

- Application log: Nhật kí ứng dụng
- Event logs: Nhật kí sự kiện
- Service logs: Nhật kí dịch vụ
- System logs: Nhật kí hệ thống


## Các file log quan trọng trong hệ thống và Hành vi 

### 1. File log /var/log/kern.log

Đây là file log rất quan trọng và nó ghi lại tất cả các thông tin về những hành vi liên quan đến kernel, thông qua file log này chúng ta có thể khắc phục các lỗi và cảnh báo liên quan đến kernel. Những thông tin được ghi lại trong log này được Linux tạo ra trong suốt quá trình vận hành hệ thống, không chỉ giới hạn trong lúc khởi động. Các lỗi về phần cứng, sự cố driver, hoặc cảnh báo về filesystem sẽ được ghi lại ở đây.

**path**: `/var/log/kern.log`

***Mô phỏng 1 hành vi ví dụ có thể sẽ tìm thấy trong file `kern.log`:***

Giả sử chúng ta có 1 thiết bị USB được cắm vào hệ thống, lúc này kernel sẽ nhận diện được rằng có 1 thiết bị bên ngoài vừa được kết nối vào hệ thống, thực hiện các hành động kiểm tra thông tin thiết bị, và tìm-tải 1 driver phù hợp cho thiết bị đó, log mô phỏng;

```
[20236.607122] usb 1-1.2: new high-speed USB device number 28 using ehci-pci
[20236.720003] usb 1-1.2: New USB device found, idVendor=0951, idProduct=1665
[20236.720007] usb 1-1.2: New USB device strings: Mfr=1, Product=2, SerialNumber=3
[20236.720009] usb 1-1.2: Product: DataTraveler 2.0
[20236.720012] usb 1-1.2: Manufacturer: Kingston
[20236.720014] usb 1-1.2: SerialNumber: 08606E6D402EFD91D7025267
[20236.720694] usb-storage 1-1.2:1.0: USB Mass Storage device detected
[20236.721212] scsi host6: usb-storage 1-1.2:1.0
[20237.766610] scsi 6:0:0:0: Direct-Access     Kingston DataTraveler 2.0 1.00 PQ: 0 ANSI: 4
[20237.767789] sd 6:0:0:0: Attached scsi generic sg2 type 0
[20237.768454] sd 6:0:0:0: [sdc] 15131636 512-byte logical blocks: (7.75 GB/7.21 GiB)
[20237.769158] sd 6:0:0:0: [sdc] Write Protect is off
[20237.774661] sdc: sdc1 sdc2
[20237.777526] sd 6:0:0:0: [sdc] Attached SCSI removable disk
```

Phân tích hành vi:
**1. Phát hiện 1 thiết bị external được cắm vào hệ thống**: `usb 1-1.2: new high-speed USB device number 28`

**2. Định danh (Identification)**: hệ thống thực hiện kiểm tra `idVendoc` và `idProduct`, tức là mã nhà sản xuất và mã sản phẩm. `Manufacturer: Kingston`, `SerialNumber` cung cấp các thông tin chi tiết hơn để có thể quản lí thiết bị, và nhận dạng được loại USB này là gì.

**3. Tải driver**: `usb-storage 1-1.2:1.0: USB Mass Storage device detected` - Kernel nhận diện được đây là thiết bi lưu trữ và tải module `usb-storage`.

**4. Giả lập SCSI**: `scsi host6` - Linux xử lý hàu hết các thiết bị lưu trữ thông qua lớp SCSI.

**5 Gán tên thiết bị khối**: Thiết bị được gán tên `/dev/sdc` và được lưu trữ bên trong 1 thư mục chứa các thiết bị USB, block device,... `/dev`, những dòng `sdc: sdc1 sdc2` cho thấy Kernel đã đọc bảng phân vùng và tìm được 2 phân vùng bên trong.

### 2. File log /var/log/messages 

File log này sẽ chứa nhật ký hoạt động hệ thống (Systen log). Nó chủ yếu được sử dụng để lưu trữ các thông tin liên quan đến hệ thống. Về cơ bản, file log này lưu trữ tất cả dữ liệu hoạt động trong hệ thống như mail, cron, daemon, kern, auth,...

Khi chúng ta xm file log này chúng ta có thể theo dõi các lỗi khởi động (trừ kernel), lỗi dịch vụ liên quan đến ứng dụng, những thông tin được ghi trong này thường mang tính chất thông tin và có thể dùng để xem đầu tiên khi quản trị viên muốn xem sự cố hệ thống.

**path:** `/var/log/messages or /var/log/syslog`

Lý do mà nó có tận 2 đường dẫn bởi vì nó phụ thuộc vào các bản phân phối của Linux.

***Mô phỏng hành vi trong `/var/log/messages` log - Out of memory (OOM) killer***

Đây là 1 kịch bản khá phổ biến trong hệ thống Linux, khi mà 1 tiến trình sử dụng quá nhiều tài nguyên CPU trong hệ thống thì Linux sẽ kích hoạt cơ chế (OOM) để kill 1 tiến trình tiêu tốn nhiều tài nguyên nhất trong hệ thống.

Log mô phỏng: 

```
Mar 24 18:41:04 PLEDXDBOR0G kernel: Out of memory: Killed process 2475067 (postgres) total-vm:2484556kB, anon-rss:143224kB, file-rss:0kB, shmem-rss:452kB, UID:1011 pgtables:588kB oom_score_adj:900
```
Phân tích chi tiết các trường bên trong:

- ` Out of memory: Killed process 2475067 (postgres)` Kernel đã thực hiện cơ chế (OOM) để kill đi tiến trình `2475067 (postgres)`.

- `total-vm:2484556kB`: Đây là tổng bộ nhớ ảo mà tiến trình này register với hệ thống (2.4gb). Nhưng đây chưa phải là dung lượng RAM thực tế đang sử dụng.

- `anon-rss:143224kB`: Đây là con số quan trọng khiến cho Kernel quyết định dừng tiến trình này lại. `Anonymous RSS` là lượng RAM thực tế đang chứa dữ liệu động như (heap, stack) của tiến trình. OOM dựa vào tiến trình có RSS cao để dừng.

- `oom_score_adj:900`: Đây là điểm điều chỉnh OOM, tiến trình có thang điểm càng cao trong thang từ `-1000 - +1000` thì sẽ có khả năng bị Kernel dừng cao hơn.

### 3. File log /var/log/auth.log - /var/log/secure

Chứa thông tin xác thực trên hệ thống trong máy chủ phân phối bởi Linux (Debian hoặc Ubuntu,..) được ghi lại Khi chúng ta tìm kiếm vấn đề liên quan đến cơ chế ủy quyền của người dùng thì hãy tìm kiếm trong file log này. Đây là 1 file quan trọng để kiểm tra bảo mật. Trong các bản phân phối như RedHat và CentOS thì chúng ta sẽ có sự thay thế của `secure` log cho `auth.log`

Thông qua file log này giúp cho chúng ta xác định được:

- Các lần thử đăng nhập thành công/thất bại từ các phương thức (nhập mật khẩu, remote,..).
  
- Những lần user root sử dụng lệnh `sudo`.

- Những lần thay đổi người dùng bằng lệnh `su`.

**path:** `/var/log/auth.log`

***Mô phỏng hành vi trong file `/var/log/auth.log` - Login SSH Successfully***

Đây là mô tả lại 1 bản ghi cho lần phiên đăng nhập ssh thành công, với log mô phỏng:

```
May 1 16:17:43 owl sshd: Accepted publickey for root from 192.168.0.101 port 37384 ssh2
May 1 16:17:43 owl sshd: pam_unix(sshd:session): session opened for user root by (uid=0)
May 1 16:17:43 owl systemd-logind: New session 123 of user root.
```

Phân tích qua luồng được ghi:

**1. Xác thực SSH**: Dòng đầu tiên xác nhận phương thức là `publickey` đã được chấp nhận cho root users. Và nó cũng ghi lại địa chỉ ip/port `192.168.0.101:37384`.

**2. Thiết lập môi trường (PAM)**: cho thấy PAm đã tiếp nhận yêu cầu, tải các biến môi trường và thiết ljapa phiên làm việc cho root users.

**3. Tích hợp thêm `systemd`**: `systemd-logind` cho thấy nó đã đăng kí phiên làm việc với root users và được quản lý phiên đăng nhập này.


### 4. File log /var/log/boot.log

File `boot.log` chứa những thông tin liên quan đến quá trình khởi động của các tập lệnh khởi tạo hệ thống. Nếu hệ thống gặp các liên quan đến tắt máy không đúng cách, khởi động lại hoặc lỗi khởi động. Đây là file hữu ích để chúng ta có thể vào chẩn đoán sự cố, ngoài ra nó còn cung cấp rõ khung thời gian xảy ra sự cố.

**path**: `/var/log/boot.log`

***Mô phỏng lại hành vi trong file `/var/log/boot.log` - Startup - OK/Failed***

Ghi lại trạng thái của các dịch vụ trong quá trình hệ thống nạp. Log mô phỏng lại hành vi trên được ghi lại:

```
[ OK ] Started Show Plymouth Boot Screen.
[ OK ] Reached target Multi-User System.
 Failed to start Bluetooth service.
```
- [OK]: Dịch vụ khởi động thành công và systemd đã nhận được tín hiệu phản hồi.
- "": Một dịch vụ đẫ gặp lỗi trong quá trình khởi động lên.

### 5. File log /var/log/dmesg

Khi hệ thống khởi động các thông tin liên quan đến các thiết bị phần cứng và trình điều khiển của chúng được ghi lại ở đây. Vì kernel phát hiện các thiết bị phần cứng vật lý được liên kết trong quá trình khởi động, nó sẽ ghi lại trạng thái thiết bị, lỗi phần cứng và các thông báo khác. 

File log này giúp cho chúng ta phát hiện 1 thiết bị phần cứng nào đó không hoạt động thì sẽ bị ghi lại ở đây.

**path**: `/var/log/dmesg`

***Mô phỏng hành vi trong file `/var/log/dmesg` - Hardware error***

Ngoài việc thay dõi các thiết bị mới, thì `dmesg` còn là nơi quan trọng để xem các lỗi liên quan đến phần cứng, drivers hoặc 1 kết nối kém, log mô phỏng:

```
[101100.860034] usb 6-2: new full-speed USB device number 18 using uhci_hcd
[101100.980060] usb 6-2: device descriptor read/64, error -71
[101102.912093] usb usb6-port2: unable to enumerate USB device
```

- Phát hiện được 1 kết nối USB mới vừa được ghi nhận lại với mã số 18 `usb 6-2`.

- `error-71`: Thường chỉ ra lỗi giao thức phần cứng nghiêm trọng, có thể do thiết bị hỏng hoặc có thể cổng USB bị chập chờn về điện áp bên trong.

- `unable to enumerate`: Nhân Linux đã từ bỏ nỗ lực nhận diện sau nhiều lần thử thất bại khi cố gắng đọc thông tin của `usb` để thực hiện các hành động tải driver, đặt tên,...

### 6. File log /var/log/faillog

Trong file này sẽ chứa các thông tin người dùng dã đăng nhạp thất bại. Chúng ta có thể sử dụng lệnh `faillog` để hiển thị nội dung của file. Nó là 1 file log vô cùng hữu ích để chúng ta có thể dò cùng với file log `auth.log` xem những user nào đang cố gắng thực hiện đăng nhập trái phép vào hệ thống.

**path**: `/var/log/faillog`

***Mô phỏng hành vi được ghi lại trong file log `/var/log/faillog` - List of failed login***

Thay vì chúng ta phải xem file log(dạng nhị phân), thì chúng ta có thể dùng lệnh `faillog -a` để liệt kê tất cả các lần đăng nhập vào hệ thống bởi các users:

```
t0b1ra@tobiraNduy:~$ faillog -a
Login       Failures Maximum Latest                   On

root            0        0   01/01/70 08:00:00 +0800
daemon          0        0   01/01/70 08:00:00 +0800
bin             0        0   01/01/70 08:00:00 +0800
sys             0        0   01/01/70 08:00:00 +0800
sync            0        0   01/01/70 08:00:00 +0800
games           0        0   01/01/70 08:00:00 +0800
man             0        0   01/01/70 08:00:00 +0800
lp              0        0   01/01/70 08:00:00 +0800
mail            0        0   01/01/70 08:00:00 +0800
news            0        0   01/01/70 08:00:00 +0800
uucp            0        0   01/01/70 08:00:00 +0800
proxy           0        0   01/01/70 08:00:00 +0800
www-data        0        0   01/01/70 08:00:00 +0800
backup          0        0   01/01/70 08:00:00 +0800
list            0        0   01/01/70 08:00:00 +0800
irc             0        0   01/01/70 08:00:00 +0800
gnats           0        0   01/01/70 08:00:00 +0800
nobody          0        0   01/01/70 08:00:00 +0800
systemd-network       0        0   01/01/70 08:00:00 +0800
systemd-resolve       0        0   01/01/70 08:00:00 +0800
messagebus       0        0   01/01/70 08:00:00 +0800
systemd-timesync       0        0   01/01/70 08:00:00 +0800
syslog          0        0   01/01/70 08:00:00 +0800
_apt            0        0   01/01/70 08:00:00 +0800
uuidd           0        0   01/01/70 08:00:00 +0800
tcpdump         0        0   01/01/70 08:00:00 +0800
t0b1ra          0        0   01/01/70 08:00:00 +0800
landscape       0        0   01/01/70 08:00:00 +0800
dnsmasq         0        0   01/01/70 08:00:00 +0800
t0b1ra@tobiraNduy:~$
```
```
Login    Failures Maximum Latest                   On
root          0      0   01/01/70 05:30:00 +0530
admin         5      0   02/01/26 14:10:00 +0700
```

Ở đây mình lấy 2 ví dụ, ví dụ 1 là dùng trên chính hệ thống Linux của máy mình, để xem các hành vi được ghi lại bởi hệ thống nhưng không có lần đăng nhập thất bại nào, ví dụ 2 là để mô phỏng 1 tình huống thực tế khi mà:

- User `admin` đã thực hiện 5 lần đăng nhập thất bại vào hệ thống liên tiếp vào ngày 2/1/26 lúc `14:10:00`. Điều này có thể báo hiệu người này có thể đang cố gắng 1 phiên đăng nhập bất hợp pháp.

### 7. File log /var/log/cron

Nơi lưu trữ tất cả các thông tin liên quan đến Crond,(trình làm việc schedule dựa vào thời gian), ví dụ như khi tiến trình nền `cron` khởi tạo 1 công việc, các thông báo lỗi liên quan,.. Bất cứ khi nào cron thực hiện 1 task or proccess bên trong `crontab` đã thiết lập, thì hệ thóng sẽ ghi lại các log trên và lưu bên trong `/var/log/cron`.

**path:** `/var/log/cron`

***Mô phỏng hành vi được ghi lại bên trong file log `/var/log/cron` - Execute Cmd***

```
Mar 29 16:15:01 data-processing CRON[12624]: (dataproc) CMD (/home/data-pipeline.py)
```

Đây là 1 log mô phỏng lại hành vi, thực thi 1 tiến trình `schedule task` đã được thiết lập bên trong `crontab`, phân tích chi tiết hơn về tiến trình đã được ghi lại trong file log `/cron`:

- **Thời gian nó được ghi lại**: Ngày 29/3 vào lúc 16:15:01 job trên bắt đầu thực thi.

- **data-processing**: tên của máy chủ, nơi mà task này được thực hiện.

- `CRON[12624]`: Tên dịch vụ (CRON) và PID(Process ID - 12624). Mỗi lần chạy, cron sẽ tạo ra một PID khác.

- `(dataproc)`: Tên user sở hữu tác vụ này. Lệnh này được chạy dưới quyền của người dùng `dataproc`.

- `CMD(/home/data-pipeline.py)`: Mở cmd và thực thi 1 script đã được chuẩn bị sẳn.

### 8. File log /var/log/yum.log

Chứa thông tin được ghi lại khi gói được cài đặt bằng [yum](https://vietnix.vn/lenh-yum-trong-linux/). Thông qua file log này giúp cho chúng ta có thể theo dõi việc cài đặt các thành phần hệ thống và gói phần mềm. Kiểm tra các thông tin được ghi lại ở đây để xem một gói đã được cài đặt chính xác hay chưa. Từ đó có thể khắc phục các sự cố về các package chưa được cài đặt hoặc sự cố về phần mềm.

**path:** `/var/log/yum.log`

***Mô phỏng hành vi được ghi lại bên trong `/var/log/yum.log` - Log Management Package***

Bên trong file chứa lịch sử cài đặt, cập nhật hoặc gỡ bỏ phần mềm trên các hệ thống dùm YUM để thực hiện các tác vụ trên, log mô phỏng:

```
Feb 06 10:38:35 Erased: nfs-utils
Feb 06 10:39:36 Installed: tree-1.6.0-10.el7.x86_64
Feb 06 10:45:12 Updated: kernel-3.10.0-1160.el7.x86_64
```

Phân tích qua về log:

- Bên trong log sẽ chứa thời gian cụ thể về những hành động trong hệ thống được thực thi bởi `YUM`.

- Thực hiện tải xuống `Installed: tree-1.6.0-10.el7.x86_64` gói `tree` là 1 công cụ nhỏ để dễ dàng quan sát cấu trúc thư mục khi làm việc với terminal

- Xóa đi `Erased: nfs-utils`.

- Thực hiện nâng cấp hệ thống `kernel`.

### 9. File log /var/log/maillog hoặc /var/log/mail.log

File log này lưu trữ các thông tin từ máy chủ mail đang chạy trên hệ thống bao gồm các thông tin về `postfix`, `smtpd`, `MailScanner`, `SpamAssassain` hoặc bất kì dịch vụ liên quan đến email nào khác. Nếu chúng ta cần các thông tin về cài đặt thiết lập cho `mail server` hoặc thông tin ghi lại tất cả các email đã được gửi hoặc nhận trong 1 khoảng thời gian cụ thể, kiểm tra xem lần gửi thành công/thất bại,...

**path**: `/var/log/mail.log`

***Mô phỏng hành vi trong log `/var/log/mail.log` - Log Mail Server***

Ghi lại quá trình chuyển phát thư của các daemon như `Postfix`.Log mô phỏng:

```
Aug 2 17:36:16 mail-srv postfix/smtp: 12A95860867: to=<user@example.com>, relay=mail.isp.com[1.2.3.4]:25, delay=0.5, dsn=2.0.0, status=sent (250 2.0.0 OK)
```

- **status=sent**: Thư đã được mail server nhận diện dạng mail được gửi đi, và thư dã được máy chủ tiếp theo (relay) chấp nhận thành công.

- `dsn=2.0.0 && (250 2.0.0 OK)` cho thấy rằng trạng thái gửi đi mail đã thành công.

### 10. File log /var/log/httpd/

Trong log này sẽ lưu trữ những thông tin rất hữu ích vì những thông tin nó lưu trữ liên quan đến các file `error.log` và `access.log` của Apache. Các file `error.log` chứa tất cả các lỗi gặp phải `httpd`. Những lỗi này bao gồm các vấn đề về bộ nhớ các lỗi liên quan đến hệ thống, truy cập trái phép vào tài nguyên mà clinet không được phép truy cập. `access.log` chứa 1 bản ghi của tất cả các yêu cầu nhận được qua HTTP. Giúp chúng ta theo dõi các địa chỉ IP và ID của người dùng với hành vi hợp pháp or không hợp pháp đang hành động với server.

**path:** `/var/log/httpd/`

***Mô phỏng hành vi trong log `/var/log/httpd/error.log` -- Unauthorized access to resource web server***

Khác với access log, error log ghi lại các sự cố cấu hình hoặc từ chối truy cập.Log mô phỏng:

```
[authz_core:error][pid 6587][client 127.0.0.1:38873] AH01630: client denied by server configuration: /var/www/html/admin
```

Ở đây chúng ta sẽ thấy được ip/port của client `127.0.0.1:38873` đã thực hiện 1 truy cập trái phép vào cấu hình của server, cụ thể hơn client đã cố gắng truy cập vào trang `/var/www/html/admin` nhưng vốn dĩ họ không có quyền truy cập vào, hệ thống đã thấy người dùng cố gắng truy cập trái phép và đã ghi lại ip của người dùng thực hiện hành động trên và lưu vào file `error.log`.

### 10. File log /var/log/mysqld.log or /var/log/mysql.log

File log `/mysql.log` chứa tất cả các thông tin liên quan đến cơ sở dữ liệu MySQL của người dùng. Như việc bắt đầu, dừng, khởi động lại MySQL daemon `mysqld`.  Sử dụng file log này để ấc định các vấn đề trong khi MySQL bắt đầu, tạm dừng, và trong quá trình hoạt động. Và có 1 điều quan trọng là tùy thuộc vào bản phân phối của Linux mà người dùng chạy, thì file log này sẽ có tên khác nhau:

- Với bản phân phối Debian/Ubuntu thì sẽ là `/var/log/mysql.log`.
- Đối với hệ thống RedHat, CentOS, Fedora và các hệ thống dựa trên RedHat khác sử dụng : `/var/log/mysqld.log`.

***Mô phỏng hành vi trong log `/var/log/mysql.log` - kết nối lạ từ ip vào database***

```
2026-02-02T10:15:01.123456Z   45 Connect   root@localhost on  using Socket
2026-02-02T10:15:05.654321Z   45 Query     SELECT @@version, @@version_comment
2026-02-02T10:15:10.223344Z   45 Query     SHOW DATABASES
2026-02-02T10:15:15.887766Z   45 Query     USE customer_db
2026-02-02T10:15:20.112233Z   45 Query     SHOW TABLES
2026-02-02T10:15:30.445566Z   45 Query     SELECT * FROM users WHERE admin = 1
2026-02-02T10:16:00.998877Z   45 Quit
```

Phân tích hành vi này:

**1. (Connect vào MySQL)**: Người dùng root đăng nhập thành công qua Socket với mã kết nối là 45, vào lúc `10:15:01`.

**2. (Thăm do hệ thống)**: Ngay sau đó, ghi nhận người dùng này thực hiện lệnh `SELECT @@version`.Đây là hành vi điển hình để kiểm tra phiên bản MySQL nhằm tìm kiếm các lỗ hổng (vulnerability) đã biết cho phiên bản đó.

**3. (Liệt kê ra các tài nguyên trên hệ thống):** Lệnh `SHOW DATABASE` cho thấy họ đang tìm kiếm xem trong server này có những thông tin giá trị hay thông tin credential của người dùng không.

**4. (Xâm nhập vào mục tiêu đã được lựa chọn):** Họ chọn database `customer_db` và liệt kê các bảng (SHOW TABLES).

**5. (Khai thác dữ liệu):** Hành vi nguy hiểm nhất xuất hiện lúc 10:15:30: Họ truy vấn toàn bộ thông tin từ bảng users nhưng lọc những người có quyền admin. Đây là dấu hiệu của việc đánh cắp thông tin tài khoản quản trị.

**6. (Quit)**: Sau khi có được thông tin cần tìm thì họ đã thoát khỏi phiên đăng nhập hiện tại.
