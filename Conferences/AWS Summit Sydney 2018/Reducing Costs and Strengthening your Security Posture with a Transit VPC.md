# Reducing Costs and Strengthening your Security Posture with a Transit VPC

*Mostly selling PaloAlto Networks solution.*

TL;DR; Transit VPCs protect apps and data in a cost-effective manner

- AWS enables you to scale your environment in an automated matter
- The Transit VPC with the VM-Series reduces security and connectivity management challenges associates with scale
  - Security teams can build a centralized security architecture that becomes part of the application development fabric
  - Development teams can scale as needed knowing apps and data area transparently protecting from threats and data exfiltration

See resources to [accelerate AWS Deployments](https://live.paloaltonetworks.com/cloudtemplate)

Business critical applications are rarely "stand alone" and often communicate with other applications, data sources and resources within the same VPC or different VPC/accounts. General security options are:

- Backhaul all traffic through corporate firewall
  - Costly, bandwidth intensive,
  - Ineffective
- Deploy a firewall in ever VPC

It can be hard to go from one VPC to another one. Overlay Networks makes multiple VPC act as one.

Transit VPC with Hub and Spoke model can be deployed to the cloud and private data centre.

- Dedicated spoke for shared services
  - Deploy a shared services as a spoke (DNS, logging, etc)
  - Shared services remain behind the hub
- Hardware solution instead of virtual firewall can be handy to reduce costs if your app is SSL heavy (needs a lot of encryption/decryption) which is going to be more cost-effective than a software based solution

