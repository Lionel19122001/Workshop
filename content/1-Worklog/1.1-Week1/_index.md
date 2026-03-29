---
title: "Week 1 Worklog"
date: 2026-01-01
weight: 1
chapter: false
pre: " <b> 1.1. </b> "
---
{{% notice warning %}} 
⚠️ **Note:** The following information is for reference purposes only. Please **do not copy verbatim** for your own report, including this warning.
{{% /notice %}}


### Week 1 Objectives:

* Understand the AWS Systems Manager (SSM) Parameter Store service and its use cases.
* Build a small project to centralize and retrieve application configuration using SSM parameters.
* Practice working with AWS Console and AWS CLI for secure parameter management.

### Tasks to be carried out this week:
| Day | Task                                                                                                                                                                                                                                    | Start Date | Completion Date | Reference Material                                                                 |
| --- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------- | --------------- | ---------------------------------------------------------------------------------- |
| 2   | - Define project scope for SSM Parameter Store usage <br> - Review naming conventions and folder structure for parameters (for example: `/project/dev/app/*`)                                                                            | 23/03/2026 | 23/03/2026      | <https://docs.aws.amazon.com/systems-manager/latest/userguide/systems-manager-parameter-store.html> |
| 3   | - Prepare environment: AWS account, IAM permissions, AWS CLI profile <br> - Create first parameters in Parameter Store: <br>&emsp; + `String` <br>&emsp; + `StringList` <br>&emsp; + `SecureString`                                     | 24/03/2026 | 24/03/2026      | <https://docs.aws.amazon.com/cli/latest/reference/ssm/>                           |
| 4   | - Implement parameter operations via CLI: <br>&emsp; + `put-parameter` <br>&emsp; + `get-parameter` <br>&emsp; + `get-parameters-by-path` <br> - Test parameter versioning and update flow                                              | 25/03/2026 | 25/03/2026      | <https://docs.aws.amazon.com/systems-manager/latest/userguide/parameter-store-working-with.html> |
| 5   | - Integrate SSM parameters into a sample app/script <br> - Retrieve runtime config (DB host, API key, environment flags) from Parameter Store <br> - Validate secure retrieval using `--with-decryption`                                 | 26/03/2026 | 27/03/2026      | <https://docs.aws.amazon.com/systems-manager/latest/userguide/parameter-store-integration.html> |
| 6   | - Add access control and security checks: least-privilege IAM policy <br> - Document deployment and usage steps for teammates <br> - Final test: end-to-end config retrieval and update without hardcoded values in source code         | 27/03/2026 | 27/03/2026      | <https://docs.aws.amazon.com/systems-manager/latest/userguide/security-best-practices.html> |


### Week 1 Achievements:

* Completed a mini project using AWS SSM Parameter Store as a centralized configuration service.

* Designed and applied a clear parameter naming hierarchy for environment-based configuration:
  * `/project/dev/app/*`
  * `/project/staging/app/*`
  * ...

* Created and managed multiple parameter types successfully:
  * `String`
  * `StringList`
  * `SecureString`

* Practiced core CLI commands for the full lifecycle:
  * Create/update parameters
  * Read single and grouped parameters
  * Track versions and validate updates

* Integrated parameter retrieval into a sample script/application, reducing hardcoded secrets and config values.

* Applied secure access patterns with IAM and decryption flow for sensitive values.

* Produced practical project notes so the workflow can be reused in upcoming weeks.
* ...
