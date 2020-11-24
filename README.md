# awesome-aws-lifecycle-hooks

## Hooks

### ECS

* [getsocial-rnd/ecs-drain-lambda](https://github.com/getsocial-rnd/ecs-drain-lambda)
* [aws-samples/aws-lambda-lifecycle-hooks-function](https://github.com/aws-samples/aws-lambda-lifecycle-hooks-function)
* [claranet/terraform-aws-ecs-container-instances](https://github.com/claranet/terraform-aws-ecs-container-instances)

### EKS

* [aws-samples/amazon-k8s-node-drainer](https://github.com/aws-samples/amazon-k8s-node-drainer)
* [keikoproj/lifecycle-manager](https://github.com/keikoproj/lifecycle-manager)

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
  --lifecycle-hook-name $LIFECYCLE_HOOK_NAME
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

## Misc

* https://docs.aws.amazon.com/autoscaling/ec2/userguide/lifecycle-hooks.html
* https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/autoscaling_lifecycle_hook
