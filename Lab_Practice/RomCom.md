---
title: RomCom

---

# RomCom

![image](https://hackmd.io/_uploads/BJJn6EnOZl.png)

Link đề: https://app.hackthebox.com/sherlocks/RomCom?tab=play_sherlock

Trong bài này thì chúng ta sẽ được cung cấp một ổ cứng hardware của máy Susan vì cô ấy dường như trong quá trình 1 file, đã gặp 1 số lỗi, với WinRAR, hơn nữa thì dạo gần đây WinRAR cũng đang gặp một lổ hổng cho phép những attacker có thể chiếm quyền kiểm soát, là một người làm trong Bệnh Viện thì cô ấy có rất nhiều tài liệu quan trọng. Công việc của chúng ta là cần phân tích ổ đĩa này.

Thì mình sẽ lấy ổ đĩa này và đưa vào file ftk imager để phân tích:

![image](https://hackmd.io/_uploads/Bk_QhHn_Wx.png)

Bởi vì đây là 1 file ổ cứng ảo `.vhdx` nó không giống như những file disk image khác, copy bit-to-bit, thế nên trong file hard disk image này không có quá nhiều artifact, nhưng vẫn có một số cái quan trọng vẫn khai thác được, (vdu: `$MFT`, `$J`).

Giờ mình sẽ export, file `$MFT` này ra để thực hiện phân tích:

![image](https://hackmd.io/_uploads/H1QBRShubx.png)

Mình sẽ dùng công cụ MFTECmd Explore để phân tích, nhìn cho dễ, chứ sử dụng file `.csv` thì hơi khó nhìn 1 chút.

### Task1: What is the CVE assigned to the WinRAR vulnerability exploited by the RomCom threat group in 2025?

Câu này mình lên mạng research nhanh qua thì có kết quả là **CVE-2025-8088


![image](https://hackmd.io/_uploads/SkTsRS3_Zg.png)



CVE này là 1 lổ hổng **path traversal** ảnh hưởng đến phiên bản WinRAR trên Windows cho phép kẻ tấn công thực thi mã tùy ý bằng cách tạo ra các tệp nén độc hại.

Mình sẽ nói sâu hơn về **CVE-2025-8088** này một chút bằng những thông tin mà mình đã đọc được:

> CVE-2025-8088 (WinRAR path traversal) này được các attacker khai thác thông qua 1 lỗi logic khi mã export file ra, kẻ tấn công có thể cấu hình file cho phép có 1 luồng thay thế (Alternative Data Streams - ADS) khác phía sau path chính ngăn cách bởi `:$Data`, có thể làm cho người dùng tải về 1 file `.exe, .dll,..` khác âm thầm.

![image](https://hackmd.io/_uploads/ByQq9u3ubl.png)


### Task2: What is the nature of this vulnerability?

`nature of this vulnerability`, mình hiểu nó là tấn công theo hình thức gì, thì theo như [blog](https://github.com/AdityaBhatt3010/CVE-2025-8088-WinRAR-Zero-Day-Path-Traversal), này nói thì CVE này tấn công theo kĩ thuật `path traversal`.

![image](https://hackmd.io/_uploads/B129cO2Obe.png)

### Task3: What is the name of the archive file under Susan's documents folder that exploits the vulnerability upon opening the archive file?


Giờ mình vào thư mục documents của Susan để tìm kiếm file `.rar` bên trong đây:

![image](https://hackmd.io/_uploads/S1B6sO3_Wx.png)

**Filename: Pathology-Department-Research-Records.rar**


![image](https://hackmd.io/_uploads/HkD1nu3_-g.png)

### Task4: When was the archive file created on the disk?

Giờ mình chú ý vào cột `Created on` trong `MFT explorer` để xem xem file `rar` này được tạo khi nào:

![image](https://hackmd.io/_uploads/SJYX2d3_Wx.png)

**Time created: 2025-09-02 08:13:50**

### Task5: When was the archive file opened?

Trong câu này chúng ta cần dựa vào cột `Record Changed` bởi vì thuộc tính này sẽ theo dõi bất kì sự thay đổi nào đối với metadata của file bên trong bảng MFT, không chỉ là mỗi nội dung tệp có được thay đổi hay không. 

Khi 1 tệp được tương tác hoặc mở, hệ điều hành hoặc các ứng dụng thường sẽ thay đổi các metadata này:

- Khi 1 file được Windows Defender quét qua, nó được gọi tên trong bộ nhớ, thì nó cũng sẽ thay đổi metadata.
- Ứng dụng như (WinRAR, Word) có thể đặt cờ khóa tệp (file lock) hoặc tạo các luồng dữ liệu thay thế (ADS).


Thay vì dựa vào thuộc tính `Last Accessed` bởi vì bắt đầu từ Windows 10/11, Microsoft đã tắt tính năng cập nhật Last Accessed này trên file system NTFS nhằm tăng hiệu suất.

Dựa vào đó ta có được file được opened vào lúc: **2025-09-02 08:14:04**

![image](https://hackmd.io/_uploads/BknqAu3O-e.png)

### Task6: What is the name of the decoy document extracted from the archive file, meant to appear legitimate and distract the user?


Bởi vì mình thấy được trong thư mục Documents của Susan vẫn còn xuất hiện 1 file `.pdf` khác, hơn nữa thời gian nó được tạo cùng khá gần với file `rar`:

![image](https://hackmd.io/_uploads/SJenkK2ube.png)

Mình nghĩ đây là file fake được giải nén ra từ file `.rar` kia.

**File name: Genotyping_Results_B57_Positive.pdf**

![image](https://hackmd.io/_uploads/HyRAyY2Obl.png)

### Task7: What is the name and path of the actual backdoor executable dropped by the archive file?

Với câu này, thì bởi vì mình không có được, những artifact khác, nên mình sẽ dựa vào timeline để tiếp tục phân tích, khi chúng ta giải nén 1 file `rar`, thời gian giải nén tạo ra file mới có thể sẽ rất gần với file được tạo. Và đối với đây là 1 lổ hỗng của WinRAR nữa, nên attacker rất có thể sẽ giải nén 1 file thực thi (như .exe, .dll,..).

![image](https://hackmd.io/_uploads/BkNJfKh_-l.png)

Ở đây chúng ta có thời gian cuối cùng mà file `rar` được mở là `08:14:04`.

```
Line	Tag	Entry Number	Sequence Number	Parent Entry Number	Parent Sequence Number	In Use	Parent Path	File Name	Extension	Is Directory	Has Ads	Is Ads	File Size	Created0x10	Created0x30	Last Modified0x10	Last Modified0x30	Last Record Change0x10
152280	Unchecked	117119	2	104964	2	Checked	.\Users\susan\Documents	Pathology-Department-Research-Records.rar	.rar	Unchecked	Unchecked	Unchecked	8746363	2025-09-02 08:13:50		2025-09-02 14:54:54	2025-09-02 08:13:50	2025-09-02 08:14:04
```

Và sau đó khoảng 14s, thì mình có tìm thấy 1 file `.exe` vừa được tạo ra:
```
Line	Tag	Entry Number	Sequence Number	Parent Entry Number	Parent Sequence Number	In Use	Parent Path	File Name	Extension	Is Directory	Has Ads	Is Ads	File Size	Created0x10	Created0x30	Last Modified0x10	Last Modified0x30	Last Record Change0x10
152570	Unchecked	117405	2	104988	2	Checked	.\Users\susan\AppData\Local	ApbxHelper.exe	.exe	Unchecked	Unchecked	Unchecked	1728496	2025-09-02 08:14:18		2025-09-02 08:14:18	2025-09-02 08:14:18	2025-09-02 08:14:28
```

Cùng với đó là 1 file `.lnk` cũng được tạo cùng 1 khoảng thời gian nằm trong thư mục `/startup`, và vấn đề là tại sao trong thư mục `/startup` mỗi khi người dùng mở máy tính lên lại có 1 file dùng để hiển thị cài đặt, nó khá bất thường.

```
Line	Tag	Entry Number	Sequence Number	Parent Entry Number	Parent Sequence Number	In Use	Parent Path	File Name	Extension	Is Directory	Has Ads	Is Ads	File Size	Created0x10	Created0x30	Last Modified0x10	Last Modified0x30	Last Record Change0x10
152569	Unchecked	117404	2	115462	1	Checked	.\Users\susan\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Startup	Display Settings.lnk	.lnk	Unchecked	Unchecked	Unchecked	2018	2025-09-02 08:14:18		2025-09-02 08:14:18		2025-09-02 08:14:18
```
Ở câu này thì đề hỏi về 1 file executable, nên mình sẽ trả lời nó là file `.exe`:

**full path: C:\Users\Susan\Appdata\Local\ApbxHelper.exe**


### Task8: The exploit also drops a file to facilitate the persistence and execution of the backdoor. What is the path and name of this file?


Đúng như mình nghĩ, thì chắc chắn file nằm trong thư mục statup kia, chính là dùng để file persistence, bởi vì khi kết nối giữa attacker và máy có gián đoạn, thì mỗi khi victim khởi động lại máy, thì mã độc sẽ tiếp tục thực thi:

**full path: C:\Users\Susan\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Startup\Display Settings.lnk**

### Task9: What is the associated MITRE Technique ID discussed in the previous question?


Kĩ thuật persistence startup bằng 1 file lnk, mình có research thử thì mình thấy MITRE Technique ID này khá phù hợp:

![image](https://hackmd.io/_uploads/ry3tSt3O-l.png)

**ID: T1547.009**


### Task10: When was the decoy document opened by the end user, thinking it to be a legitimate document?

Chúng ta xem lần cuối cùng mà file `.pdf` dùng để giả dạng hợp pháp được sử dụng là khi nào:
```
Line	Tag	Entry Number	Sequence Number	Parent Entry Number	Parent Sequence Number	In Use	Parent Path	File Name	Extension	Is Directory	Has Ads	Is Ads	File Size	Created0x10	Created0x30	Last Modified0x10	Last Modified0x30	Last Record Change0x10
152568	Unchecked	117403	2	104964	2	Checked	.\Users\susan\Documents	Genotyping_Results_B57_Positive.pdf	.pdf	Unchecked	Unchecked	Unchecked	91441	2025-09-02 08:14:18		2025-09-02 08:14:18		2025-09-02 08:15:05
```

***Last opened: 2025-09-02 08:15:05**

# Technique 

Thì trong bài này sau khi làm xong, có 1 vài kĩ thuật khá mới cũng như kiến thức dễ quên, trong bài thì mình sẽ note lại:

### NTFS-ADS (Alternative Data Streams) and CVE-2025-8088

Trong NTFS có khả năng chạy được nhiều luồng dữ liệu khác nhau trong cùng 1 lúc: luồng chính không tên (nội dung mặc định) và 1 số lượng luồng thay thế có tên khác phía sau như (payload.exe,..). Nói rõ hơn trong Microsoft Windows 1 luồng thay thế sẽ nằm phía sau đường dẫn của nguồn chính như dạng sau:


![Screenshot 2026-02-25 183441](https://hackmd.io/_uploads/BJrndK3d-x.png)

Chúng ta sẽ thấy được phía sau 1 đường dẫn chính tới file `zap.sh` là `::$Data` - đây chính là luồng thay thế sẽ thực thi kèm theo với luồng chính nếu nó được cấu hình, đây là vấn đề. Giả sử như khi chúng ta giải nén 1 thư mục, thì bên trong 

![image](https://hackmd.io/_uploads/ByrooFnd-g.png)

Như thế này, thì trên thanh ở trên, chúng ta chỉ có thể thấy được nó ghi size của file rar, mà chúng ta không thể biết được bên trong nó có gì. Và thực tế bên trong nó chỉ hiển thị 1 file CV bình thường.

Thế nhưng, thực tế bên trong nó lại có rất nhiều những file trong luồng ADS khác, cũng đang được tải xuống cùng:

![image](https://hackmd.io/_uploads/rkcHnKndbe.png)

Khi nhìn vào bên ngoài, chúng ta cũng chỉ nghĩ, đây là những file `rar` rác được tạo cùng trong thư mục `/temp` và không có gì quá quan trọng, Nhưng thực tế thì:

![image](https://hackmd.io/_uploads/HJag6Y3dZx.png)

Đây là khi kẻ tấn công, đã sử dụng kĩ thuật `path_traversal` nhắm đánh lừa với người giải nén rằng, đó chỉ là những file bình thường, nhưng thực tế lại đang tải về các file `.dll` file này và khi 1 chương trình nguy hiểm chạy nó sẽ gọi file `.dll` này để thực thi. 

Đây là cách mà attacker đã thực hiện để khai thác vào lổ hổng **CVE-Path_Traversal** này

### Persistence startup: shortcut file (.lnk)

Kẻ tấn công có thể tạo hoặc sửa đổi các lối tắt(shortcut) để thực thi một chương trình trong quá trình khởi động hệ thống hoặc khi người dùng đăng nhập. Các file `.lnk` này sẽ được trỏ đến tệp thực thi khi nó được nhấp vào hoặc được kích hoạt bởi một tiens trình khởi động của hệ thống.

Kẻ tấn công có thể lạm dụng file `lnk` bằng cách sửa đổi file lnk của trình duyệt (vdu như các file extention của browser) để thực hiện liên tục khởi chạy mã độc.




