### Setup Resources into Azure.
 Create the Domain Controller VM(Window Server 2022) named DC-1.

![image](https://github.com/jghis/configure-ad/assets/132087784/b5e822c2-727a-411e-9649-754fb7960b33)

On this picture we created a Domain Controller VM(Window Server 2022) named DC-1.

![image](https://github.com/jghis/configure-ad/assets/132087784/bbe471fb-bc3a-4a24-b0a4-198eea2f52e5)

Then we gave it a username and a password.

![image](https://github.com/jghis/configure-ad/assets/132087784/0d1a3220-dfd8-4686-9a73-7bf27ba651c4)

On this picture we notice that the virtual machine is successfully deployed.


After creating the Domain Controller  set up the NIC(network interface card) private IP address from dynamic to static. This to avoid that the private IP address changes.

Select Networking then select Network configuration then IP configuration and  change the configuration from dynamic to static.

![image](https://github.com/jghis/configure-ad/assets/132087784/b6b0f704-e3e2-4254-af6b-02df2da080eb)

![image](https://github.com/jghis/configure-ad/assets/132087784/312f79be-d088-47fe-bbc6-e55d3315145c)

![image](https://github.com/jghis/configure-ad/assets/132087784/74591462-9d7c-4e92-8b17-26fdfeaa81d7)

On this picture we set up the Domain Controller  private IP address from dynamic to static to avoid it's private IP address to change.

  create the Client virtual machine VM ( Window 10) named Client-1. Make sure we use the same Resource Group and Vnet that was created for DC-1.
Make sure that both VMs are in the same Vnet(virtual network)

![image](https://github.com/jghis/configure-ad/assets/132087784/c1698ae5-154e-480d-ae94-7300b2a8045c)

Client-1 has the same Resource Group than the Domain Controller.

![image](https://github.com/jghis/configure-ad/assets/132087784/d3b69763-f6de-46da-a40c-e8c7b6204c88)

 Giving Client-1 a username and a password.

![image](https://github.com/jghis/configure-ad/assets/132087784/ca67367b-54c1-4b41-89ed-906471198f4b)

On this picture we notice that Client-1 has the same virtual Network than the Domain Controller.


After all this is done we should ensure connectivity between client-1 and the Domain Controller.
Ensure Connectivity between Client-1 and DC-1
To do so loggin into Client-1 using  Microsoft Remote desktop connection and ping DC1's private IP address with Ping -t. 

![image](https://github.com/jghis/configure-ad/assets/132087784/8601f0be-174f-4a19-8d49-ee37528f9acb)

The ping will faill because DC-1 local windows Firewall will block the ICMPv4 traffic. 

To remedy to that Loggin to the Domain Controller and enable ICMPv4 trafic on the local windows Firewall.
After enabling ICMPv4 check back to Client-1 to see the ping succeed.

![image](https://github.com/jghis/configure-ad/assets/132087784/1129610c-345c-40dc-a287-9187cd41a2e5)

 On this picture we logged in to the Domain Controller  using Microsoft Remote Desktop connection and select Window  Defender Firewall with advanced  Security.
 
![image](https://github.com/jghis/configure-ad/assets/132087784/e59ef741-8e71-4701-bd82-ffa53d08e500)
Next we seleced  Inbound Rules

![image](https://github.com/jghis/configure-ad/assets/132087784/57f877ea-aa78-471d-abb5-5cb6f54fc477)

Then we  enabled ICMPv4 trafic


![image](https://github.com/jghis/configure-ad/assets/132087784/692343d3-e2b2-4499-8915-ab11f5dbc723)

Finally when we checked back to client-1 we noticed that the ping succeeded.

### Install Active Directory

  Logging to DC-1 and install Active Directory Domain Services.
  
  ![image](https://github.com/jghis/configure-ad/assets/132087784/3a2c405b-d8da-4d6c-aee8-75a15fc4d654)

  Go to DC-1 Server Manager  select add roles and features

  ![image](https://github.com/jghis/configure-ad/assets/132087784/38467905-156f-4b05-8681-a39e08970bea)

  We want Active Directory Doamain Services to be installed on DC-1

  ![image](https://github.com/jghis/configure-ad/assets/132087784/9b804944-a985-421e-a253-dc44d8ac4c12)

  Select active Directory Domain services

  ![image](https://github.com/jghis/configure-ad/assets/132087784/9b6e561b-ed4a-4274-af40-74449ccce0f0)

  Prerequisites checked.

  ![image](https://github.com/jghis/configure-ad/assets/132087784/957c5e85-47f8-4067-b4c3-fd39a323495b)

  Active Directory successfully installed.
  
  ### Promote DC-1 to a Domain Controller: 
 
  ![image](https://github.com/jghis/configure-ad/assets/132087784/e799e281-16af-44d5-892e-1d41e5703ad8)
 
  Setup a new Forest as mydomain.com and give a password.  We will be logged out of the server.
  
 ![image](https://github.com/jghis/configure-ad/assets/132087784/e9e7d5c3-4274-4964-a960-96520ea99e2a)

  Restart and log back into DC-1 as user: mydomain.com\techuser

  

### Create an Admin and Normal User Account in AD


![image](https://github.com/jghis/configure-ad/assets/132087784/39ce6924-61fc-4936-9282-48662c057466)

    In DC-1 select   click on Tools and select Active Directory Users and computers.
    In Active Directory Users and Computers (ADUC)   we created an organizational Unit called "-EMPLOYEES" and another one named "-ADMINS"
    
    ![image](https://github.com/jghis    /configure-ad/assets/132087784/db511f9d-b03f-46bf-9ccc-c41f76784dc0)

     We Created a new employee named "jane Doe"

     ![image](https://github.com/jghis/configure-ad/assets/132087784/54a99b6c-65e8-49f0-b229-cb8d4cb8c961)

     We gave jane Doe  a password.

    ![image](https://github.com/jghis/configure-ad/assets/132087784/2dcfb558-8a46-4763-a8c7-a8b18358feae)

     
     we added  jane.doe to the "Domain Admins" Security Group.


     ![image](https://github.com/jghis/configure-ad/assets/132087784/cb8ddb89-5657-4870-a75a-178c74327f91)

    
     Close the Remote Desktop connection and log back in as "mydomain.com\jane.doe"
    Use jane.doe as our Admin account from now on.

###  Join Client-1 to the Domain (mydomain.com)
   
    Remote desktop into client-1 as techuser
    
    ![image](https://github.com/jghis/configure-ad/assets/132087784/c9f3b8c6-2bf3-44b4-b817-2d43bbb66041)

    Remote desktop into cient-1 as the original local admin(techuser) and join it to the Domain.
    Go to setting select rename this PC advanced click change and select Domain then type domain.com
    Computer will restart.

    ![image](https://github.com/jghis/configure-ad/assets/132087784/2fcbf4b8-ab97-4e11-8ced-7b64df5ce978)

    From Azure portal select DC-1 go to networking  and copy DC-1 private IP address.

  

    ![image](https://github.com/jghis/configure-ad/assets/132087784/ba957a99-083f-473e-9840-0811af79f778)

    From the Azure portal, set Client-1's DNS setting to the DC's private IP address.
    
    ![image](https://github.com/jghis/configure-ad/assets/132087784/b5c8a2c9-a958-4c54-b6f8-cf236cd193a0)

     From the Azure portal, restart Client-1
    
    ![image](https://github.com/jghis/configure-ad/assets/132087784/b85593e4-9d79-4b1f-a725-2ac094cc916d)

     Joigning client-1 to the Domain Controler and log back into Client-1
    
    Login to the Domain Controller (Remote Desktop) and verify Client-1 shows up in Active Directory Users and Computers inside the "Computers" container 
    on the root of the Domain.

###  Setup Remote desktop for non-administrative Users on Client-1
   
    ![image](https://github.com/jghis/configure-ad/assets/132087784/04057003-b41c-4e54-94bb-e1752d4d85fc)

    Log into Client-1 as mydomain.com\jane.doe and open system properties
    Click "Remote desktop"
    Allow "domain users"access to remote desktop
    Now we can log into Client-1 as a normal, non-administrative user.
    
### Create additional Users
     
     Login to DC-1 as jane.doe and create a bunch of additional users
     Go to Active Directory Users and Computers
     Select -Employees
     Select new
     Select Users
     
     ![image](https://github.com/jghis/configure-ad/assets/132087784/fcbda746-f623-46c8-96d1-c4aeddc71948)
     
     ![image](https://github.com/jghis/configure-ad/assets/132087784/10bb2e86-521c-4af8-84ae-8dbbfdad879f)

      We created the user john Doe
     
     ![image](https://github.com/jghis/configure-ad/assets/132087784/5ae66f17-e255-4ca5-99a5-8305cb368bbb)

     ![image](https://github.com/jghis/configure-ad/assets/132087784/f79b3489-f1b6-469f-adb5-81a7556c9f85)

     We created the user karen Doe

     ![image](https://github.com/jghis/configure-ad/assets/132087784/817ca9bf-90ad-4ffe-ad1b-9e0818e1ed97)

     We created the user ken Doe

      ![image](https://github.com/jghis/configure-ad/assets/132087784/32b15847-2166-448c-991b-23806f7fbf8a)

      All users created.

      

     


     

     
     
