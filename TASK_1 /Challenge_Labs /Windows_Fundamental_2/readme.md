### TASK 2: System Configuration and Advanced System Settings

**The System Configuration** (`MSConfig`) là một advance troubleshootingss, và nó có có mục đích là giúp chẩn đoán các sự cố khởi động. **System configuration** nằm trong [system engineering](https://en.wikipedia.org/wiki/Systems_engineering) được biết đến là một tiến ích tích hợp của Windows. Nó cho phép bạn khởi động, tắt trình điều khiển hoặc các dịch vụ. 

<img width="640" height="431" alt="image" src="https://github.com/user-attachments/assets/da6e5486-a132-46d7-8ae6-ae64c94ec84c" />


**Advanced System Settings** là một bảng điều khiển trong Windows cung cấp các tùy chọn sâu để tinh chỉnh hiệu suất và hoạt động của hệ điều hành, đồng thời cho phép người dùng tùy chỉnh các tính năng phức tạp như quản lý bộ nhớ ảo, hiệu ứng hình ảnh, thiết lập khởi động và quản lý bộ xử lý.

<img width="798" height="918" alt="image" src="https://github.com/user-attachments/assets/cfe8cadd-297c-4e03-9ed2-26e3a216efbb" />

**What is the name of the service that lists Systems Internals as the manufacturer?**

<img width="636" height="432" alt="image" src="https://github.com/user-attachments/assets/42402dc7-a7e3-40c2-97ee-b2c0c3491287" />

<img width="884" height="143" alt="image" src="https://github.com/user-attachments/assets/d8d03fb2-ab49-4b20-ae80-eb08dccd1787" />

**Whom is the Windows license registered to?**

<img width="638" height="433" alt="image" src="https://github.com/user-attachments/assets/f1f73a84-18ab-466c-900a-ca93032f37c9" />

Sau đó ta ấn vào launch của `About Windows` để xem được thêm thông tin về giấy phép Windows hiện tại

<img width="512" height="473" alt="image" src="https://github.com/user-attachments/assets/32d5bbd6-e501-4ea3-83e5-0de94312ef6c" />

<img width="866" height="121" alt="image" src="https://github.com/user-attachments/assets/eab60b58-5b1c-47a9-b6eb-14cbfa0e4564" />

**What is the command for Windows Troubleshooting?**

<img width="631" height="428" alt="image" src="https://github.com/user-attachments/assets/bf252e2b-ec01-4fab-9634-53f879570a73" />

<img width="917" height="143" alt="image" src="https://github.com/user-attachments/assets/5e4f086e-3443-4484-a69c-5f9ed1c02ed5" />

**What command will open the Control Panel? (The answer is  the name of .exe, not the full path)**
Đây là đường dẫn đầy đủ để có thể launch được `control panel`. Tên **System Properties**

<img width="633" height="428" alt="image" src="https://github.com/user-attachments/assets/0a25a4ee-7c67-4e3f-a942-de746d4144eb" />

<img width="877" height="138" alt="image" src="https://github.com/user-attachments/assets/b95adff1-b06e-46cc-a5a3-100508355b2e" />

### TASK 3: Change UAC Settings

Tính năng UAC của Windows có thể bật hoặc tắt bất cứ lúc nào. UAC có 4 level của việc bảo mật, trong đó nó sẽ điều khiển cách mà Windows thông báo khi ứng dụng hoặc người dùng cố gắng để tạo ra các sự thay đổi lên hệ thống.

- **Always notify**: là mức bảo mật cao nhất, sẽ luôn luôn thông báo khi có bất cứ ứng dụng nào cố gắng để thay đổi.

<img width="840" height="618" alt="image" src="https://github.com/user-attachments/assets/9f1dd463-9d0b-4499-9f7b-f3b13b2e8841" />

- **Notify for apps**:  Nó sẽ không thông báo khi chính người dùng thay đổi mà chỉ có ứng dụng thì thông báo.

<img width="841" height="616" alt="image" src="https://github.com/user-attachments/assets/7054f802-8875-4164-bffe-a601619e37e1" />

- **Notify without dimming**: sẽ không thông báo với người dùng chỉ thông báo các thay đổi từ ứng dụng, nhưng không làm tối màn hình (`1 cơ chế cho thấy windows vào trạng thái bảo mật và hiện ra màn hình 1 thông báo cho phép cấp quyền hay khoong`)

<img width="840" height="615" alt="image" src="https://github.com/user-attachments/assets/0c3d93a4-80ec-442c-bdc4-1acd78909b17" />

- **Never notify**: Không bao giờ thông báo khi ứng dụng và người dùng thực hiện thay đổi, mức bảo mật thấp nhất.

<img width="831" height="622" alt="image" src="https://github.com/user-attachments/assets/d1536289-3147-4c7b-8541-ff7dc0f5151f" />

**What is the command to open User Account Control Settings? (The answer is the name of the .exe file, not the full path)**

Chúng ta mở `msconfig` vào tab tools và xem mục `Change UAC Settings`

<img width="944" height="655" alt="image" src="https://github.com/user-attachments/assets/d394c856-17bd-46b0-ad50-9d7f3788cff4" />

<img width="877" height="160" alt="image" src="https://github.com/user-attachments/assets/3c7e897d-241b-405f-8c98-64c80499ed99" />

### TASK 4: Computer Management

TASK này chúng ta sẽ đi qua 1 chút về một công cụ khác của **System Configuration** panel đó là **Computer Management** (`compmgmt`), tính năng của nó bao gồm 3 phần chính là **System tools**, **Storage**, **Service Application**

<img width="940" height="781" alt="image" src="https://github.com/user-attachments/assets/b9631abe-f820-49d4-bd69-9b0b87d1db0f" />

**Task Scheduler** là một công cụ có sẳn trong Windows giúp người dùng thực hiện một số hành động và tác vụ trên máy tính như tự động chạy một phần mềm nào đó có sẳn trên máy tính. Task Scheduler có rất nhiều tính năng hỗ trợ cho máy tính, khả năng tự động hóa tác vụ người dùng muốn chạy trên Windows nhanh chóng và hiệu quả. Một Task có thể chạy được các ứng dụng, script,... và task sẽ có thể cấu hình để chạy tại 1 thời điểm cụ thể, là khi vừa đăng nhập hoặc đăng xuất.

<img width="2158" height="998" alt="image" src="https://github.com/user-attachments/assets/0e4c4f0b-3269-4c4a-ba32-70ed72cb78d4" />

Trong khung ở giữa sẽ cho chúng ta những thông tin về, thời gian tác vụ chạy, trạng thái, tên, lần chạy cuối, kết quả cuối. Bên ô dưới chúng ta có thể tìm hiểu được tác vụ được chạy là gì. Ở đây ta thấy trong hình là tác vụ powershell thực hiện 1 lệnh `powershell.exe -Command Get-ComputerInfo ^> C:\Logs\sysinfo.txt` lệnh này sẽ lấy về các thông tin của máy tính và ghi nó vào `sysinfo.txt`. Trong attack thì đây có thể là 1 hành động dùng để khám phá xem kẻ tấn công đang ở trong máy thật hay `sandbox` hoặc `vm machine`.

**Event Viewer** là cho phép chúng ta có thể xem được các sự kiện đã xảy ra trên máy tính. Những bản ghi này của các sự kiện có thể được coi là các dấu vết kiểm tra mà có thể được được sử dụng để hiểu được các hoạt động của hệ thống. Giúp ích cho việc chẩn đoán các vấn đề và phân tích các hành động đã thực thi trên máy tính, giúp chúng ta tìm được các dấu vết của cuộc tấn công tại ban đầu.

<img width="489" height="145" alt="image" src="https://github.com/user-attachments/assets/0ba9e1f5-1ca8-4007-9618-b2dddad4bd21" />

**Share Folder** cho chúng ta thấy danh sách 1 list các folder được share và đã được share hoàn thành mà người khác kết nối tới.

<img width="548" height="100" alt="image" src="https://github.com/user-attachments/assets/85a7d59e-7107-4ee5-9b7d-d871bdd53f0b" />

**local Users and Group** `lusrmgr.msc` là nơi quản lý các người dùng hiện có trên máy tính.

<img width="941" height="780" alt="image" src="https://github.com/user-attachments/assets/0cb4139c-4403-46e3-8beb-5a19669ccfbb" />

**Device Manager** cho phép chúng ta có thể xem và cấu hình phần cứng, nó liệt kê tất cả danh sách các thiết bị phần cứng được Windows nhận diện, kể cả các vấn đề liên quan đến Driver thiết bị chưa nhận diện được. Windows Manager dùng để quản lý các thiết bị phần cứng trong máy tính của người dùng.

<img width="269" height="289" alt="image" src="https://github.com/user-attachments/assets/bb1745af-f552-4628-b09f-b0dda5db42b1" />

**Storage**

Bên trong storage bao gồm **Windows Server Backup** và **Disk Management**. Trong đó thì **Disk Management** dùng để quản lý ổ đĩa và giúp chúng ta có thể phân vùng ổ đĩa, gộp ổ đĩa, tạo ổ đĩa mới, và gán tên cho ổ đĩa.

<img width="833" height="211" alt="image" src="https://github.com/user-attachments/assets/dee91729-a60e-4722-a42f-2297e4272b9c" />

**Services and Applications**

**Service** là một loại ứng dụng đặc biệt mà chạy trong nền. Bạn có thể liệt kê và xem được tất cả các dịch vụ và trạng thái của nó bên trong mục services. Trong mục **Services** nó sẽ hiển thị: tên, trạng thái và các giá trị khác. Nếu như bạn muốn có thêm được nhiều thông tin cho bất cứ dịch vụ nào. Thì chuột phải vào phần services và nhấn chọn `Properties`.

<img width="2369" height="1232" alt="image" src="https://github.com/user-attachments/assets/f9fbbec1-91a7-46e3-adea-b58b529d2566" />

<img width="705" height="828" alt="image" src="https://github.com/user-attachments/assets/5be2bfa9-48d3-4461-83d6-d643ec65fff0" />

**WMI Control**

Cấu hình và điều khiển dịch vụ **Windows Management Instrumentiton (WMI)**, đây là dịch vụ cho phép các scripts languages (như là VBScript hoặc WIndows Powershell) dùng để quản lý máy tính cá nhân Microsoft Windows và server, bằng cách trực tiếp và remote. Microsoft cung cấp giao diện command-line gọi là (Windows Management Instrumentation Command-line (WMIC)).

**What is the command to open Computer Management?
(The answer is the name of the .msc file, not the full path)**

Mở `msconfig` vào tab tools và tìm computer management.

<img width="930" height="660" alt="image" src="https://github.com/user-attachments/assets/8ed4d792-e64b-46bf-b2e3-ab952916f460" />

<img width="875" height="165" alt="image" src="https://github.com/user-attachments/assets/6846f804-3576-439b-b043-814717adb44d" />

**When is the npcapwatchdog scheduled task set to run at?**

Tìm tác vụ `npcawatchdog` -  là một dịch vụ (service) chạy ngầm của Npcap, một trình điều khiển và thư viện bắt gói tin mạng cho Windows, có nhiệm vụ giám sát trạng thái hoạt động của Npcap và tự động khởi động lại hoặc xử lý các sự cố liên quan đến trình điều khiển, đảm bảo tính ổn định và khả năng hoạt động liên tục của tính năng bắt/gửi gói tin mạng thô. 

<img width="1546" height="775" alt="image" src="https://github.com/user-attachments/assets/4e430d55-0b89-4d79-bde3-9b77e4bd2952" />

Chúng ta sẽ thấy ở mục `triggers` sẽ tự động chạy khi máy được khởi động.

<img width="880" height="147" alt="image" src="https://github.com/user-attachments/assets/cea9f10e-2dd3-4c3d-b59c-fc2f6f520f93" />

**What is the name of the hidden folder that is shared?**

Ở đây chúng ta sẽ vào mục share folder để kiếm. 
<img width="1543" height="781" alt="image" src="https://github.com/user-attachments/assets/8e6a1504-5c25-4a5d-8ec2-46b902472d78" />

Chọn share và tiếp tục.
<img width="1543" height="792" alt="image" src="https://github.com/user-attachments/assets/a7da9b6c-4981-4b52-98cf-fcb10baa9340" />

<img width="899" height="123" alt="image" src="https://github.com/user-attachments/assets/1ca55b2f-a446-451d-b051-8a88ae697bea" />

### TASK 5: System Infomation

Windows bao gồm một công cụ gọi là Microsoft System Infomation (Msinfo32.exe). Công cụ này thu thập thông tin về máy tính và hiển thị cái nhìn toàn diện về phần cứng, thành phần hệ thống và môi trường phần mềm, có thể sử dụng để chẩn đoán các vấn đề xảy ra với máy tính.

Những thông tin trong phần `System Summary` được chia thành 3 phần chính sau:

- **Hardware Resources**: là các đường dẫn bus có thể gán, có thể chỉ định địa chỉ, cho phép các thiết bị ngoại vi và bộ xử lý hệ thống giao tiếp với nhau. **Hardware resources** đều bao gồm I/O port, address, interrupt vector, và các khối cho địa chỉ bộ nhớ bus-relative.

- **Components**: bao gồm các thông tin cụ thể về các thiết bị phần cứng đã được tải xuống hoặc được kết nối với máy tính.

<img width="3631" height="1877" alt="image" src="https://github.com/user-attachments/assets/ad44e1ad-4a1c-4792-84ed-57bd84b50289" />

- **Software Enviroment**: bao gồm các thông tin về các phần mềm đã được đưa vào hệ điều hành và phần mềm mà người dùng đã tải xuống.

<img width="3219" height="1608" alt="image" src="https://github.com/user-attachments/assets/3590157c-d23a-4715-bd48-e7c11913b71e" />

> Trong hình là `Enviroment variables` (biến môi trường) chứa các thông tin về môi trường hệ điều hành. Những thông tin này bao gồm các chi tiết về đường dẫn hệ điều hành, số các bộ xử lý được sử dụng bởi hệ điều hành và các nơi cho folder khác.
>
> Chúng ta có thể thêm vào các biến môi trường ở vị trí này `Control Panel > System and Security > System > Advanced system settings > Environment Variables` OR `Settings > System > About > system info > Advanced system settings > Environment Variables`

**System Summary** sẽ hiển thị các thông số kĩ thuật cho máy tính đó như là nhãn hiệu và mô hình bộ xử lí.

<img width="3622" height="1730" alt="image" src="https://github.com/user-attachments/assets/a130803e-0a5d-4544-b12e-8d4526cee4b5" />

**What is the command to open System Information? (The answer is the name of the .exe file, not the full path)**
Mở `msconfig` và tìm system infomation

<img width="931" height="664" alt="image" src="https://github.com/user-attachments/assets/691c22df-9bd6-43fc-879f-dbf3fb9f28e7" />

<img width="886" height="121" alt="image" src="https://github.com/user-attachments/assets/9eda176e-83be-49ed-a685-6fa75b73cdce" />

**What is listed under System Name?**
Bật `msinfo32` và xem trong mục thông số `system summary`

<img width="823" height="666" alt="image" src="https://github.com/user-attachments/assets/5ff4ad0e-b51a-4f2c-b6af-1e2f10cb2d38" />

<img width="902" height="131" alt="image" src="https://github.com/user-attachments/assets/1c421ddd-f2d6-440f-914f-c7e3ae201520" />

**Under Environment Variables, what is the value for ComSpec?**
Vào mục `software enviroment` để xem biến môi trường của `comspec`
<img width="833" height="654" alt="image" src="https://github.com/user-attachments/assets/982279f5-e3e4-434f-bc04-bf085b28add6" />

<img width="897" height="114" alt="image" src="https://github.com/user-attachments/assets/7579677c-1bae-4662-8b32-1c9a15b5df9d" />

### TASK 6: Resource Monitor

**Resources Monitor (resmon)**: hiển thị mỗi tiến trình và tổng hợp các thông tin được sử dụng tài nguyên trong thời gian thực bao gồm các tiến trình `hardware` CPU, memory, disk, network. Hơn nữa còn cung cấp các chi tiết về tiến trình `software` được sử dụng cho module và xử lý các tệp riêng lẻ. 

Trong mục Overview tab, `Resmon` hiển thị:

- **CPU**

<img width="1245" height="547" alt="image" src="https://github.com/user-attachments/assets/f8393b38-7bb9-4d36-96e7-73a3228810ff" />

- **Memory**

<img width="1250" height="433" alt="image" src="https://github.com/user-attachments/assets/6cacfc72-7be1-4f7d-9b8a-e1821a26299e" />

- **Disk**

<img width="1248" height="431" alt="image" src="https://github.com/user-attachments/assets/b62249da-9cff-479b-9f00-77b140a96c24" />

- **Network**

<img width="1243" height="386" alt="image" src="https://github.com/user-attachments/assets/24f40b5a-9a31-45ac-ba21-38266f9b3206" />

**What is the command to open Resource Monitor? (The answer is the name of the .exe file, not the full path)**

<img width="926" height="665" alt="image" src="https://github.com/user-attachments/assets/2bd9476b-1ef0-4bea-b093-7044a510ec54" />

<img width="874" height="112" alt="image" src="https://github.com/user-attachments/assets/f35ca0c6-630d-4e68-a248-2b7dcb1f1665" />

### TASK 7: Command Prompt

**In System Configuration, what is the full command for Internet Protocol Configuration?**
<img width="932" height="647" alt="image" src="https://github.com/user-attachments/assets/61b0275a-0de8-4a68-892f-73e5433e38f1" />


<img width="898" height="127" alt="image" src="https://github.com/user-attachments/assets/cf63c500-495c-4567-84f2-f77b88fb04ea" />

**For the ipconfig command, how do you show detailed information?**

<img width="1884" height="1494" alt="image" src="https://github.com/user-attachments/assets/832f2e50-220a-4d15-a608-17be0fffd531" />

<img width="873" height="118" alt="image" src="https://github.com/user-attachments/assets/905380ea-0a59-46e7-9fb5-928717536184" />

### TASK 8: Registry Editor

**Regedit** là mọt công cụ dùng để hiển thị các **Regitry hive** bên trong Windows Registry, giúp chúng ta có thể quản tìm kiếm được các thông tin qua trọng về cấu hình hệ thống cho người dùng, ứng dụng và cả thiết bị phần cứng.

<img width="3189" height="1417" alt="image" src="https://github.com/user-attachments/assets/92f7a3cc-7e39-4338-95f2-39761d199400" />

**The registry** chứa các thông tin mà Windows liên tục tham chiếu đến trong suốt quá trình hoạt động:
- Hồ sơ cho từng người dùng.
- Các metadata về ứng dụng và chương trình được tải xuống, các tài liệu, thư mục, file được tạo ra trên hệ thống.
- Phần cứng nào được hiện diện trên hệ thống.
- Các thông tin về mạng được sử dụng.

**What is the command to open the Registry Editor? (The answer is the name of  the .exe file, not the full path)**

<img width="923" height="656" alt="image" src="https://github.com/user-attachments/assets/768c141e-db28-4f71-942c-c1a12f2771ed" />

<img width="873" height="118" alt="image" src="https://github.com/user-attachments/assets/4864d69d-0f2b-4a8e-9be4-f0f4c8d22686" />



