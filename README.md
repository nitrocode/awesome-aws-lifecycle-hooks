# awesome-aws-lifecycle-hooks

I was learning about lifecycle hooks recently. Before I added my own, I thought I'd do some research in the lifecycle hooks available. I was hoping to find a simple terraform module lambda for ECS. After some searching, I curated this list and thought "Why not another awesome list?" And the list was born.

Feel free to contribute.

## Hooks

### ECS

* [aws-samples/ecs-cid-sample](https://github.com/aws-samples/ecs-cid-sample) - Drain using cloudwatch event, sns, and python lambda. Deploy with cloudformation.
* [getsocial-rnd/ecs-drain-lambda](https://github.com/getsocial-rnd/ecs-drain-lambda) - Drain using cloudwatch event and golang lambda. Deploy with sls.
* [terraform-community-modules/tf_aws_ecs_instance_draining_on_scale_in](https://github.com/terraform-community-modules/tf_aws_ecs_instance_draining_on_scale_in)
* [ktruckenmiller/aws-ecs-spot-instance-drainer](https://github.com/ktruckenmiller/aws-ecs-spot-instance-drainer)
* [blinkist/terraform-aws-airship-ecs-instance-draining](https://github.com/blinkist/terraform-aws-airship-ecs-instance-draining) - Drain using cloudwatch event, sns, and python lambda. Deploy lambda with terraform.
* [btisdall/ecs-cid](https://github.com/btisdall/ecs-cid)
* [docker-production-aws/lambda-lifecycle-hooks](https://github.com/docker-production-aws/lambda-lifecycle-hooks/tree/final)
* [ericdahl/tf-ecs](https://github.com/ericdahl/tf-ecs) - Drain using cloudwatch event, sns, and python lambda. Deploy with terraform.
* [claranet/terraform-aws-ecs-container-instances](https://github.com/claranet/terraform-aws-ecs-container-instances) - Drain using cloudwatch event, sqs, and python lambda. Deploy with terraform.

### EKS

* [aws-samples/amazon-k8s-node-drainer](https://github.com/aws-samples/amazon-k8s-node-drainer)
* [keikoproj/lifecycle-manager](https://github.com/keikoproj/lifecycle-manager)

### Backup

* [aws-samples/aws-lambda-lifecycle-hooks-function](https://github.com/aws-samples/aws-lambda-lifecycle-hooks-function) - backup data to s3 using sns and lambda

## Invocation conditions

| Condition                       | Invoked? |
| ------------------------------- | -------- |
| Spot interruption               | Yes |
| EC2 instance degradation        | Yes |
| ASG instance refresh            | Yes |
| ASG max instance lifetime       | Yes |
| [EC2 manual termination from CLI](https://docs.aws.amazon.com/cli/latest/reference/autoscaling/terminate-instance-in-auto-scaling-group.html) | Yes |
| EC2 manual termination from UI  | No |

## Testing

```bash
# set variables
INSTANCE_ID=i-aaaabbbbcccc
ASG_NAME=asg-xyz
LIFECYCLE_HOOK_NAME=lifecycle-xyz

# terminate a specific instance id
aws autoscaling \
  terminate-instance-in-auto-scaling-group \
  --should-decrement-desired-capacity \
  --instance-id $INSTANCE_ID

# once the instance is in a Terminating:Wait stage, continue the lifecycle
aws autoscaling \
  complete-lifecycle-action \
  --lifecycle-action-result CONTINUE \
  --lifecycle-hook-name $LIFECYCLE_HOOK_NAME \
  --auto-scaling-group-name $ASG_NAME \
  --instance-id $INSTANCE_ID
```

References
* [ How do I delay Auto Scaling termination of unhealthy Amazon EC2 instances so I can troubleshoot them?](https://aws.amazon.com/premiumsupport/knowledge-center/auto-scaling-delay-termination/)
* [aws autosclaing terminate-instance-in-auto-scaling-group](https://docs.aws.amazon.com/cli/latest/reference/autoscaling/terminate-instance-in-auto-scaling-group.html)
* [aws autosclaing complete-lifecycle-action](https://docs.aws.amazon.com/cli/latest/reference/autoscaling/complete-lifecycle-action.html)

## Blogs

* 03 Sep 2020 - [Graceful shutdown using AWS Auto Scaling groups and Terraform](https://circleci.com/blog/graceful-shutdown-using-aws/)
* 04 Oct 2019 - [Autoscaling like a pro: how to use EC2 Auto Scaling Lifecycle Hooks, the right way.](https://medium.com/proud2becloud/autoscaling-like-a-pro-how-to-use-ec2-auto-scaling-lifecycle-hooks-the-right-way-da7ef4448a03)
* 22 Sep 2019 - [Scale down a Kube Cluster Minion without Downtime using AWS Autoscaling Lifecycle Hook — Part III](https://www.powerupcloud.com/bscale-down-a-kube-cluster-minion-without-downtime-using-aws-autoscaling-lifecycle-hook-part-3/)
* 24 Sep 2018 - [AWS Auto Scaling Group: Working With Lifecycle Hooks](https://dzone.com/articles/aws-auto-scaling-group-working-with-lifecycle-hook)
* 05 Jun 2018 - [Amazon EC2 Auto Scaling lifecycle hooks to Export Instance Logs After Marked For Terminate](https://blog.fourninecloud.com/auto-scaling-lifecycle-hooks-to-export-server-logs-when-instance-terminating-58e06d7c0d6a)
* 16 May 2018 - [AWS Auto Scaling Lifecycle](https://jayendrapatil.com/aws-auto-scaling-lifecycle/)
* 25 Jan 2017 - [How to Automate Container Instance Draining in Amazon ECS](https://aws.amazon.com/blogs/compute/how-to-automate-container-instance-draining-in-amazon-ecs/)
* 04 Nov 2015 - [Under the Hood: AWS CodeDeploy and Auto Scaling Integration](https://aws.amazon.com/blogs/devops/under-the-hood-aws-codedeploy-and-auto-scaling-integration/)
* 20 Jan 2015 - [Deep Dive Into Auto Scaling Lifecycle Hooks](https://www.rightbrainnetworks.com/2015/01/20/deep-dive-into-auto-scaling-lifecycle-hooks/)

## Misc

* https://docs.aws.amazon.com/autoscaling/ec2/userguide/lifecycle-hooks.html
* https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/autoscaling_lifecycle_hook
