# Linux Fundamentals 1

## Task 1: Introduction

Ở task đầu tiên này chúng ta được giới thiệu sơ lược về hệ điều hành Linux, khá là phổ biến trên thế giới với thiết bị android, siêu máy tính, home applications,...

- Chúng ta tập làm quen với cách sử dụng câu lệnh để tương tác với Linux.
- Một số câu lệnh cần thiết cho việc tương tác với file system.
- Tìm kiếm các file và các toán tử của **shell**.

<img width="770" height="197" alt="image" src="https://github.com/user-attachments/assets/0469d1f7-05ea-4bee-8c64-17e966063ad0" />
<img width="192" height="192" alt="logo-O35E636P" src="https://github.com/user-attachments/assets/37efbed2-ad04-4ba0-9d88-e6fabff5cd6d" />

Và task đầu này chúng ta cũng không cần phải trả lời câu hỏi.

## Task 2: A bit of Background on Linux 

**Linux** thực chất là một thuật ngữ chung cho rất nhiều những hệ điều hành dựa trên UNIX(hệ điều hành khác). Bởi vì Linux là một mã nguồn mở nên Linux có đa dạng các phiên bản phù hợp với cấu hình và kích thước phù hợp với những hệ thống được sử dụng.

### Research: What year was the first release of a Linux operating system?<img width="192" height="192" alt="logo-O35E636P" src="https://github.com/user-attachments/assets/3ccd29c2-e0f2-4c1e-854f-0dd0edbda857" />


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


