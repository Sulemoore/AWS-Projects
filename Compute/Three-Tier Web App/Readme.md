# 📌 Build a Three-Tier Web App on AWS
## 🎬 Architecture

## Step-01: Introduction

Three-Tier Architecture is the most common architecture in a multitier design where your product functions are divided into multiple layers so that each layer can be implemented and scaled independently.

With multitier architecture;
- 👉 It is easy to adopt new technologies without interrupting other layers.
- 👉 It provides flexibility
- 👉 For security, you can isolated each layer from the other and provide only required access.
- 👉 Application troubleshooting and management become manageable.

The three main layers are:
- 👉 Web Layer (Presentation Tier)
- 👉 Application Layer (Logic Tier)
- 👉 Database Layer (Data Tier)

Let's take a look at these layers in more detail.

### 👨🏾‍💻 The Web Layer

Also known as the presentation tier provides a user interface that helps the end user to interact with the application. This is the user-facing layer where users see and interact with. It collects information from users and pass them to the application layer for processing.

### 🏗️ The Application Layer

This is where the business logic resides hence also called the logic tier. The presentation tier gathers information or queries from users and passes them to the logic tier for processing. When the process is complete, the logic tier sends the response back to the presentation tier for user consumption.

### 💾 The Database Layer

This layer is also called the data tier. This tier stores all the information related to user profile and transactions.

### Prerequisites

This tutorial assumes that you have a basic understanding of Cloud Computing on AWS and basic Linux commands.

For this tutorial, you will need:
- 👉 An AWS account
- 👉 Download and install AWS CLI

  
## Step-02:Create the Web Layer

### Steps

- 👉 [Create custom VPC](https://github.com/Sulemoore/AWS-Projects/blob/master/Compute/Three-Tier%20Web%20App/Project-Instructions/Create%20VPC.md)
- 👉 [Create subnets](https://github.com/Sulemoore/AWS-Projects/blob/master/Compute/Three-Tier%20Web%20App/Project-Instructions/Create%20Subnets.md)
- 👉 [Create Route Tables (1 for each layer)](https://github.com/Sulemoore/AWS-Projects/blob/master/Compute/Three-Tier%20Web%20App/Project-Instructions/Create%20Route%20Tables.md)
- 👉 [Create Internet gateway](https://github.com/Sulemoore/AWS-Projects/blob/master/Compute/Three-Tier%20Web%20App/Project-Instructions/Create%20Internet%20Gateway.md)
- 👉 [Create NAT gateway](https://github.com/Sulemoore/AWS-Projects/blob/master/Compute/Three-Tier%20Web%20App/Project-Instructions/Create%20NAT%20Gateway.md)

## Step-03:Create the Application Layer
- 👉 [Create 3 EC2 Instances](https://github.com/Sulemoore/AWS-Projects/blob/master/Compute/Three-Tier%20Web%20App/Create-Servers/Bastion%20Host.md)
- 1 Jump Server/Bastion Host (in Web subnet 1)
- 2 php servers (in App subnets 2&3)
- 👉 Create Keypair
- 👉 [Create Application Loadbalancer](https://github.com/Sulemoore/AWS-Projects/blob/master/Compute/Three-Tier%20Web%20App/Load-Balancer/Create%20Load%20Balancer.md)

## Step-04:[Create the Database Layer](https://github.com/Sulemoore/AWS-Projects/blob/master/Compute/Three-Tier%20Web%20App/RDS-Database/Create%20DB.md)

- 👉 Create Subnet Group
- 👉 Create Database
- 👉Create Security Group




