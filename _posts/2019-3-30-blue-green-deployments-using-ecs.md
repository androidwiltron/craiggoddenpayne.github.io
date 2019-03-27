---
layout: post
title: Blue Green deployments, utilising Terraform and AWS ECS
image: /assets/img/bluegreenaws/cover.png
readtime: 10 minutes
tags: blue green deployment terraform aws ecs
---

### What is a blue green deployment?

Blue-green deployment is a technique that reduces downtime and risk by running two identical production environments called Blue and Green.

At any time, only one of the environments is live, with the live environment serving all production traffic. For this example, Blue is currently live and Green is idle.

As you prepare a new version of your software, deployment and the final stage of testing takes place in the environment that is not live: in this example, Green. Once you have deployed and fully tested the software in Green, you switch the router so all incoming requests now go to Green instead of Blue. Green is now live, and Blue is idle.

This technique can eliminate downtime due to app deployment. In addition, blue-green deployment reduces risk: if something unexpected happens with your new version on Green, you can immediately roll back to the last version by switching back to Blue

### Blue Green at ditto

At ditto, we perform blue green deployments by utilising ECS. You could just as easily do this with fargate, but the following information is how we set this up using ECS.

The majority of deployments follow the same pattern (using the same template).

Here is an overview of the deployment pipeline we use, to get code from source to production.

#### Build Stage (build-ecs-webapp template)
a. Build artifacts
b. Run unit tests
c. Run integration tests
d. Coverage reports
e. Store artifacts in S3

#### QA Stage (publish-ecs-webapp template)
a. Pull artifacts from S3
b. Build docker image
c. Upload docker image to repository
d. Review infrastructure changes
e. Apply infrastructure changes (This causes a blue green deployment to the environment) 

#### Prod Stage
a. Pull artifacts from S3
b. Build docker image
c. Upload docker image to repository
d. Review infrastructure changes
e. Apply infrastructure changes (This causes a blue green deployment to the environment)

The deployment to the environment is completely automated, which means we can move from development to production in a matter of minutes if needed. We write all our code on mainline and use feature toggles where necessary. This keeps the codebase clean, and always ready to deploy

### A bit more about our templates

#### Build-ECS-WebApp

The following steps take place:

- Fetch, which is triggered from a commit to git. The code is pulled from github onto the agent
- Build-Build, auto triggered and ran in parallel, which runs a script called build.sh A typical build.sh is shown below
- Build-Test, auto triggered and ran in parallel, which runs a script called test.sh A typical test.sh is shown below
- Build-Test-Report, auto triggered and ran in parallel, which runs a script called test-report.sh A typical test-report.sh is shown below (I think the coverage threshold is set to 80%)
- Build-Terraform-Build, auto triggered, which takes terraform configuration files and zips them up
- Upload, which is auto triggered, uploads the above build artifacts, and stores them in S3, alongside the current version
e.g. 
s3://gocd-build-artifacts/my-application/1.230.1/deployable.zip
s3://gocd-build-artifacts/my-application/1.230.1/terraform.zip

#### Publish-ECS-WebApp 

The following steps take place:

- Fetch-S3, auto triggered, pulls the version of the code that was built, from S3
- Docker-BuildTagPush, auto triggered, builds the docker image included in the codebase, tags it with the version and pushes to our private repo in AWS
- Post-Docker, auto triggered, used in some builds to allow running code after the docker publish
- Terraform Review, auto triggered, plans the updates to infrastructure
- Terraform Apply, manually triggered after someone reviewing the infrastructure plan. This will apply the changes to infrastructure, which in turn applies the new version of the ECS task, which causes a blue green deployment.
- The same template would be then chained on from the previous environment, allowing us to force a pipeline like Build → QA → Prod


### How this looks in AWS

Container images are maintained in ECR, so we can roll back to any version if needed: 

Tasks are maintained within ECS, and we can scale to as many instances as we need to support the demand.

Deployment is triggered, tasks are marked as inactive in AWS

The new task is started, and enters a pending state

The new task starts successfully, and a health check is performed from the load balancer to container:port

After 30 seconds or so, the old version of the containers are taken out of the cluster

Here is an example of the log, which shows the blue green deployment.