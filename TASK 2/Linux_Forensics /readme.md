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

C**Syntax**: `xxd <optione> <ten_file>`

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

**Syntax: `file <ten_file>`

Ví dụ, cụ thể:
```
┌──(nhduydeptrai㉿tobi)-[~/Pico_CTF/St3g0]
└─$ file pico.flag.jpg                                             
pico.flag.jpg: PNG image data, 585 x 172, 8-bit/color RGBA, non-interlaced                                                                         
```

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

Nhưng có một cách để attacker có thể sử dụng lệnh `echo` để thực thi một lệnh, hắn sẽ chèn lệnh đó vào dấu `$()`, lúc này trình thông dịch sẽ tạm dừng `echo` và nó thực thi lệnh bên trong `$()` trước, ví dụ:

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

