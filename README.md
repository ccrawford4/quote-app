# quote-app
This repoisotry contains the configuration files necessary to deploy a simple quote application on AWS Elastic Kubernetes Service (EKS) using an AWS Elastic Load Balancer (ELB) with 3 replica servers. Each time you refresh the page, the application generates a random unique quote.

## Prerequisites

Before starting, ensure you have the following installed:
- AWS CLI
- kubectl
- eksctl
- Access to an AWS account with necessary permissions

## Configuration

Rename `.env.example` to `.env` and update it with your AWS credentials and configuration:

```
AWS_REIGON=your-aws-region
AWS_POLICY_ARN=your-aws-policy-arn
AWS_ACCESS_KEY=your-aws-access-key
AWS_SECRET_KEY=your-aws-secret-key
AWS_VPC_ID=your-aws-vpc-id
AWS_ACCOUNT_NUMBER=your-aws-account-number
```

## Steps to Deploy

1. **Create an EKS Cluster**:
   Use `eksctl` to create an EKS cluster. Example command:
   ``` 
   eksctl create cluster --name your-cluster-name --region your-region
   ```

2. **Set up IAM**:
Use AWS IAM to create policies and user groups for controlling access to the AWS account.

3. **Tag VPC Subnets**:
Tag the VPC subnets appropriately for the ELB (public subnets with `kubernetes.io/role/elb` and private subnets with `kubernetes.io/role/internal-elb`).

4. **Install Cert-Manager and AWS Load Balancer Controller**:
Deploy cert-manager and the AWS Load Balancer Controller in your EKS cluster to manage certificates and load balancers.

5. **Deploy Applications using Ingress**:
Deploy your applications to the EKS cluster using Ingress objects to communicate with AWS ELBs.

6. **Access the Application**:
Once deployed, access the quote application using the ELB's DNS name provided in the Ingress configuration.

## Application Architecture

The quote application is deployed on AWS EKS with 3 replicas for high availability. It uses an AWS Elastic Load Balancer to distribute traffic across these replicas. Each time you refresh the page, a random unique quote is generated.

## Credits

This project was inspired by and based on the LinkedIn Learning Course "Running Kubernetes on AWS" by Kim Schlesinger. Special thanks to Kim Schlesinger and LinkedIn Learning for providing comprehensive and valuable insights into deploying applications on AWS using Kubernetes.

For more detailed information and advanced topics on running Kubernetes on AWS, consider enrolling in the course on [LinkedIn Learning](https://www.linkedin.com/learning/running-kubernetes-on-aws-eks-22163437/operating-kubernetes-clusters-on-aws?u=2204681).

---

**Note**: This project is an implementation example and may have been adapted or modified from the original course material.




