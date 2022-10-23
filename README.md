# cleanup-cloud-resources
In order to clean up the resources after testing, We can use cloud-nuke -> https://github.com/gruntwork-io/cloud-nuke.
I am using cloud nuke to clean up the resources I created using terrafom (forgot to run terraform destroy) or manually for testing and development work.
This will make sure that I wont have to incurr any unwanted expenses in Cloud. 

Install cloud-nuke is very straight forward:

`brew install cloud-nuke`

Before running cloud-nuke, need to setup AWS credentials using aws cli.

```
aws configure
AWS Access Key ID:
AWS Secret Access Key:
Default region name:
Default output format:
```
The user/role should have the permissions to delete the resources in AWS.

We can see the resources can be deleted by cloud nuke using following command:

```shell
cloud-nuke aws --list-resource-types
```

finally I am setting cron to clean up the resources automatically everyday at 11.26 pm on AWS.

```shell
26 11 * * * ./cleanup-aws-resources.sh
```

cloud nuke also support excluding region/resource type so that cloud-nuke will not delete those resources.
I am exluding us-east-1 region and AWS resource type IAM, as I dont want them to be deleted.
