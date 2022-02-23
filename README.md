# AWS SSM State Manger with Ansible Playbooks

Demo shows how AWS SSM State Manager Associate `AWS-ApplyAnsiblePlaybooks` can be run from S3 or a GitHub repository. Two playbooks are leveraged with `s3-local.yml` and `github-local.yml` to demonstrate how they can be used directly from Github.com or from an S3 bucket.

## Project Structure and Deployment

The project contains both the Ansible playbook and the CloudFormation templates to deploy the SSM State Manager Associations. Within the `./ansible` directory you will find two playbook files which leverage different roles. Edit the `s3-local.yml` or the `github-local.yml` by adding new roles to the `./ansible/roles/` directory and updating the playbook files.

Within the `./cloudformation` directory are the templates to be deployed. Start by deploy the [cloudformation/ansible-playbook-s3-bucket.yml](cloudformation/ansible-playbook-s3-bucket.yml) in to an AWS account which you want to centrally locate your Ansible Playbooks. The template will ask for the AWS Organization ID which will allow all EC2s the ability to list and download the necessary playbook directories.

After deployment of [cloudformation/ansible-playbook-s3-bucket.yml](cloudformation/ansible-playbook-s3-bucket.yml), you can setup a pipeline to deliver the Ansible Playbooks. The current project uses GitHub Actions and GitHub Action Secrets to deliver all contents of the `./ansible` directory to the S3 Bucket. For the purpose of testing, there are two GitHub workflows: one for delivering to a /test/ prefix and one delivering to a /production/ prefix. The two prefixes can be used to test your Ansible Playbooks without impacting production workloads.



## Resources

* [Walkthrough: Creating associations that run Ansible playbooks](https://docs.aws.amazon.com/systems-manager/latest/userguide/systems-manager-state-manager-ansible.html)
* [CloudFormation - AWS::SSM::Association](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-ssm-association.html#cfn-ssm-association-instanceid)