---
title : "Kiểm thử"
date : 2024-01-01
weight : 4
chapter : false
pre : " <b> 2.1.4 </b> "
---

Phần này dùng để kiểm thử toàn bộ luồng hoạt động end-to-end của Slack App sau khi hoàn tất cài đặt.

#### 1. Danh sách kiểm tra trước khi test
Trước khi chạy test cases, hãy xác nhận:

- Slack app đã được cài vào workspace.
- Đã tạo đủ slash commands:
	- `/create_param`
	- `/update_param`
	- `/delete_param`
- Request URL của từng command đều trỏ đến Lambda Function URL.
- SSM parameter `slack-signing-secret` tồn tại và có giá trị đúng.
- Lambda execution role có quyền SSM cần thiết.

#### 2. Chuẩn bị quy ước đặt tên test
Nên dùng tên parameter riêng để tránh trùng lặp, ví dụ:

```text
/workshop/slack/test-db-password
```

Bạn có thể dùng bất kỳ định dạng tên nào hợp lệ với SSM Parameter Store.

#### 3. Các test case chức năng

##### Test case A: Tạo parameter
1. Trong Slack, chạy lệnh:

```text
/create_param /workshop/slack/test-db-password String my-secret-123
```
![overview](/images/2.1-Slack/26-test.png)

2. Kết quả trên Slack:
- ![overview](/images/2.1-Slack/27-test.png)

3. Kiểm tra trên AWS Console:
- Mở **Systems Manager** -> **Parameter Store**.
- Tìm `/workshop/slack/test-db-password`.
- Xác nhận:
	- Tên đúng.
	- Type là `String`.
	- Value đã được lưu.
![overview](/images/2.1-Slack/28-test.png)

##### Test case B: Cập nhật parameter
1. Trong Slack, chạy lệnh:

```text
/update_param /workshop/slack/test-db-password my-secret-456
```
![overview](/images/2.1-Slack/29-update.png)

2. Kết quả trên Slack:
![overview](/images/2.1-Slack/30-update.png)

3. Kiểm tra trên AWS Console:
- Mở parameter và xác nhận giá trị mới là `my-secret-456`.
![overview](/images/2.1-Slack/31-update.png)

##### Test case C: Xóa parameter
1. Trong Slack, chạy lệnh:

```text
/delete_param /workshop/slack/test-db-password
```
![overview](/images/2.1-Slack/32-delete.png)

2. Kết quả trên Slack:
![overview](/images/2.1-Slack/33-delete.png)

3. Kiểm tra trên AWS Console:
- Tìm parameter trong Parameter Store.
- Xác nhận parameter không còn tồn tại.
![overview](/images/2.1-Slack/34-delete.png)

#### 4. Kiểm tra CloudWatch logs
Sau mỗi test case:

1. Mở **CloudWatch** -> **Log groups**.
2. Chọn log group của Lambda function.
![overview](/images/2.1-Slack/35-cloudwatch.png)
![overview](/images/2.1-Slack/36-cloudwatch.png)
![overview](/images/2.1-Slack/37-cloudwatch.png)
