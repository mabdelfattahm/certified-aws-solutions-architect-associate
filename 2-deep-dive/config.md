# AWS Config

- Helps with auditing and recording compliance of AWS resources
- Helps record configurations and changes over time
- Provides the ability of storing the configuration data into S3 where it can be analyzed by Athena
- Problems AWS Config Solves:
    - Check if there is unrestricted SSH access to a security group
    - Check if buckets have public access
    - Find out how did an ALB configuration change over time
- We can receive alerts (SNS notifications) for any change
- AWS Config is a per region service, but it can be aggregated across regions and accounts

## AWS Config Resource

- Ability to view the compliance of a resource over time
- Ability to view configuration of a resource over time
- View CloudTrails API calls if enabled

## AWS Config Rules

- Can use AWS managed config rules (over 75) which can be used by the users
- Can also make custom config rules (must be defined using AWS Lambda)
    - eg. Evaluate if each EBS disk is of type GP2
    - eg. Evaluate if each EC2 instance is of type t2.micro
- Rules can be evaluated/triggered:
    - For each config change
    - At regular time intervals
- Evaluation of rules can trigger CloudWatch events if the rule is non-compliant
- Rules can have auto remediations: if a resource is not compliant, the is an option to trigger auto remediation, example: stop instances with non-approved tags
- **AWS Config Rules do not prevent actions from happening (no deny)**

### Config Rules - Remediations

- Automate remediation of non-compliant resourcecs using SSM Automation Documents
- Use AWS-Managed Automation Documents or create custom Automation Documents
    - Tip: you can create custom Automation Documents that invokes Lambda function
- You can set **Remediation Retries** if the resource is still non-compliant after auto- remediation

### Config Rules - Notifications

- Use EventBridge to trigger notifications when AWS resources are noncompliant
- Ability to send configuration changes and compliance state notifications to SNS (all events – use SNS Filtering or filter at client-side)

## CloudWatch vs CloudTrail vs Config

- **CloudWatch**
    - Performance monitoring (metrics, CPU, network, etc.) and dashboards
    - Events and alerting
    - Log aggregation and analysis
- **CloudTrail**
    - Record API calls made within an account
    - Define trails for specific resources
    - It is a global service
- **Config**
    - Record configuration changes
    - Evaluate resources against compliance rules
    - Get timeline of changes and compliance

### CloudWatch vs CloudTrail vs Config - For an ELB (Elastic Load Balancer)

- **CloudWatch**:
    - Monitoring Incoming connections metric
    - Visualize error codes as % over time
    - Make a dashboard to get an idea of your load balancer performance
- **Config**:
    - Track security group rules for the Load Balancer
    - Track configuration changes for the Load Balancer
    - Ensure an SSL certificate is always assigned to the Load Balancer (compliance)
- **CloudTrail**:
    - Track who made any changes to the Load Balancer with API calls
