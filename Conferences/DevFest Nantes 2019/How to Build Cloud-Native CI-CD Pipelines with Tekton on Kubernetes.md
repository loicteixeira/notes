---
speakers:
- Vincent Demeester
topics:
- Cloud
- DevOps
---

# How to Build Cloud-Native CI/CD Pipelines with Tekton on Kubernetes

## What is a cloud-native CI/CD?

### What is Cloud-Native?

- Microservices in containers
- Dynamically orchestrated
- Optimised resource utilisation

It brings some complexity and it's hard to manage. But it also means that each little sqaure can be managed by a different team.

### What is Cloud-Native CI/CD?

- Uses Containers
- Run Serverless, run serverless with no CI/CD engine to manage and maintain
	- Scaling up and down resources as eneded
	- You specifiy what you want to run, freed of the much of responsability to manage the underlying resources
- DevOps, designed with microservices and distributed teams in mind
- Specification & Standards
	- Any k8s resource can be manipulated (e.g. with controllers, admission webhooks
	- Anything builr on k8s can be manipulated with k8s tools
- Infrastructure agnostic
- Reusable components
	- Write it once, use it again and again w/ different resources/parameters
	- K8s is itself a building block, that enables the creation of more building blocks

### Jenkins is great but...

- Not built for container environments
- Need babysitting and lots of attention
- Quickly becomes an overhead
- Has brittle configuration
- Doesn't fit microservices team structures
- Suffers from plugins mania

## Tekton

### What is it?

An open-source projects to provide a set of shared and standerad component for building K8s-style CI/CD system. It is Governed by the Continous-Delivery Foundation

- Extends the k8s API
- Runs things in containers, runs itself in containers
- Able to build images from your tool of choice (source-to-omage, janiko, jib, docker, etc)
- Deploy to multiple platfor;s (serverless, virtual machines and k8s)
- Provides a powerful CLI
- Integrated CI/CD experience with OpenShift Pipelines, OpenShift Developer Console, IDE plugins

### Concept

#### Steps

- A command running in a containers
- Kubernetes container spec (env vars, volumes, config maps, secrets)

#### Tasks

- Define a unite of work to be executed
- List of steps run sequentially
- Step containers run in the task prod
- Has inputs, outputs and parameters
- Can run independent of pipelines

#### Pipeline

- Combine multiple tasks
- Express task order (grap)
- Has inputs and parameters
- Links tasks inputs and outputs
- Pipeline tasks run on different nodes

#### Pipeline Resources

- Inputs and outputs of tasks and pipelines
	- Git repository, Image in registry, etc
- Decoupled from pipeline definition (allow for writing of generic pipelines)
- Reusable across pipelines

#### TaskRun and PipelineRun

- Runtime CRDs
- Invocation of Task and PIpeline
- Reference tasks and pipelines
- Provide inputs, outputs and params

#### Task Catalog

- Catalog of reusable Tasks
	- Image buld: bulidadh, kaniki, buildpacks, etc
	- Source-toImage: Java, Python
- Import and compose pipelines

See [tektoncd/catalog](https://github.com/tektoncd/catalog) and [openshift/pipeline-catalog](https://github.com/openshift/pipeline-catalog).

#### Triggers

- Running pielines in response to an event (GH webhooks, Cloud Event, etc)
- Base components to create Prow / Jenkins-x

See [kubernetes/test-infra](https://github.com/kubernetes/test-infra).

#### Operator (Operator Hub)

Product by RedHat.

Allows you to install tools, in this case Tekton CD, without having to update your YAML files, etc.

Services updates are also taken care off.

## Demo

The demo gods weren't with us 🙁

Triggers aren't quite there yet but builds can be started via the CLI too. You would have to bind resources manually and the CLI will prompt you if there are any missing parameters.

Reminder that Tekton brings the building blocks but the real value is integrating it with a CI solution.

## What is next for Tekton?

- Getting out of alpha
- PipelineResource design work
- Stand-alone PIpeline with Triggers (no need for Prow, etc)
- Catalog integration
- Metrics, performance testing, etc
- UX work: CLI, Dashboard, VS Code plugin
- Pipeline-as-code (in the same repo as the code)

### Tentative roadmap

- 2020:
	- Tekton Triggers 0.2
	- Tekton Pipeline Beta
	- Catalog Integration (pipeline, ci, etc)
	- Notification, manual approval and more advanced concepts

## Links

- [Website](https://tekton.dev)
- [GitHub](https://github.com/tektoncd)
