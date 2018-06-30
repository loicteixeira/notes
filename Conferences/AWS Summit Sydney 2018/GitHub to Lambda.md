# GitHub to Lambda: Developing, Testing and Deploying Serveless Apps

## GitHub Enterprise 2.13 Overview

- Better Collaboration
  - Team discussions: can be private when issues/pull-request will be public (not always)
  - Commit co-authors: we don't work alone anymore
- Extending the GitHub platform
  - GitHub Apps can be installed directly on org or users, act on their own behalf and don't take a license seat
  - GraphQL API version 4
- Enabling administrators
  - Can use LDAP and/or the built-in one at the same time
- Extended pre-receive hooks
  - Help enforce org policies, e.g. ensure every branch starts with the username
  - Support push options (`-o` or `--push-options` to not pollute the commit with metadata)
- Hotpatching for clustering
- Grafana in your monitor Dashboard

## Automating Serverless Deployments using GitHub, Lambda and CodeStar

CodeStar is a cloud-based service for creating, managing and working with software development projects on AWS.

GitHub will notify CodeStar of configuration changes in GitHub.

1. Need admin IAM user (with CodeStar, Lambda and S3 full access)
2. Create CodeStar project giving access to GitHub (it can create the repo for you)
   - CodeStar orchestrate: CloudFormation, CodeBuild, CloudWatch, Lambda, S3
3. Clone locally
4. Create a Role for the Lambda function to run under (read/write to S3, Cloudwatch)
5. Remove existing stack
6. Revise permissions
   - Find the associated role and edit the policy
7. Revise code and run

Go further by having branches building and deploying to lambda test environments.