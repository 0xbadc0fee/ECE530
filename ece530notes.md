
# Table of Contents

1.  [Module 1](#org6fdfd1b)
    1.  [Overview](#org23a4aa6)
    2.  [Section 1<sub>1</sub>](#orgb1e37c5)
        1.  [Notes:](#org8e0e592)
        2.  [Watch lectures](#orgdffd5e1)
        3.  [Quiz 1.1 (100pts)](#org73a6b1c)
    3.  [Section 1<sub>2</sub>](#org0a0a28b)
        1.  [Notes:](#org058e103)
        2.  [Watch Lectures](#org8c339b4)
    4.  [Section 1<sub>3</sub>](#orga61583e)
        1.  [Notes:](#org6e91022)
        2.  [Watch Lectures](#orgeb5dfaa)
        3.  [Quiz 1.3 (100pts)](#org32bcdf4)
    5.  [Section 1<sub>4</sub>](#org5a918c0)
        1.  [Notes:](#orgc7bc632)
        2.  [Watch Lectures](#orgcae7c71)
        3.  [Homework 1: IaaS Infrastructure (140pts) <code>[8/8]</code>](#org0488120)
2.  [Module 2](#org9bbb681)
    1.  [Overview](#orgcd09265)
    2.  [Section 2<sub>1</sub>](#orgda0c0d9)
        1.  [2<sub>1</sub><sub>1</sub> AWS Intro](#org121d7f7)
        2.  [2<sub>1</sub><sub>2</sub> AWS Infrastructure](#org603c4fc)
        3.  [2<sub>1</sub><sub>3</sub> AWS Networking](#orge5e1eb1)
        4.  [2<sub>1</sub><sub>4</sub> AWS EC2 & EBS](#orgba76898)
        5.  [2<sub>1</sub><sub>5</sub> Google Cloud](#org4f20bd2)
        6.  [2<sub>1</sub><sub>6</sub> MS Azure](#org9513fbf)
        7.  [Quiz 2<sub>1</sub>](#org4e99bfd)
    3.  [Section 2<sub>2</sub>](#org83e5bef)
        1.  [2<sub>2</sub><sub>1</sub> Cloude Edge](#org079d869)
        2.  [2<sub>2</sub><sub>2</sub> Sharding](#orgbd89c59)
        3.  [2<sub>2</sub><sub>3</sub> Critical Path](#org8389ab3)
        4.  [Quiz 2<sub>2</sub>](#org6e18aa3)
3.  [Module 3](#org8669e4a)
    1.  [Overview](#org2d9395b)
    2.  [Section 3<sub>1</sub>](#org2676107)
        1.  [3<sub>1</sub><sub>1</sub> CAP Theorem](#org6638802)
        2.  [3<sub>1</sub><sub>2</sub> CAP Theorem Examples](#org72e1185)
        3.  [3<sub>1</sub><sub>3</sub> CAP Theorem Details](#orgcfcc0fc)
        4.  [3<sub>1</sub><sub>4</sub> CAP Theorem and the Cloud](#org1980b35)
        5.  [Assignment: CAP Theroem Reading Notes](#orge3ef5e5)
    3.  [Section 3<sub>2</sub>](#org076ff3f)
        1.  [3<sub>2</sub><sub>1</sub> [C]onsistency](#orgf9f4710)
        2.  [3<sub>2</sub><sub>2</sub> Distributed Systems](#org42ddda2)
        3.  [3<sub>2</sub><sub>3</sub> Two Phase Commit](#org0fda68f)
        4.  [QUIZ 3.2](#org0a358b2)
    4.  [Section 3<sub>3</sub>](#org2e06d10)
        1.  [3<sub>3</sub><sub>1</sub> Byzantine Failures](#orgec3553a)
        2.  [3<sub>3</sub><sub>2</sub> Examples of Failure Modes](#org9eb80ec)
        3.  [3<sub>3</sub><sub>3</sub> Synchronous and Asynchronous Execution](#org42953c7)
        4.  [3<sub>3</sub><sub>4</sub> Data Partioning](#org94a5409)
        5.  [QUIZ 3.3](#orgdbde44e)
    5.  [Section 3<sub>4</sub>](#org717a75d)
        1.  [3<sub>4</sub><sub>1</sub>](#org75003b7)
        2.  [3<sub>4</sub><sub>2</sub>](#orgfe8842d)
        3.  [3<sub>4</sub><sub>3</sub>](#org8a2595c)
        4.  [3<sub>4</sub><sub>4</sub>](#orgbd48fac)
        5.  [3<sub>4</sub><sub>5</sub>](#orgdaa4add)
        6.  [Reading Assignment: DYNAMO](#org7204449)
    6.  [Homework #2](#org89ec9d3)
4.  [Module 4](#org65b3074)
5.  [Module 5](#org0ef6d12)



<a id="org6fdfd1b"></a>

# Module 1


<a id="org23a4aa6"></a>

## Overview

-   Categorize the cloud services
-   Purpose on how the cloud is used today


<a id="orgb1e37c5"></a>

## Section 1<sub>1</sub>


<a id="org8e0e592"></a>

### Notes:

-   1.1.1 Intro
    -   &#x2026;how its used today
    -   development of I/O systems
    -   history of the infrastructure
    -   using computers we don't own through infrastructure.
-   1.1.2 Utility
    -   utility infrastructure model, contrast to trad&#x2026; trad requires forecast of use and growth.
    -   old way, over buy in anticipation of growth, leaves gaps in utilization / demand
    -   demand is not linear, goes up and down&#x2026; leave surpluses, expensive surpluses, also create deficits
    -   cloud computing is designed from scratch to scale up and down accourding to infrastructure demand
-   1.1.3 From Mainframes to IoT
    -   Mainframes + Terminals &#x2026;
    -   PC's , 1980's, users have their own systems&#x2026;
    -   Networked PCs, centralized storage system, adding security..
    -   1990s-2000s web revolution, web applications, google, facebook, web servers /services
    -   Scalar expansion of web, becoming very complicated,
    -   Internet of Things, giving internet to every device, all over the world, wireless sensors, embedded devices
-   1.1.4 Datacenters and Supercomputers
    -   Datacenters
        -   Explosion of web size == need large facilities for networked computers / servers
        -   very 'fixed' to locations, can't easily relocated datacenters
        -   &#x2026; Mega Datacenters, lot's of HVAC, physical accomodation for power / heat /emissions etc.
        -   need lots of $$, power (1.5% of all USA electricity in 2007), land, skills, etc.
        -   really onlcy practical for a few very, very large companies&#x2026;
    -   Supercomputers
        -   collective computing, exceeding that of other built systems
        -   high processing capability
        -   high data handling cap
        -   unique ability to solve certain computational challenges
        -   require complex scheduling systems
        -   requires advanced / complex networking / fibre / etc
        -   fastes is anhe-2 (china), very elegant MareNostrom (Spain)
    -   1.1.5 CyberInfrastructure
        -   High performance computing
            -   when you have application that exceed the capabilities of desktops
            -   includes: supercomputers, cluster computers, distributed comp, grid comp, exotic hardware (FPGA, etc)
            -   Grid Computing:
                -   HPC built as geogrphicall distributed system from collection of comp, net, storage all via h/s network
            -   Cyberinfrastructure
                -   kewords: DISCOVERY, COLLABORATION
                -   comprised of instruments, sensors, HPC systems, data storage systems, visualization facilities, all networked via h/s
                -   Layers: 0=base, 1=middleware(net, OS), 2=services, 3=applications&#x2026; CyberInfrastructure lives in the middle 2
        -   CLOUD COMPUTER != CYBERINFRASTRUCTURE, but is "part of" cyberinfrastructure,


<a id="orgdffd5e1"></a>

### DONE Watch lectures


<a id="org73a6b1c"></a>

### DONE Quiz 1.1 (100pts)


<a id="org0a0a28b"></a>

## Section 1<sub>2</sub>


<a id="org058e103"></a>

### Notes:

-   1.2.1 Benefits of Cloud Computing
    -   Outsource Datacenter
        -   economies of scale
        -   now afford special skills
        -   dev can concentrate on core comp's
        -   shorter lead times
        -   lower capital expenditures
        -   compute power becomes utility commodity like electricity / gas
    -   Benefits cont.
        -   Reduced capital and operating costs
            -   can start small and grow, pay-as-you-go / pay-as-you-grow
        -   Simplified app deployment and management
            -   common programming model across mobile, browser client, server, cloud
            -   access to strong ecosystem of resources
            -   integration with existing IT
            -   vendors handle new tech & integration
    -   Considerations as a Cloud Engineer:
        -   Your instances WILL DIE
        -   You will share resources
        -   the archictecture WILL CHANGE
        -   you will never see the lights
    -   DO NOT TRUST THE CLOUD
        -   you must assume that any failure that can happen in the cloud will happen
-   1.2.2 Common Cloud Vendors
    -   Amazon Web Services AWS (since 2006)
        -   Provide:
            -   different types of services
            -   migration tools
            -   analytics
            -   mobile services
        -   Services
            -   mobile services
            -   machine learning
            -   networking
            -   security
            -   hosting
        -   Scope
            -   covers 190 countries across world
            -   globally located data centers
            -   high reliability, scalable, low-cost infrastructure, high adoption rate
        -   History
            -   2003 B. Black / C. Pinkman paper, aws infrastructure
            -   2004 simple queue service launched
            -   2007 over 180000 dev's using platform
            -   2010 all of amazon.com moved to aws
            -   2011 some major outages suffered, EBS problems
            -   2012 first 'Re-Invent' Conference
            -   2020 commitment to 100% renewable energy
    -   Goolge Cloud
        -   Provides
            -   Compute
            -   Storage
            -   Big Data
            -   Machine Learning
        -   Comparison
            -   slower to roll out services but more mature when rolled out
            -   not as many total services as AWS
        -   History
            -   2008 google app engine announced
            -   2010 google cloud storage launched
            -   2012 google compute engine launched
    -   Microsoft Azure
        -   Provides
            -   Platform as a service
            -   Infrastrucutre as a service
            -   Datacenter Infrastructure
        -   Comparison
            -   not as many services but very very mature and stable
        -   History
            -   2008 annouced windows azure platform
            -   2010 azure commercially available
            -   2014 outage affecting major websited including MSN.com
-   1.2.3 What if Cloud Dies (i.e. vendor pulls the plug)
    -   Consider retaining as much in-house capacity as you need to stay alive, disaster plan
    -   maintain accessibility outstide of cloude / networking infrastructure / bandwidth capacity / etc.
    -   Ultra-Sensitive Data
        -   data you can't trust ANYWHERE else
        -   can't use external cloud but maybe internal cloud&#x2026;
        -   flag your data, go ahead and host low security on cloud, but know what is high and what is low security
    -   Legal aspects
        -   Law requires certain data be handled certain ways
        -   location based: can data be hosted in a different countries datacenter? JURISDICTIONS
        -   content based: health data, financial data, educational data, PII data, etc
        -   Don't rely on LAW to be STATE OF THE ART, LAW is REACTIVE and slow, not PROACTIVE.  THINK AHEAD OF THE LAW.
    -   Cloud availability issues
        -   what assurance that your provider will have enough resources?
        -   how bad of damage if you can't scale up quickly when you needed to (burst situations)?
        -   what remedies if their services fail and cause you damage? (damages covered in SLA, service level agreement)
        -   Amazon approach&#x2026; SPOT MARKET vs GENERAL MARKET, different pricing based on level of assurances


<a id="org8c339b4"></a>

### DONE Watch Lectures


<a id="orga61583e"></a>

## Section 1<sub>3</sub>


<a id="org6e91022"></a>

### Notes:

-   1.3.1 What is the Cloud (3 part definition)
    -   Cloud Characteristics
        -   Common characteristics
            -   massive scale, homgenentiy, virtualization, low cost sftwar, resilient computing
            -   geographic distr, service orientation, advanced security..
        -   Essential characteristics
            -   On demand self services
            -   broad network access
            -   rapid elasticity
            -   resource pooling
            -   measured service
        -   NIST Cloud Computing Model, see slide
            -   Models vary by how much you manage vs how much vendor manages
    -   Service Models
        -   On-prem (private) / You manage all..
        -   IaaS / you manage apps - dbases
        -   PaaS / you manage apps
        -   SaaS / everything managed by vendor (tenant cloud, edge impulse, etc)
    -   Deployment Models
        -   Public
        -   Private
        -   Community
        -   Hybrid
-   1.3.2 Deployment Models
    -   Public
        -   Used by many other entities other than your company
        -   hosted off prem
    -   Private
        -   used only by you
        -   hosted on prem
        -   full control
        -   can have at same time as a public, not mutually exclusive.
    -   Hybird
        -   Some combination of Public / Private, sharing some data, some functions, some storage
    -   4 Deployment models
        -   Enterprize -> Cloud
        -   Private Cloud within Enterprise, resources accessed via INTRANET / LOCAL net
        -   Community Cloud, INTRANET and INTERNET (VPN), linking clouds together securely
        -   Hybrid Cloud, mixing public and private enterprise, intranet and internet, , more complicated.
            -   orchestration systems like Kubernets allows to deploy across hybrid, mixed, setups
    -   Rationale
        -   Private Cloud
            -   data security
            -   avoid vendor lock-in
            -   SLA performance, reliability
            -   cost savings.  sometimes it's cheaper to roll your own, especially if data secrecy is an issue
        -   Enterprise level considerations when going cloud..
            -   CPU/HR , GB/day, ongoing costs
            -   hidden costs, mangement, training, onboarding, etc.
            -   different cloud models required for different applications
    -   Deployment Summary
        -   Clouds (how it's structured / built )
            -   Private
            -   Public
            -   Hybrid
        -   Services (what it does)
            -   IaaS
            -   PaaS
            -   SaaS
        -   Users (how they interact with it)
            -   Dashboards
            -   Browsers
            -   IoT Devices
    -   SaaS Maturity Model
        -   L1: Ad-Hoc / Custom / Single instance per customer "single tenant"
        -   L2: Configurable per customer
        -   L3: Configurable and multi-tenant
        -   L4: Scalable, Configurable, multi-tenant // load balancer between tenant and infrastructure
    -   SaaS Defined
        -   model of software deployment where application is hosted as a service provided to customers across the internet
        -   alleviates burden of software maint / support BUT users relinquish control over version and customization
-   1.3.3 Virtualization & Virtual Machines
    -   Virtualization
        -   you can't physically touch the cloud machines, hardware can and will frequently change
        -   to avoid dependency on specific hardware, write programs for virtual machines from the start
            -   level 5  Cloud Applications
            -   level 4  Cloud Services
            -   level 3  Operating System
            -   level 2  Virtual Machine Manager
            -   level 1  Hardware / Physical
-   1.3.4 Opportunities and Challenge
    -   Benefits
        -   Use high-scale / low-cost providers
        -   anytime/place access via web
        -   rapid scalability up or down and load balancing
        -   no on prem IT staff to hire
    -   Risks
        -   Performance, reliablity, SLA structure
        -   control of data, service parameters
        -   application features / customization
        -   interaction between cloud providers
        -   non standar API - mix of SOAP and REST
        -   privacy, security, trust..
        -   some think the return to supercomputer is opposite of what pc's gave us, freedom from mainframe
        -   high integration means high dependency
        -   monopolies
-   1.3.5 Advantages (Detailed)
    -   Lower computer costs
        -   less power, less compute required
        -   since apps run on cloud, less local storage req'd
        -   PC itself can be less expensive, thin client
        -   PC needs fewer peripherals, cd's, dvd's, etc.
    -   Improved Performance
        -   fewer large programs running on PC, fewer resources consumed, pc is "faster" or at least less occupied
        -   fewer memory processes, services running, thing boot up faster and run more smoothly
    -   Reduced Software Costs
        -   fewer expensive software purchases per device
        -   usually have access to suite of tools would otherwise need to purchase separately (g-suite, o365, etc)
    -   Instant Software Updates
        -   No longer responsible for patching yourself
        -   updates scheduled automatically
        -   when access via web client, always getting the latest version
    -   Improved document format compatibility
        -   everything using standardized extensions, file formats, etc (.docx, .pdf, .csv, etc)
        -   if everyone sharing doc's through same cloud, should never be a format or versioning conflict.
    -   Unlimited Storage Capacity
        -   Cloud computing == virtually unlimited storage
        -   PC 1TB is tiny compared to cloud storage
    -   Increased Data Reliability
        -   If one node goes down, data is still safe
        -   Cloud acts like a data safe, archive
    -   Universal Document Access
        -   no problem with cloud because not taking documents with you
        -   docs live and remain in cloud, you access and edit them as you need through a portal
        -   docs are instantly available regardless of where you are.
    -   Latest Version Available
        -   No complicated migrations / upgrades / conversions
        -   Cloud always has latest version of docs and apps both
    -   Easier Group Collaboration (remember SharePoint :(  )
        -   Sharing docs easily and reliably == more collaboration
        -   can allow many users access to few docs with out fear of issues
        -   multiple users can collaborate on multiple projects all at same time
    -   Device Independent
        -   agnostic, no pref Mac, Win, Linx, etc
        -   hardware agnostic, no pref pc, thin client, desktop, etc
-   1.3.6 Disadvantages (Detailed)
    -   Always on Internet Connection
        -   cloud compute impossible w/o reliable connection
        -   internet used both for applications and documents.  I.E. MS-Word and Documents / Excel and Spreadsheets / etc.
        -   dead internet == no work being produced
    -   Poor performance if low-speed connections
    -   Features might be limited
        -   fewer options with cloud Word vs Office Word, etc
    -   Can be slow
        -   constantly handling files, back and forth between client and server, etc
    -   Stored data may not be secure
    -   Stored data can be lost
        -   need some kind of phys backup
    -   HPC Systems
        -   not clear you can run heavy software from cloud
        -   Scheduling resources
    -   General Concers
        -   Each cloud vendor using different protocols / different API's
        -   i.e. amazon created it's on DB system (not SQL)


<a id="orgeb5dfaa"></a>

### DONE Watch Lectures


<a id="org32bcdf4"></a>

### DONE Quiz 1.3 (100pts)


<a id="org5a918c0"></a>

## Section 1<sub>4</sub>


<a id="orgc7bc632"></a>

### Notes:

-   1.4.1
    -   IaaS: OpenStack
        -   Open source cloud computing platform
        -   Infrastructure as a service solution
        -   Many independent services
    -   Quick Facts:
        -   joint project by rackspace and NASA
        -   launched in 2010, now community of 15,000 people in 136 countries
        -   OpenStack 1 million+ lines of code in Python
    -   Community Support
        -   over 200 companies helping
    -   High level architecture
        -   [Overview](https://access.redhat.com/webassets/avalon/d/Red_Hat_OpenStack_Platform-11-Architecture_Guide-en-US/images/fce6394275bd3444892c5d3a91ccf17c/RHEL_OSP_arch_347192_1015_JCS_01_Interface-Overview.png)
            -   Dashboard is launch point, provides UI to:
                -   network, storage, compute, identity, image, object storage.
-   1.4.2
    -   OpenStack Services
        -   <span class="underline">Compute: NOVA</span>
            -   on demand networked virtual machines
            -   KVM & Xen available choices for hypervisors or linux container like Docker
        -   <span class="underline">Network: NEUTRON</span>
            -   allowing users to create their own networks and then attach interfaces to them
            -   highly configurable
            -   legacy networksing: nova-network
                -   simplicity
                -   lack functionality like VPN, load balancing, firewall. (EDIT, it now has these abilities)
        -   <span class="underline">Block Storage: CINDER</span>
            -   provides persistent block level storage devices for openstack instances
            -   manages the creation attaching and detaching of the block devices to servers
        -   <span class="underline">Objecst Storage: SWIFT</span>
            -   accepts files to upload, modifications to metadata, mods to container creation
            -   swift architectre is very distributed, no single point of failure, scales horizontally
        -   <span class="underline">Identity: Keystone</span> (difficult to configure, easy to lock yourself out)
            -   provides single point of integration for OpenStack polic, catalog, token, and uthentication.  like group policy object
            -   supports multiple forms of authenticaiotn including standard usernameand password credentials, token-based systems and AWS-style.
            -   User.Tenant.Role.
        -   <span class="underline">Image Storage: GLANCE</span>
            -   provides discovery, registration, and delivery services for disk image servers
            -   can also be used to store and catalog unlimited number of backups
        -   <span class="underline">Dashboard: HORIZON</span>
            -   Bringing together all of the above for user access UI
            -   provides administrators graphical interface for access, provisioning, automation.
        -   <span class="underline">Compared to AWS</span>

<table border="2" cellspacing="0" cellpadding="6" rules="groups" frame="hsides">


<colgroup>
<col  class="org-left" />

<col  class="org-left" />

<col  class="org-left" />
</colgroup>
<thead>
<tr>
<th scope="col" class="org-left">Service</th>
<th scope="col" class="org-left">OpenStack</th>
<th scope="col" class="org-left">AWS</th>
</tr>
</thead>

<tbody>
<tr>
<td class="org-left">compute</td>
<td class="org-left">Nova</td>
<td class="org-left">EC2</td>
</tr>


<tr>
<td class="org-left">Network</td>
<td class="org-left">Neutron</td>
<td class="org-left">VPC</td>
</tr>


<tr>
<td class="org-left">Blk Strge</td>
<td class="org-left">Cinder</td>
<td class="org-left">EBS</td>
</tr>


<tr>
<td class="org-left">Obj Strge</td>
<td class="org-left">Swift</td>
<td class="org-left">S3</td>
</tr>


<tr>
<td class="org-left">Img Mgmt</td>
<td class="org-left">Glance</td>
<td class="org-left">AMI</td>
</tr>


<tr>
<td class="org-left">Dashboard</td>
<td class="org-left">Horizon</td>
<td class="org-left">Console</td>
</tr>


<tr>
<td class="org-left">Identity</td>
<td class="org-left">Keyston</td>
<td class="org-left">IAM</td>
</tr>
</tbody>
</table>


<a id="orgcae7c71"></a>

### DONE Watch Lectures


<a id="org0488120"></a>

### DONE Homework 1: IaaS Infrastructure (140pts) <code>[8/8]</code>

-   [X] Keystone <code>[4/4]</code>
    -   [X] Generate Token
    -   [X] Generate demo and admin users
    -   [X] Retrieve User list
    -   [X] Retrieve role list
-   [X] Glance <code>[2/2]</code>
    -   [X] import cirros OS image
    -   [X] retrieve image list
-   [X] Nova <code>[3/3]</code>
    -   [X] retrieve VM list
    -   [X] create VM
    -   [X] login to VM
-   [X] Neutron <code>[1/1]</code>
    -   [X] create a network
-   [X] Horizon <code>[2/2]</code>
    -   [X] login with proper account
    -   [X] retrieve service info
-   [X] Cinder <code>[2/2]</code>
    -   [X] create a volume
    -   [X] retrieve volume list
-   [X] Swift <code>[2/2]</code>
    -   [X] create a container
    -   [X] upload and download files
-   [X] Extra Points <code>[4/4]</code>
    -   [X] create a VM with public network connected
    -   [X] import and create a vm with ubuntu image inside openstack
    -   [X] attach volume to VM
    -   [X] install one extra service (Ceilometer, Heat, etc)


<a id="org9bbb681"></a>

# Module 2


<a id="orgcd09265"></a>

## Overview


<a id="orgda0c0d9"></a>

## Section 2<sub>1</sub>


<a id="org121d7f7"></a>

### DONE 2<sub>1</sub><sub>1</sub> AWS Intro

-   AWS Biz:
    subsidiary of amazon, pay as you go, cloud on demand, launched in 2002
-   server farms throughout the world
-   @2020, 212 services
-   2017, dominant 34% of cloud
-   Collection of remote compute services&#x2026;
-   Compute:
    -   Elastic Compute EC2
    -   Elastic MapReduce (EMR), hadoop on EC2
-   Storage
    -   Simple Storage Service (S3) - storage
    -   Glaciaer = low cost long term storage (high redundancy, low access time)
    -   Elastic Block Storage (EBS) - persistent block storage
-   Database
    -   DynamoDB = NoSQL backed by SSD
    -   ElasticCache = in-memory cache based Memcached
    -   Relational databse services (RDS) = MySQL, Postgres, Aurora w/ MySQL
-   Platform Model:
    -   | Deployment & Admin |
    -   | App Services
    -   | Compute | Storage | Database |
    -   | Networking |
    -   | AWS Global Infrastructure |


<a id="org603c4fc"></a>

### DONE 2<sub>1</sub><sub>2</sub> AWS Infrastructure

-   World wide, divided into regions, i.e. Europe, SA, US, etc
-   Availability 'Zones'
-   Region = geographic area.  Regions have multiple 'locations', 11 regions.
-   Each region has 2 availability zones, distinct data centers
-   Each EC2 region isolated from each other
-   failover and fault tolerance built into the cloud already, all we have to do is build our applications.
-   Edge Locations
    -   52 edge locations
    -   Edge locations are CDN edge poitns
        -   more edge locations than regions
    -   Used to cache data physically close to the user
-   Global infrastructure
    -


<a id="orge5e1eb1"></a>

### DONE 2<sub>1</sub><sub>3</sub> AWS Networking

-   Domain Name System, port 53, HA & Scalable DNS
-   'Router 53' is the name of the AWS service
-   VLAN: AWS Direct connect uses vlan. 802.1q
    -   dedicated connection, multiple vitural nic
-   client can use same conenctio for private and public management traffice
-   AWS Direct Connect:  High Throughput dedicated, 10gb/s,
-   VPC Virtual Private Cloud: provisionally logically isolated section of aws cloud wehre you can launch aws resources in a virtual network that you define.
-   i.e. create a public store front, publice facing subnet for webservers


<a id="orgba76898"></a>

### DONE 2<sub>1</sub><sub>4</sub> AWS EC2 & EBS

-   EC2 Elastic Compute (re: Nova)
    -   reconfigurable capacity
    -   provision virtual instances (os's)
    -   marketplace for pre-configured instances
    -   uses Xen virtualization (Xen = hypervizor)
    -   Elastic load balancing done automatically
        -   scaling based on demand
        -   min and max instance thresholds
        -   triggers for scaling in and scaling out
        -   uses metrics collected by aws `cloudwatch`
        -   free
-   EBS Elastic Block Storage (re: Cinder)
    -   Data.  Datastores, content networks, databases, all the assests your web apps need to either store or present over the web.
    -   Mount specific BLOCK devices (i.e. sda1, sdh, sdb, etc) logical drives.
    -   BLOCKS available (like vmware datastores) to multip vm's from variety of use scenarios.
    -   can be up to 1TB ea
    -   EBS built on replicated storage so if one phys device goes down, can failover to another.
    -   EC2 handles INSTANCES / EBS handles STORAGE


<a id="org4f20bd2"></a>

### DONE 2<sub>1</sub><sub>5</sub> Google Cloud

-   GCP Google Cloud Platform
-   infrastrucutre services; Google Search, Gmail, YouTube all sparked the GCP growth
-   IaaS, PaaS, and serverless computing environments
-   1st, need datacenters.  Distributed world wide.  Low latency
-   600 services
-   divided by types; Ingest, Storage, Process / Analyze, Explore & Viz
-   Market share, GCP growing but still a fraction of AWS


<a id="org9513fbf"></a>

### DONE 2<sub>1</sub><sub>6</sub> MS Azure

-   MS AZURE, (formerly WINDOWS AZURE)
-   same IaaS / Paas model
-   somewhat specialized to MS products (office)
-   Big differ between AWS and Azure is 6-8yr head start with AWS
-   Azure has lots of datacenters, some specifically USGOV
-   54 Regions around globe, increasing ea year (54 @ 2018)
-   1 Azure GEOGRAPHY has multiple REGIONS
-   Stack:
    -   App Services
    -   Software Services
    -   Platform Services (SQL | .NET | Live | Share-Point | CRM)
    -   Infrastructure Services
-   Details of AZURE LAYER
    -   specialized OS called Microsoft Azure, runs "fabric layer"
    -   manages compute and storage resource clusters within MS datacenters that it then presents to the application layer running on top of Azure Layer
    -   Described as a "cloud layer" running on top of a number of Windows Server systems (Windows server 2008), optimized for Hyper-V hypervisors.
-   Design of AZURE
    -   Scaling of compute and storage controlled by "fabric" layer
    -   Also provides management (i.e. Keystone & Nova)
-   Benefits of AZURE
    -   easy for windows users / offices
    -   active directory, sharepoint, O365, etc
    -   less overhead for IT staff
-   .. vs GCP
    -   GCP stronger in ML, big data, container support
-   .. vs AWS
    -   AWS hyper generalized, open standards, everything to everyone
-   Overall cloud biz
    -   2018 200 billion, 2022 340 billion, &#x2026;
-   No public data avail on how big AZURE really is
-   Amazon specifies AWS revenue, MS only reports Azure growth rate (2019 62%, 2018 78%) over previous (compound ?)


<a id="org4e99bfd"></a>

### DONE Quiz 2<sub>1</sub>


<a id="org83e5bef"></a>

## Section 2<sub>2</sub>


<a id="org079d869"></a>

### DONE 2<sub>2</sub><sub>1</sub> Cloude Edge

-   Clients talk to clouds via web browsers & standards
    -   just the outer 'skin' of it though
    -   much more going on underneath, can host entire businesses end to end
-   Big Picture..
    -   Client req handled by first tier layer, PHP, ASP etc
    -   these are light services, very fast, nimble
    -   first tier caches info (ssl, keys, etc) for use in second tier)
    -   second tier is called 'shards'
-   Many styles of 'cloud' system
    -   at the edge, cloud is taylored for vast # of clients and quick response
    -   further inside, taylored to high volume services that run pipeline of info
    -   deepest inside, world of virtual computer clusters, scheduled with each other, being controlled and scheduled by mapreduce&#x2026;
-   Outer Tiers: replication is KEY
    -   replicate PROCESSING
    -   replciate DATA
    -   replicate CONTROL INFORMATION (keys, ssl, managment info)


<a id="orgbd89c59"></a>

### DONE 2<sub>2</sub><sub>2</sub> Sharding

-   Sharding happens at TIER 2
-   This is where caching first takes place (last search, ssl keys, cookies)
-   Sharding is a method for allocating data items to nodes of a distributed caching or storage system based on the result of a hash function computed on the item identifier. It is ubiquitously used in key-value stores, CDNs and many other applications.
-   Caching in tier 2 is what makes tier 1 work
    -   ..always use cached data when possible
    -   ..replicate data within cache to spread load
    -   ..not everything needs to be fully replicated, so we use 'shards' with just a few replicas
    -   ..uses key value pairing to securely link caches to their users, destinations, services, etc.
-   Sharding is readlly HORIZONTAL scaling.  SPREADING the ability to ACCESS the cloud across mulitple instances.
-   HOW? database table example.  Like breaking down 10,000 row database into smaller tables, with also smaller indecies, and running them in parallel across more instances.  Same singular table data, but all runs and accesses faster while also having some built in fault toleration.  (1 table going down won't take out whole database)
-   Smaller indexes = = faster queries = = faster applications
-   Example Cache services (kw DISTRIBUTED HASH TABLE):
    -   Memcached / Redis
        -   in-memory key-value stored chuncks of arbitrary data
    -   Dynamo
        -   service created by amazon
    -   BigTable
    -   IBM WebSphere eXtreme Scale
-   Necesasry to ALWAYS shard data?
    -   YES.  if almost every external request is going to use it anyway, YES DO SHARD
    -   understands patterns of access to the cloud data /services you manage
-   UPDATING REPLICAS
    -   So yo uhave replicas now, of course you need to sync / update them right
    -   also happens according to 'patterns' of access
    -   some can be singular updated, others must be done across parallel machines running concurently
    -   term sharding is for data, but might talk about 'parallel computation on a shard'
    -


<a id="org8389ab3"></a>

### DONE 2<sub>2</sub><sub>3</sub> Critical Path

-   Critical path.. notion of what is important in a querie / request..
-   what actions contribute to any percievable delay between the user's request and the response to their request.
-   What if a request triggers and update
    -   if updated done asynchronously, user might not notice on their end..
        -   often work this way
        -   avoids waiting for slow services to prcess the updat but may force their tier-one services to 'guess' outcomes
    -   Many cloud systems use these sort of tricks to speed response times
-   Tier 1 PARALLELISM
    -   parallelism speeds up first tier services
    -   asks itself, will it be faster&#x2026;
        -   for x to just compute response
        -   or for x to subdivide work by spreading it out over subservices
    -   `Werner Vogels` (amazon) commented that amazon pages have content from 50 or more parallel sub services that ran, in real time, your request!
    -   networks, data centers, infrastructure can all faile along the way adn create inconsistencies..


<a id="org6e18aa3"></a>

### DONE Quiz 2<sub>2</sub>


<a id="org8669e4a"></a>

# Module 3


<a id="org2d9395b"></a>

## Overview

-   Concepts:
    -   CAP Theorem
    -   Failure Modes
    -   Stronge and Eventual Consistency
    -   Partitioning Algorithms


<a id="org2676107"></a>

## Section 3<sub>1</sub>


<a id="org6638802"></a>

### DONE 3<sub>1</sub><sub>1</sub> CAP Theorem

-   KW 'Distributed Systems'
-   ref Eric Brewer (keynote ACM PODC 2000)
    -   Pick 2&#x2026;
    -   Consistency, Availability, Partition Tolerance
    -   only possible to get 2/3
        -   Consistency: all nodes see same data at same time
        -   Availability: every req gets a reply
        -   Partition Tolerance: system continuse to operate despite arbitrary message loss / failure of parts / fracture
-   Interactions with Web Services
    -   operations commit or fail in entirety (ATOMIC)
    -   committed transaction are visible to all future trx (CONSISTENT)
    -   un-commited trx isolated from each other (ISOLATED) like git
    -   once commited, trx is permament (DURABLE)
-   Consistency: Atomic Data Object
    -   total order on all operations such that each operation looks as if it were complete at a single instance
    -   equivalent to requiring req's if the distributed memory to act as if they were executing in a single node, responding to operations one at a time.
    -   Atomic read/write shared memory
        -   any read operation that begins after a write operation completes must return THAT value, or the result of a later write operation
-   Consistency: What does it mean?
    -   re CAP Theorem means 2 things;
        1.  That update to same data item are applied in some agreed-upon order
        2.  that onece an update is achnowledged to an external user, it won't be forgotten.
    -   Not all systems need both properties
-   Consistency: Risks (also inconsistencies)
    -   inconsistency causes bugs
        -   client can't trust the servers&#x2026;
    -   Weak or Best Effort consistency&#x2026;
        -   strong security guarantees DEMAND consistency
        -   would user trust medical health data to system with weak consistency?
-   ACID to BASE
    -   ACID
        -   [A]tomic:  all trx succeeds, or roll back pre trx
        -   [C]onsistent: can't leave incompleted
        -   [I]solated: can't interfere / contradict each other
        -   [D]urable: completed trx's persist, even when servers reboot.
    -


<a id="org72e1185"></a>

### DONE 3<sub>1</sub><sub>2</sub> CAP Theorem Examples

-   Book Store / Shop:
    -   to keep inv accurate, maybe you lock database once trx starts so that only ever the actual inventory is displayed in web..
    -   &#x2026; only works in small scale, consider larger example, like amazon.
    -   if big, maybe you used cached data&#x2026;
    -   if big, maybe consider violating AC[I]D isolation, let transactions contradict each other to an extent&#x2026;
-   Vogels @ Amazon
    -   CTO at amazon
    -   involved in buiding a new shopping cart service
        -   old one used strong consistency for replicated data
        -   new one built over DHT distributed hash table (CHORD), weak consistency, but eventual convergence
        -


<a id="orgcfcc0fc"></a>

### 3<sub>1</sub><sub>3</sub> CAP Theorem Details

-   Consistency: Eventual / Convergence
    -   informal guarantee that if no new updates, eventually all accesses to item with return last updated result
    -   i.e. BASE:
        -   [B]asically
        -   [A]vailable
        -   [S]oft state
        -   [E]ventual consistency
-   Core Problem
    -   when can we sweep consistency under the rug?
        -   if we weaken a safety critical property, bad things can happen&#x2026;
        -   sites like amazon and ebay do OK w/ weak guarantees, model just doesn't demand otherwise&#x2026;
        -   embracing weaker nature, reduces syncronization, better response time
    -   but what if applications in question are high-assurance, must be accurate every transaction??
    -   [A]vailability (C[A]P):
        -   for a distributed system to be condinuously available, every request received by non-failing node must result in a response
        -   any algorithm used by the service MUST eventually TERMINATE
        -   no BOUNDS on how long algorithm may run before TERMINATING, therefore susceptible to UNBOUNDED computations&#x2026;
    -   [P]artition Tolerance (CA[P]):
        -   network allowed to lose messages from one node to another
        -   when partitioned messages between nodes in different partitions are lost
        -   requirements:
            -   atomicity: every response is atomic / even though parts of messages might not be delivered
            -   available: every node receiving a request MUST provide a response / even though parts of messages might not be delivered.
            -   if system behaves AS IF all nodes were AVAILABLE, then it is considered partiion tolerant
    -   Web Services problem:
        -   similarly expected to by HIGHLY AVAILABLE (every req gets a resp)
        -   when services go down, cause real world problems (finance, healthcare, telecomm, etc)
        -   FAULT TOLERANCE:
            -   When some nodes crash or some communication links fail, it is important that the services still performa as expected. One desirable fault tolerance property is the ability to survive a network partitioning into mulitiple components..
            -


<a id="org1980b35"></a>

### 3<sub>1</sub><sub>4</sub> CAP Theorem and the Cloud

-   Is CAP valid in the CLOUD ??
    -   data centers networks don't normally have partition failures&#x2026;
        -   but wide area links do fail&#x2026;
        -   most services design to do updates in single place and mirror read only data to others..
        -   so CAP scenario can't really pop up&#x2026;
    -   Brewer's arguments about not waiting for a slow service to respond make sense
        -   Argues for using any single replica you can find&#x2026;
        -   but does this preclude that replica being CONSISTENT??
-   Properties you might want in the CLOUD
    -   CONSISTENCY: updates in specified order
    -   DURABILITY: once accepted, not forgotten
    -   real-time RESPONSIVENESS: replies within BOUNDED delay
    -   SECURITY: only permits AUTHORIZED actions by AUTHORIZED parties
    -   PRIVACY: won't discloser personal data
    -   FAULT-tolerance: failures can't prevent system from providing desired results
    -   COORDINATION: actions won't interfere or contradict each other
-   Cloud services and their properties

<table border="2" cellspacing="0" cellpadding="6" rules="groups" frame="hsides">


<colgroup>
<col  class="org-left" />

<col  class="org-left" />
</colgroup>
<thead>
<tr>
<th scope="col" class="org-left">Service</th>
<th scope="col" class="org-left">Properties it guarantees</th>
</tr>
</thead>

<tbody>
<tr>
<td class="org-left">Memcached</td>
<td class="org-left">No special guarantees</td>
</tr>


<tr>
<td class="org-left">Google GFS</td>
<td class="org-left">File is current if locked</td>
</tr>


<tr>
<td class="org-left">BigTable</td>
<td class="org-left">Shared key-value pair with consistent properties</td>
</tr>


<tr>
<td class="org-left">Dynamo</td>
<td class="org-left">Amazon shopping cart eventual convergence</td>
</tr>


<tr>
<td class="org-left">Databases</td>
<td class="org-left">Snapshot isolation</td>
</tr>


<tr>
<td class="org-left">MapReduce</td>
<td class="org-left">functional compute model w/ strong guarantee</td>
</tr>


<tr>
<td class="org-left">Zookeeper</td>
<td class="org-left">Yahoo! file system, sophisticated properties</td>
</tr>


<tr>
<td class="org-left">PNUTS</td>
<td class="org-left">Yahoo! database, shared data, consistency options</td>
</tr>


<tr>
<td class="org-left">Chubby</td>
<td class="org-left">locking services, strong guarantees</td>
</tr>
</tbody>
</table>

-   Conclusions:
    -   Notice that services&#x2026;
        -   most of them cost 10's or 100's of MILLIONS to create..
        -   huge investment upfront
        -   i.e. Oracle has billions invested..
    -   CAP isn't about telling ORACLE how to build a database product&#x2026;
        -   CAP is a warning to YOU that strong properties CAN easily lead to SLOW services
        -   but thinking in terms of WEAK properties is often SUCCESSFUL strategy that yields good solutions requiring less effort


<a id="orge3ef5e5"></a>

### DONE Assignment: CAP Theroem Reading Notes

1.  [X] Spanner, TrueTime & CAP &#x2026;
    1.  Read & Review
2.  [X] CAP 12 years later&#x2026;
    1.  Read & Review
3.  [X] Submit summary


<a id="org076ff3f"></a>

## Section 3<sub>2</sub>


<a id="orgf9f4710"></a>

### TODO 3<sub>2</sub><sub>1</sub> [C]onsistency

-   Tiers:
    clouds have tiers, levels.
    -   tier 1: lightweight, responsive, web based, also route or handle some services
    -   tier 2: key value pair. stores / caches credentials and authorizations.
    -   tier (inner): online services that handle requests not handled in the first tier.  persistent files, transactional services, shielded from load though.
    -   tier (backend): running offline services, indexing web overnight, updates, scheduled loads,
-   Replication:
    -   core feature of cloud
    -   to handle more work, make more copies
    -   if load increases, make more copies&#x2026;
    -   if load decreases, kill redundant duplicates&#x2026;
    -   load balancing: spread requests over the duplicated nodes
-   Things we can replicate in the cloud:
    -   Files / Storage
        -   compare "write once" data (images, photos) to evolving data (spreadsheets, inventory, logs, etc)
    -   Computation
        -   replicate a single request and distribute it across the duplicated nodes to share comp load
    -   not just FASTER, also more FAULT TOLERANT
-   Things to "MAP" in REPLICATION
    -   data
    -   fault tolerant req processing
    -   coordination and syncronization
    -   parameters & configuration data
    -   security keys and credentials
    -   user / group / membership information (like AD, GPO)
-   ..back to CONSISTENCY
    -   want REPLICATED data to behave in CONSISTENT manner
    -   an INCONSISTENT service appears as BROKEN
    -   DIFFICULT CHALLENGE, how to get many copies to act like just one??
-   IMPLEMENTATION
    -   need a 'reference' system, some kind of MASTER copy
-   DANGERS of INCONSISTENCY
    -   lack of TRUST
    -   when to trust "weak" or "best effort" consistency?
    -


<a id="org42ddda2"></a>

### TODO 3<sub>2</sub><sub>2</sub> Distributed Systems

-   

-   

-   

-   


<a id="org0fda68f"></a>

### TODO 3<sub>2</sub><sub>3</sub> Two Phase Commit


<a id="org0a358b2"></a>

### TODO QUIZ 3.2


<a id="org2e06d10"></a>

## Section 3<sub>3</sub>


<a id="orgec3553a"></a>

### TODO 3<sub>3</sub><sub>1</sub> Byzantine Failures


<a id="org9eb80ec"></a>

### TODO 3<sub>3</sub><sub>2</sub> Examples of Failure Modes


<a id="org42953c7"></a>

### TODO 3<sub>3</sub><sub>3</sub> Synchronous and Asynchronous Execution


<a id="org94a5409"></a>

### TODO 3<sub>3</sub><sub>4</sub> Data Partioning


<a id="orgdbde44e"></a>

### TODO QUIZ 3.3


<a id="org717a75d"></a>

## Section 3<sub>4</sub>


<a id="org75003b7"></a>

### TODO 3<sub>4</sub><sub>1</sub>


<a id="orgfe8842d"></a>

### TODO 3<sub>4</sub><sub>2</sub>


<a id="org8a2595c"></a>

### TODO 3<sub>4</sub><sub>3</sub>


<a id="orgbd48fac"></a>

### TODO 3<sub>4</sub><sub>4</sub>


<a id="orgdaa4add"></a>

### TODO 3<sub>4</sub><sub>5</sub>


<a id="org7204449"></a>

### TODO Reading Assignment: DYNAMO


<a id="org89ec9d3"></a>

## TODO Homework #2


<a id="org65b3074"></a>

# Module 4


<a id="org0ef6d12"></a>

# Module 5

