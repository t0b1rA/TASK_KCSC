# Linux Fundamentals 1

## Task 1: Introduction

Ở task đầu tiên này chúng ta được giới thiệu sơ lược về hệ điều hành Linux, khá là phổ biến trên thế giới với thiết bị android, siêu máy tính, home applications,...

- Chúng ta tập làm quen với cách sử dụng câu lệnh để tương tác với Linux.
- Một số câu lệnh cần thiết cho việc tương tác với file system.
- Tìm kiếm các file và các toán tử của **shell**.

<img width="770" height="197" alt="image" src="https://github.com/user-attachments/assets/0469d1f7-05ea-4bee-8c64-17e966063ad0" />

Và task đầu này chúng ta cũng không cần phải trả lời câu hỏi.

## Task 2: A bit of Background on Linux 

**Linux** thực chất là một thuật ngữ chung cho rất nhiều những hệ điều hành dựa trên UNIX(hệ điều hành khác). Bởi vì Linux là một mã nguồn mở nên Linux có đa dạng các phiên bản phù hợp với cấu hình và kích thước phù hợp với những hệ thống được sử dụng.

### Research: What year was the first release of a Linux operating system

Năm 1991 hệ điều hành Linux đầu tiên được phát hành `Linux Kernel 0.01`.

<img width="755" height="170" alt="image" src="https://github.com/user-attachments/assets/dd5f6213-1e0a-452b-84cd-f072f942ce0c" />

## Task 3: Interacting with your first Linux Machine

<img width="792" height="781" alt="image" src="https://github.com/user-attachments/assets/da1822a2-6215-405f-a105-185ab586ac27" />

Câu này web cho chúng ta 1 máy ảo, và không cần trả lời câu hỏi.

### Task 4: Running Your First few Commands

Ở task này chúng ta được giới thiệu về hai lệnh khá phổ biến của Linux là lệnh `echo` và lệnh `whoami` rất hữu dụng trong Linux.

- `echo`: là lệnh giúp cho người dùng có thể in ra một chuỗi trên màn hình terminal, hoặc có thể giúp ghi đè vào 1 file văn bản cũ thành file văn bản mới bằng ký hiệu `>`, or ghi nối tiếp vào cuối file bằng ký hiệu `>>`.

- `whoami`: là lệnh giúp người dùng biết được tên của user đang thao tác với terminal hiện tại, và quyền của user đó

### If we wanted to output the text "TryHackMe", what would our command be?

<img width="768" height="136" alt="image" src="https://github.com/user-attachments/assets/923cc831-93de-4965-81f6-cb1bef91c4be" />

### What is the username of who you're logged in as on your deployed Linux machine?

Sử dụng lệnh `whoami`.

<img width="710" height="119" alt="image" src="https://github.com/user-attachments/assets/326e1e3e-6157-4371-9041-e33040aa7991" />

<img width="402" height="211" alt="image" src="https://github.com/user-attachments/assets/8ccfa82e-7671-4c9d-995e-d353e6bc44fa" />

## Task 5: Interacting With the Filesystem!

Ở task này chúng ta tiếp tục được giới thiệu với 4 command khác thông dụng trong Linux đó là:

- Lệnh `ls`: cho phép người dùng liệt kê ra các file và folder bên trong 1 folder cụ thể.

<img width="620" height="108" alt="image" src="https://github.com/user-attachments/assets/7af9e082-3f06-4a4e-b974-dbfddc2c362e" />


- Lệnh `cd`: cho phép người dùng có thể điều hướng đến các thư mục khác.

<img width="603" height="138" alt="image" src="https://github.com/user-attachments/assets/e4782783-1728-4ee9-b968-60e152a699e6" />

- Lệnh `cat`: cho phép chúng ta đọc được nội dung bên trong của 1 file.

<img width="537" height="73" alt="image" src="https://github.com/user-attachments/assets/e4768114-8399-4cb0-a425-fcf42d08f569" />

- Lệnh `pwd`: cho phép in ra đường dẫn cụ thể đến vị trí hiện tại mà người dùng đang đứng trong thư mục đang làm việc hiện tại. Đặc biệt là `pwd` sẽ tính từ gốc của file hệ thống cho đến vị trí đứng hiện tại.

<img width="479" height="71" alt="image" src="https://github.com/user-attachments/assets/161fbdc7-2a3d-4ee8-9393-8007148fb4a7" />

### On the Linux machine that you deploy, how many folders are there?

<img width="633" height="49" alt="image" src="https://github.com/user-attachments/assets/caded7f2-fa15-4505-acdb-5be1c0f01575" />

<img width="392" height="189" alt="image" src="https://github.com/user-attachments/assets/27ee1ce2-0490-48ed-9e59-86ed7888e425" />

Có 4 folder trong thư mục `home/`.

### Which directory contains a file? 

Chỉ có `folder4` là có chứa 1 file `note.txt` còn lại đều là thư mục rỗng.

<img width="418" height="56" alt="image" src="https://github.com/user-attachments/assets/29d71a9b-2dee-4837-b363-6098aac3d2aa" />

<img width="369" height="175" alt="image" src="https://github.com/user-attachments/assets/61d55026-c222-4ea8-83d3-4cf976337c8a" />

### What is the contents of this file?

```
tryhackme@linux1:~/folder4$ cat note.txt 
Hello World!
```
<img width="378" height="162" alt="image" src="https://github.com/user-attachments/assets/87d44d7c-8086-4f22-af32-9b344237ac01" />

### Use the cd command to navigate to this file and find out the new current working directory. What is the path?

```
tryhackme@linux1:~/folder4$ pwd 
/home/tryhackme/folder4
```
<img width="395" height="223" alt="image" src="https://github.com/user-attachments/assets/fa54f923-43d7-4b5d-a5c3-95b8cca2807e" />

### Task 6: Searching for Files

Ở task này chúng ta được giới thiệu về một cách để tìm kiếm các file trong Linux một cách hiệu quả, bằng lệnh `find`

- Lệnh `find` cho phép người dùng tìm kiếm các file theo option được chọn (có thể là name, size,...).

- `find -name <ten_file>` giúp chúng ta đưa ra được 1 đường dẫn đầy đủ tới file đó, nếu nó có tồn tại trong hệ thống.

- `find -name <*.txt>`: cho phép chúng ta có thể tìm được đường dẫn đầy đủ của tất cả các file có đuôi `.txt` trong hệ thống.

```
tryhackme@linux1:~$ find -name *.txt
./folder1/passwords.txt
./Documents/todo.txt
tryhackme@linux1:~$
```

Ngoài ra chúng ta còn được giới thiệu về lệnh `grep`. Lệnh `grep` cho phép chúng ta tìm kiếm nội dung của file với 1 giá trị cụ thể mà chúng ta cần.

```
tryhackme@linux1:~$ grep "81.143.211.90" access.log
81.143.211.90 - - [25/Mar/2021:11:17 + 0000] "GET / HTTP/1.1" 200 417 "-" "Mozilla/5.0 (Linux; Android 7.0; Moto G(4))"
tryhackme@linux1:~$
```

> Lệnh `wc` cho phép chúng ta đếm có tổng cổng bao nhiêu mục bên trong 1 file.

Ngoài ra chúng ta cũng có thể tìm kiếm đệ quy, tức là `moi` tất cả các thư mục có chứa giá trị chúng ta tìm bên trong 1 thư mục gốc lớn.
Bằng option `-R recursive` 

```
grep -R "PRETTY_NAME" /etc/
grep: /etc/sudoers: Permission denied
/etc/os-release:PRETTY_NAME="Ubuntu"
```
### Use grep on "access.log" to find the flag that has a prefix of "THM". What is the flag? Note: The "access.log" file is located in the "/home/tryhackme/" directory.

Ở câu này chúng ta cần tìm 1 flag với giá trị là `THM`, và chúng ta biết bên trong file `.log` có rất nhiều mục nhỏ bên trong, việc cat nó sẽ rất lâu, dùng `grep` để tìm kiếm giá trị THM bên trong file.

<img width="1196" height="122" alt="image" src="https://github.com/user-attachments/assets/89763ced-a1c0-487d-a3d7-34fee079af34" />

## Task 7: An Introduction to Shell Operators

| Symbol/Operator | Mô tả |
| --- | --- |
| & | Toán tử này cho phép chạy 1 lệnh bên trong nền của terminal |
| && | Toán tử này cho phép kết hợp nhiều lệnh 1 lúc trên 1 dòng |
| > | Toán tử này cho phép ghi output vào 1 file cụ thể nào đó (thay đổi nội dung file cũ thành cái output mới) |
| >> | Toán tử này cho phép ghi nối vào 1 file cũ ở phần dưới cùng |

**Operator "&"**

Cho phép chúng ta chạy một lệnh trong nền của terminal, để có thể tiết kiệm thời gian nếu việc chạy lệnh đó quá lâu, Ví dụ:

```
t0b1ra@tobiraNduy:~$ ping google.com > /dev/null &
[1] 1343
t0b1ra@tobiraNduy:~$ jobs
[1]+  Running                 ping google.com > /dev/null &
```

Chúng ta thực hiện `ping` đến **google.com** và xuất output của nó vào `/dev/null` để cho màn hình terminal trông bớt loạn hơn bởi process ping đang chạy. Đặc biệt với mỗi lệnh với `&` đều sẽ có 1 PID cho biết số proccess đang chạy.
> Chúng ta có thể kết hợp với lệnh `jobs` để biết được tiến trình đang chạy nền là gì.


**Operating "&&"**

Cho phép thực hiện nhiều command 1 lúc trên 1 dòng:

```
t0b1ra@tobiraNduy:~$ cat flag1.txt && cat flag2.txt
flag{Hello_world}
flag{World_hello}
```

**Operating ">"**

Lệnh này cho phép ghi output vào 1 file và thay đổi toàn bộ nội dung file cũ:

```
t0b1ra@tobiraNduy:~$ echo "flag{Hello_world_new}" > flag1.txt
t0b1ra@tobiraNduy:~$ cat flag1.txt
flag{Hello_world_new}
```

**Operating ">>"**

Lệnh này cho phép ghi output nối tiếp vào phần cuối cùng của 1 file:

```
t0b1ra@tobiraNduy:~$ echo "flag{Hello_world_new_er}" >> flag1.txt
t0b1ra@tobiraNduy:~$ cat flag1.txt
flag{Hello_world_new}
flag{Hello_world_new_er}
```

### If we wanted to run a command in the background, what operator would we want to use?

<img width="1121" height="128" alt="image" src="https://github.com/user-attachments/assets/41ea878e-b72b-46ec-b11b-eace49ba05b2" />

### If I wanted to replace the contents of a file named "passwords" with the word "password123", what would my command be?

Có replace nên ta sẽ sử dụng toán tử `>` để ghi đè lên nội dung cũ.

<img width="1150" height="115" alt="image" src="https://github.com/user-attachments/assets/09520ae1-5c38-4875-a065-c11ae02ec446" />

### Now if I wanted to add "tryhackme" to this file named "passwords" but also keep "passwords123", what would my command be

Add thì phải sử dụng `>>` để ghi nối tiếp vào phần cuối của file.

<img width="1111" height="127" alt="image" src="https://github.com/user-attachments/assets/1d7e4cb1-92c0-45aa-a17d-b78b766d692d" />


# Linux Fundamental 2

## Task 1: Introduction to Flags and Switches

Task này thì chúng ta được giới thiệu về các arguments được cung cấp cho các commands, để người dùng có thể sử dụng các lệnh trở nên hiệu quả hơn.

Giả sử với lệnh `ls`, khi chúng ta thông thường chỉ sử dụng `ls` or `l` đơn lẻ để xem bên trong 1 thư mục có những fild hay folder khác nào, nhưng đối với các hidden file - (file với dấu chấm phía trước `.hiddenfile`), đối với file này chúng ta cần sử dụng option `ls -a` để liệt kê tất cả gồm hidden file để có cái nhìn tổng quan nhất.

- Khi chúng ta chỉ dùng `ls`:

<img width="1335" height="150" alt="image" src="https://github.com/user-attachments/assets/c79c63de-4e74-41f6-8288-d74d6e0ef397" />

- Khi chúng ta sử dụng thêm option `-a` cho lệnh `ls`:

<img width="1476" height="218" alt="image" src="https://github.com/user-attachments/assets/7fe77cf2-abed-457b-b737-e45aca3f73a4" />

*Lúc này chúng ta mới thấy được 1 file flag bị ẩn bằng cách tạo hidden file có dấu `.` đằng trước*.

Ngoài ra chúng ta còn có thể dùng lệnh `man` - lệnh này giúp hiển thị một trang dễ nhìn hơn cho các command có các option đi kèm theo như `ls, mv, rm,...` sử dụng lệnh này sẽ liệt kê ra 1 trang hướng dẫn rõ ràng hơn là lệnh `--help / -h`.

<img width="1479" height="745" alt="image" src="https://github.com/user-attachments/assets/8160faee-37a1-4079-9814-4fe4a7ce3941" />

<img width="1478" height="638" alt="image" src="https://github.com/user-attachments/assets/f43e5c7d-5a20-4d82-b149-53c816fa29de" />


### What directional arrow key would we use to navigate down the manual page?

Dùng phím mũi tên xuống (- down)

<img width="774" height="129" alt="image" src="https://github.com/user-attachments/assets/1f8a8982-972e-42f3-8738-44714be1d1c2" />

### What flag would we use to display the output in a "human-readable" way?

Thông thường chúng ta có thể sử dụng option `-h` hoặc là `--help` để liệt kê ra hướng dẫn cho một command dưới dạng người đọc được.

## Task 4: Filesystem Interaction Continued

Trong task này chúng ta sẽ được học cách làm việc với các file và thư mục trong filesystem bên trong Linux như:
- Tạo ra 1 file hoặc folder.

- Di chuyển file và folder đó.

- Xóa đi file hoặc folder.

| Command | Full name | Purpose |
| --- | --- | --- |
| touch | touch | tạo ra 1 file trống không có gì cả |
| mkdir | make directory | tạo ra 1 thư mục trống |
| cp | copy | sao chép 1 file hoặc 1 thư mục |
| mv | move | giúp đổi tên file hoặc thư mục, hoặc có thể dùng để thay đổi vị trí của file hoặc thư mục trong filesystem |
| rm | remove | xóa đi 1 file hoặc thư mục |
| file | file | xác định được file đó là file gì |



**Tạo ra các file và thư mục (touch, mkdir)**

Lệnh `touch` giúp người dùng tạo ra một file trống bên trong, chúng ta nên sử dụng thêm lệnh `echo` hoặc `nano` để có thể điền thêm dữ liệu vào cho file đó. Và lệnh `mkdir` giúp cho người dùng tạo ra thư mục bên trong:

<img width="1448" height="191" alt="image" src="https://github.com/user-attachments/assets/57d4c35b-bdd5-4269-9ab9-e6e218759c71" />

```
t0b1ra@tobiraNduy:~/file1$ touch file.txt
t0b1ra@tobiraNduy:~/file1$ ls
file.txt
```
<img width="1493" height="760" alt="image" src="https://github.com/user-attachments/assets/a65085e7-9e98-42cf-9399-b8bddbc792de" />

Và 1 file được tạo ra luôn là 1 file trống.

```
t0b1ra@tobiraNduy:~/file1$ nano file.txt
t0b1ra@tobiraNduy:~/file1$ cat file.txt
flag in side file
```
Và cũng có thể sử dụng lệnh `nano` hoặc lệnh `echo` để có thể viết thêm thông tin cho file trống.

**Lệnh remove files và folders (rm)**

Dùng lệnh `rm <ten_file>` để có thể xóa đi 1 file và lệnh `rm -R <ten_folder>` để thực hiện xóa đệ quy một folder 

`rm <ten_file>`

```
t0b1ra@tobiraNduy:~/file1$ ls
1.4  file.txt  file1.1  file1.2  file1.3
t0b1ra@tobiraNduy:~/file1$ rm file.txt
t0b1ra@tobiraNduy:~/file1$ ls
1.4  file1.1  file1.2  file1.3
```

`rm -R <folder>`

<img width="1369" height="175" alt="image" src="https://github.com/user-attachments/assets/395747af-30a3-4985-a5d7-5be0eae9b2a4" />

**Copying và Moving file / folder**

- Lệnh `cp`:

Chúng ta có thể sử dụng lệnh `cp` để copy toàn bộ nội dung của 1 file và tạo thành 1 file khác:
**syntax** : `cp <file_duoc_copy> <file_da_copy>`
```
t0b1ra@tobiraNduy:~$ cp file.txt file2.txt
t0b1ra@tobiraNduy:~$ cat file.txt
flag{copy_file}
t0b1ra@tobiraNduy:~$ cat file2.txt
flag{copy_file}
```
- Lệnh `mv`, chúng ta có thể sử dụng cho việc đổi tên 1 file or di chuyển 1 file sang thư mục khác.

```
t0b1ra@tobiraNduy:~$ mv file2.txt file2_sau_khi_doi_ten.txt
t0b1ra@tobiraNduy:~$ cat file2_sau_khi_doi_ten.txt
flag{copy_file}
```

Nội dung file sẽ được giữ nguyên, chỉ thay đổi tên của file.

Hoặc chúng ta cũng có thể thay đổi vị trí của toàn bộ file đó đi sang thư mục khác.
<img width="1482" height="481" alt="image" src="https://github.com/user-attachments/assets/6f5ab21e-a3c1-42d7-8578-30650916da4c" />


**Determine File type**

Lệnh `file` giúp cho chúng ta có thể xác định một file đó là loại file gì, bằng cách dùng lệnh `file <ten_file>`.

```
t0b1ra@tobiraNduy:~/folder_new/folder_new_2$ file file2_sau_khi_doi_ten.txt
file2_sau_khi_doi_ten.txt: ASCII text
t0b1ra@tobiraNduy:~/folder_new/folder_new_2$
```

### Task 5 Permissions 101

Trong task này mình sẽ học về một số người dùng chỉ được thực hiện 1 vài hành động cho 1 vài file hoặc folder nhất định trong hệ thống. Chính là các quyền của các user.

Trong filesystem Linux một file hoặc 1 thư mục có thể có 1 số những đặc trưng xác định cả hành động được cho phép của file và những user hay group có khả năng thực hiện những hành động, như:

- Đọc

- Viết

- Thực thi

#### Phân quyền trong Linux

Trong Linux, thì một người dùng sở hữu 1 file đó, nhưng khi các quyền được thiết lập cho các user khác nữa, thì sẽ có 1 group user khác cũng sở hữu 1 bộ quyền lên tập tin đó giống hoặc khác nhau, Nhưng không liên quan đến chủ sở hữu. 

Ví dụ: 1 chủ sở hữu 1 file quan trọng trong cho các khách hàng, user này có khả năng chỉnh sửa, xem, xóa file này.  Nhưng khi 1 khách hàng muốn đăng tải hoặc chỉnh sửa lại dùng chung 1 bộ quyền với chủ sở hữu, thì sẽ có thể gây ảnh hưởng đến khách hàng khác. 

- Thông qua đó mới có 1 bộ quyền cho những user nhất định, để không nắm toàn quyền như chủ sở hữu.

**Switching Between Users**

Người dùng có thể sử dụng lệnh `su` cho việc thay đổi tài khoản, nếu họ có `passwd`, hoặc nếu không có bạn bắt buộc cần là 1 root user or 1 sử dụng quyền root thông qua `sudo` - Cần phải được root user thêm vào 1 groups có quyền `sudo`.

**Syntax switch user:** `su -l (--login) <ten_user>`

```
tryhackme@linux2:~$ su user2
Password:
user2@linux2:/home/tryhackme$
```

Sau khi chuyển đổi tài khoản, thì phiên làm việc sẽ có sự thay đổi từ người dùng `tryhackme` qua người dùng `user2`:

```
tryhackme@linux2:~$ su -l user2
Password:
user2@linux2:~$ pwd
user2@:/home/user2$
```

#### File Permission in Numeric Format

Chúng ta cũng cần phải tìm hiểu hơn về cách Linux phân quyền của các file và folder cho những user khác, như là quyền viết, đọc, và thực thi được hiển thị dưới dạng:

`rwxrwxrwx`

Format này được chia thành 3 lớp như sau:
|Section | Applies to | Example |
| --- | --- | --- |
| First 3 | Owner | rwx | 
| Next 3 | Group | rwx |
| Last 3 | Others | rwx |

Và mỗi chữ cái bên trong `rwx` đại diện cho 1 quyền cụ thể:

- `r`: read 
- `w`: write
- `x`: execute

Thông thường khi gán quyền cho 1 file hoặc folder thì chúng ta thường sử dụng những con số như `777`, `766`, thì các con số này đều đại diện cho những quyền mà user đó có với 1 file cụ thể.

| Permissions | Value |
| --- | --- |
| Read (r) | 4 |
| Write (w) | 2 |
| Execute (x) | 1 |

Khi chúng ta gán quyền cho 1 nhóm thì chúng ta thực hiện tính toán các con số này trong 1 nhóm để tạo nên quyền cho các user với file/folder cụ thể.


| Groups | Permissions | Calculation | Value |
| --- | --- | --- | --- |
| Owner | rwx | 4 + 2 + 1 | 7 |
| Groups | rwx | 4 + 2 + 1 | 7 |
| Others | rwx | 4 + 2 + 1 | 7 |

Với 1 file được cấp full quyền cho mọi người dùng sẽ có giá trị là `rwxrwxrwx = 777`

Ví dụ dễ hình dung hơn:

| Symbolic | Numeric | Meaning |
| rwxr-xr-x | 755 | Người dùng chủ sở hữu có mọi quyền, còn những user khác chỉ có thể đọc và thực thi |
| rw-r-r-- | 644 | Chủ sỡ hữu có quyền đọc và ghi, còn những user khác chỉ có quyền đọc |
| rwx------ | 700 | Chỉ có chủ sỡ hữu | 

### On the deployable machine, who is the owner of "important"?

<img width="828" height="169" alt="image" src="https://github.com/user-attachments/assets/e60fc033-1520-4353-94e2-b396fc8da669" />

Ta dùng lệnh `ls -lh` để kiểm tra quyền của tất cả các file và folder bên trong home, ở đây chúng ta thấy được file important có owner là `user2` ở cột kế bên cột phân quyền.

<img width="782" height="135" alt="image" src="https://github.com/user-attachments/assets/27f79ce7-03bd-4d38-8b9f-fae6dd704699" />

### What would the command be to switch to the user "user2"?

Để chúng ta có thể chuyển đổi tài khoản sang user2, chúng ta có thể sử dụng lệnh `su user2`.

<img width="775" height="125" alt="image" src="https://github.com/user-attachments/assets/165a0245-ff9a-4cd8-b20f-353c29f45831" />

### Output the contents of "important", what is the flag?

Bởi vì file `important` có quyền read cho tất cả các user nên chúng ta có thể đọc được nội dung bên trong file important mà không phải chuyển đổi người dùng:

```
tryhackme@linux2:~$ cat important 
THM{SU_USER2}
tryhackme@linux2:~$ 
```

Dùng lệnh cat để đọc được nội dung bên trong của file.

## Task 6: Common Directories

Trong task này chúng ta sẽ học thêm về 1 vài thư mục phổ biến và quan trọng bên trong `/` directory:

**/etc**

Thư mục root này là 1 trong những thư mục root quan trọng nhất trong hệ thống, nó lưu trữ những file cấu hình hệ thống máy tính, và các shell script giúp cho hệ thống có thể startup, các file chứa danh sách những quyền được sudo của user và groups trong hệ thống.

Như trong thư mục `/etc` chúng ta có 2 file là `passwd` và `shadow`:
- `passwd`: Lưu trữ thông tin của tất cả người dùng trong hệ thống, và mọi người đều có khả năng đọc được nội dung của file này.
- `shadow`: Lưu trữ cách quản lý mật khẩu của người dùng dưới dạng mã hash, và ngày thay đổi mật khẩu của tất cả người dùng, và tên của người dùng đó.

**/var**

Thư mục /var cho lưu trữ những dữ liệu của các ứng dụng và dịch vụ gần đây được truy cập và được modify bởi người dùng. Ví dụ, 1 file log được chạy trong service hoặc application thì sẽ được viết bên trong `/var/log`, hoặc dữ liệu khác không liên quand dến 1 người dùng cụ thể.

**/root**

Thư mục /root này giống như một thư mục `/home` của người dùng `root`. Những người dùng không có quyền root thì sẽ không thể truy cập vào được thư mục này, thư mục này chỉ cho phép mỗi người dùng `root` lưu trữ các file và folder của họ.

**/tmp**

File temp này được sử dụng để lưu trữ những file mà người dùng gần đây sử dụng nó sẽ tạo ra 1 file temp để backup nằm trong đây, và khi nào người dùng ngưng sử dụng ứng dụng hoặc dịch vụ đó, or người dùng shutdown máy thì các file này sẽ bị xóa. Bởi vì đây là 1 file được lưu trên RAM nên nó sẽ biến mất khi máy được tắt đi.

### What is the directory path that would we expect logs to be stored in?

Ở đây em biết được rằng là thư mục log của hệ thống Linux, sẽ được lưu trữ bên trong thư mục `/var` của Linux đây là thư mục lưu trữ dữ liệu của những file hoặc folder được sử dụng thường xuyên gần đây và cũng đồng thời có file log bên trong.

<img width="679" height="563" alt="image" src="https://github.com/user-attachments/assets/fc58322c-473b-45e0-8522-2d729e737ac9" />

<img width="811" height="137" alt="image" src="https://github.com/user-attachments/assets/4b3e16eb-d968-402a-abb0-db550036a0a1" />

### What root directory is similar to how RAM on a computer works?

Trong Linux có chúng ta có thư mục `/tmp` dùng lưu các file liên quan đến các ứng dụng hoặc dịch vụ hiện tại đang chạy trong máy tính, nói nó giống RAM là bởi vì khi là nó chỉ lưu các file này tạm thời, khi máy tính tắt nguồn, hoặc bị sập thì những file bên trong thư mục `/tmp` sẽ biến mất, như những dữ liệu được lưu trong RAM sẽ biến mất.

### Name the home directory of the root user 

Trong Linux thì thư mục `/home` của root user chính là thư mục `/root` chỉ có user với đặc quyền root mới có thể truy cập vào được hoặc là root user.

<img width="826" height="123" alt="image" src="https://github.com/user-attachments/assets/ea234308-32de-4032-9188-41a4032eef44" />


# Linux Fundamentals 3

Ở đây 2 task đầu vẫn là introduction về những gì chúng ta học hôm nay về các kĩ năng quản lí các gói, tự động hóa và nhật ký của dịch vụ và ứng dụng ở task 1 và task 2 là hướng dẫn cách dùng ssh truy cập vào Linux machine.

### Task 3: Terminal Text Editors

Task này, mình sẽ được giới thiệu về các công cụ chỉnh sửa văn bản bên trong Linux khá phổ biến, là:

- `nano`: công cụ được tích hợp sẳn trong hầu hết mọi phiên bản của Linux, dùng để chỉnh sửa văn bản cực kì phổ biến. Với **syntax**: `nano <file_name>`. Sau khi mà chúng ta nhấn enter, thì nó sẽ đưa chúng ta sang giao diện 1 trang trống, và cho phép chúng ta thực hiện chỉnh sửa nó.

<img width="926" height="596" alt="image" src="https://github.com/user-attachments/assets/52a0e64b-9392-46cc-b510-1ddd6be33ae7" />

- Bên cạnh đó `nano` còn có 1 số tính năng như:  
  - Tìm kiếm văn bản.
  
  - Dán và sao chép.
  
  - Nhảy đến số dòng nhất định trong văn bản.
  
  - Tìm kiếm dòng hiện tại mà bạn đang đứng.

Sau khi thao tác xong, có thể nhấn tổ hợp phím `Ctrl + O` để lưu lại file và `Ctrl + X` để thoát ra.

- `VIM`: là một công cụ chỉnh sử văn bản nâng cao hơn so với `nano` và cũng phức tạp hơn rất nhiều, khi chúng ta phải tập làm quen với việc sử dụng dòng lệnh để trong chính trình soạn thảo văn bản trên

- Để tạo/mở một file văn bản:

`vi <FILE_NAME>`

Đặc biệt bên trong `vim` có 3 chế độ rất quan trọng mà chúng ta cần tìm hiểu 
