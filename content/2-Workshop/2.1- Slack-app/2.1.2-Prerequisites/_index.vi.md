---
title : "Điều kiện tiên quyết"
date : 2024-01-01
weight : 2
chapter : false
pre : " <b> 2.1.2 </b> "
---

Phần này liệt kê tài khoản, quyền hạn và công cụ cần có trước khi bắt đầu cài đặt.

#### 1. Tài khoản AWS và region
- Có tài khoản AWS đang hoạt động.
- Có quyền truy cập region dùng trong workshop (khuyến nghị: `us-east-1`).
- Có kiến thức cơ bản về AWS Lambda, IAM và SSM Parameter Store.

#### 2. Quyền IAM
IAM user/role của bạn cần có quyền tạo và chạy Lambda function, đọc Slack secret, ghi log và quản lý SSM parameters.

Có thể dùng policy tương tự sau:

```json
{
	"Version": "2012-10-17",
	"Statement": [
		{
			"Sid": "SSMParameterCRUD",
			"Effect": "Allow",
			"Action": [
				"ssm:PutParameter",
				"ssm:GetParameter",
				"ssm:GetParameters",
				"ssm:GetParametersByPath",
				"ssm:DeleteParameter",
				"ssm:DeleteParameters",
				"ssm:DescribeParameters"
			],
			"Resource": "*"
		}
	]
}
```

#### 3. Lambda runtime và công cụ
- Có kiến thức Python 3.10+.
- Quen thuộc với `boto3` để gọi AWS APIs.

#### 4. Slack workspace: https://slack.com/
- Có Slack workspace mà bạn có quyền tạo app.
- Có thể tạo và cấu hình slash commands.
- Có quyền truy cập thông tin xác thực của Slack app:
	- `Signing Secret`
	- `Bot/User OAuth Token` (nếu implementation của bạn có gửi tin nhắn ngược lại channel)

#### 5. Truy cập mạng và endpoint
- Slack có thể truy cập endpoint Lambda của bạn qua Internet (Lambda Function URL hoặc API Gateway).
- Nếu tổ chức có chính sách mạng nghiêm ngặt, cần đảm bảo request từ Slack không bị chặn.

#### 6. Kiểm tra nhanh trước khi setup
Trước khi sang phần cài đặt, hãy xác nhận bạn có thể:
- Mở AWS Console ở đúng region mục tiêu.
- Tạo một test parameter trong SSM Parameter Store.
- Tạo Slack app trong workspace của bạn.
