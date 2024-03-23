# Movie Picture

This is the Movie Picture project part of the Udacity Cloud DevOps Engineer Course
The base of this project is provided by Udacity.
On top of that, my code enriches it, in order to meet the project exam.

## Continuous Integration:
### Front-End
- You need to create a folder .github/workflows to contain the CI .yml workflow.
- In the end you should have something like '/repo/.github/workflows/frontend-ci.yml'
- The version of the node to use, is specified in the .nvmrc (node version manager)

## Continuous Integration
### Back-End
Create the two flows:
1. backend-ci.yml
2. frontend-ci.yml

The command `actions/checkout@` is important to initialize the repository. If you don't put it, it doesn't find you directory.

## Continuous Deployment

1. You need to create a user. Go to IAM --> 'piero-cicd'

### Terraform commands
- `terraform init`
- `terraform plan`
- `terraform apply`
- `terraform destroy`