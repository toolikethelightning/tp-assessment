# TP Assessment
[Terraform repo](https://github.com/toolikethelightning/tp-assessment-terraform)

### Approach
**CI/CD - using GitHub Actions**
  * For this repo, there are two jobs - testing, and deploying the application (the latter of which includes building the Docker container).
  * For the [Terraform repo](https://github.com/toolikethelightning/tp-assessment-terraform) - there are two workflows - Planning, and Applying the Terraform configuration.
  * This was my first time using GH Actions as CI, so I tried to keep things as simple as possible.
---
**Infrastructure**
* Using **Terraform Cloud** for storing remote state, and executing Terraform runs  
* Followed guides such as AWS' [VPC with servers in private subnets and NAT](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-example-private-subnets-nat.html) to layout the infrastructure

### Problems Encountered
* **PRs** were used in both repos, and I have commented where there were problems to solve - for example, there were a few in [the PR](https://github.com/toolikethelightning/tp-assessment/pull/2) tackling the deployment flow.

* Testing the service locally, I encountered an issue with [MacOS already using port 5000](https://progressstory.com/tech/port-5000-already-in-use-macos-monterey-issue/), hence the use of `5001`.


* AWS Permissions - I encountered a couple of specific issues here:
  * Insufficient permissions to add Tags to ECR Repos
  * Insufficient permissions to deploy a CF Logs Group
    * I hadn’t thought at the time it may be possible to use a default group, and didn’t investigate this properly.
  * Insufficient permissions to update an ASG Target (` not authorized to perform: iam:PassRole ... because no identity-based policy allows the iam:PassRole action`)

* Docker Build - I've previously run into a problem here, which was fixed by setting `--platform=linux/amd64` - see [here](https://stackoverflow.com/questions/67361936/exec-user-process-caused-exec-format-error-in-aws-fargate-service).

### Useful Links
* [Deploying to Amazon ECS](https://docs.github.com/en/actions/deployment/deploying-to-your-cloud-provider/deploying-to-amazon-elastic-container-service)
* [Automate Terraform with GitHub Actions](https://developer.hashicorp.com/terraform/tutorials/automation/github-actions)
* [amazon-ecs-deploy-task-definition](https://github.com/aws-actions/amazon-ecs-deploy-task-definition)
* [learn-terraform-github-actions](https://github.com/hashicorp-education/learn-terraform-github-actions/tree/main)
