---
layout: post
title: ECS AWS WebApps - A simple pattern for deploying anything quickly using terraform 
image: /assets/img/graphql-authenticated-session/cover.png
readtime: 3 minutes
tags: AWS ECS Docker Terraform
---

One of the best things I like about infrastructure as code, and terraform in particular, is the ability to quickly, and securely deploying something, based on a pattern that you know works.

This blog post looks into a pattern we use at ditto music, to deploy a services, apis, ci build agents, websites and basically anything that can be run on a docker container. This post uses ECS as the example technology, but it could be as easy to swap out to use fargate, since it's now available in the eu-west-2 London region. 

<amp-img src="/assets/img/ecs-webapps/architecture.png"
  width="974"
  height="564"
  layout="responsive">
</amp-img>
