# lab8-monitor-soar-infra
Monitor &amp; Maintain SIEM / SOAR Infrastructure: Integrating CloudWatch Agent with Custom Configurations to Stream EC2 Metrics for Infrastructure Observability
💻 Lab 8: Monitor & Maintain SIEM / SOAR Infrastructure
Project Repository: lab8-monitor-soar-infra
Author: Dr. Ime Ben
Instance: i-087d6c7189a71da58
Date Completed: July 29, 2025
Region: Europe (Ireland) eu-west-1

💻 Lab 8: Monitor & Maintain SIEM / SOAR Infrastructure
Project Repository: lab8-monitor-soar-infra
Author: Dr. Ime Ben
Instance: i-087d6c7189a71da58
Date Completed: July 29, 2025
Region: Europe (Ireland) eu-west-1
🧩 Objective
To monitor and maintain the SIEM/SOAR infrastructure by:
- Installing and configuring the Amazon CloudWatch Agent.
- Writing and deploying a custom JSON configuration.
- Validating and starting the agent to stream EC2 system metrics.
- Ensuring visibility and observability for ongoing SIEM/SOAR operations.
⚙️ Tools & Technologies Used
- AWS EC2 (Amazon Linux 2)
- Amazon CloudWatch Agent
- Custom JSON config file
- Shell commands (nano, yum, systemctl)
- GitHub for documentation
🛠️ Implementation Steps
1. ✅ Installation of CloudWatch Agent
Command:
sudo yum install amazon-cloudwatch-agent -y
Result: Confirmed successful installation.
2. 🧾 Custom JSON Configuration
Path:
 nano /home/ec2-user/config.json

Sample structure:
{
  "metrics": {
    "append_dimensions": {
      "InstanceId": "${aws:InstanceId}"
    },
    "metrics_collected": {
      "cpu": {
        "measurement": ["cpu_usage_idle", "cpu_usage_user", "cpu_usage_system"],
        "metrics_collection_interval": 60
      },
      "disk": {
        "measurement": ["used_percent"],
        "metrics_collection_interval": 60,
        "resources": ["/"]
      },
      "mem": {
        "measurement": ["mem_used_percent"],
        "metrics_collection_interval": 60
      }
    }
  }
}
3. 🧪 Configuration Validation
Used fetch-config:
/opt/aws/amazon-cloudwatch-agent/bin/amazon-cloudwatch-agent-ctl \
-a fetch-config \
-m ec2 \
-c file:/home/ec2-user/config.json \
-s

Validated schema:
/opt/aws/amazon-cloudwatch-agent/bin/amazon-cloudwatch-agent -schematest \
-config /opt/aws/amazon-cloudwatch-agent/etc/amazon-cloudwatch-agent.toml
4. 🚀 Agent Launch & Verification
Command:
/opt/aws/amazon-cloudwatch-agent/bin/amazon-cloudwatch-agent-ctl -a status

Output:
{
 "status": "running",
 "starttime": "2025-07-29T17:27:19+00:00",
 "configstatus": "configured",
 "version": "1.300055.3"
}
🔍 Results & Observations
- System metrics were successfully pushed to CloudWatch.
- Verified cpu, memory, and disk utilization metrics.
- Improved observability for incident-detection-lab.
🧠 Skills & Learning Outcomes
- Real-world configuration and validation of CloudWatch Agent.
- Custom metric ingestion to support infrastructure observability.
- Practical application of JSON schema and monitoring practices.
- Strengthened SIEM/SOAR maintenance and visibility skills.
⚠️ Challenges Faced
- Initial file path errors (no such file or directory).
- JSON parsing error due to misformatted character.
- Required correcting file path and valid JSON syntax.
✅ Best Practices
- Always validate your JSON configuration using schema tests.
- Use append_dimensions for contextual metrics.
- Monitor status with amazon-cloudwatch-agent-ctl -a status.
📌 Key Takeaways
This lab showcased the importance of continuous monitoring within a security operations infrastructure. 
The integration of custom CloudWatch metrics enables deeper insights, proactive alerts, and sustained observability 
across EC2-based SIEM/SOAR platforms.
📸 Screenshots & Logs
All screenshots and command outputs are stored on GitHub:
📂 https://github.com/ime-cloud-sec-analyst/lab8-m


