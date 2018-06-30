# Expert Tips for Successful Kubernetes Deployment on AWS

>  Kubernetes started at Google and is a container Orchestrator.

## Manage

Use Kops, Kubeadm, Kubespray for cluster setup.

Kops allows you to:

- Generate CloudFormation or Terraform scripts
- Provision infrastructure and cluster components

EKS:

- Gives you a single endpoint.
- Creates an `etcd` instance alongside to each container to persist the state of the Kubernetes nodes deployed

## Consider networking

Every pod needs it's own IP address and all pods should be able to talk to one another

There are many network providers:

- Kubenet for simple use-cases
- Amazon VPC CNI for more complex use-cases

EKS uses Kubenet by default which uses the VPC for routes. It is limited to 50 routes (so 50 nodes). One way around that is to use Overlay Networks or use VPC CNI. Both solutions bring network policies (which are additives).

## Monitor

There are many moving parts (cluster, node, container, application) all emitting events.

You need log aggregation:

- Amazon CloudWatch (collect), Elastic search (index), Fluentd (store) and Kibana (visualise)
- DataDog

## Build, Ship, Run...

Kubernetes is a platform for automating deployment and scaling of applications.

You should have a workflow in place for everything to be automated (see their published blog post).