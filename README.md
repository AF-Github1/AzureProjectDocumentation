# AzureProjectDocumentation
Self learning Azure documentation



**Read this before doing anything else**

**If you intend to make use of student benefits**

Azure has been a bit finicky relating to student login for me. After multiple attempts of logging in to my student account/converting my normal account to a student account I eventually landed upon this particular site and went through the apply link at the top of the page. 

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


**Relevant Links**

**Main site**

https://portal.azure.com/

**Documentation**

https://learn.microsoft.com/en-ca/azure/?product=popular

**What will be handled in this document**

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

**Login information**

These are the credentials used for every machine unless stated otherwise. Feel free to use your own.

Username: administrator_enta
Password: Passw0rd@ENTA


**Creating your first virtual machine in Azure**

If you have handled other cloud platforms like AWS then this will be mostly intuitive to you but I would still recommend reading through this as there are some differences.



After having successfully logged in to your account, from the main page either through the top left dropdown menu or the search box, look for the Virtual machines option and select it


![image](https://github.com/AF-Github1/AzureProjectDocumentation/assets/133685290/722f4947-ed9c-496a-845b-0f1b678b4f45)


Then press the create button in the middle of the screen. 
The option chosen should be Azure virtual machine.

Azure virtual machine preset configuration lets you pick between a few pre configured presets before letting you customize your machine much like the previous option

The last 2 options require you to create a private cloud. This option is unavailable to me as the Student Subscription does not let me access this feature so it will not be discussed here.


![image](https://github.com/AF-Github1/AzureProjectDocumentation/assets/133685290/261da530-7a8d-46c4-90ea-a241eba36139)

**The Basics tab**


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


**The Disks tab**

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




**The Networking tab**


![image](https://github.com/AF-Github1/AzureProjectDocumentation/assets/133685290/1d8d93d2-fc76-489a-8774-d5a13c062cb9)

Virtual Network

If you haven’t already you will need to create a virtual network for your machine. After choosing create new you should be able to see a default choice for an address range. You can choose that one for now, but feel free to specify your own.

![image](https://github.com/AF-Github1/AzureProjectDocumentation/assets/133685290/f4792a77-03ae-41a8-93e3-b17e1d47decc)
















































