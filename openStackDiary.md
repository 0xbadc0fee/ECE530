
# Table of Contents

1.  [HW 1](#orgcf4c477)
2.  [Roadmap](#orgb9c0771)
3.  [Envrionment Installation Journal](#org6ccc837)
    1.  [Pre-install Tests / Notes](#orgea6f075)
        1.  [Trial / Test VM's <code>[6/6]</code>](#orgf340202)
        2.  [General Notes:](#org4f141c3)
        3.  [Hypervisor Install Notes](#orgc31c1a7)
        4.  [Home Lab Config Notes:](#org1dab605)
        5.  [Environment Install Task List / YOGA / UBUNTU (1 VM per host method)](#org88fa07d)
    2.  [Environment Install Footnotes](#org057c0c5)
4.  [Project(s) Installation Journal](#org881d388)
    1.  [Projects(s) Install Task List / YOGA / UBUNTU](#orga916aae)
        1.  [Keystone: Install <code>[6/6]</code>](#org142c895)
        2.  [Keystone: HW RESULTS <code>[4/4]</code>](#org245866f)
        3.  [Glance: Install (on controller) <code>[10/10]</code>](#org6e986c7)
        4.  [Glance: HW RESULTS <code>[2/2]</code>](#org0879a7d)
        5.  [Placement: Install](#org9bba602)
        6.  [Placement: HW RESULTS](#orgd81df2a)
        7.  [Neutron: Install](#org41bf5e7)
        8.  [Neutron: HW RESULTS](#orga77fa1a)
        9.  [Horizon: Install](#org61af0c2)
        10. [Horizon: HW RESULTS](#orgcc6b282)
        11. [Cinder: Install](#orgf92918a)
        12. [Cinder: HW RESUlts](#org9d8a4bb)



<a id="orgcf4c477"></a>

# HW 1

Set up OpenStack, see Mod 1 rubric


<a id="orgb9c0771"></a>

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


<a id="org6ccc837"></a>

# Envrionment Installation Journal


<a id="orgea6f075"></a>

## Pre-install Tests / Notes


<a id="orgf340202"></a>

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


<a id="org4f141c3"></a>

### General Notes:

-   Use Yoga Install Instructions <https://docs.openstack.org/swift/yoga/install/>
-   Use minimal install version of OS (Ubuntu 20.0.4)
-   Use 64bit version of OS
-   Build Ea Host as it's own VM.  Can take snapshots, rollbacks, etc.
    (note that many vm's WILL have reduced performance as number of VMs increases)


<a id="orgc31c1a7"></a>

### Hypervisor Install Notes

-   Installed on HP ProLiant MicroServer, 4 TB, 32GB Ram
-   Balance min requirements per vm host comparing Ubuntu min req's and OpenStack min Req's, if room, install each service on sep host.
-   Build template vm and then replcate for each service, make edits as needed (#of nics, # of cores, etc)
-   Per yoga install&#x2026; controller node: 1 core, 4GB ram, 5GB hdd
-   per yoga install&#x2026; compute node:1 core, 2gb ram, 10GB hdd
-   Ubuntu lts server&#x2026; 2 core, 4gb ram, 25gb hdd
-   template build&#x2026;. 2 core, 6gb ram, 40 gb hdd, 2 NIC

---


<a id="org1dab605"></a>

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


<a id="org88fa07d"></a>

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


<a id="org057c0c5"></a>

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

    sgc@ops-cntrl-01:~$ cat /etc/netplan/00-installer-config.yaml
    # This is the network config written by 'subiquity'
    network:
      ethernets:
        ens160:
          addresses:
            - 10.0.0.11/24
          gateway4: 10.0.0.1
          nameservers:
                  addresses: [8.8.8.8, 1.1.1.1]
        ens192:
          dhcp4: false
          dhcp6: false
      version: 2

-   Be sure that both /etc/hosts and /etc/hostname have the corect names.
-   If all is working, should be able to SSH to host (i.e. 10.0.0.11) and when logged in host name will display correctly in terminal

-   <span class="timestamp-wrapper"><span class="timestamp">&lt;2023-03-30 Thu&gt; </span></span> NOTE: Archive Enablement:
    using OpenStack Yoga for Ubuntu 20.04 LTS (server 64bit)
    -   add-apt-repository cloud-archive:yoga

---

---


<a id="org881d388"></a>

# Project(s) Installation Journal


<a id="orga916aae"></a>

## TODO Projects(s) Install Task List / YOGA / UBUNTU


<a id="org142c895"></a>

### TODO Keystone: Install <code>[6/6]</code>

-   REF: Projects Install Doc / Yoga / Keystone ([link](https:docs.openstack.org/keystone/yoga/doc-keystone.pdf))
-   TARGET(S): controller
-   USER: root (either 'sudo -i'  or 'su -')
-   [X] **Initialize SQL**

    # mysql
    MariaDB > CREATE DATABASE keystone;
    MariaDB > GRANT ALL PRIVILEGES ON keystone.* TO 'keystone'@'localhost' IDENTIFIED BY 'pwd123';
    MariaDB > GRANT ALL PRIVILEGES ON keystone.* TO 'keystone'@'%' IDENTIFIED BY 'pwd123';  replace dbpass with password

-   NOTE: A good test here would be to exit root (#), and as user ($) try to access the database.  If you get 1045 errors, that indicates an authentication problem and the rest of the process will fail until authentication is working.  When done testing from user, remember to return to root for remainder of process.  If the below does not produce a connection to SQL, stop and troubleshoot.
-   [X] **Test SQL Connection**
    
        $ mysql -u keystone -p
        MariaDB [(none)]>

-   [X] **Instlal Kestone Package**

    # apt install keystone
    # vi /etc/keystone/keystone.conf (make edits per docs)
    # su -s /bin/sh -c "keystone-manage db_sync" keystone

-   [X] **Initialize Repositories**

    # keystone-manage fernet_setup --keystone-user keystone --keystone-group keystone
    # keystone-manage credential_setup --keystone-user keystone --keystone-group keystone

-   [X] **Bootstrap ID service**

    keystone-manage bootstrap --bootstrap-password pwd123 --bootstrap-admin-url http://controller:5000/v3/ --bootstrap-internal-url http://controller:5000/v3/ --bootstrap-public-url http://controller:5000/v3/ --bootstrap-region-id RegionOne 

-   [X] **Edit Env Variables**

    $ export OS_USERNAME=admin
    $ export OS_PASSWORD=ADMIN_PASS
    $ export OS_PROJECT_NAME=admin
    $ export OS_USER_DOMAIN_NAME=Default
    $ export OS_PROJECT_DOMAIN_NAME=Default
    $ export OS_AUTH_URL=http://controller:5000/v3
    $ export OS_IDENTITY_API_VERSION=3

-   NOTE: Before doing the above, do a '$ printenv' and look at the environment variables.  There should already be populated a number of OS\_ (openstack) entries.  If not, it may mean that the bootstraping commands did not complete correctly.  This happened to me.  After backing up and going through the bootstrapping commands again I found 5 of the 7 above env variables already in print env.  After adding the missing two, the rest of the process ran correctly.


<a id="org245866f"></a>

### TODO Keystone: HW RESULTS <code>[4/4]</code>

-   [X] **Confirm Token Assignment**

    +------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
    | Field      | Value
             |
    +------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
    | expires    | 2023-04-03T21:10:00+0000
             |
    | id         | gAAAAABkKzKY1kcGmTmr2azLTezITAUGLjV7a_N_t90aZRQvr-lF7I0Oo3mq7sbeYBmKVEa_3rqiKuZipSpm_TMRKzObbF7yl_lup9-VkYmvl3_daPTAT5MDxrr_qHPqF0vl2TQMBZYA1we_-_RVnrUuHzPw9BR71TUXFiote79KFPSzxXkt7Es |
    | project_id | af55244dfe134e73bb68d80af4842abb
             |
    | user_id    | 483616691ea84ae3936b9cadd1725b4f
             |
    +------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

-   [X] **Confirm demo (myuser) and admin users are created**

    sgc@controller:~$ openstack --os-auth-url http://controller:5000/v3 \
    > --os-project-domain-name Default --os-user-domain-name Default \
    > --os-project-name admin --os-username admin token issue
    Password:
    +------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
    | Field      | Value
             |
    +------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
    | expires    | 2023-04-03T21:10:00+0000
             |
    | id         | gAAAAABkKzKY1kcGmTmr2azLTezITAUGLjV7a_N_t90aZRQvr-lF7I0Oo3mq7sbeYBmKVEa_3rqiKuZipSpm_TMRKzObbF7yl_lup9-VkYmvl3_daPTAT5MDxrr_qHPqF0vl2TQMBZYA1we_-_RVnrUuHzPw9BR71TUXFiote79KFPSzxXkt7Es |
    | project_id | af55244dfe134e73bb68d80af4842abb
             |
    | user_id    | 483616691ea84ae3936b9cadd1725b4f
             |
    +------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
    
    sgc@controller:~$ openstack --os-auth-url http://controller:5000/v3 \
    > --os-project-domain-name Default --os-user-domain-name Default \
    > --os-project-name myproject --os-username myuser token issue
    Password:
    +------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
    | Field      | Value
             |
    +------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
    | expires    | 2023-04-03T21:14:47+0000
             |
    | id         | gAAAAABkKzO3m0xEVmt5KXdpNRarHdbsQKu_R3Kvl_vsl_Qj4zLRd1sKbFmj6hLiImTpjfF2drCIqH0-NRIUfPKERlTJcj9k-1-Lw8W5b94eeDWs-m77VlXJLcpIjGiSehIM4TDhYqYuWmu4r_zs_OH5v3CllqhdtpV9HuMOku5jID5Ytf4YiPM |
    | project_id | 9e2b1df7e13e4e90a1dfe3d12e96374e
             |
    | user_id    | 2e7b44d196454070a7f6da6d66b61b5a
             |
    +------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

-   [X] **Confirm user list can be retrieved**

    MariaDB [keystone]> SELECT * FROM user
        -> ;
    +----------------------------------+-------+---------+--------------------+---------------------+----------------+-----------+
    | id                               | extra | enabled | default_project_id | created_at          | last_active_at | domain_id |
    +----------------------------------+-------+---------+--------------------+---------------------+----------------+-----------+
    | 2e7b44d196454070a7f6da6d66b61b5a | {}    |       1 | NULL               | 2023-04-03 20:05:06 | NULL           | default   |
    | 483616691ea84ae3936b9cadd1725b4f | {}    |       1 | NULL               | 2023-04-03 19:55:11 | NULL           | default   |
    +----------------------------------+-------+---------+--------------------+---------------------+----------------+-----------+
    2 rows in set (0.000 sec)

-   [X] **Confirm role list can be retrieved**

    MariaDB [keystone]> SELECT * FROM role;
    +----------------------------------+--------+-------+-----------+-------------+
    | id                               | name   | extra | domain_id | description |
    +----------------------------------+--------+-------+-----------+-------------+
    | 0b25f16d85fa4fcdbbf560c8776b009c | admin  | {}    | <<null>>  | NULL        |
    | 27490b2ef72343719edaad6ef2d3baa6 | myrole | {}    | <<null>>  | NULL        |
    | 53a2975840ca44d1876980c8267a1c1b | member | {}    | <<null>>  | NULL        |
    | 78965140ce3941b7806c809bdabe86e8 | reader | {}    | <<null>>  | NULL        |
    +----------------------------------+--------+-------+-----------+-------------+
    4 rows in set (0.001 sec)
    
    MariaDB [keystone]>

---


<a id="org6e986c7"></a>

### TODO Glance: Install (on controller) <code>[10/10]</code>

-   [X] **DB Configuration**
    
        # mysql
        MariaDB [(none)] CREATE DATABASE glance;

-   [X] Source the admin credentials (./os-scripts/) `$ . admin-openrc`
-   [X] Create the `glance` user
    
        sgc@controller:~/os-scripts$ openstack user create --domain default --password-prompt glance
        User Password:
        Repeat User Password:
        +---------------------+----------------------------------+
        | Field               | Value                            |
        +---------------------+----------------------------------+
        | domain_id           | default                          |
        | enabled             | True                             |
        | id                  | 5e99d020af48473da06c73a4ce96e50a |
        | name                | glance                           |
        | options             | {}                               |
        | password_expires_at | None                             |
        +---------------------+----------------------------------+
-   [X] Add the admin role to the glance user and service project
    
        $ openstack role add --project service --user glance admin
-   [X] Create the glance service entry
    
        openstack service create --name glance \
        --description "OpenStack Image" image
-   [X] Create the Image Service API
    
        $ openstack endpoint create --region RegionOne \
          image public http://controller:9292
-   [X] Install glance packages
    
        # apt install glance
-   [X] Make edits to `/etc/glance/glance-api.conf`
    -   Online documentation is does not match conf file installed via steps above.
    -   [oslo<sub>limit</sub>] section was missing but may not matter, not doing quota's
    -   `use_keystone_quotas` is now `use_keystone_limits`, but no impact, left default false.
-   [X] Populate Image service database and restart service
    
        # su -s /bin/sh -c "glance-manage db_sync" glance
        # service glance-api restart
-   [X] Verify Operation (see doc [link](https://docs.openstack.org/glance/yoga/install/verify.html))


<a id="org0879a7d"></a>

### TODO Glance: HW RESULTS <code>[2/2]</code>

-   [X] HW Glance 1: Import Cirros OS Image

    sgc@controller:~$ glance image-create --name "cirros" \
    > --file cirros-0.4.0-x86_64-disk.img \
    > --disk-format qcow2 --container-format bare \
    > --visibility=public
    +------------------+----------------------------------------------------------------------------------+
    | Property         | Value                                                                            |
    +------------------+----------------------------------------------------------------------------------+
    | checksum         | 443b7623e27ecf03dc9e01ee93f67afe                                                 |
    | container_format | bare                                                                             |
    | created_at       | 2023-04-04T01:24:37Z                                                             |
    | disk_format      | qcow2                                                                            |
    | id               | 25c894f6-fe98-4da3-a8d9-89ef27508d46                                             |
    | min_disk         | 0                                                                                |
    | min_ram          | 0                                                                                |
    | name             | cirros                                                                           |
    | os_hash_algo     | sha512                                                                           |
    | os_hash_value    | 6513f21e44aa3da349f248188a44bc304a3653a04122d8fb4535423c8e1d14cd6a153f735bb0982e |
    |                  | 2161b5b5186106570c17a9e58b64dd39390617cd5a350f78                                 |
    | os_hidden        | False                                                                            |
    | owner            | af55244dfe134e73bb68d80af4842abb                                                 |
    | protected        | False                                                                            |
    | size             | 12716032                                                                         |
    | status           | active                                                                           |
    | tags             | []                                                                               |
    | updated_at       | 2023-04-04T01:24:37Z                                                             |
    | virtual_size     | 46137344                                                                         |
    | visibility       | public                                                                           |
    +------------------+----------------------------------------------------------------------------------+
    sgc@controller:~$

-   [X] HW Glance 2: Retrieve Image List

    sgc@controller:~$ glance image-list
    +--------------------------------------+--------+
    | ID                                   | Name   |
    +--------------------------------------+--------+
    | 25c894f6-fe98-4da3-a8d9-89ef27508d46 | cirros |
    +--------------------------------------+--------+
    sgc@controller:~$

---


<a id="org9bba602"></a>

### TODO Placement: Install


<a id="orgd81df2a"></a>

### TODO Placement: HW RESULTS

---


<a id="org41bf5e7"></a>

### TODO Neutron: Install


<a id="orga77fa1a"></a>

### TODO Neutron: HW RESULTS

---


<a id="org61af0c2"></a>

### TODO Horizon: Install


<a id="orgcc6b282"></a>

### TODO Horizon: HW RESULTS

---


<a id="orgf92918a"></a>

### TODO Cinder: Install


<a id="org9d8a4bb"></a>

### TODO Cinder: HW RESUlts

---
