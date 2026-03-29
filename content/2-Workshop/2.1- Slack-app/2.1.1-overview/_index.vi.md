---
title : "Tổng quan"
date : 2024-01-01
weight : 1
chapter : false
pre : " <b> 2.1.1 </b> "
---

Đây là một hệ thống tự động hóa serverless dựa trên Slack, cho phép người dùng quản lý AWS SSM Parameter Store trực tiếp thông qua slash command trên Slack. Bằng cách tích hợp Slack với AWS Lambda, hệ thống cho phép tạo, cập nhật và xóa parameters mà không cần truy cập AWS Console.

Ứng dụng xử lý request từ Slack, xác thực bằng Slack signing secret, sau đó thực thi thao tác tương ứng trên SSM Parameter Store. Giải pháp được thiết kế tập trung vào bảo mật, tính đơn giản và khả năng bảo trì, sử dụng IAM theo nguyên tắc đặc quyền tối thiểu và cấu trúc mã nguồn dạng module.

Giải pháp này giúp tăng hiệu quả vận hành bằng cách tự động hóa quy trình quản lý parameters và cung cấp giao diện thân thiện với người dùng ngay trong Slack.

#### Kiến trúc:
![overview](/images/5-Workshop/5.1-Workshop-overview/diagram1.jpg)

#### Thành phần:
- **Slack**: giao diện slash command và nơi phát sinh request.
- **AWS Lambda**: xác thực request và xử lý tạo parameter.
- **AWS SSM Parameter Store**: nơi lưu trữ an toàn cho cấu hình và secrets.
- **CloudWatch Logs:** thu thập và lưu logs từ Lambda để giám sát, debug và xử lý sự cố.

#### Luồng xử lý tổng quan:
- Người dùng gửi slash command từ Slack (ví dụ: `/create_param`).
- Slack gửi HTTP POST request trực tiếp đến AWS Lambda (qua Lambda Function URL).
- Lambda xác thực request (Slack signature, định dạng command, dữ liệu đầu vào).
- Lambda xử lý command và tạo parameter trong SSM Parameter Store.
- SSM lưu parameter (hoặc trả lỗi nếu không hợp lệ hay đã tồn tại).
- Lambda định dạng response.
- Lambda trả response về Slack.
- Slack hiển thị kết quả cho người dùng.
