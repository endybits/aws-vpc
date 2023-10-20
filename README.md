# aws-vpc
A jorney by AWS Networking VPC


Imagine that you are a  Colud Engineer at Cloud-bits company. You have be asked by your company to configure and deploy a new Application, with a fault-tolerance design, highly availabe, reliabile and scalable.
After you met with the dev-team and undestand that the new app was desiged and developed as a multi-tier architecture, you decide deploying the app in a single **Amazon VPC** and replicate it through multiple subnets configured across multiple Availability Zones

![NewApp-Architecture drawio](https://github.com/endybits/aws-vpc/assets/22806426/891f3e8c-a220-469a-8e8e-0e3512986268)


Stage 1.

### Step 1. Create VPC

![image](https://github.com/endybits/aws-vpc/assets/22806426/0144f03d-2b49-45cc-be85-04a14f6852ca)

![image](https://github.com/endybits/aws-vpc/assets/22806426/2b480ac6-66ce-4aaa-9637-c35d19e72570)

![image](https://github.com/endybits/aws-vpc/assets/22806426/169b4d41-9421-40ed-aae7-bbf4ea12fea8)


### Step 2. Create subnets

![image](https://github.com/endybits/aws-vpc/assets/22806426/d116a52b-56db-4263-93d6-e0660f02d8c3)

![image](https://github.com/endybits/aws-vpc/assets/22806426/0e6bf59b-e723-479f-b4b3-94cc96a5ea88)

![image](https://github.com/endybits/aws-vpc/assets/22806426/67601539-c23b-4e1a-a761-62da2dcece31)

![image](https://github.com/endybits/aws-vpc/assets/22806426/87139ad6-8072-4e73-bd96-b527f3259d54)

![image](https://github.com/endybits/aws-vpc/assets/22806426/80e9be51-6278-4854-ac4e-7c0c98febcd0)

![image](https://github.com/endybits/aws-vpc/assets/22806426/e6ad2dea-0a7f-44ca-8322-3bcad63ad7c5)


### Step 3. Create a Internet Gateway

![image](https://github.com/endybits/aws-vpc/assets/22806426/230747bb-9fe1-406e-b57e-f56d2b6ac476)

### Step 3a. Attach IGW to VPC

![image](https://github.com/endybits/aws-vpc/assets/22806426/02e32896-c866-4d64-80ab-38bb03070beb)

Select our VPC

![image](https://github.com/endybits/aws-vpc/assets/22806426/ec5b9a47-2be0-4a28-8606-841e3b213e46)

Now the status changed

 ![image](https://github.com/endybits/aws-vpc/assets/22806426/c4d5aa6d-8578-4a1a-8549-de598ca5cf93)


### Step 4. Create Route Table for Public subnets

![image](https://github.com/endybits/aws-vpc/assets/22806426/e2bc9fed-ce36-43a0-803e-a25776dfe0c6)

#### Step 4a. Edit route
![image](https://github.com/endybits/aws-vpc/assets/22806426/fc10f6ba-2841-45e2-be0b-768b6b806c26)

#### Step 4b. Add a Route for IGW access. 

![image](https://github.com/endybits/aws-vpc/assets/22806426/7be946fc-0239-4972-ba7c-3c4b102c350d)

Notice the IP Address `0.0.0.0/0` means all traffic, any IP can access. Select the IGW and save changes


![image](https://github.com/endybits/aws-vpc/assets/22806426/21337ef8-1bfd-465a-903c-1c6ebeea77d9)

#### Step 4c. Public Subnet Associations

![image](https://github.com/endybits/aws-vpc/assets/22806426/d2e7cc96-f815-4b64-bb95-d640658d165b)

![image](https://github.com/endybits/aws-vpc/assets/22806426/c9f7a491-a851-484c-bf79-15a6ca2911d6)


### Step 5. Create Route Table for Private subnets

![image](https://github.com/endybits/aws-vpc/assets/22806426/457830fe-a12d-4153-9122-19acec3fffdd)

#### Step 5a. Private Subnet Associations
Unlike Step 4c, you must to associate the private subnets.
Furthermore, as this rout table is for internal traffic in the associated subnets, you don't need to edit the Route table for IGW access.

![image](https://github.com/endybits/aws-vpc/assets/22806426/8155306e-bed3-46d2-a468-f2325129388e)


### Step 6. Lauch an Instance in the Public Subnet

![image](https://github.com/endybits/aws-vpc/assets/22806426/3b14c588-15d5-4e05-88e1-c455765fdeb0)


#### 6b. Define a key-pair login and copy in an accessible folder for you.

![image](https://github.com/endybits/aws-vpc/assets/22806426/0ebae752-37ad-4712-9b1e-077efb68849d)


#### 6c. Edit networking settings: 
- Select your custom VPC, your public subnet and enable Auto-assign public IP (to make the instance reachable throught the internet. 

![image](https://github.com/endybits/aws-vpc/assets/22806426/b000a7e0-5ea6-4e61-9970-39c7187931c2)

Wait until the Instance status is Runnung, then  

![image](https://github.com/endybits/aws-vpc/assets/22806426/a2d01589-20d0-4c7d-a01c-2e75c915d089)


![image](https://github.com/endybits/aws-vpc/assets/22806426/ec23d150-7a86-4789-a2e3-f6eba3f2f380)

Click over Connect button

![image](https://github.com/endybits/aws-vpc/assets/22806426/2b1c23ec-726a-4dc7-aa97-f7de76e6a098)

use your .pem file to connect via ssh. In my case I first copied the file in my `.ssh` folder ans used this command `ssh -i "~/.ssh/first-ec2-key-pair.pem" ec2-user@13.211.227.21`

![image](https://github.com/endybits/aws-vpc/assets/22806426/a0706556-617f-40bd-a74a-df10bb75d179)
