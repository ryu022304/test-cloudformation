# TEST-CLOUDFORMATION

## Orverview
Start Apache server on AWS EC2 instance using CloudFormation.

## Requirement
- Rain v1.2.0
- AWS CLI v2.1.19

## Usage
### Deploy
1. `git clone this repository` and `cd /path/to/repository`
2. Install [rain](https://github.com/aws-cloudformation/rain)
3. `rain deploy network.yaml`
4. Input your IP address and keyname
5. `rain deploy frontend.yaml`

```
$ rain deploy network.yaml
Enter a value for parameter 'MyIp' "own IP adrress" (default value: 0.0.0.0): x.x.x.x
CloudFormation will make the following changes:
Stack network:
  + AWS::EC2::SecurityGroup TestHTTPSecurityGroup
  + AWS::EC2::InternetGateway TestInternetGateway
  + AWS::EC2::RouteTable TestRouteTable
  + AWS::EC2::Route TestRoute
  + AWS::EC2::SecurityGroup TestSSHSecurityGroup
  + AWS::EC2::SubnetRouteTableAssociation TestSubnetRouteTableAssociation
  + AWS::EC2::Subnet TestSubnet
  + AWS::EC2::VPCGatewayAttachment TestVPCGatewayAttachment
  + AWS::EC2::VPC TestVPC
Do you wish to continue? (Y/n) Y
Deploying template 'network.yaml' as stack 'network' in ap-northeast-1.
Stack network: CREATE_COMPLETE
  Outputs:
    TestSSHSecurityGroupId: sg-xxxxxxxxxxxxxx # exported as network-TestSSHSecurityGroupId
    TestSubnetId: subnet-xxxxxxxxxxxxxx # exported as network-TestSubnetId
    TestHTTPSecurityGroupId: sg-xxxxxxxxxxxxxx # exported as network-TestHTTPSecurityGroupId
Successfully deployed network

$ rain deploy frontend.yaml
Enter a value for parameter 'MyKey' "public key for ssh access to EC2 instance" (default value: test-key): 
Enter a value for parameter 'NetworkStackName' (default value: network): 
CloudFormation will make the following changes:
Stack frontend:
  + AWS::EC2::Instance TestInstance
Do you wish to continue? (Y/n) 
Deploying template 'frontend.yaml' as stack 'frontend' in ap-northeast-1.
Stack frontend: CREATE_COMPLETE
  Outputs:
    InstancePublicIp: y.y.y.y
Successfully deployed frontend

$ ssh -i /path/to/test-key.txt ec2-user@y.y.y.y
Warning: Permanently added 'y.y.y.y' (ECDSA) to the list of known hosts.

       __|  __|_  )
       _|  (     /   Amazon Linux 2 AMI
      ___|\___|___|

https://aws.amazon.com/amazon-linux-2/
[ec2-user@ip-10-0-1-z ~]$ sudo systemctl status httpd
● httpd.service - The Apache HTTP Server
   Loaded: loaded (/usr/lib/systemd/system/httpd.service; enabled; vendor preset: disabled)
   Active: active (running)
~~~
```

### Destroy
1. `rain rm frontend`
2. `rain rm network`

```
$ rain rm frontend
Stack frontend: CREATE_COMPLETE
Are you sure you want to delete this stack? (y/N) y
Successfully deleted stack 'frontend'

$ rain rm network
Stack network: CREATE_COMPLETE
Are you sure you want to delete this stack? (y/N) y
Successfully deleted stack 'network'

```
