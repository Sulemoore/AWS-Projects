# Create a Bastion Host/Jump Server in Public Subnet

- Name: `my-3-Tier-Bastion`
- Create Security group for Bastion host.
- Allow SSH from 0.0.0.0/0

![Screenshot 2023-08-31 at 10 04 44 PM](https://github.com/Sulemoore/AWS-Projects/assets/101164153/d61390f6-773e-44ce-9014-46f7bf807abb)

## Create 2 more servers in Private Subnets.
- Create Security group for App Server (Use 1 SG for both Servers).
- Allow SSH from Bastion Host SG.
  
![Screenshot 2023-08-31 at 10 15 20 PM](https://github.com/Sulemoore/AWS-Projects/assets/101164153/acd8d53e-177c-4afe-a03a-eaa28885ceff)

## Connect to Bastion Host using Terminal
- Navigate to your Keypair directory

- Change Permision for Keypair
```
chmod 400 Keypairname.pem
```
- SSH into Bastion host

```
ssh -i Keypair.pem ec2-user@IP Adress
```
## From Bastion host, Connect to App Server 1.

- Add Keypair to file
- Copy Keypair Metadata and then

```
vi Keypair
```

- Paste the keypair *make sure to delete the trailing %*

- Change Permision for Keypair
```
chmod 400 Keypairname.pem
```
- SSH into Bastion host

```
ssh -i Keypair.pem ec2-user@IP Adress-Server 1
```
## [Install Packages on Servers](
