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
### Local Environment Setup
These steps grant the correct excution of the workflow:
1. Create an admin user. Go to IAM --> `<username>` with an attached Administration Policy.
2. Create the access with Key/Secret pair, and store the credentials.
3. Configure your local CLI with the command: `aws configure`. It will require to provide:
- AWS User Id
- AWS User Id Secret Key
- AWS Region
- AWS output format

Use the feature of the admin user, to configure the connection to AWS.

To verify if everthing is working correctly, configure the connection to the EKS cluster:
`aws eks --region <region> update-kubeconfig --name <cluster_name>`

Once this is in place, you can launch `kubectl get svc` or `kubectl get nodes` to check if you can reach the AWS cluster.

### Launch the Terraform configuration
From the terraform folder, launch `terraform init` and `terraform apply`.

This will create all the resources, including the `github-action-user`, with the default policies.


### Set the GITHUB remote user
We want to set the `github-action-user` to properly allow GitHub to talk and executes CI/CD towards AWS.

To do so, we need to:
1. Launch `chmod +x init.sh` and right after `.\init.sh` with aws configured with the admin user.
2. The previous command will grant the `github-action-user` to talk with EKS through an external platform.
3. Go to IAM and create an Access Key for the `github-action-user`. Store the Key and Secret Key.
4. Test locally if you can reach the cluster:
- launch again `aws configure` and update the key and secret, with the new one of the `github-action-user`
- launch again `kubectl get svc` or `kubectl get nodes` to verify if you are still reaching the cluster.

## Useful AWS CLI commands:
### Interaction with IAM
- LIST ATTACHED POLICIES: `aws iam list-attached-user-policies --user-name github-user-action`
- LIST INLINE POLICIES: `aws iam list-user-policies --user-name github-user-action`
- DELETE INLINE POLICY: `aws iam delete-user-policy --user-name github-action-user --policy-name <PolicyName>`
- DELETE USER: `aws iam delete-user --user-name github-action-user`
. LIST ACCESS KEY: `aws iam list-access-keys --user-name github-action-user`
- DELETE ACCESS KEY: `aws iam delete-access-key --user-name github-action-user --access-key-id <AccessKeyId>`