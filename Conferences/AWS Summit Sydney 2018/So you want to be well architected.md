# So you want to be well architected

The Well-Architected framework is a set of questions to find out if you are (well architected) or what you should do. It isn't static and will evolve, therefore you should run through it during development, before deploying and throughout the life of your product.

Why do it? It reduce firefighting by identifying and fixing issues before they occur.

Remember to learn, measure and improve:

>  Good intentions never work – Jeff Bozos

## Principles

Get the whitepapers at https://aws.amazon.com/well-architected.

### General

- Stop guessing capacity needs
- Test systems at production scale
- Automate to make architectural experimentation easy
- Drive your architecture using data
- Improve through Game Days

### Operational Excellence

> Prepare, Operate & Evolve

- Perform Operations with Code
- Annotated Documentation
- Make Frequent, Small & Reversible Changes
- Refine Operations Procedures Frequently
- Anticipate Failures
- Learn from all Operation Failures

### Security

>  Security is Job #0 but we often have security at the edge and still have a soft core.

- Implement a strong identity foundation
- Enable traceability
  - Use CloudTrail
- Apply security at all layers
- Automate security best practices
- Protect data in transit and at rest
  - Use KMS to bring your own keys or have new one managed (and rotated)
- Prepare for security events

### Reliability

> Foundations, Change Management & Failure Management

- Test recovery procedures
- Automatically recover from failure
- Scale horizontally to improve availability
- Stop guessing capacity
- Manage change through automation

### Performance Efficiency

> Selection, Review, Monitoring & Tradeoff

- Democratise advanced technologies
- Go global in minutes
- Use serverless architectures
- Experiment more often
- Mechanical sympathy

### Cost Optimisation

> Cost effective resources, Matched supply & demand, Expenditure awareness, Optimising over time

- Adopt a consumption model
- Benefit from economies of scale
- Stop spending money on data centre operations
- Analyse and attribute expenditure
- Drive your architecture using data
- Use managed services to reduce cost of ownership

## Summary

- Strategy & best practices for architecting in the cloud
- Questions allows you to *measure* your architecture against best practices and provide clarity on where to focus next
- Making *informed decisions* about architecture in the cloud
- Questions are a *starting point*
- Not a binary "yes" or "no"
- Consistency of reviews
- Ongoing process