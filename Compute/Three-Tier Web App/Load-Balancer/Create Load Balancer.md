### Create an Application Loadbalancer

- Name: 'my-3-tier-ALB`
- Create in 3 AZ's
- 
![Screenshot 2023-09-02 at 11 03 11 PM](https://github.com/Sulemoore/AWS-Projects/assets/101164153/d7d66b1c-600d-47e6-bf17-37712570924d)

### Create Security group

- Allow inbound rule on Port 80 with source 0.0.0.0/0
- Link App SG to Loadbalancer SG


![Screenshot 2023-09-02 at 11 02 49 PM](https://github.com/Sulemoore/AWS-Projects/assets/101164153/9bb948bc-fda5-428c-9ad3-9af913f68802)

### Create Target Group
- Your Targets are the 2 App Servers

![Screenshot 2023-09-01 at 1 16 02 AM](https://github.com/Sulemoore/AWS-Projects/assets/101164153/6f46186d-acb6-4d3d-91ce-8803a8085b64)
