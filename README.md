# AzureProjectDocumentation
Self learning Azure documentation




# Read this before doing anything else

**If you intend to make use of student benefits**

Azure has been a bit finicky relating to student login for me. After multiple attempts of logging in to my student account/converting my normal account to a student account I eventually landed upon this particular site(https://azure.microsoft.com/en-us/pricing/offers/ms-azr-0170p/) and went through the apply link at the top of the page. 

I am currently unsure if this was this particular link that finally managed to confirm my student status, or if the Azure platform takes its time to confirm my status.

Regardless, I have now access to my free student benefits and can confirm for fellow ENTA students that the student offer as of the moment of writing this section (05/07/2023) is still functional.

**Student benefit limitations**

There are a few services you will not be able to access on a student subscription. But more problematic, there is a limit on how many public IPs and CPUs you can make use of at any time. As such you will not only be limited by your credits, but by what the platform enables you to do or create.

**If this is your first time using this sort of platform**

Free credits in a 12 month period does not mean complete free unlimited use of Azure resources for 12 months. 

More powerful machines will imply a larger price per hour which will be deducted from your credits. 

And unless configured to work otherwise, your machines will keep running even if you log off from your account, making it a necessity to turn off/delete any machines or any other service that you will not need running after you stop working with Azure for the day. 

Not doing this will be a quick way to spend all of your credits in a somewhat short span of time, and if you do run out of credits you will be locked out of using the platform and anything you might have in it until you pay for normal access or get another student subscription.

You can check your credits by going to the search box in the main page and writing/selecting ‘Education’. Education overview will show the expiration date and current amount of the credits you have available.

![image](https://github.com/AF-Github1/AzureProjectDocumentation/assets/133685290/fd19836c-336d-4b1f-96e0-f1f3bb20df71)


# Relevant Links

**Main site**

https://portal.azure.com/

**Documentation**

https://learn.microsoft.com/en-ca/azure/?product=popular

# What will be handled in this document

Understanding Azure’s Virtual Machines
	Creation
	Management
	Editing
	Access	

Understanding Azure’s features and solutions
	Role of a Resource Group
	Implementing services in your VMs
Azure Storage Account
	Creation
	Management
		Containers
		File Shares (Windows and Linux)
		Website Hosting

# Login information

These are the credentials used for every machine unless stated otherwise. Feel free to use your own.

Username: administrator_enta
Password: Passw0rd@ENTA


# Creating your first virtual machine in Azure

If you have handled other cloud platforms like AWS then this will be mostly intuitive to you but I would still recommend reading through this as there are some differences.



After having successfully logged in to your account, from the main page either through the top left dropdown menu or the search box, look for the Virtual machines option and select it


![image](https://github.com/AF-Github1/AzureProjectDocumentation/assets/133685290/722f4947-ed9c-496a-845b-0f1b678b4f45)


Then press the create button in the middle of the screen. 
The option chosen should be Azure virtual machine.

Azure virtual machine preset configuration lets you pick between a few pre configured presets before letting you customize your machine much like the previous option

The last 2 options require you to create a private cloud. This option is unavailable to me as the Student Subscription does not let me access this feature so it will not be discussed here.


![image](https://github.com/AF-Github1/AzureProjectDocumentation/assets/133685290/261da530-7a8d-46c4-90ea-a241eba36139)

# The Basics tab


**Subscription**

The paid or offered service from which the costs of operating your machine will be deducted and will also define what are the services you can access. I chose Azure for Students, pick according to your own subscriptions.

**Resource Group**

Can aggregate numerous other machines, services that can be assigned to your machine or serve as a tracker to the costs of any created machine that uses the resource group. Choose a name and create a new resource group if you don’t already have one.

**Virtual machine name**

How the machine will be identified in the interface. Call it what you will.

**Region**

Location of the servers where the machine will be hosted. To note that different regions may have different availability of services, redundancy features or differences in latency. 
Leave this in its default state for now.

**Security Type**

Defines the amount of protection machines will have, highest being confidential. You may leave this in its default state.

To note, you can’t change the security type of a virtual machine after it has launched. And certain security types will not work with some of the operating systems.

**Image**

The specific operating system you want for your machine. Choose what you prefer, taking in account that the security type chosen previously may not be available.

**VM architecture**

This relates to processor speeds. Arm64 are less powerful but more cost efficient. Again, the option to choose between them will depend on the Security Type and Image chosen previously. 

This information doesn’t particularly matter because pricing of the machine seems to be affected only by the Size and Disks chosen. So always pick the best option here if you can, which should be x64 which so happens to be the default state when available.

**Azure Spot Discount**

Azure enables users to get a discount on currently unused resources, with the condition that if Azure suddenly needs to make use of said resources, it will boot out any machines making use of them, interrupting their processes or even deleting the machines, although this action is left to the user to choose. Leave this blank.

**Size**

Your disk size and RAM are initially picked together. To add more space you will need to go to the Disks tab which we will handle a bit further later in this document. For now, a Windows machine should be more than fine with 8GB of ram, with Linux you can go down to 2 gb, unless you will make use of a graphical interface.

**Administrator account**

Give it whatever credentials you want. I personally used the ones in the Login Information section.

**Inbound port rules**

This defines the initial access configurations.

You should leave the 3389 port for RDP open in order to use a remote desktop client to enter your machine. You can also just directly configure any of the inbound rule settings after the machine has launched through the Networking tab after selecting the machine you want to configure.

![image](https://github.com/AF-Github1/AzureProjectDocumentation/assets/133685290/ab501892-323d-47b4-83e4-7499d3ae8c02)


If at any time you are unsure about what is the actual price of the machine you created, microsoft provides its own pricing calculator where you can simulate how expensive a machine you create will be. It is free to use.

https://azure.microsoft.com/en-us/pricing/calculator/


# The Disks tab

![image](https://github.com/AF-Github1/AzureProjectDocumentation/assets/133685290/d59ea17c-ed2c-4e1f-aac1-921cf39fb602)


**VM disk encryption**

As a student account using a student subscription I do not have access to this feature so it will not be discussed

**OS disk**

Choice between SSD or HDD disks. SSD will be faster but more expensive. We won’t need any particularly fast disk so choose HDD.

Pricing and characteristics are must better explained in Azure’s own documentation so check the following link if you want a more in depth look

https://learn.microsoft.com/en-ca/azure/virtual-machines/disks-types

Tick the Delete with VM box so you get rid of the disk when you delete the machine.

**Key management**

Key used for encrypting the disk. Not a choice here as we do not have access to disk encryption. As such the default option is the only option.

**Ultra disk compatibility**

The most powerful option for disks. Completely unnecessary for an example and significantly more expensive. Do not tick this box.

**Data Disks**

Enables creating additional disks besides the one where your OS will be installed on. It follows the same rules as before with a few additional options


![image](https://github.com/AF-Github1/AzureProjectDocumentation/assets/133685290/b08cc03b-897e-4e8d-8767-9f65f6cef489)


**Source Type**

If you already have disk images, you can add them here. In our case we are making a fresh disk so leave this on None

**Size**

Same as before, change it to a more reasonable size and type of disk.

**Shared Disk**

If you are going to share your disk with multiple machines then you will need to tick yes. Since this is only an example, leave it on no.

And again don't forget to tick ‘Delete disk with VM’, unless you have enabled disk sharing, as enabling disk sharing will disable this option.




# The Networking tab


![image](https://github.com/AF-Github1/AzureProjectDocumentation/assets/133685290/1d8d93d2-fc76-489a-8774-d5a13c062cb9)

**Virtual Network**

If you haven’t already you will need to create a virtual network for your machine. After choosing create new you should be able to see a default choice for an address range. You can choose that one for now, but feel free to specify your own.

![image](https://github.com/AF-Github1/AzureProjectDocumentation/assets/133685290/f4792a77-03ae-41a8-93e3-b17e1d47decc)

**Public IP**

You can choose between dynamic and static assignments. Static is good if you plan to use a machine multiple times or to host some sort of service, but since this is only an example choose the dynamic assignment after ticking SKU basic. 


![image](https://github.com/AF-Github1/AzureProjectDocumentation/assets/133685290/cd50f310-542a-4f4c-92f2-01416017523b)



This is important because Static IP assignments have a cost associated with them


Might be a low cost but it is a cost nonetheless. A penny saved is a penny earned.

NIC network security group and Public Inbound ports

Refers to the security rules of what or can not enter your machine. Leave the 3389 RDP port open in order to later access it through a remote desktop app. Again, you can later be more specific in the inbound rules when you configure your networking settings of your machine after it is done launching.

Tick both boxes for deletion of public IP /NIC and accelerated networking. Accelerated networking is a free feature that enables better performance for your interfaces, although it is only enabled for certain VM sizes.


# The Management tab

![image](https://github.com/AF-Github1/AzureProjectDocumentation/assets/133685290/6577da9e-52b3-434a-a8f8-b3aa4bd5b936)

You can leave this entire section in its default state. I will explain what the options mean though.


**Identity and Azure AD**

These refer to RBAC options for accessing the machine. These would only really matter in an organization, in the context of configuring a general purpose machine for ourselves, it is  unnecessary.

**Auto-shutdown**

Can be useful if you plan to keep a machine around and want to keep it shutdown during off work hours for safety/pricing concerns

**Site Recovery**

Enables creating of backups for your machine on the side of Azure in case of loss of data/functionality. It does have a cost associated.


**The Monitoring Tab**

![image](https://github.com/AF-Github1/AzureProjectDocumentation/assets/133685290/83f39a37-85ad-4075-9778-706ccbffae44)

**Alerts**

Azure has its own alert system that enables a user to be notified whenever certain resource utilization thresholds are reached in the machine

![image](https://github.com/AF-Github1/AzureProjectDocumentation/assets/133685290/4c2757b6-12be-48f7-91fa-7e1b980828b7)


Each option also has its own dropdown menu in order to customize the message contents


![image](https://github.com/AF-Github1/AzureProjectDocumentation/assets/133685290/89756df3-a67d-49dc-b9b7-7baecb8c2da2)


**Diagnostics**

These options basically just define if you want logs to be generated for the booting of any of your VMs. We can leave this on its default setting.

# The Advanced/Tags tab

Unlike the previous tabs, these ones are quite explicit in what each of their options do so I will not go into a lot of detail here. There are still a couple of important points


In Performance (NVMe) it depends on the machine image and the size chosen to determine if it is supported by NVMe or not. There is no pricing associated with this. If you can use it, enable it.

Otherwise, you can leave everything on its default settings.



# The Review + Create Tab

Where you can see all of the configurations and options you have chosen in the previous tabs. 

It will also show the estimated pricing for the size chosen for your machine.
This does not include the pricing for any additional disks or other paid options you have chosen to add like static IPs.

Check and fix anything that is not as you want and press create. After waiting a bit your machine should be created and you now have the option to go to resource location.


![image](https://github.com/AF-Github1/AzureProjectDocumentation/assets/133685290/f9597479-31ee-4a01-9159-62bd743dc9f3)

**Additional Configuration on your created VM**

![image](https://github.com/AF-Github1/AzureProjectDocumentation/assets/133685290/4de23e86-1c9d-494f-b382-818273bb876a)

After pressing Go to resource you will be able to see a few tabs that let you configure various settings related to your VM


A lot of these options are essentially the same as you have configured before. 
As such if your needs change and you don’t wish to create another machine you can just make any necessary alterations through this menu (barring the few exceptions mentioned in the previous section of course)





Although I won’t go in detail for every single option as it would either be mostly redundant or a bit too far out of my current knowledge base (like scripting or developing your own code to then implement on your sites), I will still focus on a few features that present something particularly relevant to know


# Settings

**Networking**

Lets you define the inbound and outbound rules for your machine in order to control what can come in and out.

**Connect**

Lets you pick different ways of accessing your machine. If you have enabled RDP, you can just download the file in order to access your VM instead of typing out the IP and other information in your remote desktop app.


![image](https://github.com/AF-Github1/AzureProjectDocumentation/assets/133685290/9be3ba5c-b277-423d-bfb9-8b6ae1098d9e)

**Microsoft Defender for Cloud**

Unable to be used on a student subscription


# Operations

This section handles updates, backup/disaster recovery and script injection

# Monitoring

Handles resource utilization monitoring and alert customization. Equivalent to the Monitoring tab mentioned previously.

# Automation

As the name implies, lets you define tasks like booting up/shutting down the machine at certain times, sending out alerts to emails and associating said taks with Azure provided services.


# Help

Mostly handles the accounting in AAA. Checks what a user has done on a machine and at what times, handles diagnostics, instance screenshots, lets a user redeploy the VM, change its password and even access the terminal through the browser

**Serial Console**

Access to the terminal. Carefully read the instructions on screen as you are not immediately given direct access.

But after accessing the cmd through this window, it works just as you would expect


![image](https://github.com/AF-Github1/AzureProjectDocumentation/assets/133685290/b488a766-34b9-4d00-b9aa-7990e0d72e69)

# Azure Storage Account

Azure Storage Account is a cloud service that lets you store numerous different types of data (sql database data, text, image, video, etc). 
It is more cost effective and more convenient than creating a dedicated VM to store backup data or making disks, as it even enables you to ‘mount’ the account to different machines in the same Resource Group.

**Creating your Azure Storage Account**

Go to storage accounts

![image](https://github.com/AF-Github1/AzureProjectDocumentation/assets/133685290/788a3350-8b8e-431e-b6a3-59d6a8e658b3)

Press create. 

Now on the Basics Tab you will need to take some care in choosing the Resource Group.

For a machine to be able to access the Storage Account, it will need to be in the same workgroup.

As for Instance Details, give it whatever name you want, leave performance on standard and change Redundancy from its default to LSR. LSR is cheaper and we won’t be doing anything that is worth keeping in this account.

![image](https://github.com/AF-Github1/AzureProjectDocumentation/assets/133685290/020ee4ed-58f8-49cd-8333-1ccc8123097f)


For the advanced tab every setting can be left on its default as it will not affect any operation.



# Storage Account Networking tab 


Controls what can access the storage account. If you choose to enable public access only to certain virtual networks/IPs, you will need to choose the same network in which your other VMs are.


![image](https://github.com/AF-Github1/AzureProjectDocumentation/assets/133685290/28013e50-cbb3-410f-8c99-0f03c2a4ed7d)

If you are going to ever do anything important with any of your machines/storage accounts I recommend taking a bit of care for your inbound rules. Within around an hour of one of my machines being created I already had multiple brute force attempts. 

![image](https://github.com/AF-Github1/AzureProjectDocumentation/assets/133685290/c445be18-8ccf-4f0a-8804-9028e134d11a)

**Microsoft network routing vs Internet routing**

Microsoft network routing handles traffic within the Azure network while Internet Routing lets traffic be routed over public internet. Generally you would choose internet routing if you have external users to the Azure platform, but in this case you can leave it to Microsoft network routing as it is faster.

# Storage Account Data protection tab

This only really matters for any long term Storage Accounts where you would need to delete older data/want to keep older versions of data. You can leave everything in their default state.


![image](https://github.com/AF-Github1/AzureProjectDocumentation/assets/133685290/105122db-ed12-465d-b4f2-060a12f86142)


# Storage Accounts Encryption Tab

Defines on how you wish to handle encryption by either letting the platform handle it or providing your own key. Leave it in its default state for now.

![image](https://github.com/AF-Github1/AzureProjectDocumentation/assets/133685290/4d202f45-9735-450c-abde-b98363202732)

# Storage Accounts Review tab

Same as before, check if there are any changes you wish to make and press create when done.


# Connecting your Azure Storage Account to your VM to share files

Even if the Azure Storage Account is in the same Resource Group it doesn’t mean that VMs have automatic access to said account.


After creation of your account go to the networking section of your storage account and tick the ‘Add your client IP address’. 

![image](https://github.com/AF-Github1/AzureProjectDocumentation/assets/133685290/1d873d72-3b4a-4910-b61b-2e5fc81aac95)

You will also want to add the virtual network that corresponds to your VMs

![image](https://github.com/AF-Github1/AzureProjectDocumentation/assets/133685290/5022acb9-24fc-4b06-9034-8663b806a05a)


If you do not do this you will be locked out of using some of the features of your storage account.

![image](https://github.com/AF-Github1/AzureProjectDocumentation/assets/133685290/0ab5f34f-3fac-4bf3-b93e-e4f6cfbc5834)

It may take a while for this message to stop appearing after you change the relevant settings.


Now go to the container section and add a new container

![image](https://github.com/AF-Github1/AzureProjectDocumentation/assets/133685290/91196b4d-0230-4ce9-8c8f-61814c4a80c4)


Give it a name and keep the rest of the settings on their default. Public access only really matters if you were to share this storage with outsiders.

![image](https://github.com/AF-Github1/AzureProjectDocumentation/assets/133685290/7f7d0319-46d2-4fb0-ae32-318428112d53)

After creation select the container you just created and you will want to create a file in the actual machine you are using to access Azure. Create a text file and write something in it.

After creating said file, press upload and choose the file.

![image](https://github.com/AF-Github1/AzureProjectDocumentation/assets/133685290/1ea2b5b6-8344-4028-8850-4e6152a43a02)

After uploading the file it should appear in your interface

![image](https://github.com/AF-Github1/AzureProjectDocumentation/assets/133685290/3690eefe-2d9d-4588-9229-c91a20fec5b8)


This is the way you directly store a file inside your storage container. 

But let's say you want to share files with any associated VMs


Below Containers, press File Shares and create a new file share.

![image](https://github.com/AF-Github1/AzureProjectDocumentation/assets/133685290/3d6f474a-d193-4580-b336-5895ddcc7fbc)

![image](https://github.com/AF-Github1/AzureProjectDocumentation/assets/133685290/e1f348f4-965b-493d-9833-36683e60274b)


Give it a name, leave the tier at its default as it is the cheapest option and press create

After creating your new file share, select it, upload the same file you created previously and press connect.

![image](https://github.com/AF-Github1/AzureProjectDocumentation/assets/133685290/0a27833c-369a-4f03-8f69-5230f261f52a)

In the Connect options screen choose a drive letter. I would recommend establishing some logic as to how you name your drives as if you have already used the letter you naturally won’t be able to mount your storage account to the same driver.


![image](https://github.com/AF-Github1/AzureProjectDocumentation/assets/133685290/57132cd5-842b-4b4b-badf-cb5b11d7fa73)

You will then need to expand the script section and copy it. This is to be copied to the Windows powershell in your VM

![image](https://github.com/AF-Github1/AzureProjectDocumentation/assets/133685290/31e95a0a-69a5-4661-ab77-44032c0fa21f)


A successful process should look like this
![image](https://github.com/AF-Github1/AzureProjectDocumentation/assets/133685290/441fa327-58bc-4a81-b91b-4cb163ecc0d9)


And if you then go to check on your files, you should be able to see any mounted storage accounts that you have created and associated with your VM.



![image](https://github.com/AF-Github1/AzureProjectDocumentation/assets/133685290/4b597829-e043-4325-a5b1-fbbd96f77b49)


And here you can alter the files in your storage from inside your VM.

Open one of these storage accounts and open up the file you created and make any change to the text within. Save your changes.



![image](https://github.com/AF-Github1/AzureProjectDocumentation/assets/133685290/67bffb0d-4089-43df-afbf-4a82afa56520)

Then go back to your file share to the Snapshots section. Add a snapshot and open it.


![image](https://github.com/AF-Github1/AzureProjectDocumentation/assets/133685290/4417ddc4-faa3-43ee-9450-1faee2029637)


Choose the file you created, download it and open it inside another machine.


![image](https://github.com/AF-Github1/AzureProjectDocumentation/assets/133685290/58f2cf5c-ec7e-4322-aa28-fcecf4508128)

As you can see, the changes inside the VM changed the contents of the storage account. The full process has been successful.

![image](https://github.com/AF-Github1/AzureProjectDocumentation/assets/133685290/34aa5eb6-9464-4b9c-8c7c-ea9780df7a79)

# File share on Linux

Install azure cli on your linux machine. I chose an Ubuntu VM so I used the appropriate command. Yours might be different

curl -sL https://aka.ms/InstallAzureCLIDeb | sudo bash

Now login to azure through the terminal

az login

With your credentials, follow the instructions to connect to the default tenant account in order to enable subscriptions


![image](https://github.com/AF-Github1/AzureProjectDocumentation/assets/133685290/9877b98d-55fb-4c29-9346-06da34504f97)

Run the following text in a bash file. Replace your-resource-group and your-storage-account with your own names for your resource groups and storage accounts.

Remember to give out any necessary permissions with chmod.


—---

#!/bin/bash

RESOURCE_GROUP_NAME="your-resource-group"
STORAGE_ACCOUNT_NAME="your-storage-account"

# This command assumes you have logged in with az login
HTTP_ENDPOINT=$(az storage account show \
    --resource-group $RESOURCE_GROUP_NAME \
    --name $STORAGE_ACCOUNT_NAME \
    --query "primaryEndpoints.file" --output tsv | tr -d '"')
SMBPATH=$(echo $HTTP_ENDPOINT | cut -c7-${#HTTP_ENDPOINT})
FILE_HOST=$(echo $SMBPATH | tr -d "/")

nc -zvw3 $FILE_HOST 445

—---

Make another bash where again you replace the names for your own


#!/bin/bash


RESOURCE_GROUP_NAME="resource-group-name"
STORAGE_ACCOUNT_NAME="storage-account-name"
FILE_SHARE_NAME="file-share-name"

MNT_ROOT="/mount"
MNT_PATH="$MNT_ROOT/$STORAGE_ACCOUNT_NAME/$FILE_SHARE_NAME"

sudo mkdir -p $MNT_PATH

—---


Afterward it's only a matter of running this inside another bash script.  Again change the names on the document for the names you chose for your own fileshares/storage accounts/resource groups 


#!/bin/bash

# This command assumes you have logged in with az login
HTTP_ENDPOINT=$(az storage account show \
    --resource-group July10Demonstration \
    --name july10storage \
    --query "primaryEndpoints.file" --output tsv | tr -d '"')
SMB_PATH=$(echo $HTTP_ENDPOINT | cut -c7-${#HTTP_ENDPOINT})july10fileshare

STORAGE_ACCOUNT_KEY=$(az storage account keys list \
    --resource-group July10Demonstration \
    --account-name july10storage \
    --query "[0].value" --output tsv | tr -d '"')

sudo mount -t cifs $SMB_PATH /mount -o username=july10storage,password=$STORAGE_ACCOUNT_KEY,serverino,nosharesock,actimeo=30,mfsymlinks




You should now be able to access the file share through the terminal and create a document.

Alternatively, you can follow a similar process like what was done for Windows and just get the script from the connect option on your storage account

![image](https://github.com/AF-Github1/AzureProjectDocumentation/assets/133685290/9c61a704-1c4f-4dbb-b928-92671c74c3ef)

Regardless of how you went about it, checking the snapshots for your storage account should now present any new documents you decide to add through your VM.

![image](https://github.com/AF-Github1/AzureProjectDocumentation/assets/133685290/9d097b9a-3aab-481e-b834-f2d35536a1de)

# Using your Azure Storage Account/Visual Studio Code to host a website through a Windows10 VM

Besides storing data, Storage Accounts can also serve as a hosting service for a static website.

Go to the Static website tab in the Data management section of one of your Storage Accounts

Enable static website and define a name for both index document and error document. I named these index.html and 404.html

After saving it should show you the link to access your site. As we have yet to define anything for the site it should just show an error message if you try to access it.

![image](https://github.com/AF-Github1/AzureProjectDocumentation/assets/133685290/9cc5a5ae-586b-438d-b99d-359bf2a794bc)


Now if you haven’t already, create a Windows 10 VM. Its characteristics aren’t too important, just make sure it will have enough disk space for Visual Studio Code and its extensions and that you can actually access it.

Install Visual Studio Code in your machine

Press the extensions section in the left menu (should be the 5th option) and look for Azure Storage. Installing Azure Storage will automatically install the other 2 extensions you see in the image.

![image](https://github.com/AF-Github1/AzureProjectDocumentation/assets/133685290/90a81377-16ca-4f7d-9de5-a57187b0c21e)

Now you will want to manually create a folder where you will store both your index.html and 404.html files.

I created it directly within one of my Storage Account file shares instead of a file inside the machine itself so even if I were to eventually delete the VM the configurations would not be lost, and would enable other VMs to potentially serve as backups.

![image](https://github.com/AF-Github1/AzureProjectDocumentation/assets/133685290/38a5e6ae-df1f-4ce3-a444-c77db51a02b6)

Now inside of each one of your html files you will add the following text

index.html

<!DOCTYPE html>
<html>
  <body>
    <h1>This is a test for the documentation. ENTA</h1>
  </body>
</html>


404.html

<!DOCTYPE html>
<html>
  <body>
    <h1>CHECKING FOR 404</h1>
  </body>
</html>


It doesn’t actually matter what text you pick it's just a way to identify the file

Now you will want to right click in the empty space below explorer and select the option ‘Deploy to Static Website via Azure Storage’


![image](https://github.com/AF-Github1/AzureProjectDocumentation/assets/133685290/feeaf915-7acc-4f20-be06-1fa6d3b8a369)


It will ask you to sign in, use your Azure credentials, after signing in go back to visual studio and on the top side of the screen select your subscription in the search bar.

There may occur an error in this part of the process.

How to fix subscription not appearing in the search bar if you have a subscription


Go to View>Command Palette

![image](https://github.com/AF-Github1/AzureProjectDocumentation/assets/133685290/034e5b93-0da5-4412-94c3-e58621a264ae)

Use the Azure: Select Tenant command

Choose the default option that appears or create a new tenant. It will ask you to sign in again.

After you do this when reattempting the Azure Storage deployment process, you should now be able to select between the active subscriptions for your account.

In my case I chose my Azure for Students subscription.

From this point your site should be functional. Grab the link for your static web site and look it up in a search engine. It should show the message you chose to put in your index.html file.

![image](https://github.com/AF-Github1/AzureProjectDocumentation/assets/133685290/61df34c7-a1a2-4698-b31c-51d76e84948a)

Access to said site will depend on the networking settings for your storage account. Something like you see on the image below will enable essentially every single connection, while if you were to limit it to the private network you share with your VM, then only your VM would be able to access your site.

If you are getting an error message trying to access your site and believe you have done all other configurations right, then check the Networking section. 

![image](https://github.com/AF-Github1/AzureProjectDocumentation/assets/133685290/ff3ca4b5-f7d2-49e2-80d7-2dec84122c23)

This concludes the process for hosting your own website through your Storage Account.


