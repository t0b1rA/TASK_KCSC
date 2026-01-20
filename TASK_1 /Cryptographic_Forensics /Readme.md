## Base16, Base32, Base64, Base85

### BASE16

Cơ chế: là nó sẽ sử dụng 16 kí tự từ `0-9` và từ `A-F`. Trong 1 byte nó sẽ có 8 bit, thì base16 này nó sẽ chia đôi 8 bit ra là 4 bit và 4 bit, và nó sẽ mã hóa theo 4 bit 1, tương ứng. 

Ví dụ: "Chữ M trong bảng mã ASCII là `77` thì nó có giá trị nhị phân là `01001101`:
- Thì Base16 nó sẽ tách 8 bit này ra thành 4 bit 1 và thực hiện mã hóa, 4 bit đầu là `0100` sẽ tương ứng `=4`, 4 bit sau `1101` sẽ tương ứng với `=D`.
- Lúc này chữ `M` sẽ được mã hóa base16 thành `4D`

### BASE64

Cơ chế mã hóa của base64 sử dụng các kí tự từ `A-Z`, `a-z`, `0-9` và từ `+ - /, ...` , đặc biệt nó sẽ không xử lí từng byte một lẻ giống như base16, mà nó sẽ xử lí thành từng cụm 3 byte một:
- Từ 3 byte đó nó sẽ chuyển đổi 24 bit (3x8), sau đó nó sẽ tiếp tục cắt 24 bit này thành 1 cụm 6 bit một, xong sau đó sẽ thực hiện tính toán nhị phân thành số thập phân, và so sánh với bảng ASCII để tìm ra kí tự tương ứng.
- Do việc từ 1 chuỗi và cắt 3 byte 1 ra, để thực hiện phân nhỏ hơn, nên sẽ có 1 số đoạn không đáp ứng chuỗi byte có số byte không chia hết cho 3, nên mới sử dụng `=` để padding thêm vào cho đủ.

Ví dụ: Mã hóa đơn giản chữ "MAN" thành base64:
- Đầu tiên 3 byte M, A, N sẽ được gom lại thành 1 nhóm, và sẽ được tách ra thành từng bit: `M (77):01001101`, `a (65):01000001`, `N (78):01001110`
- Sau đó thực hiện ghép nó thành 1 chuỗi 24 bit: `010011010100000101001110`.
- Rồi cắt thành 4 phần mỗi phần 6 bit để chuyển thành kí tự khác tương ứng: `010011`, `010100`, `000101`, `001110`.
- Cuối cùng là thực hiện tính toán từ nhị phan thành thập phân:
  - 010011: 19 - T
  - 010100: 20 - U
  - 000101: 5  - F
  - 001110:	14 - O
 
Cuối cùng là từ "Man" ta biến đổi thành được "TUFO"

### BASE85

Khác với Base16 và Base64 thì Base85 nó thực hiện ghép 4 byte một thành 1 chuỗi 32 bit sau đó tính toán số học, chứ không phải cắt thành từng phần. Base85 thực hiện lấy 32bit đó sau đó thực hiện chia cho 85, tạo thành các số dư. Kết quả nó sẽ tạo ra 5 con số dư. Mỗi số dư sau khi chia với 85 sẽ + với 33 `!` để có thể so sánh với bảng ASCII tạo thành kí tự có thể in được.

## AES, RSA

### AES
AES là một thuật toán mã hóa theo khối (Block Cipher) hoạt động trên các khối dữ liệu 128-bit.

**Cấu trúc dữ liệu**: dữ liệu đầu vào 128-bit được sắp xếp thành một ma trận 4x4 gọi là `State Array`.

**Quy Trình mã hóa**: Số lượng vòng lặp của thuật toán AES tùy thuộc vào độ dài của khóa:
- AES 128-bit: 10 vòng
- AES 192-bit: 12 vòng
- AES 256-bit: 16 vòng

Mỗi vòng (trừ vòng cuối) bao gồm 4 phép biến đổi:
- SubBytes
- ShiftRows
- MixColumns
- AddRoundKey

Cuối cùng quan trọng nhất là thuật toán được tính theo mode nào:
- **ECB** nó bảo toàn cấu trúc acur dữ liệu gốc, làm cho các khối bị lặp lại, và tần suất xuất hiện của các khối trong bản mã là tương đồng với nhau.
- Cơ chế hoạt động của **ECB**:
  - Chia dữ liệu thành các khối độc lập (vd: 16 bytes)
  - Mỗi khối được mã hóa riêng biệt với cùng 1 keys.
  - Công chứa Cipherblock = Encrypt(PlainBlock, Key)

- **CBC (Cipher Block Chaining)** : Dùng kết quả của khối trước XOR với khối sau. **CBC** bắt buộc dữ liệu phải chia hết cho kích thước khối. Nếu file gốc không đủ, nó sẽ thêm Padding (theo chuẩn PKCS#7)
- Cơ chế hoạt động của **CBC**:
  - Mã hóa: trước khi mã hóa khối hiện tại, nó được XOR với khối mã hóa (Ciphertext) của khối trước đó
  - Khối đầu tiên: Vì là khối đầu nên nó sẽ phải cần 1 giá trị ngẫu nhiên **IV** (vector ban đầu).
  - Công thức: `Cipherblock_Current = Encrypt(PlainblockCurrent XOR CipherblockPrevious)`

- **GCM (Galois/Counter Mode)**: đây là chuẩn hiện đại (TLS, HTTPS, VPN) kết hợp giữa tốc độ và tính toàn vẹn.
- Cơ chế hoạt động của **GCM**:
  - Stream Cipher: GCM thực chất không mã hóa dữ liệu trực tiếp bằng AES, Nó dùng AES để mã hóa một bộ đếm (counter).
  - Dòng dữ liệu sinh ra từ bộ đếm (Keystream) sẽ được XOR với dữ liệu gốc (Plaintext) để tạo ra bản mã.
  - Nonce (Number used once): Giống IV nhưng quan trọng hơn. Mỗi lần mã hóa nó sẽ dùng 1 nonce khác nhau.
  - Auth tag: Cuối cùng, nó tạo ra một đoạn mã (tag) để đảm bảo dữ liệu không bị chỉnh sửa.  
  
### RSA (Rivest–Shamir–Adleman)
RSA dựa trên bài toán Phân tích thừa số nguyên tố (Integer Factorization Problem).

Quy trình tạo khóa:
- Chọn 2 số nguyên tốc lớn p,q với p khác q và hoàn toàn ngẫu nhiên.
  
- Tính số N = p.q
  
- Tính hàm: $\phi(N) = N.(1-\frac{1}{p}).(1-\frac{1}{q})$

- Chọn 1 số tự nhiên e sao cho: $1 < e < \phi(N)$ và $gcd(e, \phi(N)) = 1$

- Sau đó tìm d sao cho $e.d \equiv 1 \pmod{\phi(N)}$

Khi này ta sẽ có 2 cặp khóa bí mật và công khai:
- Khóa bí mật: $(N, d)$

- Khóa công khai: $(N, e)$

Trong 1 bài Forensics thì attacker sẽ có thể thực hiện mã hóa file của người dùng, hoặc trao đổi khóa dưới malware và C2 để có thể giải mã được đoạn PlainText mà chúng ta cần biết được để có thể có manh mối. Và cơ chế mã hóa đoạn PlainText bằng thuật toán RSA là:
- Đầu tiên chuyển đổi đoạn plaintext từ văn bản sang dạng số, gọi là m
- Sử dụng khóa công khai, mã hóa `m` theo công thức:

  $c \equiv m^{e} \pmod{N}$

- Khi attacker thực hiện gửi cho malware một giá trị `c` tức là đoạn plaintext đã má hóa, nó sẽ dùng khóa bí mật để giải mã:
  
  $m \equiv c^{d} \pmod{N}$

- Cuối cùng attacker nhận được một chuỗi số đã giải mã, chỉ cần biến đổi trở về dạng số đó về dạng văn bản là có được đoạn văn bản gốc.

