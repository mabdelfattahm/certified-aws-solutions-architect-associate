# AWS CloudTrail

- **Provides governance, compliance and audit for an AWS account**
- CloudTrail is enabled by default
- CloudTrail provides a **history of events/API calls made within an AWS account** from:
    - AWS Console
    - SDK
    - CLI
    - AWS services
- Logs from CloudTrail can be put into CloudWatch Logs or S3
- **A trail can be applied to All Regions (default) or a single Region.**
- If a resource is deleted in AWS, investigate CloudTrail first!

## CloudTrail Events

- **Management Events:**
    - Management events provide insight into management operations that are performed on resources in your AWS account. These are also known as control plane operations. Management events can also include non-API events that occur in the account
    - Operations that are performed on resources in your AWS account
    - Examples:
        - Configuring security (IAM AttachRolePolicy)
        - Configuring rules for routing data (Amazon EC2 CreateSubnet)
        - Setting up logging (AWS CloudTrail CreateTrail)
    -** By default, trails are configured to log management events.**
    - Can separate **Read Events** (that don’t modify resources) from **Write Events** (that may modify resources)

- **Data Events**:
    - These events provide insight into the resource operations performed on or within a resource. These are also known as data plane operations
    - **By default, data events are not logged (because high volume operations)**
    - Amazon **S3** object-level activity (ex: GetObject, DeleteObject, PutObject): can separate Read and Write Events
    - AWS **Lambda** function execution activity (the Invoke API)

- CloudTrail records account activity and service events from most AWS services and logs the following records:
    - The identity of the API caller
    - The time of the API call
    - The source IP address of the API caller
    - The request parameters
    - The response elements returned by the AWS service

## CloudTrail Insights

- Enable **CloudTrail Insights to detect unusual activity** in your account:
    - inaccurate resource provisioning
    - hitting service limits
    - Bursts of AWS IAM actions
    - Gaps in periodic maintenance activity
- CloudTrail Insights analyzes normal management events to create a baseline
- And then **continuously analyzes _write_ events to detect unusual patterns**
    - Anomalies appear in the CloudTrail console
    - Event is sent to Amazon S3
    - An EventBridge event is generated (for automation needs)

## CloudTrail Events Retention

- Events are stored for 90 days in CloudTrail
- To keep events beyond this period, log them to S3 and use Athena
