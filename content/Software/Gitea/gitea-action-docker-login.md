---
tags:
 - GiteaActions
---
# Docker Login In Gitea Actions

This page is a WIP - the intention is to be able to create [[Docker]] containers inside [[gitea]] actions.

## Enable Actions For Repo

Go into the project settings and enable Gitea Actions.

## Create DOCKER_USERNAME secret 

go to Settings > Actions > Secrets and Add DOCKER_USERNAME as a secret. Set it to your gitea username.

## Create a personal access token

Go to your user settings > Applications and > Generate Token - enter name like "Docker CI for <ProjectName>", 

Under permissions, tick `package` (read/write) and `repository` (read/write)

## Create DOCKER_TOKEN secret

Go back to your project settings and go Settings > Actions > Secrets and add DOCKER_TOKEN, set the value to the token you just generated.