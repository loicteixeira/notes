# Advanced Container Security

Run ECS and EKS on EC2 (more control) or via Fargate (more managed). Looking at ECS Fargate today.

Challenges:

- Containers can be transient
- Clusters can be complex distributed system by themselves
- Complex image provenance
- Less isolated (containers share a kernel)

## Security in AWS

Shared Responsibility Model: AWS have the responsibility *of* the cloud and the Customer *in* the cloud.

- Customer Data
  - Secret: Use Parameter Store (Encryption, Versioning, Access Control, Audit logs, Versioning, APIs). Secret manager is more recent and adds automatic rolling of secrets.
- IAM: Can have a role, ENI and Security Group per task
- Network and Firewall Configuration: You can use a security group as both a source and destination allowing micro-segmentation without complex sub-netting.
- Connection between containers go out of the network interface and back in (even when on same host) so it can go through all the other checks.

Security Benefit of Fargate:

- Patching of OS (used to be the customer's responsibility with EC2)
- Network security
- Cluster-level isolation
- No runtime access for users (can't ssh into instance or use docker exec)
- No privileged access for containers

IAM with Fargate has one more level:

- Cluster: Who can launch and stop and describe task
- App: Task's use of AWS resources
- Execution (new): ECR pull, logs, ENI creation, ELB register/deregister

## How do we secure the container image?

- No secrets
- Trusted base images
- One service per container
- No console troubleshooting tools (you can't use them anyway in Fargate)
- Unique and informative image tags
- Use `Clair` to scan image for vulnerability in CI/CD
