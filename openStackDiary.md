
# Table of Contents

1.  [HW 1](#org3a4b560)
2.  [Roadmap](#org1996482)
3.  [Envrionment Installation Journal](#org7c0f52b)
    1.  [Pre-install Tests / Notes](#org0913531)
        1.  [Trial / Test VM's <code>[6/6]</code>](#orge542e32)
        2.  [General Notes:](#org7be608c)
        3.  [Hypervisor Install Notes](#org4885c1a)
        4.  [Home Lab Config Notes:](#orgf4a8e8a)
        5.  [Environment Install Task List / YOGA / UBUNTU (1 VM per host method)](#org19f04e2)
    2.  [Environment Install Footnotes](#orgfef0dec)
4.  [Project(s) Installation Journal](#orgc13f63d)
    1.  [Projects(s) Install Task List / YOGA / UBUNTU](#orgc10ed89)
        1.  [Keystone: Install <code>[6/6]</code>](#orgd5be1aa)
        2.  [Keystone: HW RESULTS <code>[4/4]</code>](#org1fb13c8)
        3.  [Glance: Install (on controller) <code>[10/10]</code>](#org5a92298)
        4.  [Glance: HW RESULTS <code>[2/2]</code>](#org6951912)
        5.  [Placement: Install <code>[4/4]</code>](#org42d0c4e)
        6.  [Placement: HW RESULTS <code>[1/1]</code>](#orgc611240)
        7.  [Nova: Install <code>[3/3]</code>](#org601c2cc)
        8.  [Nova: HW RESULTS <code>[3/3]</code>](#org04193e5)
        9.  [Neutron: Install <code>[3/3]</code>](#org5986b32)
        10. [Neutron: HW RESULTS <code>[1/1]</code>](#orgedb4cea)
        11. [Horizon: Install <code>[3/3]</code>](#org622321b)
        12. [Horizon: HW RESULTS <code>[2/2]</code>](#org6a7963c)
        13. [Cinder: Install <code>[2/2]</code>](#org5be6c8d)
        14. [Cinder: HW RESULTS <code>[0/2]</code>](#org53ba3a3)
        15. [Swift: Install <code>[5/5]</code>](#org3fdc5ae)
        16. [Swift: HW RESULTS <code>[1/2]</code>](#orgb0ddb4c)



<a id="org3a4b560"></a>

# HW 1

Set up OpenStack, see Mod 1 rubric


<a id="org1996482"></a>

# Roadmap

1.  Environment Installation
    1.  Security
    2.  Host Networking
    3.  NTP
    4.  Package Archives
    5.  SQL
    6.  Message Queue
    7.  Memcached
    8.  Etcd
2.  Projects Installation
    1.  Keystone
    2.  Glance
    3.  Placement
    4.  Nova
    5.  Neutron
    6.  Horizon
    7.  Cinder


<a id="org7c0f52b"></a>

# Envrionment Installation Journal


<a id="org0913531"></a>

## Pre-install Tests / Notes


<a id="orge542e32"></a>

### DONE Trial / Test VM's <code>[6/6]</code>

-   [X] Install a HyperVisor (VMware / esxi)
-   [X] Create multiple VM's for OpenStack Components
    -   [X] CPU = 6 Cores
    -   [X] RAM = 6 GB
    -   [X] <del>HDD = 200 GB</del>
-   [X] DO NOT USE AUTODEPLOY TOOLS
-   [X] Take Screenshots for steps, attach here in journal
-   [X] Collect information for use in publishing as a report
-   [X] Create a references section for external resources, links


<a id="org7be608c"></a>

### General Notes:

-   Use Yoga Install Instructions <https://docs.openstack.org/swift/yoga/install/>
-   Use minimal install version of OS (Ubuntu 20.0.4)
-   Use 64bit version of OS
-   Build Ea Host as it's own VM.  Can take snapshots, rollbacks, etc.
    (note that many vm's WILL have reduced performance as number of VMs increases)


<a id="org4885c1a"></a>

### Hypervisor Install Notes

-   Installed on HP ProLiant MicroServer, 4 TB, 32GB Ram
-   Balance min requirements per vm host comparing Ubuntu min req's and OpenStack min Req's, if room, install each service on sep host.
-   Build template vm and then replcate for each service, make edits as needed (#of nics, # of cores, etc)
-   Per yoga install&#x2026; controller node: 1 core, 4GB ram, 5GB hdd
-   per yoga install&#x2026; compute node:1 core, 2gb ram, 10GB hdd
-   Ubuntu lts server&#x2026; 2 core, 4gb ram, 25gb hdd
-   template build&#x2026;. 2 core, 6gb ram, 40 gb hdd, 2 NIC
    ![img](./img/environment000setup(12)-small.png)

---


<a id="orgf4a8e8a"></a>

### Home Lab Config Notes:

-   Hypervisor (HVS): HP Proliant Microserver Gen10, 4tb, 32gb ram, 4 NICS,
-   Router (RTR): pfSense Firewall / Router, 4 NICS (WAN,LAN,OPT1,OTP2),
    -   WAN : ISP
    -   LAN: CLASS C 192.168.1.1/24
    -   OPT1: CLASS A 10.0.0.1/24 DHCP4=FALSE
    -   OPT2: CLASS C 203.0.113.1/24 DHCP4=TRUE
-   Physical Network
    -   RTR igb0 <-> ISP
    -   HVS igb0 <-> RTR igb1
    -   HVS igb1  X
    -   HVS igb2 <-> RTR igb2
    -   HVS igb3 <-> RTR igb3
-   Virtual Network
    -   vSwitch1 = management network <-> HVS igb2
    -   vSwitch2 = provider network <-> HVS igb3
        ![img](./img/environment000setup(13)-small.png)

---


<a id="org19f04e2"></a>

### DONE Environment Install Task List / YOGA / UBUNTU (1 VM per host method)

-   [X] 5.1 <span class="underline">Security</span> (Preconfigure VM's) <code>[5/5]</code>
    (specs from testing above, using HP Proliant Microserver & ESXI 7.0)
    -   [X] CPU = 2 cores
    -   [X] RAM = 4 GB
    -   [X] HDD = 40 GB
    -   [X] NICs = 2x
    -   [X] 5x Instances
        -   [X] 'controller'
        -   [X] 'compute1'
        -   [X] 'block1'
        -   [X] 'object1'
        -   [X] 'object2'
-   [ ] <span class="underline">SNAPSHOTS</span> (baremetal)
-   [X] 5.2 <span class="underline">Host Networking</span> <code>[6/6]</code>
    -   [X] 'controller'<code>[3/3]</code>
        -   [X] Management NIC : 10.0.0.11/24, gw:10.0.0.1
        -   [X] Provider NIC  : via netplan, set dhcp4 & dhcp6 false, do not set static ip
        -   [X] Edit etc/hosts: see pg 20 in pdf version of install docs
    -   [X] 'compute1'<code>[3/3]</code>
        -   [X] Management NIC : 10.0.0.31/24, gw:10.0.0.1
        -   [X] Provider NIC : via netplan, set dhcp4 & dhcp6 false, do not set static ip
        -   [X] Edit etc/hosts: see pg 22 in pdf version of install docs
    -   [X] 'block1'<code>[2/2]</code>
        -   [X] Management NIC : 10.0.0.41/24, gw:10.0.0.1
        -   [X] Edit etc/hosts: see pg 23 in pdf version of install docs
    -   [X] Confirm Connectivity: <code>[7/7]</code>
        -   [X] from @controller, ping -c 4 docs.openstack.org == PASS
        -   [X] from @controller, ping -c 4 compute1
        -   [X] from @compute, ping -c 4 openstack.org
        -   [X] from @compute, ping -c 4 controller
        -   [X] repeat ping from @block1
        -   [X] repeat ping from @object1
        -   [X] repeat ping from @object2
            ![img](./img/environment000setup(9)-small.png)
    -   [X] 'object1'
    -   [X] 'object2'
-   [X] 5.3 <span class="underline">NTP</span> <code>[3/3]</code>
    -   [X] Controller Node
    -   [X] Other Nodes
    -   [X] Verify
-   [ ] <span class="underline">SNAPSHOTS</span> (post-NTP, pre-package install)
-   [X] 5.4 <span class="underline">Package Archives</span> (repeat on all nodes) <code>[1/1]</code>
    -   [X] Enable Repository / Ubuntu 20.04 / Yoga
-   [X] <span class="underline">SQL</span> (on controller) <code>[3/3]</code>
    -   [X] Install Package
    -   [X] Create & Edit config file
    -   [X] Finalize
-   [X] <span class="underline">Message Queue</span> (on controller) <code>[3/3]</code>
    -   [X] Install Package
    -   [X] Add openstack user
    -   [X] Permit config, write, & read access for user
-   [X] <span class="underline">Memcached</span> (on controller) <code>[3/3]</code>
    -   [X] Install package (python3 version)
    -   [X] edit config file
    -   [X] Finalize (start service)
-   [X] <span class="underline">Etcd</span> (on controller) <code>[2/2]</code>
    -   [X] Install Package
    -   [X] edit config files
        ![img](./img/environment000setup(11)-small.png)

---


<a id="orgfef0dec"></a>

## Environment Install Footnotes

-   From <https://docs.openstack.org/install-guide/environment-networking.html> :

> The example architectures assume use of the following networks:
> <span class="underline">Management on 10.0.0.0/24 with gateway 10.0.0.1</span>
> This network requires a gateway to provide Internet access to all nodes for administrative purposes such as package installation, security updates, DNS, and NTP.
> <span class="underline">Provider on 203.0.113.0/24 with gateway 203.0.113.1</span>
> This network requires a gateway to provide Internet access to instances in your OpenStack environment.
> You can modify these ranges and gateways to work with your particular network infrastructure.
> Network interface names vary by distribution. Traditionally, interfaces use eth followed by a sequential number. To cover all variations, this guide refers to the first interface as the interface with the lowest number and the second interface as the interface with the highest number.
>  Note
> Ubuntu has changed the network interface naming concept. Refer Changing Network Interfaces name Ubuntu 16.04.
> Unless you intend to use the exact configuration provided in this example architecture, you must modify the networks in this procedure to match your environment. Each node must resolve the other nodes by name in addition to IP address. <span class="underline">For example, the controller name must resolve to 10.0.0.11, the IP address of the management interface on the controller node.</span>

-   <span class="timestamp-wrapper"><span class="timestamp">&lt;2023-03-30 Thu&gt; </span></span> NOTE: Installation Guide / Controller Node / Configure Network Interfaces&#x2026;
    Documentation refers to old legacy method of network config using networkinterfaces.  Since Ubuntu 20.04 use /etc/netplan, not /etc/network/interfaces

     1  $ cat /etc/netplan/00-installer-config.yaml
     2  # This is the network config written by 'subiquity'
     3  network:
     4    ethernets:
     5      ens160:
     6        addresses:
     7          - 10.0.0.11/24
     8        gateway4: 10.0.0.1
     9        nameservers:
    10                addresses: [8.8.8.8, 1.1.1.1]
    11      ens192:
    12        dhcp4: false
    13        dhcp6: false
    14    version: 2

-   Be sure that both /etc/hosts and /etc/hostname have the corect names.
-   If all is working, should be able to SSH to host (i.e. 10.0.0.11) and when logged in host name will display correctly in terminal

-   <span class="timestamp-wrapper"><span class="timestamp">&lt;2023-03-30 Thu&gt; </span></span> NOTE: Archive Enablement:
    using OpenStack Yoga for Ubuntu 20.04 LTS (server 64bit)
    -   add-apt-repository cloud-archive:yoga

---

---


<a id="orgc13f63d"></a>

# Project(s) Installation Journal


<a id="orgc10ed89"></a>

## TODO Projects(s) Install Task List / YOGA / UBUNTU


<a id="orgd5be1aa"></a>

### DONE Keystone: Install <code>[6/6]</code>

-   REF: Projects Install Doc / Yoga / Keystone ([link](https:docs.openstack.org/keystone/yoga/doc-keystone.pdf))
-   TARGET(S): controller
-   USER: root (either 'sudo -i'  or 'su -')
-   [X] **Initialize SQL**

    1  # mysql
    2  MariaDB > CREATE DATABASE keystone;
    3  MariaDB > GRANT ALL PRIVILEGES ON keystone.* TO 'keystone'@'localhost' IDENTIFIED BY 'pwd123';
    4  MariaDB > GRANT ALL PRIVILEGES ON keystone.* TO 'keystone'@'%' IDENTIFIED BY 'pwd123';  replace dbpass with password

![img](./img/service010keystone(0)-small.png)

-   NOTE: A good test here would be to exit root (#), and as user ($) try to access the database.  If you get 1045 errors, that indicates an authentication problem and the rest of the process will fail until authentication is working.  When done testing from user, remember to return to root for remainder of process.  If the below does not produce a connection to SQL, stop and troubleshoot.
-   [X] **Test SQL Connection**
    
        1  $ mysql -u keystone -p
        2  MariaDB [(none)]>

-   [X] **Instlal Kestone Package**

    1  # apt install keystone
    2  # vi /etc/keystone/keystone.conf (make edits per docs)
    3  # su -s /bin/sh -c "keystone-manage db_sync" keystone

-   [X] **Initialize Repositories**

    1  # keystone-manage fernet_setup --keystone-user keystone --keystone-group keystone
    2  # keystone-manage credential_setup --keystone-user keystone --keystone-group keystone

-   [X] **Bootstrap ID service**

    1  # keystone-manage bootstrap --bootstrap-password pwd123 --bootstrap-admin-url http://controller:5000/v3/ --bootstrap-internal-url http://controller:5000/v3/ --bootstrap-public-url http://controller:5000/v3/ --bootstrap-region-id RegionOne 

-   [X] **Edit Env Variables**

    1  $ export OS_USERNAME=admin
    2  $ export OS_PASSWORD=ADMIN_PASS
    3  $ export OS_PROJECT_NAME=admin
    4  $ export OS_USER_DOMAIN_NAME=Default
    5  $ export OS_PROJECT_DOMAIN_NAME=Default
    6  $ export OS_AUTH_URL=http://controller:5000/v3
    7  $ export OS_IDENTITY_API_VERSION=3

![img](./img/service010keystone(2)-small.png)

-   NOTE: Before doing the above, do a '$ printenv' and look at the environment variables.  There should already be populated a number of OS\_ (openstack) entries.  If not, it may mean that the bootstraping commands did not complete correctly.  This happened to me.  After backing up and going through the bootstrapping commands again I found 5 of the 7 above env variables already in print env.  After adding the missing two, the rest of the process ran correctly.


<a id="org1fb13c8"></a>

### DONE Keystone: HW RESULTS <code>[4/4]</code>

-   [X] **Confirm Token Assignment**

     1  +------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
     2  | Field      | Value
     3           |
     4  +------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
     5  | expires    | 2023-04-03T21:10:00+0000
     6           |
     7  | id         | gAAAAABkKzKY1kcGmTmr2azLTezITAUGLjV7a_N_t90aZRQvr-lF7I0Oo3mq7sbeYBmKVEa_3rqiKuZipSpm_TMRKzObbF7yl_lup9-VkYmvl3_daPTAT5MDxrr_qHPqF0vl2TQMBZYA1we_-_RVnrUuHzPw9BR71TUXFiote79KFPSzxXkt7Es |
     8  | project_id | af55244dfe134e73bb68d80af4842abb
     9           |
    10  | user_id    | 483616691ea84ae3936b9cadd1725b4f
    11           |
    12  +------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

-   [X] **Confirm demo (myuser) and admin users are created**

     1  $ openstack --os-auth-url http://controller:5000/v3 \
     2  > --os-project-domain-name Default --os-user-domain-name Default \
     3  > --os-project-name admin --os-username admin token issue
     4  Password:
     5  +------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
     6  | Field      | Value
     7           |
     8  +------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
     9  | expires    | 2023-04-03T21:10:00+0000
    10           |
    11  | id         | gAAAAABkKzKY1kcGmTmr2azLTezITAUGLjV7a_N_t90aZRQvr-lF7I0Oo3mq7sbeYBmKVEa_3rqiKuZipSpm_TMRKzObbF7yl_lup9-VkYmvl3_daPTAT5MDxrr_qHPqF0vl2TQMBZYA1we_-_RVnrUuHzPw9BR71TUXFiote79KFPSzxXkt7Es |
    12  | project_id | af55244dfe134e73bb68d80af4842abb
    13           |
    14  | user_id    | 483616691ea84ae3936b9cadd1725b4f
    15           |
    16  +------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
    17  
    18  sgc@controller:~$ openstack --os-auth-url http://controller:5000/v3 \
    19  > --os-project-domain-name Default --os-user-domain-name Default \
    20  > --os-project-name myproject --os-username myuser token issue
    21  Password:
    22  +------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
    23  | Field      | Value
    24           |
    25  +------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
    26  | expires    | 2023-04-03T21:14:47+0000
    27           |
    28  | id         | gAAAAABkKzO3m0xEVmt5KXdpNRarHdbsQKu_R3Kvl_vsl_Qj4zLRd1sKbFmj6hLiImTpjfF2drCIqH0-NRIUfPKERlTJcj9k-1-Lw8W5b94eeDWs-m77VlXJLcpIjGiSehIM4TDhYqYuWmu4r_zs_OH5v3CllqhdtpV9HuMOku5jID5Ytf4YiPM |
    29  | project_id | 9e2b1df7e13e4e90a1dfe3d12e96374e
    30           |
    31  | user_id    | 2e7b44d196454070a7f6da6d66b61b5a
    32           |
    33  +------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

![img](./img/service010keystone(7)-small.png)

-   [X] **Confirm user list can be retrieved**

    1  MariaDB [keystone]> SELECT * FROM user
    2      -> ;
    3  +----------------------------------+-------+---------+--------------------+---------------------+----------------+-----------+
    4  | id                               | extra | enabled | default_project_id | created_at          | last_active_at | domain_id |
    5  +----------------------------------+-------+---------+--------------------+---------------------+----------------+-----------+
    6  | 2e7b44d196454070a7f6da6d66b61b5a | {}    |       1 | NULL               | 2023-04-03 20:05:06 | NULL           | default   |
    7  | 483616691ea84ae3936b9cadd1725b4f | {}    |       1 | NULL               | 2023-04-03 19:55:11 | NULL           | default   |
    8  +----------------------------------+-------+---------+--------------------+---------------------+----------------+-----------+
    9  2 rows in set (0.000 sec)

-   [X] **Confirm role list can be retrieved**

     1  MariaDB [keystone]> SELECT * FROM role;
     2  +----------------------------------+--------+-------+-----------+-------------+
     3  | id                               | name   | extra | domain_id | description |
     4  +----------------------------------+--------+-------+-----------+-------------+
     5  | 0b25f16d85fa4fcdbbf560c8776b009c | admin  | {}    | <<null>>  | NULL        |
     6  | 27490b2ef72343719edaad6ef2d3baa6 | myrole | {}    | <<null>>  | NULL        |
     7  | 53a2975840ca44d1876980c8267a1c1b | member | {}    | <<null>>  | NULL        |
     8  | 78965140ce3941b7806c809bdabe86e8 | reader | {}    | <<null>>  | NULL        |
     9  +----------------------------------+--------+-------+-----------+-------------+
    10  4 rows in set (0.001 sec)
    11  
    12  MariaDB [keystone]>

---


<a id="org5a92298"></a>

### DONE Glance: Install (on controller) <code>[10/10]</code>

-   [X] **DB Configuration**
    
        1  # mysql
        2  MariaDB [(none)] CREATE DATABASE glance;

-   [X] Source the admin credentials (./os-scripts/) `$ . admin-openrc`
-   [X] Create the `glance` user
    
         1  $ cd ~/os-scripts
         2  $ openstack user create --domain default --password-prompt glance
         3  User Password:
         4  Repeat User Password:
         5  +---------------------+----------------------------------+
         6  | Field               | Value                            |
         7  +---------------------+----------------------------------+
         8  | domain_id           | default                          |
         9  | enabled             | True                             |
        10  | id                  | 5e99d020af48473da06c73a4ce96e50a |
        11  | name                | glance                           |
        12  | options             | {}                               |
        13  | password_expires_at | None                             |
        14  +---------------------+----------------------------------+
-   [X] Add the admin role to the glance user and service project
    
        1  $ openstack role add --project service --user glance admin
-   [X] Create the glance service entry
    
        1  $ openstack service create --name glance \
        2  $ --description "OpenStack Image" image
-   [X] Create the Image Service API
    
        1  $ openstack endpoint create --region RegionOne \
        2  $ image public http://controller:9292

![img](./img/service020glance(0)-small.png)

-   [X] Install glance packages
    
        1  # apt install glance
-   [X] Make edits to `/etc/glance/glance-api.conf`
    -   Online documentation is does not match conf file installed via steps above.
    -   [oslo<sub>limit</sub>] section was missing but may not matter, not doing quota's
    -   `use_keystone_quotas` is now `use_keystone_limits`, but no impact, left default false.
-   [X] Populate Image service database and restart service
    
        1  # su -s /bin/sh -c "glance-manage db_sync" glance
        2  # service glance-api restart
-   [X] Verify Operation (see doc [link](https://docs.openstack.org/glance/yoga/install/verify.html))


<a id="org6951912"></a>

### DONE Glance: HW RESULTS <code>[2/2]</code>

-   [X] HW Glance 1: Import Cirros OS Image

     1    $ glance image-create --name "cirros" \
     2  > --file cirros-0.4.0-x86_64-disk.img \
     3  > --disk-format qcow2 --container-format bare \
     4  > --visibility=public
     5  +------------------+----------------------------------------------------------------------------------+
     6  | Property         | Value                                                                            |
     7  +------------------+----------------------------------------------------------------------------------+
     8  | checksum         | 443b7623e27ecf03dc9e01ee93f67afe                                                 |
     9  | container_format | bare                                                                             |
    10  | created_at       | 2023-04-04T01:24:37Z                                                             |
    11  | disk_format      | qcow2                                                                            |
    12  | id               | 25c894f6-fe98-4da3-a8d9-89ef27508d46                                             |
    13  | min_disk         | 0                                                                                |
    14  | min_ram          | 0                                                                                |
    15  | name             | cirros                                                                           |
    16  | os_hash_algo     | sha512                                                                           |
    17  | os_hash_value    | 6513f21e44aa3da349f248188a44bc304a3653a04122d8fb4535423c8e1d14cd6a153f735bb0982e |
    18  |                  | 2161b5b5186106570c17a9e58b64dd39390617cd5a350f78                                 |
    19  | os_hidden        | False                                                                            |
    20  | owner            | af55244dfe134e73bb68d80af4842abb                                                 |
    21  | protected        | False                                                                            |
    22  | size             | 12716032                                                                         |
    23  | status           | active                                                                           |
    24  | tags             | []                                                                               |
    25  | updated_at       | 2023-04-04T01:24:37Z                                                             |
    26  | virtual_size     | 46137344                                                                         |
    27  | visibility       | public                                                                           |
    28  +------------------+----------------------------------------------------------------------------------+
    29  sgc@controller:~$

![img](./img/service020glance(3)-small.png)

-   [X] HW Glance 2: Retrieve Image List

    1    $ glance image-list
    2  +--------------------------------------+--------+
    3  | ID                                   | Name   |
    4  +--------------------------------------+--------+
    5  | 25c894f6-fe98-4da3-a8d9-89ef27508d46 | cirros |
    6  +--------------------------------------+--------+

![img](./img/service020glance(2)-small.png)

---


<a id="org42d0c4e"></a>

### DONE Placement: Install <code>[4/4]</code>

-   [X] Create Database <code>[1/1]</code>
    -   [X] &#x2026; MySQL
        
            MariaDB [(none)]> CREATE DATABASE placement;
            Query OK, 1 row affected (0.000 sec)
            MariaDB [(none)]> GRANT ALL PRIVILEGES ON placement.* TO 'placement'@'localhost' \
                -> IDENTIFIED BY 'pwd123';
            Query OK, 0 rows affected (0.000 sec)
            MariaDB [(none)]> GRANT ALL PRIVILEGES ON placement.* TO 'placement'@'%' \
                -> IDENTIFIED BY 'pwd123';
            Query OK, 0 rows affected (0.001 sec)
            MariaDB [(none)]>
-   [X] Configure Access (placement password 'pwd123') <code>[4/4]</code>
    -   [X] Create placement service user
        
            $ . admin-openrc
            $ openstack user create --domain default --password-prompt placement
            User Password:
            Repeat User Password:
            +---------------------+----------------------------------+
            | Field               | Value                            |
            +---------------------+----------------------------------+
            | domain_id           | default                          |
            | enabled             | True                             |
            | id                  | 40bc9dd8e8cc497482a2101cfb6fafb1 |
            | name                | placement                        |
            | options             | {}                               |
            | password_expires_at | None                             |
            +---------------------+----------------------------------+
            sgc@controller:~/os-scripts$
    -   [X] Add placement user to project with admin role
        
            $ openstack role add --project service --user placement admin
    -   [X] Create the placement API entry in the service catalog:
        
            $ openstack service create --name placement --description "Placement API" placement
            +-------------+----------------------------------+
            | Field       | Value                            |
            +-------------+----------------------------------+
            | description | Placement API                    |
            | enabled     | True                             |
            | id          | 37eca454070c402aa6b9851f5259d263 |
            | name        | placement                        |
            | type        | placement                        |
            +-------------+----------------------------------+
    -   [X] Create the Placement API service endpoints:
        
            $ openstack endpoint create --region RegionOne placement public http://controller:8778
            $ openstack endpoint create --region RegionOne placement internal http://controller:8778
            $ openstack endpoint create --region RegionOne placement admin http://controller:8778
    -   Output:
        
            +--------------+----------------------------------+
            | Field        | Value                            |
            +--------------+----------------------------------+
            | enabled      | True                             |
            | id           | f566771fd27c4093a2f37af9b0aa876c |
            | interface    | public                           |
            | region       | RegionOne                        |
            | region_id    | RegionOne                        |
            | service_id   | 37eca454070c402aa6b9851f5259d263 |
            | service_name | placement                        |
            | service_type | placement                        |
            | url          | http://controller:8778           |
            +--------------+----------------------------------+
            
            +--------------+----------------------------------+
            | Field        | Value                            |
            +--------------+----------------------------------+
            | enabled      | True                             |
            | id           | 6791ffa5a75544d3af6e0474b678f345 |
            | interface    | internal                         |
            | region       | RegionOne                        |
            | region_id    | RegionOne                        |
            | service_id   | 37eca454070c402aa6b9851f5259d263 |
            | service_name | placement                        |
            | service_type | placement                        |
            | url          | http://controller:8778           |
            +--------------+----------------------------------+
            
            +--------------+----------------------------------+
            | Field        | Value                            |
            +--------------+----------------------------------+
            | enabled      | True                             |
            | id           | 58884a5d851141f5bea62d1af92ce83a |
            | interface    | admin                            |
            | region       | RegionOne                        |
            | region_id    | RegionOne                        |
            | service_id   | 37eca454070c402aa6b9851f5259d263 |
            | service_name | placement                        |
            | service_type | placement                        |
            | url          | http://controller:8778           |
            +--------------+----------------------------------+
-   [X] Install and Configure Components <code>[3/3]</code>
    -   [X] Install placement and required database libraries (requires pip package)
        
            # pip install openstack-placement pymysql
    -   [X] Create and edit /etc/placement/placement.conf
        
            # mkdir /etc/placement
            # touch /etc/placement/placement.conf
            # vi /etc/placement/placement.conf
            (... make edits per docs ...)
        
        -   **WARNING: IN ABOVE, YOU MUST REMOVE THE TEXT " # use noauth2 if not using keystone"**
    -   [X] Populate the placement database
-   [X] Finalize Installation
    ![img](./img/service030placement(0)-small.png)


<a id="orgc611240"></a>

### DONE Placement: HW RESULTS <code>[1/1]</code>

-   [X] N/A, no placement resulst for HW required.

---


<a id="org601c2cc"></a>

### DONE Nova: Install <code>[3/3]</code>

NOTE: Nova installation will require steps done on both 'controller' and 'compute1'
NOTE: Nova installation will include the following services:

1.  `nova-api` service
2.  `nova-api-metadata` service
3.  `nova-computer` service
4.  `nova-scheduler` service
5.  `nova-conductor` module
6.  `nova-novncproxy` daemon
7.  `nova-spicehtml5proxy` daemon
8.  the queue (RammitMQ)
9.  SQL database

1.  DONE Controller Node: Prerequisites (doc 3.2.1.3) <code>[8/8]</code>

    1.  [X] Create Database(s)
        
            MariaDB [(none)]> CREATE DATABASE nova_api;
            Query OK, 1 row affected (0.000 sec)
            
            MariaDB [(none)]> CREATE DATABASE nova;
            Query OK, 1 row affected (0.001 sec)
            
            MariaDB [(none)]> CREATE DATABASE nova_cell0;
            Query OK, 1 row affected (0.000 sec)
            
            MariaDB [(none)]> GRANT ALL PRIVILEGES ON nova_api.* TO 'nova'@'localhost' IDENTIFIED BY 'pwd123';
            Query OK, 0 rows affected (0.023 sec)
            
            MariaDB [(none)]> GRANT ALL PRIVILEGES ON nova_api.* TO 'nova'@'%' IDENTIFIED BY 'pwd123';
            Query OK, 0 rows affected (0.001 sec)
            
            MariaDB [(none)]> GRANT ALL PRIVILEGES ON nova.* TO 'nova'@'localhost' IDENTIFIED BY 'pwd123';
            Query OK, 0 rows affected (0.001 sec)
            
            MariaDB [(none)]> GRANT ALL PRIVILEGES ON nova.* TO 'nova'@'%' IDENTIFIED BY 'pwd123';
            Query OK, 0 rows affected (0.001 sec)
            
            MariaDB [(none)]> GRANT ALL PRIVILEGES ON nova_cell0.* TO 'nova'@'localhost' IDENTIFIED BY 'pwd123';
            Query OK, 0 rows affected (0.000 sec)
            
            MariaDB [(none)]> GRANT ALL PRIVILEGES ON nova_cell0.* TO 'nova'@'%' IDENTIFIED BY 'pwd123';
            Query OK, 0 rows affected (0.001 sec)
            
            MariaDB [(none)]> exit
    2.  [X] refresh admin credentials
    3.  [X] Create Compute Service credentials
        `$ openstack user create --domain default --password-prompt nova`
        
            User Password:
            Repeat User Password:
            +---------------------+----------------------------------+
            | Field               | Value                            |
            +---------------------+----------------------------------+
            | domain_id           | default                          |
            | enabled             | True                             |
            | id                  | 5265a363fa7448d28fb3dbeb3e207f41 |
            | name                | nova                             |
            | options             | {}                               |
            | password_expires_at | None                             |
            +---------------------+----------------------------------+
        
        `$ openstack role add --project service --user nova admin`
    4.  [X] Create Compute API service endpoints
    5.  [X] `openstack endpoint create --region RegionOne compute public http://controller:8774/v2.1`
    6.  [X] `openstack endpoint create --region RegionOne compute internal http://controller:8774/v2.1`
    7.  [X] `openstack endpoint create --region RegionOne compute admin http://controller:8774/v2.1`
    8.  OUTPUT:
        
            +--------------+----------------------------------+
            | Field        | Value                            |
            +--------------+----------------------------------+
            | enabled      | True                             |
            | id           | c5095a0dbe6042129e5c16fe7aea8a2b |
            | interface    | public                           |
            | region       | RegionOne                        |
            | region_id    | RegionOne                        |
            | service_id   | 5c50e287f96c40a69a6f17c7153631ff |
            | service_name | nova                             |
            | service_type | compute                          |
            | url          | http://controller:8774/v2.1      |
            +--------------+----------------------------------+
            
            +--------------+----------------------------------+
            | Field        | Value                            |
            +--------------+----------------------------------+
            | enabled      | True                             |
            | id           | 037ca65f5b494c6691037e0ecde56810 |
            | interface    | internal                         |
            | region       | RegionOne                        |
            | region_id    | RegionOne                        |
            | service_id   | 5c50e287f96c40a69a6f17c7153631ff |
            | service_name | nova                             |
            | service_type | compute                          |
            | url          | http://controller:8774/v2.1      |
            +--------------+----------------------------------+
            
            +--------------+----------------------------------+
            | Field        | Value                            |
            +--------------+----------------------------------+
            | enabled      | True                             |
            | id           | de4fc9eabb394888af11d21316106a15 |
            | interface    | admin                            |
            | region       | RegionOne                        |
            | region_id    | RegionOne                        |
            | service_id   | 5c50e287f96c40a69a6f17c7153631ff |
            | service_name | nova                             |
            | service_type | compute                          |
            | url          | http://controller:8774/v2.1      |
            +--------------+----------------------------------+
    9.  [X] Install Placement Service (completed prior, see previous section)

2.  DONE Controller Node: Install & Configure Components (doc 3.2.1.3 cont) <code>[8/8]</code>

    1.  [X] Install packages
        `# apt install nova-api nova-conductor nova-novncproxy nova-scheduler`
    2.  [X] Edit /etc/nova/nova.conf
        -   confusing step on [neutron] edits to nova.conf, duplicated in neutron setupd
    3.  [X] Populate `nova-api` database
        `# su-s /bin/sh -c "nova-manage api_db sync" nova`
    4.  [X] Register cell0 database
        `# su -s /bin/sh -c "nova-manage cell_v2 map_cell0" nova`
    5.  [X] create `cell1` cell
        `# su -s /bin/sh -c "nova-manage cell_v2 create_cell --name=cell --verbose" nova`
    6.  [X] Populate the `nova` database
        `# su -s /bin/sh -c "nova-manage db sync" nova`
    7.  [X] Verify nova `cell0` and `cell1` registered correctly
        `#su -s /bin/sh -c "nova-manage cell_v2 list_cells" nova`
    8.  [X] Finalize and restart services
        
            # service nova-api restart
            # service nova-scheduler restart
            # service nova-conductor restart
            # service nova-novncproxy restart

3.  DONE Install and Configure Compute Node (doc 3.2.1.4) <code>[3/3]</code>

    **NOTE: DO THESE STEPS ON THE COMPUTE NODE, NOT THE CONTROLLER NODE**
    **NOTE: to sync admin credential scripts, use SCP to copy ~/os-scripts to target node**
    
    1.  [X] Install packages
    2.  [X] Make edits to /etc/nova/nova.conf (on compute node)
    3.  [X] Finalize


<a id="org04193e5"></a>

### DONE Nova: HW RESULTS <code>[3/3]</code>

-   [X] Screenshot: Retrieve a VM list
    -   Nova was working and I had set up 3 vm's and had logged into 2 of them.  After that Nova crashed and would no longer connect.  I did not get screenshots before the crash.  The VM's were named 'provider-instance', 'provider-instance1', and 'provider-insance2'.  'provider-insance' was on the admin project.  The other two were on the demo project with the user name of 'myuser' and attached to the 'provider' network.

-   [X] Screenshot: Create a VM
    ![img](./img/testVM.png)
-   [X] Screenshot: Login VM
    ![img](./img/nova_cirros.png)

---


<a id="org5986b32"></a>

### DONE Neutron: Install <code>[3/3]</code>

1.  DONE Verifiy connectivity <code>[4/4]</code>

    -   [X] controller to compute1
        
            sgc@controller:~$ ping -c 2 compute1
            PING compute1 (10.0.0.31) 56(84) bytes of data.
            64 bytes from compute1 (10.0.0.31): icmp_seq=1 ttl=64 time=0.121 ms
            64 bytes from compute1 (10.0.0.31): icmp_seq=2 ttl=64 time=0.251 ms
            
            --- compute1 ping statistics ---
            2 packets transmitted, 2 received, 0% packet loss, time 1026ms
            rtt min/avg/max/mdev = 0.121/0.186/0.251/0.065 ms
    -   [X] controller to WAN
    
        sgc@controller:~$ ping -c 2 www.google.com
        PING www.google.com (142.250.217.68) 56(84) bytes of data.
        64 bytes from sea09s29-in-f4.1e100.net (142.250.217.68): icmp_seq=1 ttl=56 time=17.8 ms
        64 bytes from sea09s29-in-f4.1e100.net (142.250.217.68): icmp_seq=2 ttl=56 time=17.3 ms
        
        --- www.google.com ping statistics ---
        2 packets transmitted, 2 received, 0% packet loss, time 1002ms
        rtt min/avg/max/mdev = 17.270/17.544/17.818/0.274 ms
    
    -   [X] compute1 to controller
    
        sgc@compute1:~$ ping -c 2 controller
        PING controller (10.0.0.11) 56(84) bytes of data.
        64 bytes from controller (10.0.0.11): icmp_seq=1 ttl=64 time=0.295 ms
        64 bytes from controller (10.0.0.11): icmp_seq=2 ttl=64 time=0.353 ms
        
        --- controller ping statistics ---
        2 packets transmitted, 2 received, 0% packet loss, time 1003ms
        rtt min/avg/max/mdev = 0.295/0.324/0.353/0.029 ms
    
    -   [X] compute1 to WAN
    
        sgc@compute1:~$ ping -c 2 www.google.com
        PING www.google.com (142.250.69.196) 56(84) bytes of data.
        64 bytes from sea30s08-in-f4.1e100.net (142.250.69.196): icmp_seq=1 ttl=56 time=16.6 ms
        64 bytes from sea30s08-in-f4.1e100.net (142.250.69.196): icmp_seq=2 ttl=56 time=16.2 ms
        
        --- www.google.com ping statistics ---
        2 packets transmitted, 2 received, 0% packet loss, time 1002ms
        rtt min/avg/max/mdev = 16.179/16.399/16.620/0.220 ms
        sgc@compute1:~$

2.  DONE Install and configure controller node <code>[5/5]</code>

    -   [X] Prerequisites (6.2.1) <code>[4/4]</code>
        -   [X] Create Database
            -   `$ mysql -u root -p`
            -   `MariaDB [(none)] CREATE DATABASE neutron;`
            -   `MariaDB [(none)]> GRANT ALL PRIVILEGES ON neutron.* TO 'neutron'@'localhost' \`
                `IDENTIFIED BY 'NEUTRON_DBPASS';`
            -   `MariaDB [(none)]> GRANT ALL PRIVILEGES ON neutron.* TO 'neutron'@'%' \`
                `IDENTIFIED BY 'NEUTRON_DBPASS';`
        -   [X] Re-source admin credentials
            -   `$. ./os-scripts/admin-openrc`
        -   [X] Create service credentials
            -   Create neutron user
                `$ openstack user create --domain default --password-prompt neutron`
            -   Add admin role to neutron user
                `$ openstack role add --project service --user neutron admin`
            -   Create Neutron service entity
                `$ openstack service create --name neutron \ =
                      =--description "OpenStack Networking" network`
        -   [X] Create Networking service API Endpoints
            -   $ `openstack endpoint create --region RegionOne \`
                `network public http://controller:9696`
            -   $ `openstack endpoint create --region RegionOne \`
                `network internal http://controller:9696`
            -   $ `openstack endpoint create --region RegionOne \`
                `network admin http://controller:9696`
    -   [X] Configure Networking Options (6.2.2) <code>[6/6]</code>
        -   Selected Provider Network, see environment notes on homelab
        -   [X] Install components
            
                # apt install neutron-server neutron-plugin-ml2 \
                neutron-linuxbridge-agent neutron-dhcp-agent \
                neutron-metadata-agent
        -   [X] Configure server component
        -   [X] Configure modular layer 2 plug-in
        -   [X] Configure linux bridge agent
        -   [X] Configure DHCP agent
        -   [X] Configure Metadata agent (6.2.3)
    -   [X] Create provider network (not possilbe until neutron is finished?? why in docs?) <code>[3/3]</code>
        -   [X] source credentials
        -   [X] create the network (not possilbe until neutron install is finished??)
            -   OUTPUT:
                
                    sgc@controller:~$ openstack network create  --share --external \
                    >   --provider-physical-network provider \
                    >   --provider-network-type flat provider
                    +---------------------------+--------------------------------------+
                    | Field                     | Value                                |
                    +---------------------------+--------------------------------------+
                    | admin_state_up            | UP                                   |
                    | availability_zone_hints   |                                      |
                    | availability_zones        |                                      |
                    | created_at                | 2023-04-08T20:42:50Z                 |
                    | description               |                                      |
                    | dns_domain                | None                                 |
                    | id                        | 5c3c019c-274b-4c72-8d19-7f1f9b99d4d4 |
                    | ipv4_address_scope        | None                                 |
                    | ipv6_address_scope        | None                                 |
                    | is_default                | None                                 |
                    | is_vlan_transparent       | None                                 |
                    | mtu                       | 1500                                 |
                    | name                      | provider                             |
                    | port_security_enabled     | True                                 |
                    | project_id                | af55244dfe134e73bb68d80af4842abb     |
                    | provider:network_type     | flat                                 |
                    | provider:physical_network | provider                             |
                    | provider:segmentation_id  | None                                 |
                    | qos_policy_id             | None                                 |
                    | revision_number           | 1                                    |
                    | router:external           | External                             |
                    | segments                  | None                                 |
                    | shared                    | True                                 |
                    | status                    | ACTIVE                               |
                    | subnets                   |                                      |
                    | tags                      |                                      |
                    | updated_at                | 2023-04-08T20:42:50Z                 |
                    +---------------------------+--------------------------------------+
                    sgc@controller:~$
        -   [X] create a subnet on the network
            -   OUTPUT:
    -   [X] Configure compute service to use the networking service (6.2.4)
    -   [X] Finalize (6.2.5)

3.  DONE Install and configure compute node <code>[5/5]</code>

    -   [X] Install the components (6.3.1)
        `# apt install neutron-linuxbridge-agent`
    -   [X] Configure the common component (6.3.2)
    -   [X] Configure networking options (6.3.3)
    -   [X] Configure the compute service to use the networking service (6.3.4)
    -   [X] Finalize (6.3.5)


<a id="orgedb4cea"></a>

### DONE Neutron: HW RESULTS <code>[1/1]</code>

-   [X] Screenshot: Create a Network
    ![img](./img/network.png)

---


<a id="org622321b"></a>

### DONE Horizon: Install <code>[3/3]</code>

-   [X] Install packages
    `# apt install openstack-dashboard`
-   [X] Edit /etc/openstack-dashboard/local<sub>settings.py</sub>
-   [X] Append to /etc/apache2/conf-available/openstack-dashboard.conf
-   FOOTNOTE:
    After following the installation instructions, I could not access the horizon dashboard via a browser.  I was testing the web portal from a physical laptop on the same network as the horizon dashboard.  Every time I tried to access it I received HTTP 500 errors.  Trying to access <http://controller/> yielded an Apache2 test page.  Trying to access <http://controller/horizon/> failed.  The error logs in /var/log/apache2/error.log indicated a problem with the code used to disable layer-3 networking in the /openstack/local<sub>settings.py</sub> file.  I removed the code added in order to disable layer-3 networking and the horizon dashboard then loaded correctly.


<a id="org6a7963c"></a>

### DONE Horizon: HW RESULTS <code>[2/2]</code>

-   [X] Login in with proper account (screenshot)
    ![img](./img/service060horizon(3).png)
-   [X] Retrieve service information (screenshot)

![img](./img/service060horizon(2)-small.png)

---


<a id="org5be6c8d"></a>

### TODO Cinder: Install <code>[2/2]</code>

-   [X] Configure 'controller' node <code>[4/4]</code>
    -   [X] Prerequisites <code>[4/4]</code>
        -   [X] Create database & grand access
        -   [X] refresh admin credentials
        -   [X] create service credentials
        -   [X] create service api endpoints
            ![img](./img/service070cinder(0)-small.png)
    -   [X] Install & Configure Components <code>[0/0]</code>
        1.  Install Package(s)
            `#$ apt install cinder-api cinder-scheduler`
        2.  Edit /etc/cinder/cinder.conf
            1.  [database]
            2.  [DEFAULT]&#x2026; RabbitMQ
            3.  [DEFAULT]&#x2026; Keystone
            4.  [DEFAULT]&#x2026; my<sub>ip</sub>
        3.  Set [oslo<sub>concurrency</sub>] lock path
        4.  Poplulate the Block Storage database:
    -   [X] Configure Compute service to use Block Storage
        -   Edit /etc/nova/nova.conf [cinder]&#x2026;
            `os_region_name = RegionOne`
    -   [X] Finalize Installation
        -   `# service nova-api restart`
        -   `# service cinder-scheduler restart`
        -   `# service apache2 restart`
-   [X] Configure 'block1' node <code>[0/0]</code>
    ![img](./img/service070cinder(1)-small.png)


<a id="org53ba3a3"></a>

### TODO Cinder: HW RESULTS <code>[0/2]</code>

-   [ ] Screenshot: Create a volume
    No screenshot.  Volume created, but NOVA crashed and still troubleshooting connection.
-   [ ] Screenshot: Retrieve a volume list
    No Screenshot.  Was able to see the volume in horizon before nova crashed but nova being offline is interfering with many of even the CLI version of openstack commands.

---


<a id="org3fdc5ae"></a>

### TODO Swift: Install <code>[5/5]</code>

-   [X] Install and Configure Controller Node (5.9.3)
    -   [X] Prerequisites
        -   [X] 1. Source admin credentials
            `# ./os-scripts/admin-openrc`
        -   [X] 2. Create identity service credentials
        -   [X] 3. Create object storage api endpoints
    -   [X] Install and configure components
        -   [X] 1. Install Package(s) (MUST BY PYTHON3!)
            
                # apt-get install swift swift-proxy python3-swiftclient python3-keystoneclient python3-keystonemiddleware memcached
        -   [X] 2. Create /etc/swift directory
        -   [X] 3. Obtain proxy service config file from object storage repository
            
                # curl -o /etc/swift/proxy-server.conf https://opendev.org/openstack/swift/raw/branch/master/etc/proxy-server.conf-sample
        -   [X] 4. Edit /etc/swift/proxy-server.conf
            -   [DEFAULT]
            -   [pipeline:main]
                
                    pipeline = catch_errors gatekeeper healthcheck proxy-logging cache container_sync bulk ratelimit authtoken keystoneauth container-quotas account-quotas slo dlo versioned_writes proxy-logging proxy-server
            -   [app:proxy-server] 
                
                    use = egg:swift#proxy
                    ...
                    account_autocreate = True
            -   [filter:keystoneauth]
                
                    use = egg:swift#keystoneauth
                    ...
                    operator_roles = admin,user
            -   [filter:authtoken]
                
                    paste.filter_factory = keystonemiddleware.auth_token:filter_factory
                    ...
                    www_authenticate_uri = http://controller:5000
                    auth_url = http://controller:5000
                    memcached_servers = controller:11211
                    auth_type = password
                    project_domain_id = default
                    user_domain_id = default
                    project_name = service
                    username = swift
                    password = SWIFT_PASS
                    delay_auth_decision = True
            -   [filter:cache]
                
                    use = egg:swift#memcache
                    ...
                    memcache_servers = controller:11211
-   [X] Install and Configure Storage Node(s) (5.9.4)
    (repeat steps for each storage node)
    -   [X] Prerequisites <code>[8/8]</code> 
        -   [X] 1. Install packages
            `# apt-get install xfsprogs rsync`
        -   [X] 2. format devices
            `# mkfs.xfs /dev/sdb`
            `# mkfs.xfs /dev/sdc`
        -   [X] 3. create mount points
            `# mkdir -p /srv/node/sdb`
            `# mkdir -p /srv/node/sdc`
        -   [X] 4. parse UUID
            `# blkid`
        -   [X] 5. edit /etc/fstab
            
                        UUID="<UUID-from-output-above>" /srv/node/sdb xfs noatime 0 2
                UUID="<UUID-from-output-above>" /srv/node/sdc xfs noatime 0 2
        -   [X] 6. mount devices
            `# mount /srv/node/sdb`
            `# mount /srv/node/sdc`
        -   [X] 7. edit /etc/rsyncd.conf
            
                        uid = swift
                gid = swift
                log file = /var/log/rsyncd.log
                pid file = /var/run/rsyncd.pid
                address = 10.0.0.51
                
                [account]
                max connections = 2
                path = /srv/node/
                read only = False
                lock file = /var/lock/account.lock
                
                [container]
                max connections = 2
                path = /srv/node/
                read only = False
                lock file = /var/lock/container.lock
                
                [object]
                max connections = 2
                path = /srv/node/
                read only = False
                lock file = /var/lock/object.lock
        -   [X] 8. start rsync service
            `# service rsync start`
    -   [X] Install & Configure Components <code>[7/7]</code>
        -   [X] 1. Install packages
            `# apt-get install swift swift-account swift-container swift-object`
        -   [X] 2. Obtain accounting, container, & object service configs from repository
            
                # curl -o /etc/swift/account-server.conf https://opendev.org/openstack/swift/raw/branch/master/etc/account-server.conf-sample
                # curl -o /etc/swift/container-server.conf https://opendev.org/openstack/swift/raw/branch/master/etc/container-server.conf-sample
                # curl -o /etc/swift/object-server.conf https://opendev.org/openstack/swift/raw/branch/master/etc/object-server.conf-sample
        -   [X] 3. Edit /etc/swift/account-server.conf
            -   [DEFAULT]
                
                              ...
                    bind_ip = 10.0.0.51
                    bind_port = 6201
                    user = swift
                    swift_dir = /etc/swift
                    devices = /srv/node
                    mount_check = True
            -   [pipeline:main]
                
                    pipeline = healthcheck recon container-server
            -   [filter:recon]
                
                              use = egg:swift#recon
                    ...
                    recon_cache_path = /var/cache/swift
        -   [X] 4. Edit /etc/swift/container-server.conf
            -   [X] DEFAULT
            -   [X] pipeline:main
            -   [X] filter:recon
        -   [X] 5. Edit /etc/swift/object-server.conf
            -   [X] DEFAULT
            -   [X] pipeline:main
            -   [X] filter:recon
        -   [X] 6. Ensure ownership of mount point structure
        -   [X] 7. Create `recon` directory and assign ownership
-   [X] Create and Distribute Initial Rings (5.9.5) <code>[4/4]</code>
    -   [X] Create account ring
        -   [X] Create base account.builder
        -   [X] add each storage node to ring
        -   [X] verify ring contents
        -   [X] rebalance ring
    -   [X] Create container ring
        -   [X] Create base account.builder
        -   [X] add each storage node to ring
        -   [X] verify ring contents
        -   [X] rebalance ring
    -   [X] Create object ring
        -   [X] Create base account.builder
        -   [X] add each storage node to ring
        -   [X] verify ring contents
        -   [X] rebalance ring
    -   [X] Distribute ring files
-   [X] Finalize Installation (5.9.6)
-   [X] Installation Screenshots
    ![img](./img/service080swift(1)-small.png)
    ![img](./img/service080swift(4)-small.png)
    ![img](./img/service080swift(6)-small.png)
    ![img](./img/service080swift(15)-small.png)
    ![img](./img/service080swift(19)-small.png)
    ![img](./img/service080swift(24)-small.png)
    ![img](./img/service080swift(26)-small.png)
    ![img](./img/service080swift(30)-small.png)
    ![img](./img/service080swift(32)-small.png)


<a id="orgb0ddb4c"></a>

### TODO Swift: HW RESULTS <code>[1/2]</code>

-   [X] Create a container
    <./img/container>
-   [ ] Upload and Download a file
    INCOMPLETE

