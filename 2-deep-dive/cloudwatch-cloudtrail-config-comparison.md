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
- **CloudTrail**:
    - Track who made any changes to the Load Balancer with API calls
- **Config**:
    - Track security group rules for the Load Balancer
    - Track configuration changes for the Load Balancer
    - Ensure an SSL certificate is always assigned to the Load Balancer (compliance)
