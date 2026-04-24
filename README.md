# database-backup-s3-bucket

1. Create S3 bucket in mumbai region
2. Create Ec2 instance and install docker & minikube 
3. Open port in security group 80, 30007,3306
4. Create RDS database with mysql and provide proper username, password, DB_name & Enpoints
5. database security group enable port 3306

# App image 
image name:- philippaul/node-mysql-app:02

# Access application
minikube service node-mysql-service

# Test connectivity from pod

kubectl exec -it <pod-name> -- sh

apk add mysql-client
mysql -h database-1.c9w824yaifoc.ap-south-1.rds.amazonaws.com -u admin -p

Finally check s3 bucket backup is received or not as per the cronJob?


=========================================================================================================
IRSA:- 
Same thing we can test through EKS cluster 
1. First OIDC need to enable 
2. Create policy with minimum permission of particular that s3 bucket 

{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": ["s3:PutObject", "s3:ListBucket"],
      "Resource": [
        "arn:aws:s3:::rahul-rds-backup-bucket",
        "arn:aws:s3:::rahul-rds-backup-bucket/*"
      ]
    }
  ]
}

3. Create the IAM role  and attach this policy 
4. Create service account in EKS cluster and provide IAM role arn in service account yaml file
5. remaining process is the same only , RDS backup will store in s3 bucket as per the cronJob.

