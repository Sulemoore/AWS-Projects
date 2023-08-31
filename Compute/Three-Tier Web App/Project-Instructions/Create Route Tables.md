# Create Routes for all layers

### Create Web Route Table
- Name: Web-public-RT
```
1. Associate with all 3 Web subnets
2. Add route to Internet gateway
```

![Screenshot 2023-08-29 at 11 27 17 PM](https://github.com/Sulemoore/AWS-Projects/assets/101164153/ad19a700-d990-4045-9509-42457dea9c39)

### Create App Route Table
- Name: App-private-RT
```
1. Associate with all 3 App subnets
2. Add route to NAT Gateway
```


### Create Db Route Table
- Name: db-private-RT
```
1. Associate with all 3 DB subnets
2. Add route to NAT Gateway
```
