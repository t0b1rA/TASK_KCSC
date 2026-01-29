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

## Every file system in Linux

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




## Linux File Hierarchy Structure 

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
