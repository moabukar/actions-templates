# GitHub Actions workflow templates

## List of GitHub Actions templates I have created:

- [Terraform Validate action template](.github/actions/terraform-validate/action.yml)
- [Auto Merge](.github/actions/auto-merge/action.yml)
- [Spacelift Deploy](.github/actions/spacelift-deploy/action.yml)
- [Markdown lint](.github/actions/markdown-lint/action.yml)
- [Docker image publish](.github/actions/docker-publish/action.yml)
- [Docker build](.github/actions/docker-build/action.yml)
- [Ansible deploy](.github/actions/ansible-deploy/actions.yml)
- [TF basic](.github/actions/tf-basic/action.yml)
- [Trivy scan](.github/actions/trivy-scan/action.yml)

## How to use the actions

### TF validate actions

```yaml

name: TF validate CI
on: [push]
jobs:
  build-and-publish:
    runs-on: ubuntu-latest

    permissions:
      id-token: write
      contents: write

    steps:
      - uses: actions/checkout@v3


      - name: Run TF validate
        uses: moabukar/actions-templates/terraform-validate@main
        # with:
        #   input1:
        #   input2:


```


### Docker publish action

```yaml

name: Docker Publish Workflow
on:
  push:
    branches:
      - branch # Customize this to your main branch

jobs:
  publish:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout Repository
        uses: actions/checkout@v3

      - name: Publish Docker Image
        uses: moabukar/actions-templates/docker-publish@main
        with:
          ECR_REPOSITORY_NAME: <Your ECR Repository Name>
          BASE_BRANCH: main # Customize this to your base branch
          SHA_TO_CHECKOUT: ${{ github.sha }}
          IMAGE_TAG_PREFIX: v1.0. # Customize the image tag prefix
          DOCKER_FILE_PATH: ./path/to/Dockerfile # Customize the Dockerfile path
          REPOSITORY_NAME: your-repo-name # Customize your repository name

```


### Markdown lint


```yaml

name: Markdown Lint Workflow
on:
  push:
    branches:
      - main  # Customize this to the branch you want to trigger the action on

jobs:
  markdown-lint:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout Repository
        uses: actions/checkout@v2  # You can use any version of checkout action

      - name: Use markdown-lint action from moabukar/actions-templates
        uses: moabukar/actions-templates/markdown-lint@main
        with:
          target-repo: ${{ github.repository }}

```
