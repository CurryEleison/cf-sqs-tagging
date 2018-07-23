# Tagging AWS SQS queues with CloudFormation

AWS SQS queues now support tagging, but the CloudFormation resource for SQS queues doesn't seem to let you set the tags. This is a workaround if you really want to be able to do this.

This repo includes two stacks:
- `sqs-tagger.yaml` sets up a lambda to handle the actual tagging and untagging of queues
- `demoqueue.yaml` demonstrates how to use the custom resource

## Using it
1. Let's assume you have a CloudFormation stack "MyStack". The stack contains an SQS queue resource, which you want to adorn with tags
1. Start by creating a CloudFormation stack from `sqs-tagger.yaml`
1. Now add a custom tag to MyStack. It needs to define `ServiceToken` which points at the lambda from `sqs-tagger.yaml`, a `QueueUrl` pointing at the Url of your queue and of course the tags.

At present this solution will only apply the tags defined in the custom resource (i.e. it will ignore tags defined at the stack level,) and it will delete tags you have applied manually. Log an issue if you think you'd like to see that changed.
