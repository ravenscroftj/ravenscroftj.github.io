- This action assumes that you have a [[Poetry]] project that you want to package into a wheel and add to a [[gitea]] pypi repo.
## Add `POETRY_USERNAME` and `POETRY_TOKEN` secrets

 1. Go to Settings > Actions > Secrets and Add `POETRY_USERNAME` as a secret. Set the value to your gitea username.
 2. In another tab, go to your user settings > Applications and > Generate Token - enter name like "Poetry CI for `<ProjectName>`", Under permissions, tick `package` (read/write) and `repository` (read/write).
 3. In the first tab, add another secret for `POETRY_TOKEN` and Paste the generated token from step 2 into the value box.


### Action YAML File

Create the action yaml in the project under `.gitea/workflows/build-wheel.yml`

```yaml
name: Build & Push Wheel
on:
push:
  branches:
    - 'main'

jobs:
wheel:
  runs-on: ubuntu-latest
  steps:

  - name: install python+pip
    run: |
      apt-get update -y
      apt-get install -y python3 python3-pip

  - name: Set up poetry
    run: pip3 install poetry

  - name: check out repo
    uses: actions/checkout@v3

  - name: Build & Publish Wheel
    run: |
      poetry config repositories.gitea https://gitea.tld/api/packages/username/pypi
      poetry publish \
        --build \
        -r gitea \
        -u ${{ secrets.POETRY_USERNAME }} \
        -p ${{ secrets.POETRY_TOKEN }}
```