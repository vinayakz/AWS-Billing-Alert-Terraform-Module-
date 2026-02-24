# AWS Billing Alert Terraform module
Welcome to AWS Billing Alert module! This module helps you set up automatic billing alerts for your AWS account. Once configured, you'll receive notifications when your AWS charges exceed specified amounts, helping you stay on top of your costs.

## Prerequisites

> [!IMPORTANT]
> **Before you begin, make sure you have the following:**  
>
> -  **Terraform (v1.5.0 or later)** installed on your local machine.  
> -  **An AWS account** with appropriate permissions.  
> -  **AWS CLI** configured with the necessary credentials.  

## Understanding the AWS Services

### AWS CloudWatch

Amazon CloudWatch is a comprehensive monitoring and observability service designed for DevOps engineers, developers, and IT managers to track AWS resources and applications in real-time. It collects, monitors, and analyzes logs, metrics, and events to help optimize performance, automate responses, and maintain system health.

### AWS SNS (Simple Notification Service)
AWS SNS a fully managed, high-throughput message broker providing pub/sub messaging for microservices, distributed systems, and serverless applications, as well as A2P (application-to-person) notifications.

### AWS Billing 

AWS Billing provides tools to manage your AWS costs and budget. This module automates the monitoring of your AWS billing, so you're notified before your bill goes beyond your expectations.

## Setup Instructions

### Clone the Repository

1. Open your terminal or command prompt.  
2. Navigate to the directory where you'd like to place the project:  
    ```bash  
    cd /path/to/your/directory  
    ``` 
3. Clone the repository:  

    ```bash
    git clone https://github.com/NotHarshhaa/aws-billing-alert-terraform.git  
    ```

4. Move into the directory:  

   ```bash  
   cd aws-billing-alert-terraform  
   ```  

### Install Terraform

Follow the steps

```bash
sudo apt-get update && sudo apt-get install -y gnupg software-properties-common curl
curl -fsSL https://apt.releases.hashicorp.com/gpg | sudo gpg --dearmor -o /usr/share/keyrings/hashicorp-archive-keyring.gpg
echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/hashicorp.list
sudo apt update
sudo apt install terraform
terraform --version
```

### Initialize Terraform
Prepare Terraform for use: 

```bash  
terraform init  
```

### Configure and Apply Changes 

#### Update Configuration Variables:  

Configure your billing alerts using the provided `terraform.tfvars.example` file:  

```hcl  
# Copy terraform.tfvars.example to terraform.tfvars and customize
aws_region            = "us-east-1"  
alert_thresholds      = [100, 150, 200]  
currency              = "USD"  
email_endpoints       = ["your-email@example.com", "team@example.com"]  
environment_tag       = "Production"  
auto_confirm_subscription = false  
sns_topic_name        = "billing-alert"  
```  

### Module Outputs
After deployment, you'll get these useful outputs:

```hcl  
# SNS topic for monitoring  
output "sns_topic_arn"  

# List of all alarm names  
output "cloudwatch_alarm_names"  
output "service_alarm_names"  

# DLQ for troubleshooting  
output "sns_dlq_arn"  

# Configuration summary  
output "configuration_summary"  
```  

## Usage

This module is designed for **simplicity and reliability**:  

1. **Quick Setup** – Copy `terraform.tfvars.example` to `terraform.tfvars`  
2. **Configure Emails** – Add your email addresses to `email_endpoints`  
3. **Set Thresholds** – Adjust `alert_thresholds` based on your budget  
4. **Deploy** – Run `terraform apply`  
5. **Monitor** – Receive alerts when charges exceed your thresholds  

### Advanced Configuration

The module supports these customizations:  
- **Multiple thresholds** – Get alerts at different spending levels  
- **Service-specific monitoring** – EC2 service charges tracked separately  
- **Custom regions and currencies** – Deploy anywhere with local currency  
- **Environment tagging** – Organize resources by environment  

### Security Features  

- **Least Privilege Access** – Only necessary permissions granted  
- **Secure Communication** – Proper SNS and SQS policies  
- **Resource Isolation** – Clear separation of concerns  
- **No Hardcoded Secrets** – All configuration via variables  

## � Customization

### Billing Thresholds

Modify the `alert_thresholds` in your `terraform.tfvars` file to configure additional thresholds:

```hcl
alert_thresholds = [100, 150, 200, 250]
```
