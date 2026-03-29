---
title: "Worklog Tuần 1"
date: 2026-01-01
weight: 1
chapter: false
pre: " <b> 1.1. </b> "
---
{{% notice warning %}}
⚠️ **Lưu ý:** Các thông tin dưới đây chỉ nhằm mục đích tham khảo, vui lòng **không sao chép nguyên văn** cho bài báo cáo của bạn kể cả warning này.
{{% /notice %}}


### Mục tiêu tuần 1:

* Hiểu dịch vụ AWS Systems Manager (SSM) Parameter Store và các trường hợp sử dụng.
* Xây dựng một mini project để quản lý cấu hình tập trung bằng SSM parameters.
* Thực hành sử dụng AWS Console và AWS CLI cho bài toán quản lý tham số an toàn.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc                                                                                                                                                                                                                          | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu                                                                 |
| --- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ------------------------------------------------------------------------------ |
| 2   | - Xác định phạm vi project với SSM Parameter Store <br> - Thống nhất quy ước đặt tên và cấu trúc nhóm parameter (ví dụ: `/project/dev/app/*`)                                                                                      | 23/03/2026   | 23/03/2026      | <https://docs.aws.amazon.com/systems-manager/latest/userguide/systems-manager-parameter-store.html> |
| 3   | - Chuẩn bị môi trường: AWS account, quyền IAM, cấu hình AWS CLI profile <br> - Tạo các parameter đầu tiên trong Parameter Store: <br>&emsp; + `String` <br>&emsp; + `StringList` <br>&emsp; + `SecureString`                   | 24/03/2026   | 24/03/2026      | <https://docs.aws.amazon.com/cli/latest/reference/ssm/>                       |
| 4   | - Thực hiện thao tác parameter bằng CLI: <br>&emsp; + `put-parameter` <br>&emsp; + `get-parameter` <br>&emsp; + `get-parameters-by-path` <br> - Kiểm tra versioning và quy trình cập nhật parameter                              | 25/03/2026   | 25/03/2026      | <https://docs.aws.amazon.com/systems-manager/latest/userguide/parameter-store-working-with.html> |
| 5   | - Tích hợp SSM parameter vào script/ứng dụng mẫu <br> - Lấy cấu hình runtime (DB host, API key, environment flags) từ Parameter Store <br> - Kiểm thử luồng đọc dữ liệu nhạy cảm với `--with-decryption`                        | 26/03/2026   | 27/03/2026      | <https://docs.aws.amazon.com/systems-manager/latest/userguide/parameter-store-integration.html> |
| 6   | - Bổ sung kiểm soát truy cập và bảo mật: IAM policy theo nguyên tắc least privilege <br> - Viết tài liệu triển khai/sử dụng cho nhóm <br> - Kiểm thử cuối: cập nhật cấu hình end-to-end không hardcode giá trị trong source code | 27/03/2026   | 27/03/2026      | <https://docs.aws.amazon.com/systems-manager/latest/userguide/security-best-practices.html> |


### Kết quả đạt được tuần 1:

* Hoàn thành mini project sử dụng AWS SSM Parameter Store làm nơi quản lý cấu hình tập trung.

* Thiết kế và áp dụng cấu trúc đặt tên parameter rõ ràng theo môi trường:
  * `/project/dev/app/*`
  * `/project/staging/app/*`
  * ...

* Tạo và quản lý thành công nhiều loại parameter:
  * `String`
  * `StringList`
  * `SecureString`

* Thực hành các lệnh CLI cốt lõi cho toàn bộ vòng đời parameter:
  * Tạo/cập nhật parameter
  * Đọc parameter đơn lẻ và theo nhóm
  * Theo dõi version và kiểm tra cập nhật

* Tích hợp việc đọc parameter vào script/ứng dụng mẫu, giảm hardcode secrets và biến cấu hình.

* Áp dụng mô hình truy cập an toàn bằng IAM và luồng giải mã cho dữ liệu nhạy cảm.

* Hoàn thiện tài liệu thực hành để có thể tái sử dụng quy trình cho các tuần tiếp theo.
* ...


