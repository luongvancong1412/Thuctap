<h1> System setup </h1>

<h2> Mục lục </h2>

- [I. System Setup](#i-system-setup)
- [II. System BIOS](#ii-system-bios)
  - [1. Chi tiết System BIOS](#1-chi-tiết-system-bios)
    - [1.1 System Information](#11-system-information)
    - [1.2 Memory Settings](#12-memory-settings)
    - [1.3 Processor Settings](#13-processor-settings)
    - [1.4 SATA settings](#14-sata-settings)
    - [1.5 NVMe Settings](#15-nvme-settings)
    - [1.6 Boot Settings](#16-boot-settings)
    - [1.7 Integrated Devices](#17-integrated-devices)
- [Tài liệu tham khảo](#tài-liệu-tham-khảo)

# I. System Setup

Mở System Setup để cấu hình:
- System BIOS
- iDRAC Settings
- Device Settings

Các bước mở System Setup:
1. Khởi động server
2. Nhấn phím `<F2>`


![Imgur](https://i.imgur.com/3BhygG0.png)

1. Chọn 1 trong 3 option của system setup

![Imgur](https://i.imgur.com/0wBSOnN.png)

# II. System BIOS

- Click `System BIOS` để vào BIOS

![Imgur](https://i.imgur.com/0wBSOnN.png)

## 1. Chi tiết System BIOS

![Imgur](https://i.imgur.com/FmQ7Yz1.jpg)

![Imgur](https://i.imgur.com/LlM54gD.jpg)

|Option|Description|
|---|---|
System Information|Cung cấp thông tin về hệ thống như: the system model name (tên kiểu hệ thống), BIOS version và Service Tag.
Memory Settings|Cung cấp thông tin và các tùy chọn liên quan đến bộ nhớ (Memory) đã cài đặt.
Processor Settings|Cung cấp thông tin và các tùy chọn liên quan đến bộ xử lý (processor) như speed (tốc độ) và cache size (kích thước bộ nhớ đệm).
SATA Settings|Cung cấp các tùy chọn để enable or disable SATA controller và ports.
NVMe Settings|Cung cấp các option để thay đổi NVMe settings. If the system contains the NVMe drives that you want to configure in a RAID array, you must set both this field and the Embedded SATA field on the SATA Settings menu to RAID mode. You might also need to change the Boot Mode setting to UEFI. Otherwise, you should set this field to Non-RAID mode.
Boot Settings|Cung cấp các option để chọn chế độ khởi động - Boot mode (là BIOS hoặc UEFI). Cho phép sửa đổi cài đặt boot UEFI and BIOS.
Network Settings|Cung cấp các option để quản lý UEFI network settings and boot protocols. Legacy network settings được quản lý từ menu Device Settings.
Integrated Devices|Cung cấp các option để quản lý integrated device controllers and ports, các tính năng và option liên quan.
Serial Communication|Cung cấp các option để quản lý serial ports, các tính năng và option liên quan.
System Profile Settings|Cung cấp các tùy chọn để thay đổi processor power management settings (các cài đặt quản lý bộ sử lý nguồn), and memory frequency (tần số bộ nhớ).
System Security|Cung cấp các tùy chọn để cấu hình system security settings như system password, setup password, Trusted Platform Module (TPM) security, and UEFI secure boot. Nó cũng quản lý nút nguồn trên hệ thống.
Redundant OS Control|Đặt thông tin redundant OS (OS dự phòng) để kiểm soát redundant OS
Miscellaneous Settings|Cung cấp các tùy chọn để thay đổi system date and time.|

### 1.1 System Information

![Imgur](https://i.imgur.com/fiZ6Rrf.jpg)

Option|Description|
|---|---|
System Model Name|Hiển thị tên server.
System BIOS Version|Hiển thị phiên bản BIOS được cài đặt trên hệ thống.
System Management Engine Version|Hiển thị phiên bản hiện tại của Công cụ quản lý hệ thống.
System Service Tag|Hiển thị số Service Tag.
System Manufacturer|Hiển thị tên nhà sản xuất hệ thống.
System Manufacturer Contact Information|Hiển thị thông tin liên hệ nhà sản xuất hệ thống.
System CPLD Version|Hiển thị thông tin phiên bản complex programmable logic device (CPLD) hiện tại của hệ thống.
UEFI Compliance Version|Hiển thị phiên bản của UEFI compliance.

### 1.2 Memory Settings

![Imgur](https://i.imgur.com/mzZcAA9.jpg)


Option|Description|
|---|---|
System Memory Size|Hiển thị kích thước bộ nhớ trong hệ thống.
System Memory Type|Hiển thị loại bộ nhớ được cài đặt trong hệ thống.
System Memory Speed|Hiển thị tốc độ bộ nhớ hệ thống.
System Memory Voltage|Hiển thị điện áp (voltage) của bộ nhớ hệ thống.
Video Memory|Hiện thị dung lượng bộ nhớ video.
System Memory Testing| Hiển thị xem kiểm tra bộ nhớ hệ thống có được chạy trong quá trình khởi động hệ thống không. Có 2 Option là Enabled và Disabled. Mặc định là Disabled.
Dram Refresh Delay|**Performance** - Cho phép `CPU memory controller` delay việc chạy các lệnh **REFRESH** , ta có thể cải thiện hiệu suất cho một số khối lượng công việc (you can improve the performance for some workloads). **Minimum** - Giảm thiểu thời gian delay, nó đảm bảo `memory controller` chạy lệnh REFRESH trong khoảng thời gian cố định (at regular intervals). Đối với servers dựa trên intel-based, cài đặt này chỉ ảnh hưởng đến các hệ thống được cấu hình với DIMMs sử dụng DRAMS 8 Gb (use 8 Gb density DRAMS).
Memory Operating Mode| Chọn các mode memory operating (chế độ vận hành bộ nhớ). Các option có sẵn là **Optimizer Mode** (chế độ tối ưu hoá), **Single Rank Spare Mode** (Chế độ dự phòng xếp hạng đơn), **Multi Rank Spare Mode** (Chế độ dự phòng nhiều hạng) và Mirror Mode (Chế độ phản chiếu - bản sao). **Cấu hình mặc định** là **Optimizer Mode**.|
Current State of Memory Operating Mode|Hiển thị trạng thái hiện tại của **memory operating mode**.
Node Interleaving|Hiển thị  **Non-Uniform Memory Architecture (NUMA)** có hỗ trợ không. Nếu trường này là **Enabled**, **memory interleaving** (tính năng xen kẽ bộ nhớ) được hỗ trợ nếu **symmetric memory configuration** (cấu hình bộ nhớ đối xứng) được cài đặt. Nếu trường này là **Disabled**, Hệ thống hỗ trợ cấu hình bộ nhớ NUMA (asymmetric - không đối xứng). Option này mặc định là **Disable**
ADDDC Setting|Enables hoặc disables tính năng **ADDDC Setting**. Khi enabled  tính năng Adaptive Double DRAM Device Correction (ADDDC), failing DRAMs are dynamically mapped out (các DRAM lỗi sẽ được ánh xạ động). Khi được đặt thành Enabled nó có thể có một số tác động đến hiệu suất hệ thống (system performance) trong một số khối lượng công việc nhất định (certain workloads). Tính năng chỉ áp dụng cho các DIMM x4. Option này mặc định là **Enabled**.
Native tRFC Timing for 16Gb DIMMs|Enables 16 Gb density DIMMs hoạt động ở Row Refresh Cycle Time (tRFC) được lập trình. Bật tính năng này có thể cải thiện hiệu suất hệ thống đối với 1 số cấu hình. Tuy nhiên, việc bật tính năng này không ảnh hưởng đến cấu hình với 16 Gb 3DS/TSV DIMMs. Option mặc định là **Enabled**.
Opportunistic Self-Refresh|Option mặc định là Disable và không được hỗ trợ khi DCPMM có trong hệ thống.
Correctable Error logging|Ghi nhật ký lỗi có thể sửa chữa. Option này mặc định là disable.
DIMM Self Healing (Post Package Repair) on Uncorrectable Memory Error|Enable/Disable Post Package Repair (PPR) on Uncorrectable Memory Error. Option này mặc định là Enabled.|

### 1.3 Processor Settings

![Imgur](https://i.imgur.com/FZNFW6s.jpg)

![Imgur](https://i.imgur.com/bWegmTV.jpg)

![Imgur](https://i.imgur.com/CgoJ7hM.jpg)

![Imgur](https://i.imgur.com/0gmqy26.jpg)


Option|Description
|---|---|
Logical Processor|Nếu option này được Enabled, BIOS sẽ hiển thị tất cả các bộ xử lý logic (logical processors).Nếu Disabled, BIOS chỉ hiển thị 1 logical processor trên mỗi core. option này mặc định là Enabled
Virtualization Technology|Enables or disables virtualization technology cho bộ xử lý processor. option mặc định là Enabled
Adjacent Cache Line Prefetch|Tối ưu hoá hệ thống cho các ứng dụng cần sử dụng khả năng truy cập sequential memory cao. This option is set to Enabled by default.
Hardware Prefetcher|Enables or disables trình cài đặt sẵn phần cứng (hardware prefetcher). This option is set to Enabled by default.
DCU Streamer Prefetcher| Enables or disables Data Cache Unit (DCU) streamer prefetcher. This option is set to Enabled by default.
DCU IP Prefetcher| Enables or disables Data Cache Unit (DCU) IP prefetcher. This option is set to Enabled by default.
Sub NUMA Cluster|Sub NUMA Clustering (SNC) là một tính năng để chia LLC thành các cụm (clusters) rời rạc dựa trên phạm vi địa chỉ, Với mỗi cụm được kết nối tới một tập hợp con của memory controllers trong hệ thống. Nó cải thiện độ trễ trung bình (average latency) cho LLC. This option is set to Disabled by default.
UPI Prefetch|Cho phép bạn lấy (get) memory được bắt đầu đọc sớm trên DDR bus. Đường dẫn Ultra Path Interconnect (UPI) Rx sẽ tạo ra bộ nhớ suy đoán (speculative memory) được đọc trược tiếp đến Bộ điều khiển Bộ nhớ Tích hợp  Integrated Memory Controller (iMC) directly. This option is set to Enabled by default.
LLC Prefetch|Enables or disables Tìm nạp trước LLC (LLC Prefetch) trên tất cả các chuỗi. This option is set to **Disabled** by **default**.
Dead Line LLC Alloc|Enables or disables Phân bổ LLC dòng chết (Dead Line LLC Alloc). This option is set to **Enabled** by **default**.
Directory AtoS|Enables or disables the Directory AtoS. Tối ưu hoá AtoS giảm độ trễ đọc từ xa để truy cập đọc lặp lại mà không cần ghi can thiệp. This option is set to **Disabled** by **default**.
Logical Processor Idling|Cho phép cải thiện hiệu quả năng lượng (energy efficiency) của một hệ thống. Nó sử dụng thuật toán đỗ xe lõi (core parking) và đỗ một số logical processors trong hệ thống, từ đó cho phép processor cores tương ứng chuyển sang trạng thái không sử dụng điện năng thấp hơn (lower power idle state). (Chỉ có thể được bật nếu OS hỗ trợ). It is set to **Disabled** by **default**.
Configurable TDP|Cho phép configure the TDP level. Các options có sẵn là Nominal, Level 1, and Level 2. This option is set to **Nominal** by **default**. NOTE This option is only available on certain stock keeping units (SKUs) of the processors.
x2APIC Mode| This option is set to **Enabled** by **default**.So với kiến trúc xAPIC truyền thống, xAPIC mở rộng khả năng định địa chỉ của bộ xử lý và nâng cao hiệu suất phân phối ngắt. Công nghệ ảo hoá (Virtualization technology) phải được **enabled** để có thể bật, tắt **x2APIC mode**. x2APIC mode bị buộc Disabled khi virtualization technology is disabled.
Number of Cores per Processor|Kiểm soát số lượng lõi được kích hoạt trong mỗi bộ xử lý. This option is set to **All** by **default**. Các tuỳ chọn khác (1, 2, 4, 6, ...)
Processor Core Speed|Hiển thị tần số lõi tối đa (maximum core frequency) của bộ xử lý. Ở đây là 2.10GHz
Processor n|Tuỳ thuộc vào số lượng bộ xử lý , có thể có tối đa 2 bộ xử lý được liệt kê.|

Các cài đặt sau được hiển thị cho từng bộ xử lý được cài đặt trong hệ thống:

Option|Description|
|---|---|
Family-Model-Stepping|Hiển thị family, model, and stepping của processor được Intel xác định. Trong hình là 6-55-4
Brand|Hiển thị tên thương hiệu. Trong hình là Inter(R) Xeon(R) Gold 6130 CPU @ 2.10GHz
Level 2 Cache|Hiển thị tổng L2 cache. (16x1MB)
Level 3 Cache|Hiển thị tổng L3 cache. (22MB)
Number of Cores|Hiển thị số cores trên mỗi processor. (16)
Maximum Memory Capacity|Hiển thị dung lượng bộ nhớ tối đa (**maximum memory capacity**) cho mỗi processor. (0.75 TB)
Microcode|Hiển thị mã vĩ mô (microcode). (0x2006B06)

### 1.4 SATA settings

![Imgur](https://i.imgur.com/FlmrauC.jpg)

![Imgur](https://i.imgur.com/WRserly.jpg)


|Option|Description|
|---|---|
|Embedded SATA|Bật tuỳ chọn embedded SATA (SATA được nhúng) thành **AHCI Mode**, or **RAID Mode**. This option is set to **AHCI Mode** by **default**.|
|Security Freeze Lock|Cho phép gửi lệnh khoá đóng băng bảo mật (Security Freeze Lock) đến các ổ đĩa SATA được nhúng trong khi POST. Option này chỉ áp dụng cho **AHCI mode**. This option is set to **Enabled** by **default**.|
Write Cache|Enables or disables lệnh cho các ổ đĩa SATA được nhúng trong khi POST. This option is set to **Disabled** by **default**.|
Port n|Cho phép đặt loại ổ đĩa (drive type) của thiết bị đã chọn.Đối với **AHCI Mode** or **RAID Mode**, **BIOS support** luôn được bật **enabled**.|

Option|Description
|---|---|
Model|Hiển thị kiểu ổ đĩa (drive model) của thiết bị đã chọn (selected device).
Drive Type|Hiển thị loại ổ đĩa (type of drive) được gắn vào SATA port.
Capacity|Hiển thị tổng dung lượng của drive. Trường này không đực xác định cho các thiết bị phương tiện di động (removable media devices) như ổ đĩa quang (optical drives).

### 1.5 NVMe Settings

![Imgur](https://i.imgur.com/JJW3kut.jpg)

Option|Description
|---|---|
NVMe Mode|Cho phép đặt NVMe mode. This option is set to **Non RAID** by **default**.

### 1.6 Boot Settings
Có thể sử Boot Settings để đặt chế độ khởi động thành BIOS hoặc UEFI . Nó cũng cho phép chỉ định thứ tự khởi động.

- **UEFI** : Giao diện chương trình cơ sở mở rộng hợp nhất (UEFI) là một giao diện mới giữa hệ điều hành và chương trình cơ sở nền tảng. Giao diện bao gồm các bảng dữ liệu với thông tin liên quan đến nền tảng, các lệnh gọi dịch vụ khởi động và thời gian chạy có sẵn cho hệ điều hành và bộ tải của nó. Các lợi ích sau đây khả dụng khi Chế độ khởi động được đặt thành UEFI :
  - Hỗ trợ các phân vùng ổ đĩa lớn hơn 2 TB.
  - Bảo mật nâng cao (ví dụ: UEFI Secure Boot).
  - Thời gian khởi động nhanh hơn.

- **BIOS** : Chế độ khởi động BIOS là chế độ khởi động kế thừa. Nó được duy trì để tương thích ngược.

![Imgur](https://i.imgur.com/bxoAq3A.jpg)

|Option|Description|
|---|---|
Boot Mode|Cho phép thiết lập chế độ khởi động của hệ thống.*THẬN TRỌNG: Việc chuyển đổi chế độ khởi động có thể ngăn hệ thống khởi động nếu OS không được cài đặt ở cùng một chế độ.*Nếu OS hỗ trợ UEFI, bạn có thể đặt tuỳ chọn này thành UEFI. Đặt trường này thành BIOS cho phép tương thích với các hệ điều hành non-UEFI . This option is set to **UEFI** by **default**. NOTE Đặt trường này thành UEFI sẽ tắt menu **BIOS Boot Settings**.
Boot Sequence Retry|Cho phép bật hoặc tắt tính năng Boot Sequence Retry. Nếu option này là Enabled và hệ thống không khởi động được, Hệ thống sẽ thử lại trình tự khởi động sau 30s. This option is set to **Enabled** by **default**.
Hard-Disk Failover|Chỉ định ổ đĩa được khởi động trong trường hợp ổ đĩa bị lỗi. Các thiết bị được chọn trong Trình tự ổ đĩa cứng (Hard-Disk Drive Sequence) trên menu Cài đặt tùy chọn khởi động (Boot Option Setting). Khi tùy chọn này được đặt thành Disable , chỉ ổ đĩa đầu tiên trong danh sách được cố gắng khởi động. Khi tùy chọn này được đặt thành Enabled , tất cả các ổ đĩa sẽ được cố gắng khởi động theo thứ tự đã chọn trong Hard-Disk Drive Sequence . Tùy chọn này không được bật cho Chế độ khởi động UEFI. This option is set to **Disabled** by **default**.
Generic USB Boot| Bật hoặc tắt tùy chọn khởi động USB. This option is set to **Disabled** by **default**.
Hard-disk Drive Placeholder|Bật hoặc tắt tùy chọn trình giữ chỗ ổ đĩa cứng (Hard-disk drive placeholder). This option is set to **Disabled** by **default**.
BIOS Boot Settings|Bật hoặc tắt các tùy chọn khởi động BIOS.LƯU Ý Tùy chọn này chỉ được bật nếu chế độ khởi động là BIOS.
UEFI Boot Settings|Bật hoặc tắt tùy chọn Khởi động UEFI.Các tùy chọn Khởi động bao gồm IPv4 PXE và IPv6 PXE.  This option is set to IPv4 by default. LƯU Ý Tùy chọn này chỉ được bật nếu chế độ khởi động là UEFI.
UEFI Boot Sequence|Cho phép bạn thay đổi thứ tự thiết bị khởi động.
Boot Options Enable/Disable|Cho phép bạn chọn thiết bị khởi động được bật hoặc tắt.|

### 1.7 Integrated Devices

![Imgur](https://i.imgur.com/TBLWP2h.jpg)

![Imgur](https://i.imgur.com/v3zAlFf.jpg)

![Imgur](https://i.imgur.com/yJtf1c3.jpg)

![Imgur](https://i.imgur.com/8to9F3a.jpg)

Option|Description|
|---|---|
User Accessible USB Ports|  Cấu hình các cổng USB mà người dùng có thể truy cập. Chọn Only Back Ports On sẽ tắt các cổng USB phía trước; chọn All Ports Off (Tắt tất cả các cổng) sẽ tắt tất cả các cổng USB phía trước và phía sau.Bàn phím và chuột USB vẫn hoạt động ở một số cổng USB nhất định trong quá trình khởi động, tùy thuộc vào lựa chọn. Sau khi quá trình khởi động hoàn tất, các cổng USB sẽ được bật hoặc tắt tùy theo cài đặt.
Internal USB Port|Bật hoặc tắt cổng USB bên trong. This option is set to On by default. NOTE The Internal SD Card Port trên cổng PCIe được điều khiển bởi Internal USB Port.

# Tài liệu tham khảo
1. https://www.dell.com/support/manuals/en-vn/poweredge-r440/per440_bios_pub/system-setup?guid=guid-d926fd8d-a977-4289-b1e7-45d0fe546139&lang=en-us