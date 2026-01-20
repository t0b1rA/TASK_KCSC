# Forensics - Steganography

## I. Những File Type thường gặp 

### 1. File image

File ảnh là một chuỗi byte biểu thị một lưới pixel và siêu dữ liệu liên quan (loại máy ảnh, không gian màu ảnh, ngày giờ được tạo,..). Hình ảnh có thể không bị mất dữ liệu, tức là chúng bảo toàn chính xác những dữ liệu bên trong. Hoặc cũng có thể mất dữ liệu, tức hình ảnh có thể đã bị mất 1 vài đặc trưng làm cho hình ảnh trở nên nhỏ hơn. 

Hình ảnh cũng có 2 loại tức là hình ảnh **raster** và hình ảnh **vector**:

- Hầu hết các hình ảnh mà chúng ta thấy là hình ảnh `raster`, nó được tạo thành từ hàng triệu pixels ghép tất cả chúng lại, và nhìn 1 cách trọn vẹn thì sẽ tạo thành 1 tấm hình hoàn chỉnh, nhưng khi chúng ta zoom nó vào chúng ta có thể sẽ thấy được những hạt hạt pixel vô cùng nhỏ bên trong 1 file ảnh `raster`. Ví dụ: `JPG, PNG, GIF`

- Mặt khác thì chúng ta có hình ảnh `vector` tức là những hình ảnh được tạo thành từ các đường thẳng và đường cong, nó giúp cho việc thay đổi kích thước của file ảnh 1 cách tùy ý mà không làm giảm chất lượng. ví dụ: `SVG, CDR`

- Tuy nhiên thì  mỗi hình ảnh đều có lợi ích riêng: khi mà hình **raster** cho phép hiển thị những hình ảnh có màu sắc phức tạp tốt hơn, còn `vector` thì hiển thị các hình ảnh đơn sắc cho phép chỉnh sửa kích thước tốt hơn như (logo, icon).

#### A. PNG file

Một file PNG bao gồm 8 byte signature đặc trưng gọi là header của file PNG để nhận dạng tệp, sau đó là các chunk (`IHDR`, `IDAT`, `IEND`) cùng với một số những option khác. Đây là cấu trúc chung của một file ảnh `png`

```
8 bytes signature: 89 50 4E 47 0D 0A 1A 0A
IHDR chunk: (Images Header - 13 bytes): chứa các thông tin về chiều rộng, chiều cao, loại màu, phương pháp nén,...
IDAT chunk: (Images data - n bytes ): chứa nội dung của file png, các pixels của hình sau khi lọc và nén bằng zlib
IEND chunk: (End of Image - 12 bytes): đánh dấu kết thúc của 1 file
```

Chunk là một vùng chứa xung quanh một số loại dữ liệu. với các loại chunk thì phần data của mỗi chunk sẽ khác nhau, nhưng đều sẽ theo một khuôn như sau:

```
Length ( 4 bytes): Độ dài của dữ liệu chunk (không bao gồm phần độ dài
Type (4 byte) Loại của chunk đó ví dụ là (IHDR, IDAT, IEND)
DATA (variable bytes): dữ liệu tùy thuộc vào loại chunk đó
CRC ( 4 bytes): Mã kiểm tra CRC32 của dữ liệu chunk (được tính từ phần Type và Data)
```

**Structure detail PNG file**

Giờ chúng ta sẽ đi sâu vào cấu trúc của file PNG này. Ở trên chúng ta nói về cấu trúc format chung của file PNG rồi, bây giờ sẽ làm rõ hơn về các Chunk trong file PNG.

**IHDR**
```
   Width:              4 bytes
   Height:             4 bytes
   Bit depth:          1 byte
   Color type:         1 byte
   Compression method: 1 byte
   Filter method:      1 byte
   Interlace method:   1 byte

```
Phần quan trọng nhất của chunk IHDR ở đây là chiều rộng/chiều cao, loại màu và độ sâu bit. Những cái khác thường sẽ được cố định. Chiều rộng và chiều cao lưu trữ, kích thước của hình ảnh và đôi khi sẽ cần phải sửa đổi. Loại màu lưu trữ thông tin về các pixel của hình ảnh, chẳng hạn như liệu chúng có cho phép độ trong suốt hay không, sử dụng bảng màu (PLTE chunk) và sử dụng thang độ xám hoặc màu sắc. Độ sâu bit cho biết lượng thông tin được sử dụng cho mỗi màu; giá trị này thường là 8.
> PLTE chunk: là một thành phần trong định dạng tệp hình ảnh PNG, có nhiệm vụ chứa dữ liệu bảng màu bao gồm các màu Đỏ (R), Xanh lá (G), Xanh lam (B) dùng cho định nghĩa 1 tập hợp các màu có sẳn, giúp cho việc hiển thị màu sẽ hiệu quả hơn.

```
Color    Allowed    Interpretation
Type    Bit Depths

0       1,2,4,8,16  Mỗi pixel là một thang độ xám (grayscale - hệ màu chỉ sử dụng các sắc thái từ đen đến trắng không có màu sắc)

2       8,16        Mỗi pixel có 1 bộ ba R, G, B

3       1,2,4,8     Mỗi pixel là một index cho bảng màu; chỉ định màu trong bảng màu PLTE phải xuất hiện


4       8,16        Mỗi pixel là một mẫu thang độ xám, theo sau là một mẫu alpha. (kênh alpha ở đây tức là quy định độ trong suốt của hình ảnh)

6       8,16        Mỗi Pixel là một bộ ba R, G, B theo sau là 1 mẫu, theo sau bởi 1 mẫu kênh alpha.
                    

```

**IDAT**
Chunk này lưu trữ các pixel thực tế của hình ảnh sau khi lọc và nén bằng zlib. Chúng ta có thể sử dụng thư viện Pillow để tải dữ liệu các pixel màu được lưu trữ trong chunk này thay vì lấy thủ công, có một cách để lấy các dữ liệu màu này là bằng công cụ `zsteg`.

**IEND**

Đây là phần chunk cuối của file PNG nó đánh dấu cho sự kết thúc của file này, nó không chứa những dữ liệu gì cả, và sẽ chứa 12 bytes tĩnh sau:
`00 00 00 00 49 45 4e 44 ae 42 60 82`

Tất cả những dữ liệu sau chunk IEND sẽ bị bỏ qua, thông thường đây là một cách để cho các attacker/author nhúng thêm dữ liệu vào sau phần này, có thể tạo thành 1 file hình khác, hoặc file zip, rar,...

#### JPG/JPEG

Khác với PNG được nhận diện qua 8 magic byte cố định ở phần đầu, thì JPG/JPEG được nhận diện bởi cặp byte mở đầu và cặp byte kết thúc

Tất cả các thành phần trong file JPG đều bắt đầu bằng byte `0xFF` theo sau là một byte định danh (Marker ID)

|Marker name | Byte Code | Ý nghĩa của nó|
| --- | ---|
| SOI (Start of image) | `FF D8` | Magic bytes bắt buộc. Báo hiệu bắt đầu file JPG |
| APPO (JFIF)| `FF E0` | Chứa thông tin định dạng chuẩn JFIF - là một chuẩn định dạng tệp hình ảnh dùng để đóng gói dữ liệu đã nén theo thuật toán JPEG|
| APP1 (Exif) | `FF E1`| Chứa metadata của file jpg |
| DQT (Define Quantization Table | `FF DB` | quyết định độ nén/ chất lượng ảnh |
| SOF0 (Start of Frame) | `FF C0` | Chứa chiều rộng, chiều cao, kênh màu |
| SOS (Start of Scan) | `FF DA` | Đánh dấu bắt đầu phần dữ liệu ảnh nén. Sau mark này là dữ liệu ảnh |
| EOI (End of Image) | `FF D9` | Kết thúc file ảnh|

#### GIF
Mặc dù em chưa gặp dạng file này trong bài CTF lần nào, nhưng mà cũng khá lạ xứng đáng để tìm hiểu. Thì file GIF cấu trúc của nó được tối ưu hóa cho việc lưu trữ các hoạt hình đơn giản và sử dụng bản màu `Palette` thay vì lưu màu trực tiếp cho từng điểm ảnh.

**Magic Byte**
Giống như những file type hình ảnh khác, thì chúng ta cũng có 6 byte signature cho file GIF là:

`47 49 46 38 39 61`

**Structure**
```
Header: `47 49 46 38 39 61`
Local Screen Description (LSD): Quy định kích thước của cả file ảnh về chiều rộng, chiều cao.
Global Color Table (GCT - Bảng màu toàn cục): Mỗi pixel trong ảnh chỉ là một con số trỏ vào hộp màu này
Các Block dữ liệu (Lặp lại nhiều lần cho Animation): Graphic Control Extention:
  - Quy định thời gian deplay của frame này và màu nào là màu alpha trong suốt.
  - Image Descriptor: Quy định kích thước và vị trí của frame hiện tại
  - Image Data: Dữ liệu hình ảnh đã nén bằng thuật toán LZW.
Trailer (Kết thúc): Chỉ gồm 1 byte duy nhất 3B
```
Author có thể giấu flag bên tròn một frame duy nhất chớp tắt nhiều lần, giấu tin trong các bảng màu,...
Tools thường sử dụng cho file GIF thông thường có thể dùng: stegsolve, ffmpeg,..

#### B. File âm thanh

File âm thanh thì nó thường sẽ chứa các dữ liệu bị giấu bên trong các tần số âm được của âm thanh chạy liên tục để quét ra hình ảnh.

**WAV** 
Đây là một định dạng file âm thanh rất phổ biến trong các bài ctf forensics. WAV là một định dạng lưu trữ âm thanh không nén, giữ nguyên chất lượng âm thanh và được sử dụng phổ biến trong các ứng dụng thu âm.

Thông thường thì những bài này thường giấu dữ liệu bên trong phần spectrogram, hoặc là thực hiện quét tần số âm thanh để tạo ra hình ảnh.
```
Chunk ID: 52 49 46 46
Format: 57 41 56 45 (ASCII: WAVE)
Chunk Size: 4 bytes -  kích thước toàn bộ file trừ 8 byte đầu

"data" chunk (64 61 74 61)
```
tools: Sonic Visualizer, Audacity

**MP3**

Dữ liệu bị nén, chia thành các Frame nhỏ liên tiếp. File MP3 thì lại không có header tổng quản lý dữ liệu như WAV mà mỗi frame tự quản lý chính nó.

Magic byte của MP3 có 2 dạng:
```
ID3 Magic Bytes (Metadata): 49 44 33
Frame Sync (Dữ liệu âm thanh): FF FB hoặc )FF Fx
```

tools:  [MP3Stego](https://github.com/fabienpe/MP3Stego)

**MKV**
MKV thực chất là một Container. Nó cso thể chứa video, audio, (MP3, FLAC, AAC,..) phụ đề và cả Fond chữ cùng 1 lúc.

```
Magic bytes: signature: 1A 45 DF A3
```

Cấu trúc EBML (Cây dữ liệu)
MKV không tổ chức theo bảng hay dòng chảy đơn thuần, nó tổ chức dạng cây (TREE):
- Header: 1A 45 DF A3
- Segment:
  - Mô tả các luồng bên trong - Tracks.
  - MKV cho phép đính kèm 1 file - Attachents
  - Chứa dữ liệu thực tế (các blocks video/audio đã nén) - Cluster.
 
Bởi vì file MKV này có thể dính kèm thêm 1 file. nên attacker có thể định kèm thêm những tệp độc hại theo với file âm thanh thông thường.

tools: [MKVToolNix](https://mkvtoolnix.download/).

#### C. File nén

Dùng để giảm bớt kích thước khi tải về hoặc upload file lên. Một số file nén phổ biến như : file zip, file rar, file 7z...

**ZIP**
 File zip là một file rất quen thuộc với phần mở rộng là `.zip`. trong 1 file zip sẽ có rất nhiều thư mục hoặc tệp bên trong, không chỉ vì nó phổ biến, mà vì rất nhiều định dạng file hiện đại thực chất là file ZIP đổi đuôi (ví dụ: .docx, .xlsx, .apk, .jar).
 ```
Header (4 bytes): 50 4B 03 04 (PK)
Central directory file header: chứa siêu dữ liệu về tệp được nén và cả header của tệp đó.
End of Central Directory Record: Đánh dấu phần kết thúc của "central directory", tổng số lượng file và thư mục đã nén
```

**RAR**
RAR là định dạng độc quyền, chia làm 2 phiên bản chính mà chúng ta có thể phân biệt qua Magic Bytes khác nhau

**Magic bytes**
RAR v4: `52 61 72 21 1A 07 00` (Rar!...)
RAR v5 hiện nay: `52 61 72 21 1A 07 01 00`

**Structure**

RAR lưu trữ dữ liệu theo các Block. Mỗi khối có một header riêng(BlockHeader, DataBlock, Recovery Records)
- BlockHeader: chứa siêu dữ liệu về kho lưu trữ và tệp bên trong.
- DataBlocks chứa các tệp đẫ được nén.
- Recovery Records cho phép sửa chữa kho lưu trữ bị hỏng, 1 tính năng của rar.

**7z**

Là định dạng nén rất mạnh mẽ, thường tạo ra các file nén với kích thước nhỏ hơn so với ZIP và cả RAR. Nếu so sánh thì 7zip > rar > zip, bởi vì nó hỗ trợ mã hóa AES đối với tên của tệp được nén và có khả năng nén đối với file với fil có kích thước lớn.

**Structure**

- Signature Header: `37 7A BC AF 27 1C`
  
- Packed Data Stream (luồng dữ liệu nén):
  - Chứa các file và thư mục đã được nén
  - Sử dụng các bộ lọc và thuật toán như LZMA, BZIP2, PPMd để giảm kích thước.
  - Dữ liệu trong luồng này thường được mã hóa theo AES.

- Header Database:
  - Chứa thông tin về cấu trúc lưu trữ (tên file, kích thước, ngày tháng,..)
  - Nằm sau khối dữ liệu nén và có thể được mã hóa

<img width="1840" height="656" alt="image" src="https://github.com/user-attachments/assets/8030fe91-961d-4f0f-8748-a00285e03d98" />


## Thư viện Pillow và OpenCV

### Pillow (PIL - Python Imaging Library)
Pillow là bản fork (kế thừa) của thư viện PIL cũ. Nó tập trung vào việc thao tác file ảnh, định dạng ảnh và các chỉnh sửa cơ bản.

Một số những đặc điểm của thư viện Pillow
- Dễ sử dụng: Cú pháp hướng đối tượng (OO).

- Hỗ trợ định dạng tốt: Pillow đọc được rất nhiều định dạng hình ảnh khác nhau.

- Chức năng chính: cắt(crop), xoay(rotate) thay đổi kích thước, chỉnh màu cơ bản, thêm chữ, chuyển đổi định dạng.

Một số các hàm thường được sử dụng trong Pillow 
| Tên Hàm | Ý nghĩa |
| --- | --- |
| Image.open(path) | mở ảnh |
| img.save(path, format)| lưu ảnh |
| img.convert(mode) | chuyển hệ màu |
| img.getpixel((x, y)) | lấy giá trị màu tại tọa độ (x,y) - trả về (R, G, B) |
| img.putpixel((x, y), value) | Gán màu cho điểm ảnh |

```
# download:
pip install Pillow
# import thư viện
from PIL import Image, ImageDraw
```

## Thư viện OpenCV
OpenCV mạnh về các thuật toán toán học, trên ma trận ảnh, giúp bạn phát hiện những thứ mắt thường không thấy được, cung cấp một loạt các chức năng và công cụ để xử lý, phan tích và hiểu hình ảnh và video.

Một số hàm trong thư viện:

|Tên hàm | Ý nghĩa |
| --- | --- |
| cv2.imread(path, flags) | Đọc ảnh |
| cv2.cvtColor(src, code) | chuyển đổi không gian màu|
| cv2.threshold(src, thresh, maxval, type) | Phân ngưỡng nhị phân hóa |
| cv2.resize(image, (width, height)) | thay đổi kích thước của hình ảnh |
| cv2.split(image) | Tách các kênh màu từ hình ảnh|
| cv2.merge(channels) | kết hợp các kênh màu tạo hình ảnh màu |

```
#download
pip install opencv-python
#import
import cv2
```


---
Một số tools có thể gặp trong bài forensics như 

[Hexed.it](https://hexed.it/), một công cụ nền tảng web khá phổ biến cho phép chúng ta nhìn được các byte bên trong 1 file ảnh, file thư mục, chỉnh sửa header, magic byte, signature bytes để chỉnh sửa được ảnh.

<img width="1875" height="1880" alt="image" src="https://github.com/user-attachments/assets/9f718a19-a779-4c1f-b6af-d0080b1aedf0" />

**binwalk:** là một công cụ giúp chúng ta có thể xem được những file khác có được nhúng bên trong file hình, hoặc bất kì 1 file nào đó không, và còn giúp giải nén các file đó ra.

<img width="1005" height="755" alt="image" src="https://github.com/user-attachments/assets/1ed4bd21-c404-487d-b3b6-268eb13d46ff" />


**Exiftool** là một công cụ giúp chúng ta truy xuất ra các metadata bên trong 1 file.

<img width="1368" height="743" alt="image" src="https://github.com/user-attachments/assets/407d41d2-9587-4e31-89a0-f6b2aae69d60" />


**foremost** là một công cụ giúp khôi phục dữ liệu từ các hệ thống bị hỏng hoặc file đã bị xóa.
```
foremost -h
foremost version 1.5.7 by Jesse Kornblum, Kris Kendall, and Nick Mikus.
$ foremost [-v|-V|-h|-T|-Q|-q|-a|-w-d] [-t <type>] [-s <blocks>] [-k <size>] 
        [-b <size>] [-c <file>] [-o <dir>] [-i <file] 

-V  - display copyright information and exit
-t  - specify file type.  (-t jpeg,pdf ...) 
-d  - turn on indirect block detection (for UNIX file-systems) 
-i  - specify input file (default is stdin) 
-a  - Write all headers, perform no error detection (corrupted files) 
-w  - Only write the audit file, do not write any detected files to the disk 
-o  - set output directory (defaults to output)
-c  - set configuration file to use (defaults to foremost.conf)
-q  - enables quick mode. Search are performed on 512 byte boundaries.
-Q  - enables quiet mode. Suppress output messages. 
-v  - verbose mode. Logs all messages to screen
                                                        
```
**gimp** là một công cụ chỉnh sửa hình ảnh, xử lý hình ảnh, làm nhòe ảnh, vẽ ảnh,....
<img width="1709" height="880" alt="image" src="https://github.com/user-attachments/assets/0f1b92ea-97e2-4b1a-81c5-2cdbac49a2a3" />


