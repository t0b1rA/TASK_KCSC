<img width="1837" height="766" alt="image" src="https://github.com/user-attachments/assets/42fc6267-4302-40c7-9ca7-a7adba4bdfad" />

Bài này chúng ta sẽ sử dụng khả năng sử dụng các hive key, và tập cách làm việc với các artifact trong windows registry, artifact windows, web browser và email. Bài này là dạng đề `SherLock`. Giờ chúng ta sẽ bắt đầu giải quyết tất cả các câu hỏi trong đề này. Đề sẽ cho chúng ta một file `.ad1` chúng ta sẽ sử dụng FTK imager để phân tích các bước đầu.

### What is the administrator's username?

<img width="425" height="740" alt="image" src="https://github.com/user-attachments/assets/e9112604-4943-4d22-88b7-d3cce544e0df" />

Đầu tiên khi ta mở file lên thì chúng ta sẽ thấy có 1 users duy nhất, vậy thì chúng ta cũng có thể kết luận được username admin của máy này là `Karen`.

<img width="1015" height="223" alt="image" src="https://github.com/user-attachments/assets/9c8a7ec7-6d81-4497-9a1f-1c8c3c9ba965" />

### What is the OS's build number?

Để tìm được những thông tin liên quan đến máy tính thì chúng ta cần vào thư mục config bên trong `system32` của Windows để trích xuất ra registry hive `SOFTWARE` và sử dụng công Registry Explorer để phân tích.

<img width="2273" height="745" alt="image" src="https://github.com/user-attachments/assets/aada125b-618b-408c-a0f1-26c2b24ce5e0" />

Đi theo path sau: `SOFTWARE\Microsoft\Windows NT\Current Version`. Bởi vì trong Windows NT chứa các tệp hệ thống , thư viện DLL, trình điều khiển drivers, cấu hình và dữ liệu phục vụ hoạt động của Windows.

<img width="1909" height="612" alt="image" src="https://github.com/user-attachments/assets/c8e0ea75-6ae8-4fbe-998e-38a136e779c2" />

Ở đây ta sẽ thấy registry data `CurrentBuildNumber` là `16299`.

<img width="1029" height="196" alt="image" src="https://github.com/user-attachments/assets/dd328a3f-d3ea-45f9-8c99-42e00acedcc8" />

### What is the hostname of the computer?

Tương tự vậy để chúng ta có thể xem các cấu hình thông tin hệ thống máy tính cũng sẽ cần trích xuất ra registry hive `SYSTEM` và sử dụng registry explorer để phân tích.

<img width="2007" height="744" alt="image" src="https://github.com/user-attachments/assets/15d8c00a-3d26-4249-b1e6-fc05d82e6b74" />

Để xem được computer name thì chúng ta đi theo path: `SYSTEM\CurrentControlSet\Control\Computername`

<img width="1800" height="630" alt="image" src="https://github.com/user-attachments/assets/7bf7cb27-d912-4f34-9e84-a07e21d97c46" />

Tên máy chủ của máy tính này là: `TOTALLYNOTAHACK`.

<img width="1033" height="200" alt="image" src="https://github.com/user-attachments/assets/005df876-3aa0-4280-925e-3e3d0582f718" />

### A messaging application was used to communicate with a fellow Alpaca enthusiest. What is the name of the software?

Câu này ứng dụng mà được sử dụng để nói chuyện với người khác, thì chắc hẳn là người dùng phải sử dụng gần đây, nên em sử dụng artifact `shimecache`,nó cho chúng ta biết cả vị trí mà file đó được thực thi, để xem thử gần đây người dùng này đã mở những ứng dụng nào. Để xem các dữ liệu bên trong `shimcache` chúng ta đi theo path sau: `SYSTEM\CurrentControlSet\Control\Session Manager\AppCompatCache`

<img width="1019" height="570" alt="image" src="https://github.com/user-attachments/assets/bfcd0180-7a32-430a-a2ea-fd73c2d441da" />

Nhìn kĩ một chút chúng ta sẽ thấy gần đây người dùng có sử dụng, `skype.exe` đã được tải xuống và thực thi gần đây. Lên gg search thử thì này là ứng dụng trò chuyện chuẩn rồi. 

<img width="819" height="143" alt="image" src="https://github.com/user-attachments/assets/c50593b4-d7fc-44f8-951b-27c537b5b734" />

<img width="1020" height="218" alt="image" src="https://github.com/user-attachments/assets/fbde269a-0954-416a-815a-eff91e98ad25" />

### What is the zip code of the administrator's post?

Câu này ban đầu em cũng thấy hơi lạ, nên em sử dụng hint của bài cho, thì chúng ta cần vào ftk imager, và trích xuất ra file `Web Data` bên trong, `Users\karen\AppData\Local\Google\Chrome\User Data\Default\Web Data` và sử dụng công cụ `SQLITE DB browser` để xem các thông tin bên trong file này.

<img width="1753" height="668" alt="image" src="https://github.com/user-attachments/assets/b1ae935a-83c7-4192-866d-5746302821a5" />

Mã zip thông thường có thể được lưu trữ trong mục autofill, để người dùng có thể sử dụng nó tiện hơn, hơn là nhớ mã zip cho một bài đăng. Nên em mở `sqlite db` chọn vào tab `Browser database`, ở đây chúng ta có thể tìm thấy ô autofill ở phía dưới tab, và hiện ra mã zip của admin sử dụng cho bài post.


<img width="1022" height="691" alt="image" src="https://github.com/user-attachments/assets/95103ea6-4398-40f6-94ce-77c3d9596790" />

<img width="1021" height="393" alt="image" src="https://github.com/user-attachments/assets/7c534a7a-2495-4870-8850-94ef43cb4dc4" />

### What are the initials of the person who contacted the admin user from TAAUSAI?

Câu này chúng ta cần sử dụng ftk imager, và trích xuất ra email `.ost` của user để dùng công cụ đọc nội dung bên trong file `.ost`

<img width="2196" height="738" alt="image" src="https://github.com/user-attachments/assets/55dcd31c-5560-468e-a44a-af2a0ad68fce" />

Sử dụng công cụ `Kernel for OST to PST`, để xem nội dung của các email bên tròn file `.ost`, như người gửi mail tới, mail mà người dùng gửi đi, metadata của file.

<img width="1863" height="1050" alt="image" src="https://github.com/user-attachments/assets/8ba938ba-df20-48ee-b61f-d3b92151f864" />

Để biết được người nào đã liên lạc với Karen từ TAAUSAI thì chúng ta cần đọc nội dung trong từng email bên trong mục `inbox`. 

<img width="2049" height="1232" alt="image" src="https://github.com/user-attachments/assets/eb173cc5-f478-4ba8-b2e2-a7bec05245a8" />

và sau 1 lúc em đọc từng email 1, thì em tìm thấy 1 người tên là: Michael dì đấy đã liên lạc với Karent, và offer cho người dùng một công việc với mức đãi ngộ rất cao 150000$ =)). Và chúng ta đồng thời cũng thấy tên viết tắt của người này là MS.

<img width="1017" height="367" alt="image" src="https://github.com/user-attachments/assets/ce402c94-6ad8-41cb-8570-003c72ffa75e" />

### How much money was TAAUSAI willing to pay upfront?

<img width="1025" height="177" alt="image" src="https://github.com/user-attachments/assets/8cf9848b-841e-4368-86d3-dcd0c6e7667f" />

### What country is the admin user meeting the hacker group in?

Câu này chúng ta đọc thêm 1 vài email, sẽ thấy được rằng người bên công ty sẽ hẹn Karent ra một địa chỉ đã được ghi sẳn tọa độ, để nói chuyện về công việc của mình.

<img width="2055" height="637" alt="image" src="https://github.com/user-attachments/assets/338bc545-3cea-49b4-b8bd-208b9666a109" />

`"27°22’50.10″N, 33°37’54.62″E"` Ở đây chúng ta sẽ có 1 tọa độ và chỉ cần copy vào gg map là sẽ có được kết quả.

<img width="1903" height="868" alt="image" src="https://github.com/user-attachments/assets/61c19971-5209-4e38-b85c-79340e492d55" />

Ở Ả rập, dịch qua tiếng a là **Erypt**.

<img width="1027" height="197" alt="image" src="https://github.com/user-attachments/assets/3c9e82bb-60b5-48b9-b4b5-e1be675cf721" />

### What is the machine's timezone? (Use the three-letter abbreviation)

Câu này nói về timezone thì chúng ta cũng có 1 path cho artifact này bên trong windows registry: `SYSTEM\CurrentControlSet\ControlTimeZoneInfomation`.

<img width="1179" height="240" alt="image" src="https://github.com/user-attachments/assets/a0a2be97-d8cd-42bf-9259-7bcf2e5064e3" />

ở đây chúng ta sẽ có `TimezoneKeyName` là `UCT`.

<img width="1024" height="197" alt="image" src="https://github.com/user-attachments/assets/5c2e42dd-3ca0-413c-8cda-e9af1fd78936" />

### When was AlpacaCare.docx last accessed?

Câu này ban đầu mình tưởng là có thể vào `ShimCache` để xem được thời gian lần cuối nó được sửa đổi, sẽ biết được khoảng thời gian có người truy cập vào nó. Nhưng mình phát hiện ra là mình đã nhầm với `Prefetch` khi mà `shimcache` chỉ cho chúng ta biết được khoảng thời gian cuối cùng file được modify chứ không liên quan đến việc file được truy cập khi nào.

Sau một lúc mò bên ổ đĩa đầu trong FTK imager không có kết quả, thì mình xem bên ổ đĩa thứ 2, và phát hiện nó nằm ngay ngắn ở đây.

<img width="1774" height="1324" alt="image" src="https://github.com/user-attachments/assets/ce085d84-0101-44d7-ad13-5bf0df262634" />

Lần cuối nó được truy cập vào là: `2019-03-17 21:52`, xem bên khung bên trái phía dưới.

<img width="1027" height="215" alt="image" src="https://github.com/user-attachments/assets/a6a3fa66-8d35-4b21-b9ac-e67d8bf700dd" />

### There was a second partition on the drive. What is the letter assigned to it?

Câu hỏi muốn chúng ta tìm được 1 ổ đĩa khác, nhưng mà ban nãy lúc làm câu tìm ứng dụng trò chuyện, mình có để ý hình như có 1 ổ đĩa khác ngoài ổ đĩa C, nên mình quyết định sử dụng lại `shimcache` một lần nữa, vì nó cung cấp đường dẫn đầy đủ, nên có thể biết được ổ đĩa đó là ổ nào. 

<img width="662" height="512" alt="image" src="https://github.com/user-attachments/assets/3a015d82-7abd-4c18-8a43-ab842d2c8835" />

 Đây chúng ta có thể tìm thấy thêm được 1 ổ `A` nữa.

<img width="1015" height="210" alt="image" src="https://github.com/user-attachments/assets/12bacc6f-cb37-4a6f-9f48-9e0656438c0e" />

### What is the answer to the question Company's manager asked Karen?

Trong quá trình offer một công việc cho Karent thì người tuyển dụng có đưa cho Karent một câu hỏi, và đợi cho Karent trả lời, chúng ta sẽ quay lại tìm cả câu hỏi và câu trả lời bên trong nội dung email.

<img width="1363" height="336" alt="image" src="https://github.com/user-attachments/assets/4a5bd7a4-ab75-4a18-84d8-4f10779df568" />

Đây là câu hỏi mà người tuyển dụng đã hỏi Karent.

<img width="852" height="280" alt="image" src="https://github.com/user-attachments/assets/1bc801fe-722f-4cdd-b2b2-63dc20f283ff" />

Còn đây là câu trả lời của Karent: `TheCardCriesNoMore`.

<img width="1022" height="219" alt="image" src="https://github.com/user-attachments/assets/e0d223c4-579b-4b2e-aed1-f06717e16818" />

### What is the job position offered to Karen? (3 words, 2 spaces in between)

Khi đọc kĩ các thông tin tuyển dụng sau khi mà người tuyển dụng nhận được câu trả lời, thì ông ấy có nhắc đến công việc mà Karent sẽ làm vì nó phù hợp với cô ấy.

<img width="1995" height="338" alt="image" src="https://github.com/user-attachments/assets/fa1399e6-9d86-48bb-bb50-202963d51127" />

<img width="1020" height="219" alt="image" src="https://github.com/user-attachments/assets/af60d416-a02e-4e9e-a8f0-e4b748600d31" />

### When was the admin user password last changed?

Để xem được mật khẩu của người dùng admin đã đổi khi nào, chúng ta cần nhớ đến 1 kiến thức, là trong windows registry thì tất cả những thông tin liên quan đến tài khoản và mật khẩu của người dùng cục bộ trong miền đều được lưu trữ bên trong registry SAM. Và để một người dùng xem trực tiếp hive này bên trong một `live machine` thì người đó cần có 1 quyền rất cao trong hệ thống để có thể có quyền xem được. 

Bây giờ chúng ta quay trở lại FTK imager để trích xuất hive SAM này ra để dùng registry explorer phân tích tiếp. 

<img width="1775" height="868" alt="image" src="https://github.com/user-attachments/assets/1257b173-7265-4b4f-b86d-b7625ef708e3" />

Để có thể xem được lần cuối mà người dùng này đổi mật khẩu khi nào chúng ta đi theo path: `SAM\Domain\Account\Users`.

<img width="2012" height="407" alt="image" src="https://github.com/user-attachments/assets/809fe584-52ed-429f-9714-85f62f0d5ae1" />

**Lưu ý**: bởi vì trong bài không ghi rõ format nên em đã thử 2 đáp án là `03/21/2019 19:13:09` và `21/03/2019 19:13:09`, thì đáp án đầu tiên được.

<img width="1021" height="215" alt="image" src="https://github.com/user-attachments/assets/6c28c1a3-1fe6-4fc5-87b6-49368a720c3c" />

### What version of Chrome is installed on the machine?

Ở đây chúng ta sử dụng FTK imager, để xem được file `Last Version` được lưu bên trong `C:\Users\Karent\AppData\Local\Google\Chrome\User Data\last Version`.

<img width="1717" height="789" alt="image" src="https://github.com/user-attachments/assets/2495f064-6fd1-48be-b48a-8b06e1bc04bf" />

### What is the URL used to download Skype?

Câu này liên quan đến phần `url` tải xuống, thì chúng ta cần trích xuất file `history` trong `Chrome` ra để sử dụng `sqlite DB` theo dõi nội dung của file.

Chúng ta sử dụng file history đó, vào tab `Browser Database` và chọn vào ô `download url chain` để nó liệt kê ra cho chúng ta tất cả những ứng dụng mà người dùng Karent này đã tải xuống, tìm chút chúng ta sẽ thấy đường dẫn đầy đủ của ứng dụng `Skype`.

<img width="2551" height="842" alt="image" src="https://github.com/user-attachments/assets/081b953b-b3e4-4a19-a329-c5ea1f4415d1" />

`https://download.skype.com/s4l/download/win/Skype-8.41.0.54.exe`

<img width="1021" height="199" alt="image" src="https://github.com/user-attachments/assets/800e169e-29b5-4a63-af52-69de6defd7db" />

### What is the domain name of the website Karen browsed on Alpaca care that the file AlpacaCare.docx is based on?

Câu này ban đầu mình nghĩ là nó sẽ nằm trong một số tên miền bên trong file `History` của Chrome nhưng mà sau 1 vài lần thử thì đều không được. Mình có đọc hint là hãy sử dụng file `.docx` đó để truy ra đường dẫn. Vậy đầu tiên chúng ta cần export nó ra từ ftk imager.

<img width="1902" height="783" alt="image" src="https://github.com/user-attachments/assets/131465b0-1efb-42b7-8855-598fe392cbed" />

Sau đó mở phần mềm đọc `wps` lên để xem. 

<img width="948" height="636" alt="image" src="https://github.com/user-attachments/assets/dfe09e93-fb10-4c36-a1ed-93f590422231" />

Lướt xuống cuối mình vẫn bị lừa thêm 1 lần nữa, lúc sau mình nhìn vào dòng cuối cùng thì nó là một `link` có thể truy cập được. Mình copy link đó dán lên `brave` thì mình thấy được tên miền của nó.

<img width="511" height="642" alt="image" src="https://github.com/user-attachments/assets/f733c42c-357d-47fa-b5e1-d2e48cae1ef6" />

Ấn chuột phải vào mình mới biết đây là một link khác. Và dán lên brave xem thử.

<img width="1270" height="1356" alt="image" src="https://github.com/user-attachments/assets/984e603c-fd7b-4a37-91eb-f172dcf91e1c" />

Thì đây là tên miền của trang web đó: `palominoalpacafarm.com`

<img width="1023" height="229" alt="image" src="https://github.com/user-attachments/assets/02fabea8-27c9-474b-9215-023c8f676d01" />

Vậy là em đã hoàn thành xong challenge Sherlock này, nó giúp cho em ôn lại kiến thức về các hive và key trong `windows registry` khá tốt, kết hợp với việc tập liên kết sử dụng nhiều công cụ để tìm ra đáp án. 
