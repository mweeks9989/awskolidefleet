# Kolide Fleet on AWS Fargate

## Usage
1. Bring your own aws account, supply creds via your method of choice
2. Initialize ECS to create the proper iam ecs role
3. Build and upload Docker image to ECR, put arn in variables.tf under ecs.
4. Bring your own public r53 zone, put the zone id and fqdn in variables.tf under alb.
5. Bring your own ACM cert fleet.<yourdnszone.fqdn> for your public r53 zone, put cert arn in variables.tf under alb.
6. Self-signed cert chain provided in pem format for app.fleet.priv provided by ca.fleet.priv. Certs exist in docker and cert dirs, better method inc.
7. Setup your own S3/Dynamo DB backend. Not required, but strongly suggested.  This is not fun to manually destroy if you lose your state.
8. Once build, SSH to instance described in the Output info.
9. Create /etc/osquery/enroll with the enroll_secret found in Fleet console and /etc/osquery/kolide.pem using the kolide.cert from the project or download it from Fleet app. Run systemctl restart osqueryd.
10. I'm a noob and this is a only a proof of concept.
11. ???????
12. Get rich or die tryin.

## Infrastructure
1. Multi-AZ capable via az_count variable, public / private subnets and routes with NAT/IGW support.
2. External ALB with verifiable ACM cert and internal ALB with self-signed cert chain (this works somehow!!??).
2. Aurora RDS cluster with multi-az support.
3. Redis Elasticache cluster with multi-az for node groups with relicas.
4. ECS Fargate cluster with multi-az support running Fleet containers.
5. Instance to test connectivity.  
6. Create canned queries in app and have fun.

## License
1. Steal whatever you want and take all the credit (doesn't align well with step #12 above).