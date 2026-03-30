---
title : "Cấu hình Slack"
date : 2024-01-01
weight : 2
chapter : false
pre : " <b> 2.1.3.2 </b> "
---
<div style="background-color: #fff3cd; border-left: 4px solid #f0ad4e; padding: 12px 16px; border-radius: 4px; margin-bottom: 16px;">
	<strong>Cảnh báo:</strong> Hãy đảm bảo workspace và app Slack đã được chuẩn bị đầy đủ trước khi tiếp tục.
</div>
Trong bước này, bạn sẽ tạo và cấu hình một Slack App có thể gửi slash command requests đến endpoint AWS Lambda của bạn.

#### 1. Tạo Slack App
1. Mở [Slack API portal](https://api.slack.com/apps).
2. Chọn **Create New App**.
3. Chọn **From scratch**.

![overview](/images/2.1-Slack/14-slack.png)
![overview](/images/2.1-Slack/15-slack.png)

4. Nhập tên app: `ssm-parameter-bot` (hoặc tên bất kỳ bạn muốn).
5. Ở bước “Pick a workspace to develop your app in”, chọn workspace nơi app Slack sẽ được tạo.
6. Chọn workspace và tạo app.

![overview](/images/2.1-Slack/16-slack.png)

#### 2. Lấy thông tin xác thực của app

Mở **Basic Information** và sao chép:
- **Signing Secret**
![overview](/images/2.1-Slack/17-ssm.png)

Mở **AWS Systems Manager**:
![overview](/images/2.1-Slack/18-ssm.png)
![overview](/images/2.1-Slack/19-ssm.png)

1. Chọn **Parameter Store**.
2. Bấm **Create parameter**.
3. Tạo parameter cho Slack Signing Secret:
- Name: `slack-signing-secret`
> **Lưu ý:** Nếu dùng tên parameter khác, hãy cập nhật giá trị tương ứng trong `slack_auth.py`.
- Description: `Slack app signing secret`
- Tier: `Standard`
- Type: `String`
- Data type: `text`
- Value: dán **Signing Secret** lấy từ Slack
1. Bấm **Create parameter**.
![overview](/images/2.1-Slack/20-ssm.png)
![overview](/images/2.1-Slack/21-ssm.png)

#### 3. Bật incoming requests
1. Trong menu cài đặt app, mở **Slash Commands**.
2. Chọn **Create New Command**.
![overview](/images/2.1-Slack/22-slackcmd.png)

3. Cấu hình:
- Sao chép URL
![overview](/images/2.1-Slack/13.png)
- Tạo command create SSM parameter
- Command: `/create_param`
- Request URL: dùng Lambda Function URL của bạn
- Short Description: `Create an SSM parameter`
- Usage Hint: `<name> <type> <value>`
- Lưu command.
![overview](/images/2.1-Slack/23-slackcmd.png)

Bạn có thể thêm các command khác, ví dụ:
- Cập nhật SSM parameter
- `/update_param`
- Request URL: dùng Lambda Function URL của bạn
- Short Description: `Update SSM parameter`
- Usage Hint: `<name> <value>`
- Lưu command.

- Xóa SSM parameter
- `/delete_param`
- Request URL: dùng Lambda Function URL của bạn
- Short Description: `Delete SSM parameter`
- Usage Hint: `<name>`
- Lưu command.

#### 4. Cài app vào workspace
1. Trong **Settings**.
2. Chọn **Install App**.
![overview](/images/2.1-Slack/24-install.png)

1. Xem và cấp các quyền được yêu cầu.
2. Xác nhận app xuất hiện trong danh sách app của workspace.
3. Bấm **Allow**.
![overview](/images/2.1-Slack/25-install.png)

#### 5. Kiểm tra cơ bản
Trước khi sang bước tiếp theo:
- Xác nhận slash command đã được tạo và đang hoạt động.
- Xác nhận Request URL trỏ đúng Lambda endpoint.
- Xác nhận Signing Secret đã được lưu an toàn.
