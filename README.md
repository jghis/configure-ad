### Setup Resources into Azure.
 Create the Domain Controller VM(Window Server 2022) named DC-1
After creating the Domain Controller  set up the NIC(network interface card) private IP address from dynamic to static. This to avoid that the private IP address changes.
  create the Client virtual machine VM ( Window 10) named Client-1. Make sure we use the same Resource Group and Vnet that was created for DC-1.
Make sure that both VMs are in the same Vnet(virtual network)
After all this is done we should ensure connectivity between the client and Domain Controller.
Ensure Connectivity between Client-1 and DC-1
To do so login into Client-1 using  Microsoft Remote desktop connection and ping DC1's private IP address with Ping -t. 
The ping will faill because DC-1 local windows Firewall will block the ICMPv4 traffic. 
To remedy to that Logging to the Domain Controller and enable ICMPv4 in on the local windows Firewall.
After enabling ICMPv4 check back to Client-1 to see the ping succeed.

Install Active Directory
  Logging to DC-1 and install Active Directory Domain Services.
  Promote as  a Domain Controller: Setup a new Forest as mydomain.com.
  Restart and log back into DC-1 as user: mydomain.com\techuser

  Create an Admin and Normal User Account in AD
    In Active Directory Users and Computers (ADUC) create an organizational Unit called "-EMPLOYEES"
    Create a new Organizational unit named "-ADMINS"
    Create a new employee named "jane Doe"
    Add jane.admin to the "Domain Admins" Security Group.
    Close the Remote Desktop connection and log back in as "mydomain.com\jane.doe"
    Use jane.doe as our Admin account from now on.

  Join Client-1 to the Domain (mydomain.com)
    From the Azure portal, set Client-1's DNS setting to the DC's private IP address.
    From the Azure portal, restar Client-1
    Remote desktop into cient-1 as the original local admin(labuser) and join it to the Domain. Computer will restart.
    Login to the Domain Controller Remote Desktop) and verify Client-1 shows up in Active Directory Users and Computers inside the "Computers" container on 
    the root of the domain.

  Setup Remote desktop for non-administrative Users on Client-1
    Log into Client-1 as mydomain.com\jane.doe and open system properties
    Click "Remote desktop"
    Allow "domain users"access to remote desktop
    Now we can log into Client-1 as a normal, non-administrative user.
    
  Create additional Users
     Login to DC-1 as jane.doe and create a bunch of additional users
