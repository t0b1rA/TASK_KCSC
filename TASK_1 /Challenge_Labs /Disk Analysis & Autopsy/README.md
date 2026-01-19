## Disk Analysis & Autopsy

Đây là 1 lab để thực hành thêm 1 số kĩ năng cho autopsy, với lab có sẳn trong challenge, thực hiện phân tích images và trả lời các câu hỏi trong bài. Công cụ `autopsy` là một công cụ rất mạnh mẽ được dùng để phân tích các disk image do `FTK imager` tạo ra, dùng để phân tích filesystem (FAT16-32-exFAT, NTFS), phân tích về Internet History, email, khôi phục tệp,...

### **What is the MD5 hash of the E01 image?**

Để coi được MD5 hash của `E01` image chúng ta vào file `HASAN2.E01.txt` ở đây nó lưu chữ những metadata của file `HASAN2.E01` này.

<img width="1366" height="671" alt="image" src="https://github.com/user-attachments/assets/98804fee-f0ca-4bf6-aa5c-3e566e059b7c" />

`md5 hash`: 3f08c518adb3b5c1359849657a9b2079

<img width="460" height="180" alt="image" src="https://github.com/user-attachments/assets/1445db2d-3319-4990-b7f1-abf16c78a990" />

### **What is the computer account name?**

Để xem được thông tin của máy tính thì chúng ta vào phần OS information trong `autopsy`
