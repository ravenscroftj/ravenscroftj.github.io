---
title: Gitea SSH Actions
tags:
 - GiteaActions
---

There are some use cases where it's good to be able to ssh into a remote machine to do something (like pull changes and deploy them).

## Add a new actions yaml

Add a file like the following to your project under `.gitea/workflows/ssh-action.yml` 

```yaml
name: Deploy Website
on: [push]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:

    - name: Do the SSH Thing
      run: |
        mkdir -p ~/.ssh/
        echo "$SSH_PRIVATE_KEY" > ~/.ssh/id_rsa
        chmod 600 ~/.ssh/id_rsa
        echo "$SSH_KNOWN_HOSTS" > ~/.ssh/known_hosts
        ssh \
          -i ~/.ssh/id_rsa \
          -t user@testhost.tld \
          "cd /project/dir; git pull; ./deploy.sh" 
      shell: bash
      env:
        SSH_PRIVATE_KEY: ${{secrets.SSH_KEY}}
        SSH_KNOWN_HOSTS: ${{secrets.SSH_KNOWN_HOSTS}}
```

### Generate an SSH Key

You'll need an ssh key that can log into the remote machine - use `ssh-keygen` to generate one.

### Set up SSH Key secret

run `cat` on the private key and copy the contents into gitea as a secret

### Store host fingerprints

run `ssh-keyscan -H testhost.tld >> known_hosts` and cat the known_hosts file.  Paste the contents into another actions secret `SSH_KNOWN_HOSTS`

This script will ssh into the remote machine using the `SSH_KEY` and `SSH_KNOWN_HOSTS` that we set up.