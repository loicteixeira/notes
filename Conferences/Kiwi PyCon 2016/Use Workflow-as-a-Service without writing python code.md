---
videos:
- https://youtu.be/pLV_JQVTn2g
---

# Use Workflow-as-a-Service without writing python code

`Mistral` is part of the *OpenStack cloud*.

It's some sort of a Celery task queue, except it uses YAML (extended with YAQL) for workflow definition.

Tasks can:

- pause the workflow and will only resume with human intervention. This allow you to inspect the state and inject new values if needed.
- can conditionally trigger other tasks.
- have policies (retry, timeout, wait-before)