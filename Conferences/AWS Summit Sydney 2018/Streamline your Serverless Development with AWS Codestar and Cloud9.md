# Streamline you Serverless Development with AWS CodeStar and AWS Cloud9

## 3 Pillars of Software Development

- Run
  - Compute: Many options like Lambda, EC2, Fargate, ECS, etc.
- Release
  - 4 main phases with corresponding AWS tools:
    - Source: CodeCommit
    - Build: CodeBuild & CodePipeline
    - Test: Third Party & CodePipeline
    - Deploy: CodeDeploy
  - All 4 phases are combined with CodeStar
- Create
  - Cloud9, a cloud based, fully featured IDE

## Cloud9

- Needs an instance to run on. You can pick the size.
- Has auto teardown on idle for saving costs
- Understand serveless applications natively (also works with single Lambda functions)
  - Created from template (blank, api gateway)
  - Automatically deployed (with corresponding resources)
  - Interactive debugging in API Gateway local or Lambda local
- Collaborative work a la Google Docs for pair coding
- Your AWS credentials already added to the instance so you can use the aws-cli directly.

## CloudStar

- Starting templates
- CI/CD integrated by default