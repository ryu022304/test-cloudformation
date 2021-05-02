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
3. `rain deploy test.yaml`
4. Input your IP address and keyname

```
$ rain deploy test.yaml                                  
Enter a value for parameter 'MyIp' "own IP adrress" (default value: 0.0.0.0/32): x.x.x.x/32
Enter a value for parameter 'MyKey' "public key for ssh access to EC2 instance" (default value: test-key): 
CloudFormation will make the following changes:
Stack test:
  + AWS::EC2::SecurityGroup TestHTTPSecurityGroup
  + AWS::EC2::Instance TestInstance
  + AWS::EC2::InternetGateway TestInternetGateway
  + AWS::EC2::RouteTable TestRouteTable
  + AWS::EC2::Route TestRoute
  + AWS::EC2::SecurityGroup TestSSHSecurityGroup
  + AWS::EC2::SubnetRouteTableAssociation TestSubnetRouteTableAssociation
  + AWS::EC2::Subnet TestSubnet
  + AWS::EC2::VPCGatewayAttachment TestVPCGatewayAttachment
  + AWS::EC2::VPC TestVPC
Do you wish to continue? (Y/n) 
Deploying template 'test.yaml' as stack 'test' in ap-northeast-1.
Stack test: CREATE_COMPLETE
  Outputs:
    InstancePublicIp: y.y.y.y
Successfully deployed test
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
`rain rm test`

```
$ rain rm test   
Stack test: CREATE_COMPLETE
Are you sure you want to delete this stack? (y/N) y
Successfully deleted stack 'test'
```
