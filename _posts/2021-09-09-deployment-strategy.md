---
layout: post
title:  "Deployment strategy"
date:   2021-09-09 21:00:00 +0700
categories: devops
tags: [devops]
---

## Rolling
Replace the running instance with the new one.
- technical difficulty : low
- pros : easy to setup
- cons : able to test only after deploy finish which might effect users

## Blue/Green
Create whole new environment and tests it. After test successfully, then change routing.
- technical difficulty : medium
- pros : able to test pre-production before release to real users
- cons : have to provision entire environment when deploy to production

## Canary
Provision both version in production but only route a few user to new feature to test if it's good. This required kind of smart routing to be part of deployment strategy.
- technical difficulty : high
- pros : get real feedback from users before make decision to totally move to new version
- cons : need additional infrastructure setup and process to route and get feedback from new version
