Amazon Web Services.......

------------EC2 Service--------------

1) Launch a virtual machine (search for EC2)
2) create all your instances from virginia region
3) create instance using t2.micro. -> this provide instance with minimum resources
4) chooose type of Amazon machine image (AMI)
	select amazon linux 2 ami (hvm), ssd volume type 64 bit axi
5) select free tire eligible service
6) next configure instance details
	 select network as vaishali default
	 in subnet select the only choice available
	 rest of the setting as default
7) click add storage.
	 Volume type go with default setting
		general purpose ssd, magnetic storage, provisioned iops ssd (more space more speed)	
8) click add tag.
9) type key as : 11thJulPuneVaishaliEC2InsKey
    type value as: 11thJulPuneVaishaliEC2InsValue
10) click configure security group
	create new security group
	security gp name: 11thjulPuneHariSG
	description: This is Sec group com for 11th Jul Pune batch
	click add rules button and select custome tcp, protocol: TCP, port range: 8080, source anywhere, rest default.
11) click review and launch
	review the details.
12) click launch
	a dialog box will open (Select an existing pair or create a new key pair)
	Select Create a new key pair.
	Key pair name:11thJulHariKeyValuePair
	click launch instances
13) go to running resources
	select your instance and name it
14) use public DNS:................ to access the resource

15) open PuTTygen 
	1) click load 
	2) select show all files and select the file (.ppm) downloaded from aws 
	3) save private  key and keep the same file name.
	4) Extension should be .ppk

16) open PuTTy
	1) go to connect in aws window and copy public dns shown in example
	2) Host Name (or IP address) : copy the above details
	3 go to SSH -> auth in the (category) of putty
	4) browse and select the .ppk file and click open
	5) puTTy security error dialig box opens, select yes and wait


a linux virtual machine will load.

-------------Steps in virtual machine--------------

1) create a folder named CloudDemo on your machine
2) create a dynamic web project in eclipse or sts (whichever has TomCat v8)
3) 

in virtual machine install java using sudo yum install - java 1.8.0


Elastic ip is used to fix the ip address


------------S3 Service--------------
apache tomcat is not being downloaded, so we will keep the tar file in S3 bucket and then use it.

1) Search S3 
   Bucket Name: (should not have capital letters) 11thjulharis3bucket
	location virginia
2) next
	default all
3) next
	 uncheck block all options
4) create bucket.

5) open bucket select upload -> select war file-> ok
	select testaws.war action -> make public 
	add tar file (tomcat) -> upload -> select -> make public
6) select war file and copy the url 
7) go to virtual machine and cd to folder paste the url -> wget url
8) select tomcat and copy the url by clicking the name.
9) go to virtual machine and cd to folder and paste the url
10) extract using tar xf filename (here tomcat). 
11) cd to webapps of ectracted tomcat and wget the TestAWS.war file from the S3 bucket using the url.
12) chech the server.xml for port number.
13) cd to bin folder of extracted tomcat.
14) ./startup.sh tostart tomcat.
13) copy the ipv4 public ip and paste the ip followed by :port/TestAWS

--------------------------------------------------------DAY 2---------------------------------------------------

Different Domain in which AWS is offering the services

	1) Compute
	2) Storage Domain
	3) Migration
	4) Security-identity
	5) Network and content delivery domain
	6) Messaging
	7)Database Domain
	8) Management

Services in compute domain---------------------------

	1)EC2 -> Resizable compute capacity machine

	2)Lambda -> It is like EC2 Service (can be seen as advanced version of EC2). This cannot be used for hosting the application like EC2, it can only be used 
			to perform some background execution like compressing the images in the application, based on certain events.

	3)Elastic Bean Stalk ->This is also the advanced version of EC2 which is used for hosting the application. This service deploy your application without worring for
				underlying hardware

	4) Elastic Load Balancer -> Is used to distribute your workload among the multiple EC2 instances. The traffic coming to the instances is equally distributed among all 
			instances.
	
	5) Autoscaling  -> It is used for automatic upscaling and down scaling. 
		ex:- If you jave a website with 5 EC2 instances, if the load is 70% then scale it to 6th instance server. Matrices can be set for CPU utilization of the EC2
			if traffic is less then reduce the CPU capacity.

Storage Domain-------------------------------

	1) S3 (Simple Storage System) -> It is object based file system. Will have to create a bucket for it.
	
	2) Cloud Front  -> It is a CDN (Content Delivery Network). It is a caging service, if user connects to a website which is very far from their location then that website
				can be caged to the location which is near to their location because response time and latency is reduced.

	Note*--
		Edge Location -> is a caged web server near your place where your website is caged.

	3) EBS (Elastic Block Storage) -> It is like a hard drive. When we use EC2, somewhere OS is stored or software are also stored. Every EC2 is backuped by default 
					EBS volume. One EBS can be connected to single machine but vice versa is not applicable.

	4) Amazon Glacier ->  It is data archive service. When you have to store data that is not used frequently


SnowBall Service--------------------------

	It is a data transfer serivce in AWS infrastructure.

Storage GateWay Service  -> It is a service which is used b/w your datacenter and the cloud. 
		ex: Suppose you have databse server and application server Strorage gateway sits b/w the web server and 
			data base server keeps on taking the snapshots of database and store it in a S3 bucket.


Database Domain-------------------------

	1)RDS -> it is not the DB, but it manages the Relation data.
	
	2) Aurora -> It is a database created by amazon. It is based on MySql only.

	3) DynamoDB -> This will manage Non_Relation database.
	
	4) Elastic Cache -> 
	
	5) Red Shift -> It is data analytics service.

Network Domain Service-------------------

	1) VPC -> It is virtual network, all the resources launched in same VPC can interact with ecah other.
	
	2) Direct Connet -> This is replacement of the dedicated internet connection. Its a lease line in the AWS infrastructure

	3) Root 53 -> This is DNS (Domain Name Service) in the AWS infrastructure.
			From URL -> Route 53 -> Computer Network
		Whenever url is entered, that url are directed to the DNS and which is converted into IP address
		So name server in the DNS are provided by the Route 53 Service

Subnet ---------------------------------

subnet -> is a portion of network which shares a common address component. You can also define subnet as all devices whose IP address have same prefix.
		Ex:  100.100.100.1
		     100.100.100.2 both machine are belonging to same subnet

Security group------------------------

	It is like a virtual firewall for your online instance control inbound and outbound traffic. Acts at instance level.

Route Table-------------------------
	contains set of rules called Routes. The Route specifies where network traffci should be directed. Route should be associated with subnet	
	Each subnet in the VPC must be associated with route  table

ACL (Access Control List)----------------------
NAT -----------
	A device forward traffic from the instance in the private subnet to the internet or other services and sends response back to the instance.

Internet Gateway  -> It is VPC component that allow communication b/w instance in your VPC and internet.
	 


---------------Database Serivces Steps---------------------------------------------			

1) Create a database
2) Select MySql
3) Templates should be free tire.
4) select switch to default flow creation (floating dialog box on the screen) if the page in not loaded in proper format.
5) also chech only free tire option.
6) click next
7) Specify the DB Details 
8) 	VPC*: vaishali custom vpc or Default VPC (vpc -0e97b.........
	subnet gp : default
	public Accesibility : yes
	availability zone us-east-1c
	VPC Security  gps: vaishali default launch wizard



this is not working----------------------------------------------------------
-----------------------Steps for Creating a VPC-------------------
Name tag : jul11thHariCustomVPC
Ipv4 CIDr Block : 10.0.0.0/26
iPv6 CIDR block: Select  No IPv6 CIDR Block
Tenacy : Default
----------------------------------------------------this is not working

set the sequrity gp to anywhere
mysql -h endpoint -P 3306 -u root -p

p is port
h is host name
u is user
second p is password





MOngo DB
40 to 50 


----------------Networking and content Delivery-------------------

1) VPC
-----------------------Steps for Creating a VPC-------------------
only 5 can be created in a particular location
Name tag : jul11thHariCustomVPC
Ipv4 CIDr Block : 10.0.0.0/26
iPv6 CIDR block: Select  No IPv6 CIDR Block
Tenacy : Default

-----------------------Create Subnet----------------------
1) NAme Tag: jul11tVaishaliPrivateSubnet_a
2) VPC* :dropdown option selete the created VPC
3) Available Zone: ap-south-1a
4) Ipv4 CIDr block : 10.0.0.0/28
click create

create one more Private subnet 
1) NAme Tag: jul11tVaishaliPrivateSubnet_b
2) VPC* :dropdown option selete the created VPC
3) Available Zone: ap-south-1b
4) Ipv4 CIDr block : 10.0.0.16/28
click create

create one more public subnet 
1) NAme Tag: jul11tVaishaliPublicSubnet_a
2) VPC* :dropdown option selete the created VPC
3) Available Zone: ap-south-1a
4) Ipv4 CIDr block : 10.0.0.32/28
click create

create one more public subnet 
1) NAme Tag: jul11tVaishaliPublicSubnet_b
2) VPC* :dropdown option selete the created VPC
3) Available Zone: ap-south-1b
4) Ipv4 CIDr block : 10.0.0.38/28
click create

go to subnet -> action -> modify auto assign ip setting -> enable auto-assign public iPv4 address.  do for public subnet a and b not private subnet a and b

Create a Route Tabel--------------------

Name Tag : jul11thVaishaliPrivateRT
VPC* : Same as above
create routt table

create one more root table---------------------
Name Tag : jul11thVaishaliPublicRT
VPC* : Same as above
create route table

check root table list------------- and subnet name----------
1) Go to route table 
2) select ur private routt table and in action edit subnet association
3) associtae with both private subnet private a and b 
4) save it

5) open public route table
6) and in action edit subnet association
7) associtae with both private subnet public a and b 
8) save it

Configure the Internet gateway--------------------------

1) create internet gateway
 	name tag : Jul11thvaishaliINternetGateway
2) click create option
3) open gateways 
5) in action attach to VPC option
4) VPC* : vaishali VPC created earlier (DropDown)

Open Route Table 
1) Select vaishali public route table select edit route option
2) click add route
3) Destination : 0.0.0.0/0
	Target List :created earlier igw-032dd4535fd0bae-4c
	propogated :no
click done.


NAT Gateway is used to download the patches
Allowes all the outbound traffic which is getting originated from ur private instance to go to  the internet and to get reply and also to get response from the private subnet.

Go to Create NAT Gateway option----------------------------------not using just configuring
1) 	Subnet: Select  Jul22thVaishaliPublicSubbnet_a
	Elastic IP Allocation ID* : Click on Create New EIP
2) click create NAT GAteWay

Name the NAT GateWay  as Jul11thVaishaliCustomeNG
Go to route table

Associtate private route by clicking edit route.
1) Add route
	Destination : 0.0.0.0/0
	Target : the GateWay NAT set above.
	

----------------------Creating a DB Instance-------------------
go to RDS Service



1)IN setting block
 	DB intstance identifier : jul11VaishaliCustomVPCDBINs
	master username: root
	some password

2) click next
3) VPC : jul11thVaishaliCustomVPC(vpc-...........)
	SubNet gp: default-vpc-ocd............

	

----------------------------------------------------------------DAY 3------------------------------------------------------------------

-------------Management Domain-------------------

	1) Cloud Watch ->  This service will watch all resources in AWS infrastructure.
		ex: An alram can be created using cloud which can trigger for CPU usage, after certain threshold.Or other paramneters.
	
	2) Cloud Formation -> This is template service 

	3) Cloud trail -> This is auditing or logging service, where cloud trail can generate a log if any error occurs and store that log in S3 bucket.

	4) CLI -> Command Line Interface. This is replacement of GUI.

	5) Ops Work -> This is a configuration management service.


-----------Security Domain---------------------

	1)IAM (Indetification Authentication Management) -> This service provide granual access to the user.

	2) KMS (Key Management Service) -> This is used to create a public and private key.

-------------Application Domain---------------------

	1) SMS (Simple Mail Service) -> can be used to send bulk mail

	2) SQS (Simple Queue Server) -> 

	3) SNS (Simple Notification service) ->



IOPS -> Input and Output Operation Per Second
PIOP ->

block level storage.

EBS -> It is distributed, replicated block storage that is optimized for consistency and low latency read and write operation.

EBS Volume -> you can attach a volume to the instance
 
EBS Snapshot -> can be used to create multiple column.

AWS provide 3 type of storage--------------------------
	
	1) General Purpose (SSD)	
	2) PIOP (SSD)
	3) Magnetic Storage.



-----------------Steps to create volume-----------------------

1) go to volumes
2) Create volume
3) check volume in terminal using lsblk command.
4) go to action and select attach volume
5) check the volume again using command lsdlk.
6) in terminal -> sudo mkfs -t ext4 /dev/xvdf   (for formatting)
		sudo mkdir /vol2
		sudo mount /dev/xvdf /vol2
		vim welcome.txt
		press i to insert
			type something
		press esc
		type :wq and press enter
		cat welcome.txt to see the file text
		cd home
		cd ec2-user
		sudo cp welcome.txt /vol2

for automounting 
	sudo vi /ect/fstab

	press i
	goto next line and type dev/xvdf /vol2 ext4 defaults 0 0
	cat /etc/fstab

--------------------Steps to create a snapshot--------------------------
Select resource type : volume

Volume : vol-0c

Desscription : some desc

Encrypted: not encrypted

Key : 11thjulharikey

value : 11thjulhariValue

open snapshot

in action -> create volume
	volume type : general purpose ssd
	ap-south-1a
	key and pair value
create a new instance in correct availability zone here 1a

in putty

	sudo mkdir /vol3
	sudo mount /dev/xvdg /vol3
	cd /vol3
	cat welcome.txt  (should be already present)



Elastic LOad Balancing -----------------------------

	Automaticallly distrubute incoming application traffice accross multiple target like EC2 instances or containers or IP addresses. 
	It can handle the varying load of your application traffic in single avalilability zone or multiple availability zone.

	# type of load balancer
	1)Application load balancer -> operates at layer no 7 of the OSI model, best suitable for load balancing of HTTp and HTTPS
	2)Network load balancer		-> operates at connection level of layer no 4 in OSI model.best suitable for load balancing of TCp protocol and Transport layer security traffic
	3)classic load balance (depricated) can only be used with EC2 instance


AutoScaling -> cloud feature that automatically adds or removes compute resources depending upon actual usage. 
	SOme time also reffered as Automatic elasticity. It ensures that additional capacity seamlessely increase during high demand and decrease when 
		demand drops which enables consistent performance


--------------------Steps for load balancing-----------------
Select your instance
action -> image -> create image
	image name -> Jul11hari
	other default option



	

go to load balancer option -> create new load balancer
	select application load balancer	
	Name : jly11thHariCustomLoadBalancer
	Scheme: internet-facing
	ip address type : ipv4
	VPC :vpc-.................|july11vaishalicustomVPC
	Availability zone : select both options and select public subnet a and b for both.
next to configure security gps
	create new security gp
	name: july11thvalishaliLOadBalancerSG
	Description : This is crefer
type :custom TCP port: 8080  source :anywhere
	HTTPs     source:anywhere 
	HTTP other default source :anywhere
next


Create a taget gp----------------------
	name:July11HariLBTargetgroput
	type :instance
	other default

click next -> next ->load balancer should be creater successfully.

Select your load balancer and copy the DNS name form description

go to security group --------------
	create new security gp
	name :11thjulhari...
description :this is for autoscalling
	custom TCP 8080 anywhere
	HTTP default anywhere
	SSH default anywhere

go to launch configuration in autoscaling--------------
	create new launch configuration
	select your AMI not (quick start)
	next
	Create launch Configuration
		name: 11thjulyHAriPublicLaiunc	
		IAM role :none
	IP Address Type: Do not assign a public IP address to any instances
	click add storage
	click next
	select existing gp
		select your security gp
	create new keypair download it and launch

select your launch configuration and click auto scale gp.
	gp name: hariSaoAnsikjd
	group size :1
	select subnet aa and c
	load balancing : select traffic from one or more load balancer (select this)
	target gp : your created target 
	HEalth check type: EC2
	Health checj point time :60
	next
	create auto scaling : select use scaling policies to adjust the capacity of this gp
	name: Scale grpup size
	Metric Type: Application load balancer request coutn per target
	target gp: your target
	instances needed: 20
	target value:1
next
	create auto scaling gp
-------------------------------------------------Do not use this plz 
		send notification to :your email address
	with these recipient
	whenever instasnce: select all
-----------------------------------------------
next

	Key: hariSaoAutoslla
	value:snhdjfked


------------Go to amazon SNS ->create topic
	Name: Hari	
	

-----------------------------------------------------------------DAY 4----------------------------------------------------


Amazon EMR  (AWS analytics services)


------------Steps for cloud watch---------------
In management and governence select cloud watch


--------------Search SNS----------
goto Topics
create a topic
Name: 11thjuly
Display name 


EC2 instance 
1 html file 
3 jsp files
ami for the instance























