# Create NAT Gateway
- NAT gateway enables instances in a private subnet can connect to services outside the VPC but external services cannot initiate a connection with those instances.
- NAT gateway will be created in a public subnet and must associate an elastic IP address with the NAT gateway at creation.
- Traffic from the NAT gateway will be routed to the internet gateway for the VPC.


Name: my-3-tier-NGW

![Screenshot 2023-08-29 at 11 36 34 PM](https://github.com/Sulemoore/AWS-Projects/assets/101164153/9319f5bc-4fb3-406a-9fa9-e6eb8ab55bf4)

- Edit route 
