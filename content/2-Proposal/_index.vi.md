---
title: "Bản đề xuất"
date: 2026-07-21
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

# Website Upload và Quản lý tài liệu trên AWS

## Kiến trúc ứng dụng Web kết hợp Amazon EC2, Amazon S3, Amazon RDS, AWS Lambda, IAM và VPC

### 1. Tóm tắt điều hành

Đề xuất này trình bày giải pháp xây dựng **Website Upload và Quản lý
tài liệu** trên nền tảng điện toán đám mây AWS. Hệ thống cho phép
người dùng tải tài liệu lên website, lưu trữ tài liệu trên Amazon S3,
quản lý thông tin tài liệu bằng Amazon RDS và thực hiện các thao tác như
xem danh sách, tải xuống và xóa tài liệu.

Ứng dụng được xây dựng theo mô hình Web Application, trong đó phần giao
diện người dùng giao tiếp với backend thông qua các API. Backend được
triển khai trên **Amazon EC2**, sử dụng Spring Boot để xử lý
nghiệp vụ và kết nối với các dịch vụ AWS.

Các file tài liệu không được lưu trực tiếp trên EC2 mà được lưu trữ tập
trung trên **Amazon S3**. Cơ sở dữ liệu **Amazon RDS**
chỉ lưu metadata của tài liệu như tên file, loại file, kích thước, thời
gian tải lên và S3 Object Key tương ứng.

Hệ thống được đặt trong **Amazon VPC**, cho phép tổ chức và kiểm
soát kết nối mạng giữa EC2 và RDS. **AWS IAM** được sử dụng để
kiểm soát quyền truy cập của các tài nguyên AWS, đặc biệt là quyền của
EC2 đối với S3.

Ngoài luồng upload thông thường, **AWS Lambda** được sử dụng để
xử lý sự kiện khi một tài liệu mới được tải lên S3. Lambda có thể thực
hiện các tác vụ như ghi log, kiểm tra metadata hoặc thực hiện những bước
xử lý tài liệu bổ sung mà không cần duy trì một server riêng.

Kiến trúc này giúp tách biệt phần xử lý ứng dụng, phần lưu trữ file và
phần lưu trữ dữ liệu, đồng thời tạo nền tảng để hệ thống có thể mở rộng
trong tương lai.

---

### 2. Tuyên bố vấn đề

#### Vấn đề hiện tại

* **Phụ thuộc vào dung lượng ổ đĩa của server**: Khi số lượng
tài liệu tăng lên, dung lượng lưu trữ của server có thể không đủ.

* **Khó mở rộng hệ thống**: Nếu cần tạo thêm EC2 instance để xử
lý lượng truy cập lớn, việc lưu file trực tiếp trên từng server có thể
dẫn đến tình trạng dữ liệu bị phân tán.

* **Khó quản lý file**: Việc lưu hàng nghìn hoặc hàng triệu tài
liệu trên filesystem của server khiến việc tổ chức, backup và quản lý dữ
liệu trở nên phức tạp.

* **Nguy cơ mất dữ liệu khi server gặp sự cố**: Nếu file chỉ
tồn tại trên một EC2 instance, sự cố đối với instance có thể ảnh hưởng
trực tiếp đến dữ liệu.

* **Tách biệt dữ liệu và ứng dụng chưa rõ ràng**: Server vừa
phải xử lý request vừa phải đảm nhiệm việc lưu trữ file.

* **Khó triển khai xử lý file tự động**: Khi cần xử lý tài liệu
sau khi upload, ứng dụng phải tự thực hiện toàn bộ công việc trên
server.

#### Giải pháp đề xuất

Hệ thống được thiết kế theo nguyên tắc cốt lõi: **EC2 xử lý ứng dụng
-- S3 lưu trữ file -- RDS lưu metadata -- Lambda xử lý sự kiện -- IAM
kiểm soát quyền -- VPC kiểm soát mạng**.

Kiến trúc chia thành các thành phần độc lập:

1. **Web Application**: Cung cấp giao diện để người dùng upload
và quản lý tài liệu.

2. **Amazon EC2**: Chạy backend Spring Boot, tiếp nhận request
từ website và xử lý nghiệp vụ.

3. **Amazon S3**: Lưu trữ file tài liệu thực tế.

4. **Amazon RDS**: Lưu metadata và thông tin quản lý tài liệu.

5. **AWS Lambda**: Tự động xử lý khi có file mới được upload
vào S3.

6. **AWS IAM**: Kiểm soát quyền truy cập giữa EC2, S3 và các
dịch vụ AWS.

7. **Amazon VPC**: Tạo môi trường mạng riêng để tổ chức EC2,
RDS và các thành phần liên quan.

Kiến trúc này giúp hệ thống tách biệt rõ ràng giữa **Compute,
Storage, Database, Security và Network**.

#### Lợi ích

* **Tách biệt lưu trữ và xử lý**: EC2 tập trung xử lý ứng dụng,
trong khi S3 đảm nhiệm lưu trữ tài liệu.

* **Khả năng mở rộng**: S3 có thể mở rộng theo số lượng tài
liệu mà không cần tăng dung lượng ổ đĩa của EC2.

* **Tăng cường bảo mật**: IAM kiểm soát quyền truy cập và VPC
giúp hạn chế việc RDS bị truy cập trực tiếp từ Internet.

* **Tự động hóa xử lý**: Lambda có thể được kích hoạt tự động
khi tài liệu mới được upload lên S3.

---

### 3. Kiến trúc giải pháp

#### Sơ đồ kiến trúc tổng thể

![Website upload Architecture](/images/2-Proposal/overall_architecture.png)

#### Chi tiết các luồng xử lý chính trong kiến trúc:

##### 1. Flow A --- Upload tài liệu

* **A1**: Người dùng chọn tài liệu trên website.

* **A2**: Frontend gửi request upload tới backend Spring Boot
đang chạy trên Amazon EC2.

* **A3**: Backend kiểm tra tên file, loại file và kích thước
file.

* **A4**: Backend sử dụng AWS SDK để upload file lên Amazon S3.

* **A5**: Sau khi upload thành công, backend lưu metadata và S3
Object Key của file vào Amazon RDS.

* **A6**: Backend trả kết quả upload về frontend.

##### 2. Flow B --- Download tài liệu

* **B1**: Người dùng chọn chức năng Download trên website.

* **B2**: Frontend gửi document ID tới backend.

* **B3**: Backend tìm metadata tương ứng trong RDS.

* **B4**: Backend lấy S3 Object Key của tài liệu.

* **B5**: Backend truy cập S3 để lấy file và trả về cho người
dùng.

##### 3. Flow C --- Xóa tài liệu

* **C1**: Người dùng gửi yêu cầu xóa tài liệu.

* **C2**: Backend kiểm tra thông tin tài liệu trong RDS.

* **C3**: Backend xóa object tương ứng trên S3.

* **C4**: Backend xóa metadata của tài liệu trong RDS.

* **C5**: Backend trả kết quả về frontend.

##### 4. Flow D --- Xử lý sự kiện bằng Lambda

* **D1**: File mới được upload lên S3.

* **D2**: S3 phát sinh ObjectCreated Event.

* **D3**: Event kích hoạt AWS Lambda.

* **D4**: Lambda thực hiện các tác vụ xử lý tài liệu như kiểm
tra metadata, ghi log hoặc tạo dữ liệu xử lý bổ sung.

#### Dịch vụ AWS sử dụng

- **Amazon EC2**: Chạy backend Spring Boot và cung cấp REST
API.

- **Amazon S3**: Lưu trữ file tài liệu.

- **Amazon RDS**: Lưu metadata và thông tin quản lý tài liệu.

- **AWS Lambda**: Xử lý sự kiện khi có tài liệu mới được
upload.

- **AWS IAM**: Quản lý quyền truy cập của EC2 và các dịch vụ
AWS.

- **Amazon VPC**: Xây dựng môi trường mạng và kiểm soát kết nối
giữa các thành phần.

---

### 4. Triển khai kỹ thuật

#### Các giai đoạn triển khai

1. **Giai đoạn 1: Phân tích & Thiết kế**

    *   Phân tích chức năng upload, download, xóa và quản lý tài liệu.

    *   Thiết kế database lưu metadata và thiết kế kiến trúc AWS.

2. **Giai đoạn 2: Xây dựng Website**

    *   Xây dựng frontend bằng HTML/CSS/JavaScript.

    *   Phát triển backend Spring Boot và các REST API.

3. **Giai đoạn 3: Tích hợp Amazon S3 & RDS**

    *   Tạo S3 Bucket và tích hợp AWS SDK vào Spring Boot.

    *   Tạo database trên Amazon RDS và lưu metadata tài liệu.

4. **Giai đoạn 4: Triển khai EC2, IAM & VPC**

    *   Triển khai Spring Boot lên Amazon EC2.

    *   Cấu hình IAM Role cho EC2 truy cập S3 theo nguyên tắc Least
Privilege.

    *   Thiết kế VPC, Public Subnet, Private Subnet và Security Group.

5. **Giai đoạn 5: Tích hợp Lambda & Kiểm thử**

    *   Cấu hình S3 ObjectCreated Event kích hoạt Lambda.

    *   Kiểm thử upload, download, xóa tài liệu và kiểm tra quyền truy
cập.

#### Yêu cầu kỹ thuật & Bảo mật

- **Phân quyền IAM**: Áp dụng nguyên tắc Least Privilege, chỉ
cấp cho EC2 những quyền S3 cần thiết.

- **Bảo vệ RDS**: Đặt RDS trong Private Subnet và giới hạn
Security Group chỉ cho phép EC2 kết nối.

- **Bảo vệ S3**: Không public toàn bộ bucket và kiểm soát quyền
truy cập tới object.

- **Kiểm tra file upload**: Kiểm tra MIME type, extension và
kích thước file trước khi lưu trữ.

- **Bảo vệ thông tin xác thực**: Không hard-code AWS Access Key
và Secret Key trong source code; sử dụng IAM Role cho EC2.

- **Mã hóa dữ liệu**: Sử dụng HTTPS/TLS cho dữ liệu truyền tải
và cơ chế mã hóa của AWS cho dữ liệu lưu trữ khi cần thiết.

---

### 5. Lộ trình & Mốc triển khai

```
+-----------------------------------------------------------------------------------+
| Giai đoạn 1: Phân tích & Thiết kế                                                 |
|   - Phân tích chức năng upload, download, delete                                  |
|   - Thiết kế database và kiến trúc AWS                                            |
+-----------------------------------------------------------------------------------+
                                      |
                                      v
+-----------------------------------------------------------------------------------+
| Giai đoạn 2: Xây dựng Website                                                     |
|   - Xây dựng Frontend HTML/CSS/JavaScript                                         |
|   - Phát triển Spring Boot Backend và REST API                                    |
+-----------------------------------------------------------------------------------+
                                      |
                                      v
+-----------------------------------------------------------------------------------+
| Giai đoạn 3: Tích hợp S3 & RDS                                                    |
|   - Cấu hình S3 Bucket                                                            |
|   - Kết nối Spring Boot với RDS và lưu metadata                                   |
+-----------------------------------------------------------------------------------+
                                      |
                                      v
+-----------------------------------------------------------------------------------+
| Giai đoạn 4: EC2, IAM & VPC                                                       |
|   - Triển khai Spring Boot trên EC2                                               |
|   - Cấu hình IAM Role, VPC, Subnet và Security Group                              |
+-----------------------------------------------------------------------------------+
                                      |
                                      v
+-----------------------------------------------------------------------------------+
| Giai đoạn 5: Lambda & Kiểm thử                                                    |
|   - Cấu hình S3 Event và Lambda                                                   |
|   - Kiểm thử chức năng, bảo mật và xử lý lỗi                                      |
+-----------------------------------------------------------------------------------+
```

---

### 6. Ước tính ngân sách

Chi phí thực tế phụ thuộc vào Region, cấu hình tài nguyên, dung lượng
file, thời gian EC2 chạy và số lượng request. Các con số dưới đây được
sử dụng để ước tính cho một hệ thống nhỏ phục vụ mục đích học tập.

| Dịch vụ AWS | Cấu hình / Quy mô ước tính | Chi phí |
| :--- | :--- | :--- |
| **Amazon EC2** | 1 instance cấu hình nhỏ, chạy backend | Phụ thuộc cấu hình và thời gian chạy |
| **Amazon S3** | Vài GB tài liệu | Phụ thuộc dung lượng và request |
| **Amazon RDS** | Database nhỏ lưu metadata | Phụ thuộc loại instance và thời gian chạy |
| **AWS Lambda** | Số lượng request thấp, xử lý event S3 | Phụ thuộc số request và thời gian thực thi |
| **AWS IAM** | IAM User / Role / Policy | Không tính phí riêng cho chức năng IAM cơ bản |
| **Amazon VPC** | 1 VPC, Subnet và Security Group | Các thành phần cơ bản không tính phí riêng; một số tài nguyên mạng có thể phát sinh phí |

{{% notice tip %}}
Để giảm chi phí khi học tập, nên sử dụng các tài nguyên có Free Tier
nếu tài khoản và Region đáp ứng điều kiện, đồng thời dừng hoặc xóa EC2
và RDS khi không sử dụng.
{{% /notice %}}
---

### 7. Đánh giá rủi ro

#### Ma trận rủi ro & Chiến lược giảm thiểu

| Rủi ro tiềm ẩn | Mức độ ảnh hưởng | Xác suất | Chiến lược giảm thiểu |
|---|---|---|---|
| **EC2 ngừng hoạt động** | Cao | Thấp/Trung bình | Lưu trữ mã nguồn và cấu hình để có thể triển khai lại ứng dụng nhanh chóng. |
| **Kết nối tới RDS thất bại** | Cao | Thấp | Kiểm tra VPC, Security Group, subnet và cấu hình kết nối database. |
| **Upload tài liệu thất bại** | Trung bình | Trung bình | Kiểm tra lỗi upload, giới hạn dung lượng và xử lý retry khi cần thiết. |
| **File không hợp lệ** | Trung bình | Trung bình | Kiểm tra MIME type, extension và kích thước file trước khi upload. |
| **Truy cập trái phép S3** | Cao | Thấp | Sử dụng IAM Least Privilege và không public toàn bộ bucket. |
| **Rò rỉ AWS credentials** | Cao | Thấp | Sử dụng IAM Role thay vì hard-code Access Key và Secret Key. |
| **RDS bị truy cập trái phép** | Cao | Thấp | Đặt RDS trong Private Subnet và chỉ cho phép EC2 truy cập thông qua Security Group. |

---

### 8. Kết quả kỳ vọng

* **Xây dựng thành công Website Upload & Quản lý tài liệu**:
Người dùng có thể upload, xem danh sách, download và xóa tài liệu thông
qua giao diện Web.

* **Triển khai ứng dụng trên AWS**: Backend Spring Boot được
triển khai trên Amazon EC2 thay vì chỉ chạy trên máy tính cá nhân.

* **Lưu trữ tập trung trên Amazon S3**: Tài liệu được tách khỏi
server ứng dụng và lưu trữ trên dịch vụ Object Storage chuyên dụng.

* **Quản lý metadata bằng Amazon RDS**: Thông tin tài liệu được
lưu trữ có cấu trúc trong cơ sở dữ liệu.

* **Tự động hóa bằng AWS Lambda**: Các sự kiện upload tài liệu
có thể kích hoạt các tác vụ xử lý tự động.

* **Tăng cường bảo mật**: IAM, VPC, Security Group và các cơ
chế kiểm soát truy cập giúp hạn chế quyền truy cập không cần thiết.

* **Khả năng mở rộng**: Kiến trúc có thể tiếp tục mở rộng với
các chức năng như đăng nhập, phân quyền tài liệu, thư mục, tìm kiếm,
chia sẻ tài liệu và xử lý PDF.

Dự án cung cấp một mô hình thực hành tổng hợp về **AWS Cloud
Architecture và Web Application Deployment**, đồng thời thể hiện mối
quan hệ giữa **Compute (EC2), Object Storage (S3), Database (RDS),
Serverless Processing (Lambda), Identity & Access Management (IAM) và
Network (VPC)**.