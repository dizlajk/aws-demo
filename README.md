# AWS demo
Simple SAM application with a frontend deployed to s3 bucket.
SAM app consists of one lambda function scheduled to run every day at 10AM, also callable by API gateway. 
Frontend part is just index file that loads data stored on s3 and displays them.

## Prerequisites
- [aws cli v2](https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2.html)
- [configured aws cli](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-configure.html)
- [sam](https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/serverless-sam-cli-install.html)
- [maven](https://maven.apache.org/download.cgi)
- [java8](https://docs.aws.amazon.com/corretto/latest/corretto-8-ug/downloads-list.html)
- [ansible](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html)
- [python3 with pip](https://www.python.org/downloads/)
- [boto3](https://boto3.amazonaws.com/v1/documentation/api/latest/guide/quickstart.html#installation)

## Structure
- `LoadDataFunction` folder - simple maven project with lambda function to load data from https://openweathermap.org/current and store it in s3 bucket
- `roles` folder - stores ansible roles
- `web` folder - stores web files, currently just index.html.
- `deploy_ansible.yaml` - ansible deployment script
- `template.yaml` - Cloudformation(SAM) template

## Deployment
- run this command in project root folder:
<code>ansible-playbook deploy_ansible.yml</code>
- trigger LoadDataFunction lambda to load data (you can find the url in aws console: CloudFormation -> demo -> Outputs -> LoadDataAPI)
- open web the application (you can find the url in aws console: S3 -> demo.web.bucket -> Properties -> Static website hosting -> Endpoint)
## TODO:
- trigger lambda after deployment
- variables for buckets, endpoints...
- partial deployment (redeploy web/lambda only)
- automatically deploy all web folder
- CI / CD pipelines
