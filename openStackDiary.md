
# Table of Contents

1.  [HW 1](#org954358e)
2.  [Roadmap](#org217a061)
3.  [Envrionment Installation Journal](#org342b97c)
    1.  [Pre-install Tests / Notes](#orgf128dad)
        1.  [Trial / Test VM's <code>[6/6]</code>](#org00f03c4)
        2.  [General Notes:](#orgdd579f4)
        3.  [Hypervisor Install Notes](#org46333f8)
        4.  [Home Lab Config Notes:](#org2b83a43)
        5.  [Environment Install Task List / YOGA / UBUNTU (1 VM per host method)](#org09350c0)
    2.  [Environment Install Footnotes](#orgb81c67a)
4.  [Project(s) Installation Journal](#org92d4acd)
    1.  [Projects(s) Install Task List / YOGA / UBUNTU](#org373d7cb)
        1.  [Keystone: Install <code>[6/6]</code>](#org2d1cefe)
        2.  [Keystone: HW RESULTS <code>[4/4]</code>](#org251631d)
        3.  [Glance: Install (on controller) <code>[10/10]</code>](#org303f4a6)
        4.  [Glance: HW RESULTS <code>[2/2]</code>](#org956c7e1)
        5.  [Placement: Install <code>[4/4]</code>](#org41aee2e)
        6.  [Placement: HW RESULTS <code>[1/1]</code>](#org7dd5127)
        7.  [Nova: Install](#org2b0be14)
        8.  [Nova: HW RESULTS](#org0bdb267)
        9.  [Neutron: Install](#org3b91252)
        10. [Neutron: HW RESULTS](#org800a6b9)
        11. [Horizon: Install](#org04a602c)
        12. [Horizon: HW RESULTS](#org6bdafd0)
        13. [Cinder: Install](#org7ca4137)
        14. [Cinder: HW RESUlts](#org07787fd)



<a id="org954358e"></a>

# HW 1

Set up OpenStack, see Mod 1 rubric


<a id="org217a061"></a>

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


<a id="org342b97c"></a>

# Envrionment Installation Journal


<a id="orgf128dad"></a>

## Pre-install Tests / Notes


<a id="org00f03c4"></a>

### TODO Trial / Test VM's <code>[6/6]</code>

-   [X] Install a HyperVisor (VMware / esxi)
-   [X] Create multiple VM's for OpenStack Components
    -   [X] CPU = 6 Cores
    -   [X] RAM = 6 GB
    -   [X] <del>HDD = 200 GB</del>
-   [X] DO NOT USE AUTODEPLOY TOOLS
-   [X] Take Screenshots for steps, attach here in journal
-   [X] Collect information for use in publishing as a report
-   [X] Create a references section for external resources, links


<a id="orgdd579f4"></a>

### General Notes:

-   Use Yoga Install Instructions <https://docs.openstack.org/swift/yoga/install/>
-   Use minimal install version of OS (Ubuntu 20.0.4)
-   Use 64bit version of OS
-   Build Ea Host as it's own VM.  Can take snapshots, rollbacks, etc.
    (note that many vm's WILL have reduced performance as number of VMs increases)


<a id="org46333f8"></a>

### Hypervisor Install Notes

-   Installed on HP ProLiant MicroServer, 4 TB, 32GB Ram
-   Balance min requirements per vm host comparing Ubuntu min req's and OpenStack min Req's, if room, install each service on sep host.
-   Build template vm and then replcate for each service, make edits as needed (#of nics, # of cores, etc)
-   Per yoga install&#x2026; controller node: 1 core, 4GB ram, 5GB hdd
-   per yoga install&#x2026; compute node:1 core, 2gb ram, 10GB hdd
-   Ubuntu lts server&#x2026; 2 core, 4gb ram, 25gb hdd
-   template build&#x2026;. 2 core, 6gb ram, 40 gb hdd, 2 NIC

---


<a id="org2b83a43"></a>

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

---


<a id="org09350c0"></a>

### TODO Environment Install Task List / YOGA / UBUNTU (1 VM per host method)

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

---


<a id="orgb81c67a"></a>

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


<a id="org92d4acd"></a>

# Project(s) Installation Journal


<a id="org373d7cb"></a>

## TODO Projects(s) Install Task List / YOGA / UBUNTU


<a id="org2d1cefe"></a>

### TODO Keystone: Install <code>[6/6]</code>

-   REF: Projects Install Doc / Yoga / Keystone ([link](https:docs.openstack.org/keystone/yoga/doc-keystone.pdf))
-   TARGET(S): controller
-   USER: root (either 'sudo -i'  or 'su -')
-   [X] **Initialize SQL**

    1  # mysql
    2  MariaDB > CREATE DATABASE keystone;
    3  MariaDB > GRANT ALL PRIVILEGES ON keystone.* TO 'keystone'@'localhost' IDENTIFIED BY 'pwd123';
    4  MariaDB > GRANT ALL PRIVILEGES ON keystone.* TO 'keystone'@'%' IDENTIFIED BY 'pwd123';  replace dbpass with password

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

-   NOTE: Before doing the above, do a '$ printenv' and look at the environment variables.  There should already be populated a number of OS\_ (openstack) entries.  If not, it may mean that the bootstraping commands did not complete correctly.  This happened to me.  After backing up and going through the bootstrapping commands again I found 5 of the 7 above env variables already in print env.  After adding the missing two, the rest of the process ran correctly.


<a id="org251631d"></a>

### TODO Keystone: HW RESULTS <code>[4/4]</code>

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


<a id="org303f4a6"></a>

### TODO Glance: Install (on controller) <code>[10/10]</code>

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


<a id="org956c7e1"></a>

### TODO Glance: HW RESULTS <code>[2/2]</code>

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

-   [X] HW Glance 2: Retrieve Image List

    1    $ glance image-list
    2  +--------------------------------------+--------+
    3  | ID                                   | Name   |
    4  +--------------------------------------+--------+
    5  | 25c894f6-fe98-4da3-a8d9-89ef27508d46 | cirros |
    6  +--------------------------------------+--------+

---


<a id="org41aee2e"></a>

### TODO Placement: Install <code>[4/4]</code>

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
        
        -   ****WARNING: IN ABOVE, YOU MUST REMOVE THE TEXT " # use noauth2 if not using keystone"****
    -   [X] Populate the placement database
-   [X] Finalize Installation


<a id="org7dd5127"></a>

### TODO Placement: HW RESULTS <code>[1/1]</code>

-   [X] N/A, no placement resulst for HW required.

---


<a id="org2b0be14"></a>

### TODO Nova: Install

NOTE: Nova installation will require steps done on both 'controller' and 'compute1'
NOTE: Nova installation will include the following services:

1.  `=nova-api=` service
2.  `=nova-api-metadata=` service
3.  `=nova-computer=` service
4.  `=nova-scheduler=` service
5.  `=nova-conductor=` module
6.  `=nova-novncproxy=` daemon
7.  `=nova-spicehtml5proxy=` daemon
8.  the queue (RammitMQ)
9.  SQL database

1.  Configure Controller Node (doc 3.2.1.3) <code>[0/4]</code>

    1.  [ ] Create Database(s)
    2.  [ ] refresh admin credentials
    3.  [ ] Create Compute Service credentials
    4.  [ ] Create Compute API service endpoints

2.  Install and Configure Compute Node (doc 3.2.1.4)


<a id="org0bdb267"></a>

### TODO Nova: HW RESULTS

---


<a id="org3b91252"></a>

### TODO Neutron: Install


<a id="org800a6b9"></a>

### TODO Neutron: HW RESULTS

---


<a id="org04a602c"></a>

### TODO Horizon: Install


<a id="org6bdafd0"></a>

### TODO Horizon: HW RESULTS

---


<a id="org7ca4137"></a>

### TODO Cinder: Install


<a id="org07787fd"></a>

### TODO Cinder: HW RESUlts

---

