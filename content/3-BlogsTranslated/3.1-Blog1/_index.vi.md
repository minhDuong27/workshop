---
title: "Blog 1 - Cập nhật Phương pháp Carbon cho Công cụ Dấu chân Carbon của Khách hàng AWS"
date: "`r Sys.Date()`"
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---

**bởi Margaret O’Toole, Alexis Bateman, Marta Fraga, và Paula Csatlos vào 23 THÁNG 4 2025 trong Featured, Sustainability**

Để hỗ trợ hành trình bền vững (sustainability) của khách hàng, chúng tôi đã ra mắt Công cụ Dấu chân Carbon của Khách hàng (Customer Carbon Footprint Tool – CCFT) trong AWS Billing and Cost Management Console vào năm 2022. CCFT là một công cụ giúp khách hàng theo dõi, đo lường và xem xét lượng khí thải carbon phát sinh từ việc sử dụng AWS của họ. CCFT tính đến các khí thải Scope 1 và Scope 2, theo định nghĩa trong Greenhouse Gas Protocol, bao trùm toàn bộ dải sản phẩm AWS, bao gồm Amazon EC2, Amazon S3, AWS Lambda, và các dịch vụ khác. Lượng khí thải được cung cấp bằng Tấn Tương đương Carbon Dioxide (MTCO2e).

Ngày hôm nay, chúng tôi công bố ba cập nhật là một phần trong quy trình liên tục để cải thiện CCFT:

- **Dễ dàng truy cập dữ liệu hơn:** chúng tôi làm cho việc truy cập dữ liệu khí thải của khách hàng trở nên dễ dàng hơn thông qua dịch vụ Billing and Cost Management Data Exports.  
- **Dữ liệu carbon chi tiết hơn:** chúng tôi tăng mức độ chi tiết trong CCFT để hiển thị theo các vùng AWS.  
- **Phương pháp được cập nhật, được xác minh độc lập:** chúng tôi công bố một phương pháp phân bổ cập nhật (v2.0) cùng với methodology document và assurance, được nhận bởi APEX.  

Kết quả của những thay đổi này, khách hàng có thể xem lượng khí thải carbon phản ánh phương pháp mới cho việc sử dụng AWS từ tháng 1 năm 2025 trở đi, và một số khách hàng có thể thấy con số ước tính khí thải thay đổi. Theo thực tiễn chung của ngành, dữ liệu CCFT từ tháng 12 năm 2024 trở về trước sẽ vẫn sử dụng phương pháp v1.0.

---

## Cập nhật hôm nay của CCFT chi tiết

### 1. Làm cho việc truy cập dữ liệu dễ hơn

Để khiến việc sử dụng dữ liệu từ CCFT dễ hơn, khách hàng bây giờ có thể xuất dữ liệu từ tháng January qua dịch vụ Data Exports của AWS trong Billing and Cost Management. Dữ liệu khí thải carbon xuất ra sẽ cung cấp ước tính lượng khí thải carbon cho tất cả các tài khoản thành viên liên kết tới tài khoản quản lý khi khách hàng sử dụng AWS Organizations.

Dịch vụ Data Exports sẽ tự động gửi các bản cập nhật hàng tháng ở định dạng CSV hoặc Parquet tới Amazon S3, cho phép khách hàng tự động hóa việc xử lý dữ liệu carbon trên toàn bộ AWS organization. Với lần xuất đầu tiên, họ sẽ nhận được tối đa 38 tháng dữ liệu lịch sử trong bucket S3 để phục vụ phân tích lịch sử. Dữ liệu cho tháng 12 năm 2024 và trước đó sẽ được tính bằng phương pháp v1.0, trong khi từ tháng 1 năm 2025 trở đi sẽ sử dụng v2.0.

Khách hàng có thể tìm hiểu thêm cách thiết lập Data Export trong the Data Exports user guide.

---

### 2. Chi tiết theo vùng AWS (Regional Granularity)

Khách hàng giờ đây có thể nhìn thấy lượng khí thải carbon được chia nhỏ theo Vùng AWS (AWS Region) (ví dụ: US East (Ohio)), với việc sử dụng Amazon CloudFront CDN được tách riêng thành một mục Dịch vụ Toàn cầu (Global Services) duy nhất. Điều này giúp khách hàng xác định vùng mà việc sử dụng của họ đóng góp nhiều nhất vào dấu chân carbon để cân nhắc lại phân bổ workloads theo vùng AWS.

---

### 3. Phương pháp cập nhật v2.0

Khách hàng thường sử dụng một loạt dịch vụ AWS trải dài nhiều vùng, và do đó việc theo dõi và phân bổ khí thải carbon dựa trên workloads có thể là thách thức.

Mặc dù không có tiêu chuẩn ngành duy nhất cho việc phân bổ khí thải carbon cho việc sử dụng đám mây tới khách hàng, bản cập nhật phương pháp v2.0 đã tận dụng các tiêu chuẩn hiện có để hỗ trợ CCFT, bao gồm: **GHG Protocol Corporate Standard, GHG Protocol Product Standard, ISO 14040/44 (LCA), ISO 14067 (Carbon footprint của sản phẩm)** và **ICT Sector Guidance**.

Khách hàng có thể đọc thêm trong full-length methodology document, nhưng dưới đây là cái nhìn ngắn gọn về cách tiếp cận:

#### Phần tổng quan khí thải Scope 1 (Trực tiếp) cho v2.0

Scope 1 bao gồm khí thải trực tiếp từ các nguồn mà AWS sở hữu hoặc kiểm soát, chẳng hạn như đốt nhiên liệu trong máy phát dự phòng tại các data center. AWS nhận dữ liệu hoạt động Scope 1 cho năm trước vào quý đầu tiên của năm tiếp theo – là kết quả của quy trình xác nhận toàn Amazon hàng năm. Sau đó, chúng tôi tính toán dữ liệu carbon ước tính với chi tiết cấp site và tổng hợp lên cấp cluster.

Một cluster AWS có thể là một vùng (ví dụ: us-east-1, eu-central-1) hoặc một cluster Edge của CloudFront (ví dụ: CF ở Bắc Mỹ, CF ở Nam Mỹ).

#### Phần tổng quan khí thải Scope 2 (Gián tiếp) cho v2.0

Scope 2 bao gồm khí thải gián tiếp từ việc mua điện, và CCFT sử dụng phương pháp market-based. Ví dụ: hỗn hợp lưới điện (grid mix) như phần trăm năng lượng không phát thải carbon từ lưới – và các hệ số phát thải (kgCO2e/kWh) – được cập nhật hàng năm và được xác minh như một phần của quy trình đảm bảo dấu chân carbon của Amazon. Đối với Scope 2, CCFT sử dụng các hệ số phát thải dựa trên vị trí địa lý và tuân theo thứ tự ưu tiên hệ số phát thải được đề nghị bởi Greenhouse Gas Protocol.

#### Tổng quan phân bổ v2.0

Mô hình trước tiên phân bổ khí thải ước tính ở cấp cluster cho các giá đỡ máy chủ (server racks) trong cluster, rồi ánh xạ các khí thải đó tới các dịch vụ AWS cụ thể dựa vào việc sử dụng tài nguyên của các giá đỡ máy chủ, đồng thời tính đến phụ thuộc giữa các dịch vụ nền tảng có phần cứng riêng (ví dụ: Amazon EC2) và các dịch vụ không nền tảng được xây trên hạ tầng đó (ví dụ: AWS Lambda). Cuối cùng, khí thải được gán cho từng tài khoản khách hàng sử dụng các dịch vụ đó.

Mô hình hoạt động như sau:

1. Phân bổ khí thải ước tính cấp cluster cho các giá đỡ máy chủ trong cluster.  
2. Phân bổ khí thải carbon ước tính liên quan tới các giá đỡ máy chủ cho các dịch vụ đám mây AWS dựa vào sử dụng tài nguyên của giá đỡ, đồng thời tính đến các phụ thuộc lẫn nhau.  
3. Phân bổ khí thải carbon ước tính cho mỗi dịch vụ đến từng tài khoản khách hàng sử dụng các dịch vụ đó.

Một số khách hàng có thể thấy lượng ước tính khí thải của họ thay đổi do cập nhật phương pháp của CCFT vì v2.0 cho phép phân bổ chính xác hơn lượng khí thải đến khách hàng, phản ánh tốt hơn việc sử dụng thực tế dịch vụ AWS của họ.

---

### Ba cập nhật chính trong phương pháp v2.0:

1. **Bây giờ chúng tôi phân bổ công suất chưa sử dụng cho tất cả khách hàng AWS.**  
   AWS chuẩn bị đủ các giá đỡ máy chủ để đáp ứng nhu cầu khách hàng. Đôi khi, điều này có nghĩa là có công suất bị lãng phí. Lượng carbon ước tính liên quan tới công suất chưa sử dụng giờ đây được phân bổ theo tỷ lệ cho tất cả khách hàng sử dụng dịch vụ AWS.  
   Điều này vì GHG Protocol, các tiêu chuẩn ISO liên quan đến báo cáo carbon cấp sản phẩm (ISO 14040 / 14044), và hướng dẫn ngành dịch vụ đám mây & trung tâm dữ liệu đòi hỏi phải bao gồm tất cả lãng phí và sự kém hiệu quả cần thiết để cung cấp sản phẩm/dịch vụ cho khách hàng.

2. **Cải thiện logic để phân bổ khí thải ước tính** từ các dịch vụ AWS không có phần cứng riêng như AWS Lambda hoặc Amazon Redshift, giữa khách hàng AWS và các đội ngũ Amazon nội bộ.

3. **Cập nhật để phân bổ chi phí chung (overhead)** liên quan đến vận hành trung tâm dữ liệu, như lượng carbon ước tính liên quan đến các giá đỡ mạng (networking racks) và việc mở rộng vùng mới cho khách hàng AWS.

---

Chúng tôi sẽ tiếp tục cải thiện công cụ của mình, làm việc từ nhu cầu của khách hàng. Khách hàng có thể tìm hiểu thêm về các cập nhật này bằng cách đọc **methodology document** và tham khảo **CCFT user guide** cùng **Data Exports user guide**.

Về phía tiến tới, chúng tôi sẽ tiếp tục đăng các cập nhật về phương pháp dựa trên dữ liệu phát triển, khoa học khí hậu và hơn nữa, và sẽ tiếp tục đầu tư vào các tính năng và chức năng hỗ trợ khách hàng trong hành trình bền vững.

---

## Cam kết đối với The Climate Pledge

Để tìm hiểu thêm về **The Climate Pledge** — cam kết của Amazon hướng tới carbon trung hòa (net-zero) vào năm 2040 — và các khoản đầu tư của chúng tôi trong việc phát triển bền vững trên mọi lĩnh vực kinh doanh, bao gồm AWS, xin vui lòng truy cập **trang bền vững (sustainability site)** tại đây.
