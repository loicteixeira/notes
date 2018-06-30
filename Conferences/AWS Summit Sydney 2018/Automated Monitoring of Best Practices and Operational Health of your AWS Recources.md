# Automated Monitoring of Best Practices and Operational Health of your AWS Recources

## Do you know what's in your AWS accounts?

Applications can expand as the business expands. Started as a simple stack but quickly scaled and it becomes hard to have an overview of the resources cost, performances, security, fault-tolerance and server limits.ents?

## Meet AWS Trusted Advisor (TA)

- Takes away the best Practices Monitoring heavy lifting
  - It's not going to revolutionise how you do things but instead will let you know of under-utilisation, mis-configuration
- Provides best practices (or checks)
- Integrate CoudWatch Events to take direct actions enabling automation

How?

1. Tag resources subject to AWS TA optimisation actions
2. Create an IAM policy and role for the Lambda function to use
3. Setup CloudWatch event rule to trigger the Lambda function
4. Setup the Lambda function to take actions recommended by TA

More on tags, they can be used to:

- Figure out what to track
- Allow different responses, e.g. stop under-utilised EC2 instances immediately if tagged `dev` but notify only if tagged `prod`

## What about Events, Scheduled Changes and AWS Health Events?

Service Health Dashboard (SHD) is a high level view but is too limited for your own application.

AWS Health & Personal Health Dashboard sits within your account and gives you a better perspective.

- Receives notification and remediation guidance
- Can forward to CloudWatch which will in turn trigger actions (via Lambda or Step Functions)

## Misc

Containers are now 1st class citizen in AWS. Use Fargate as AWS takes more of the security responsibility away form the customer (see `Security Benefit of Fargate` of the `Advanced Container Security` talk for more info).