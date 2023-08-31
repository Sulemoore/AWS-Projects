# Create 9 Subnets for the tiers📌

### Create 3 Subnets for Web tier

```
Name: Web-public-subnet-1
AZ:   us-east-1a
CIDR: 10.0.1.0/24

Name: Web-public-subnet-2
AZ:   us-east-1b
CIDR: 10.0.2.0/24

Name: Web-public-subnet-3
AZ:   us-east-1c
CIDR: 10.0.3.0/24
```
- Enable Auto Assign Public IPV4 Address for Public Subnets
  
![Screenshot 2023-08-29 at 11 20 49 PM](https://github.com/Sulemoore/AWS-Projects/assets/101164153/5086c92b-3f4a-49cd-a324-c64b6d417724)


### Create 3 Subnets for App tier

```
Name: App-private-subnet-1
AZ:   us-east-1a
CIDR: 10.0.4.0/24

Name: App-private-subnet-2
AZ:   us-east-1b
CIDR: 10.0.5.0/24

Name: App-private-subnet-3
AZ:   us-east-1c
CIDR: 10.0.6.0/24
```
![Screenshot 2023-08-29 at 11 21 10 PM](https://github.com/Sulemoore/AWS-Projects/assets/101164153/f50258d9-41d2-4fda-b66e-fa9a8c9c93a0)

### Create 3 Subnets for Db tier

```
Name: db-private-subnet-1
AZ:   us-east-1a
CIDR: 10.0.7.0/24

Name: db-private-subnet-2
AZ:   us-east-1b
CIDR: 10.0.8.0/24

Name: db-private-subnet-3
AZ:   us-east-1c
CIDR: 10.0.9.0/24
```
![Screenshot 2023-08-29 at 11 21 24 PM](https://github.com/Sulemoore/AWS-Projects/assets/101164153/47889dcc-aed6-4b59-92b3-c497fcda44ae)
