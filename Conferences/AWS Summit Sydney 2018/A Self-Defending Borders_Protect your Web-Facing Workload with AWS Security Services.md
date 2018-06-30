# A Self-Defending Borders: Protect your Web-Facing Workload with AWS Security Services

## General

Explore a use case of edge transformation using AWS WAF, AWS Shield & AWS Guard Duty. Demo of self defending AWS architecture.

Modern business challenges:

- Increased frequency
- Low capital investment
- Increase of rules and regulation
- Disparate of non-connected systems

Threats today:

- OWASp Style Attacks (XSS, Injections, etc)
- Hacktivists & Crime Syndicates (Botnets, DDoS, etc)

Solutions:

- L3-L7 Firewals (source destination checks)
- DDoS Mitigation (BGP Announcement Traffic Rerouting)
- Monitoring Static Analysis (Static App Security Testing, Log Files Analysis)


Why not implemented?

- Expensive
- Lack of Automation (Integration Challenges with DevSecOps Models)
- False Positive (Content changes often and requires new rules)

## Demo

Example of a quickly growing company with N-Tier Architecture, ERP/CRM Integration and limited IT resources.

Using `Kali Linux` for pen-testing and security auditing, a distro with hundreds of tools (e.g. `Hydra` used to brute force a port after scanning for open port on the bastion host).

Basic mitigation with:

- AWS Shield
  - Managed DDoS protection service available to all AWS customer at no additional cost (standard for L7 attacks)
  - Advanced protected is a paid service that provide additional, comprehensive protection from large and sophisticated attacks (L3 attacks)
- WAF with CloudFront
  - Helps mitigate some OWASP vulnerability (e.g. can catch some attempts of SQL Injection via query params)
  - A request is made and CloudFront decide if the request needs to be looked at by WAF which can return an error or the real resource.

Not a silver bullet. It will just give you time for you to patch.

Let's get proactive though. Self-defending borders:

- Load Balancer
- Logs generated from CloudFront saved to S3
- Honey Pot endpoint with Amazon API Gateway
- AWS Guard Duty evaluate duplicated VPC flow Log, queries to domains and CloudTrail history


Example of action: Triggers can execute a Step Function (with manual approval or automatically) to add an IP to API Gateway (to serve a honey pot endpoint) or WAF (to block), and also to a NoSQL database with a timestamp. Another scheduled Lambda can remove this IP after 10 minutes. If the attack continue, block the IP again for a longer period.