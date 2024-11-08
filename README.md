# CRONDA
Cron for deletion application (CRONDA)

 CRONDA - Cron for Deletion Application

CRONDA is an automated object management solution designed to manage scheduled deletions of resources in a cloud environment. Leveraging cron jobs, it ensures that your environment stays clean by automatically identifying and removing outdated or unused resources, helping optimize costs and maintain an organized infrastructure.

**Table of Contents**

Project Overview
Features
Architecture
Tech Stack
Setup and Installation
Usage
Contributing
License

**Project Overview**

CRONDA provides an automated way to handle resource cleanup by running cron jobs that delete specified resources on a set schedule. This helps in managing cloud resources efficiently and avoiding unnecessary costs due to idle or outdated resources.

Use Cases:

Periodic cleanup of unused snapshots, images, or backup files.
Scheduled deletion of temporary files or test resources.
Automatic removal of stale objects in a bucket or storage service.

Features

Automated Deletion: Schedule tasks for automated deletion using cron jobs.
Configurable Schedule: Easily set custom schedules for different tasks using cron expressions.
Resource Management: Supports various types of cloud resources for scheduled deletion.
Logging: Detailed logs to monitor deletion activities.
Alerting (Optional): Email or Slack alerts for actions performed (can be customized).

Architecture

The architecture is built around a cron job scheduler that triggers the deletion application. Below is a simplified flow:

Scheduler: Cron job triggers the deletion script.
Deletion Script: The script fetches the list of resources based on the configuration and applies the deletion logic.
Logging and Alerting: Logs the actions and sends notifications if enabled.

Tech Stack

Python: Core scripting language
Boto3: For interacting with AWS services
AWS Lambda (Optional): Serverless execution of deletion scripts
CloudWatch: Monitoring and alerting
Crontab: For scheduling tasks locally or in a server environment

**Setup and Installation**

Prerequisites

Python 3.8+
AWS CLI configured with necessary permissions
Git


**Clone the Repository**

git clone https://github.com/PournimaTivatane12/CRONDA.git
cd CRONDA

**Install Dependencies**

pip install -r requirements.txt

**Configuration**

Update the configuration file config.json with your AWS credentials and the resources you want to manage:

{
    "region": "us-east-1",
    "resources": [
        {"type": "ebs_snapshot", "days_threshold": 30},
        {"type": "s3_objects", "days_threshold": 15}
    ],
    "notification": {
        "enable": false,
        "email": "your-email@example.com"
    }
}


Set up your cron job using crontab:

crontab -e

Add the following line to schedule the job (e.g., runs every day at midnight):

0 0 * * * /usr/bin/python3 /path/to/CRONDA/cron_deletion_script.py >> /path/to/CRONDA/logs/cron.log 2>&1


Environment Variables (Optional)
AWS_ACCESS_KEY_ID - AWS Access Key
AWS_SECRET_ACCESS_KEY - AWS Secret Key
AWS_REGION - AWS Region

export AWS_ACCESS_KEY_ID="your_access_key"
export AWS_SECRET_ACCESS_KEY="your_secret_key"
export AWS_REGION="us-east-1"

**Usage**

Run the application manually:

python cron_deletion_script.py

Monitor logs to see the deletion activities:

tail -f logs/cron.log

**Contributing**

We welcome contributions! Please see our CONTRIBUTING.md file for guidelines on how to contribute to this project.

**License**

This project is licensed under the MIT License - see the LICENSE file for details.

