# Investigator Windows Writeup


**Whats the version and year of the windows machine?**
Để trả lời câu hỏi đầu, chúng ta bật `msinfo` lên để xem phiên bản của nó là, Microsoft Windows Server.

<img width="832" height="662" alt="image" src="https://github.com/user-attachments/assets/bf1531ff-171f-447b-b4b0-31ab7afee238" />

<img width="900" height="134" alt="image" src="https://github.com/user-attachments/assets/e6d93ef4-788a-4efb-950f-08099a97aeba" />


**Which user logged in last?**
Để biết người đăng nhập cuối cùng, em event viewer, và kiểm tra vào event id `4624` để xem ai là người cuối cùng đăng nhập. Trong phần hint nó ghi chính là lần đăng nhập sau lần đăng nhập đầu tiên của bạn, chính là log thứ 4 - `Administrator` với 2 log trên là 2 log của Windows Manager thì chúng ta không xét nó là người dùng.

<img width="1909" height="995" alt="image" src="https://github.com/user-attachments/assets/6b1677f4-1138-4b58-8ed0-743f31997e5f" />

<img width="899" height="140" alt="image" src="https://github.com/user-attachments/assets/b6f22142-e82e-4e61-bf2e-5179cd1d34ee" />

**When did John log onto the system last?**
Chúng ta có thể sử dụng 1 lệnh trong cmd là `net user <user-name>` để có thể liệt kê ra các lần đăng nhập của user mà chúng ta muốn xem, trong câu này lần đăng nhạp cuối cùng của `john` là "3/2/2019 5:48:32"

<img width="1097" height="535" alt="image" src="https://github.com/user-attachments/assets/f005d415-63f1-4e2e-b2a5-bcc29b70e903" />

**What IP does the system connect to when it first starts?**

Để ý lúc chúng ta vừa mở máy ảo lên, nó sẽ xuất hiện một cửa sổ `cmd` kết nối tới 1 địa chỉ ip `10.34.2.3` tại thư mục `C:\TMP\p.exe` rất đáng nghi khi trong thư mục tmp lại có 1 file `.exe` bên trong. Nên bây giờ em thực hiện theo manh mối này vào trong File Explorer -> C:\TMP\p.exe .

<img width="1905" height="883" alt="image" src="https://github.com/user-attachments/assets/bb743c5a-4e8d-4f7c-a0a1-94fed16fb514" />

Và khi em vào trong thư mục tmp rồi thì bên trong còn có các chương trình đáng ngờ khác, và có vẻ như đây là khu vực mà attacker thực hiện lưu các chương trình độc hại nó cài vào máy nạn nhân.

<img width="1121" height="627" alt="image" src="https://github.com/user-attachments/assets/db58906b-0322-4260-8667-4304d65020d2" />

File `p.exe` này là là 1 file thực thi mỗi khi người dùng khởi động máy tính (startup machine), nên em sẽ vào `regedit` check phần `HKLM/SOFTWARE -> Microsoft -> Windows -> CurrentVersion -> Run`

<img width="1909" height="799" alt="image" src="https://github.com/user-attachments/assets/ef587608-5655-47ce-8bb0-235863796a1a" />

Có tận 2 file `.exe` được chạy tự động ở đây `wwscript.exe` - là tiến trình hợp pháp đùng để chạy cái file `VBS` trong `WWMI` của Windows, còn tiến trình còn lại trình là tiến trình đáng nghi đang kết nối tới địa chỉ ip `10.34.2.3`

<img width="911" height="126" alt="image" src="https://github.com/user-attachments/assets/39a912c7-d9bc-4ef6-a38e-ecb04689b9b8" />

**What two accounts had administrative privileges (other than the Administrator user)?**
Chúng ta có thể vào `compmgmt.msc` rồi vào mục Local Users and Group, chọn vào mục groups và tìm administrator, để có thể xem những users nào có quyền admin

<img width="1102" height="794" alt="image" src="https://github.com/user-attachments/assets/7f492c15-33b5-4116-bd09-294d83911cec" />

<img width="898" height="163" alt="image" src="https://github.com/user-attachments/assets/69f6c7fb-708e-4e33-a2e0-f73ce982bb49" />

**Whats the name of the scheduled task that is malicous.**
Ở đây em vào phần Scheduler-task trong `compmgmt` để coi luôn. Sau đó em chọn vào phần **Task Scheduler Library**, ở đây nó liệt kê ra cho em các task đã được thiết lập để chạy.

<img width="1915" height="885" alt="image" src="https://github.com/user-attachments/assets/f3a67494-8fa1-4968-aece-590730eea64e" />

Theo như em suy nghĩ thì, ở câu hỏi trước đó, em đã tìm hiểu được là có 1 file `.exe` đã được thiết lập để thực thi kết nối tới server `10.34.2.3` mỗi lần mà máy được startup, vậy có thể nếu câu hỏi này nhắc tới `scheduler-task` thì nó phải là một task được thiết lập run mỗi khi startup.

Sau khi check 3 task đầu là execute `at system startup` thì không có gì, nên em xem tiếp tục tới task `Clean file System`

<img width="1915" height="791" alt="image" src="https://github.com/user-attachments/assets/ddf83367-f109-4b0a-9f19-1ad05ea32546" />

Nó đang thực hiện chạy script `nc.ps1` và `-I` lắng nghe tới cổng 1348. Đây là kĩ thuật `Bind Shell Backdoor`, kẻ tấn công từ bên ngoài sẽ kết nối trực tiếp đến địa chỉ IP của máy nạn nhân qua cổng `1348`. Khi kết nối thành công, kẻ tấn công sẽ thực hiện được shell từ xa.

**Scheduler-task** là một cách để duy trì `persistence` trên máy của nạn nhân, bởi vì nó sẽ thực hiện lại hành động mỗi ngày, sau khi máy nạn nhân khởi động lại, nên attacker có thể duy trì được kết nối mỗi ngày.

**What file was the task trying to run daily?**
Như ta tìm thấy ở trên.

<img width="897" height="122" alt="image" src="https://github.com/user-attachments/assets/f310e766-2404-4f1e-8f78-89e8e6f76c4c" />

**What port did this file listen locally for?**

<img width="877" height="127" alt="image" src="https://github.com/user-attachments/assets/cdde16b4-29ca-4f9d-9728-0d9812116ac0" />

**When did Jenny last logon?**
Tương tự câu trên thực hiện lệnh `net user <user-name>` jenny để xem lần cuối cô ấy đăng nhập.

<img width="1103" height="574" alt="image" src="https://github.com/user-attachments/assets/574cc2d9-d2f6-44ca-8b36-82489c129e81" />

<img width="881" height="125" alt="image" src="https://github.com/user-attachments/assets/f3f853e0-a06a-4ab2-8617-0879cc71b593" />

**At what date did the compromise take place?**
Ở đây em thấy thư mục tmp này được tạo vào ngày `3/2/2019` nó dùng để lưu các chương trình để thực hiện kết nối shell từ xa, ghi lại output mật khẩu mà nó crack được bằng công cụ,...

<img width="703" height="248" alt="image" src="https://github.com/user-attachments/assets/a6926b00-bacd-42e1-b2fe-8ff02e16daa8" />

<img width="898" height="164" alt="image" src="https://github.com/user-attachments/assets/6e49cae8-08b6-46d9-bc66-6a7b80028d9a" />

**During the compromise, at what time did Windows first assign special privileges to a new logon?**
Ở câu hỏi trước chúng ta đã có thể tìm được ngày mà máy bị xâm nhập vào là `2/3/2019`, cùng với thời gian tạo thư mục tmp bên trong file explorer là vào khoảng "4:38:30PM 3/2/2019" vậy thì trong Event Viewer em sẽ thực hiện, range lại khoảng thời gian Windows thực hiện ghi log trong khoảng thời gian là "0:00:00 AM - 11:59:00 PM" và set log được ghi lại là security thôi cho đỡ loãng.

Ở đây có rất nhiều những log thực hiện gán quyền, nên em dựa vào hint mà bài cung cấp để tìm kiếm.

<img width="658" height="116" alt="image" src="https://github.com/user-attachments/assets/78b08527-753e-4a23-b363-7c05fb1eb8df" />

<img width="1464" height="1308" alt="image" src="https://github.com/user-attachments/assets/82bc7370-3850-4fb2-8f72-da7eb606ec86" />

Thì có lẽ nó là khoảng thời gian này rồi. `03/02/2019 04:04:49 PM`

<img width="1834" height="260" alt="image" src="https://github.com/user-attachments/assets/b188ba21-a2c3-4d88-bc8f-32d357505e21" />

**What tool was used to get Windows passwords?**

Nãy bên trong thư mục tmp thì em có tìm thấy một công cụ để crack mật khẩu.

<img width="1753" height="1530" alt="image" src="https://github.com/user-attachments/assets/41947012-fcb0-40d6-a870-d747fd2f93e4" />

Ở đây nó đã thực hiện lấy được hash của user ION-PC, và crack được mật khẩu của user này là `MySecretP4ass`. Đây có lẽ là tài khoản mà attacker sử dụng đăng nhập vào, nâng quyền cho chính bản thân mình và thực hiện duy trì phiên đăng nhập vào máy người dùng.

<img width="1794" height="183" alt="image" src="https://github.com/user-attachments/assets/33b168d1-12fe-4ed3-bcbc-c708af2b3010" />

**What was the attackers external control and command servers IP?**

Ban đầu em có hơi rối khi làm câu này, và có đi tìm hiểu nhiều nguồn thì em thấy trong Windows sẽ có 1 nơi có thể được dùng để chuyển hướng các địa chỉ IP tên một tên miền cụ thể, cho phép user đặc quyền cao có thể tự động thay đổi ip được ánh xạ đến tên miền đó.Nó nằm ở `%SYSTEM32%\drivers\etc\hosts` đây là một file `local host` của Windows, cách file này hoạt động là khi bạn dùng một phần mềm và nhập tìm kiếm một tên miền (ví dụ youtube.com), thì trước tiên nó sẽ ánh xạ đến file `HOSTS` trước để tìm xem có tên miền này được ghi bên trong file không, nếu không nó sẽ truy vấn đến cơ sở dữ liệu DNS (dịch vụ tên miền) phân tán.

Qua đó em nghĩ là attacker sẽ thực hiện sửa đổi địa chỉ ip của tên miền hợp pháp nào đó, để khi đó máy attacker có thể ánh xạ địa chỉ ip đó của hắn bằng tên miền hợp pháp. Đây gọi là kỹ thuật **DNS Poisoning**

<img width="1438" height="1497" alt="image" src="https://github.com/user-attachments/assets/92c63ac2-b37e-4427-8d37-9bce73e96098" />

Tại đây chúng ta thấy 2 tên miền `google.com` và `www.google.com` có vẽ khá lạ, em sẽ thử kiểm tra bằng cmd máy chính:

<img width="1211" height="441" alt="image" src="https://github.com/user-attachments/assets/0f5396f6-6279-4319-9e14-ed76f82a2c75" />

Rõ ràng là có sự khác biệt, chắc chắn đây là kĩ thuật `DNS Poisoning` thực hiện ánh xạ tên miền đến địa chỉ ip của attacker để chuyển hướng người dùng đến server độc hại của attacker.

<img width="894" height="129" alt="image" src="https://github.com/user-attachments/assets/d88be2d4-9ddc-4f1a-9425-d9ecd8654a4f" />

**What was the extension name of the shell uploaded via the servers website?**

Có lẽ em thấy không còn khai thác được gì thêm trong thư mục tmp nữa, em để ý ở ổ C, còn có một thư mục cũng được tạo trong khoảng thời gian rất đáng ngờ là thư mục `inetpub` được tạo vào `3/2/2019 4:41 PM` nằm trong khoảng thời gian mà attacker đang thực hiện xâm nhập vào máy nạn nhân, và chuẩn bị nâng quyền.

<img width="944" height="737" alt="image" src="https://github.com/user-attachments/assets/8ae65d28-afda-441f-93c4-4041cdf19c4d" />

Bên trong thư mục có 1 thư muc khác là `wwwroot`, và trong này có 3 file: 2 file `jsp` và 1 file gif. Thông thường thì 1 file gif sẽ không mang lại nguy hiểm hay nghi ngờ gì đến cho máy tính, nhưng còn có 2 file `jsp`. Có thể đây chính là trang web của địa chỉ ip ánh xạ đến.

> Đây là một trang (JavaServer Page), một công nghệ Web có khả năng mở rộng, sử dụng dữ liệu mẫu (template data), các phần tử tùy chỉnh, (scripting languages) và đối tượng Java cho phía máy chủ.dữ Thông thường, liệu mẫu là các phần tử HTML hoặc XML, và trong nhiều trường hợp, máy khách chính là một trình duyệt Web.

<img width="879" height="706" alt="image" src="https://github.com/user-attachments/assets/4240da2b-f062-4acf-b16e-afffc7431d10" />

Và đồng thời nó cũng chính là file extention mà shell upload lên cho server.

<img width="878" height="114" alt="image" src="https://github.com/user-attachments/assets/3b8b2824-3a8c-4c61-9968-ae44738089bd" />

**What was the last port the attacker opened?**

Câu này chúng ta sẽ vào Windows Firewall để kiểm tra. Chúng ta vào phần Inbound Rules để xem xét các quy tắc mà tường lửa cho phép các dữ liêu đi vào (inbound). Cơ chế là do Windows Firewall sẽ block hết tất cả các (inbound data) chỉ cho phép các quy tắc với trạng thái `allow`.

Vào phần **filter by Group** và chọn vào **Rules without Group** tức là những quy tắc mà không thuộc về bất cứ nhóm nào,  attacker thông thường sẽ dùng những cái tên hợp pháp để đánh lừa firewall. Tuy nhiên việc các rules trong hệ thống đều thuộc 1 groups như (Core Network, World Wide Web Service), nên việc có các rules giả mạo sẽ thường được sử dụng trong mục `rules without
groups` này.

<img width="1911" height="808" alt="image" src="https://github.com/user-attachments/assets/48e0a311-e43d-4563-a042-1ace5c631bf8" />

port ở đây nó sử dụng là `1337` rất đúng khi khả nghi :)).

<img width="869" height="134" alt="image" src="https://github.com/user-attachments/assets/64e628c2-8843-4dfd-8c70-801f9bcd6ae1" />

**Check for DNS poisoning, what site was targeted?**
Như câu trước đó ta đã phân tích, việc attacker sử dụng tên miền google.com để ánh xạ đến 1 địa chỉ ip giả mạo đến server C2 của hắn, thì ở đây `site was target` là google.com.

<img width="878" height="136" alt="image" src="https://github.com/user-attachments/assets/077d32b1-3db2-41a6-8dab-732d339cb022" />







