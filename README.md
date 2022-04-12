# centos7_master
Configuration of my Centos7 master VM

# Initial setup
1. Download and install virtualbox
2. Download and install/configure the latest centos7 image (in my case a 'minimal' version)
   a. Easiest to create a separate administrator user
3. Configure the network in Virtual box to be a 'nat network'
   a. Configure a static network in the OS (/etc/sysconfig/network-scripts/ifcfg-<int> (see below example))
   b. Create a NAT network in virtualbox (same as in previous step), enable port forwarding, and attach it to your VM's interface
      * You should now be able to connect to your host via the forward rule
   c. Configure a proxy to access the internet (if required)
      * Curl a website to check if internet access is working
4. Create an SSH key
4. Connect your IDE to the VM
5. Install Ansible
   a. yum install epel-release
   b. yum install ansible (latest version)
   c. TO BE DONE. FIND A WAY TO INSTALL ANY ANSIBLE VERSION ON MASTER
   d. All epel Ansible versions: https://releases.ansible.com/ansible/rpm/release/epel-7-x86_64/

   
   
   
   
   4. Install git (any version will do)
   a. 'yum install git' (easiest)
   b. Check the version of git: git --version
5. Install wget
   a. 'yum install wget'
7. Add own user to wheel group
   a. 'visudo'
   b. Unhash the %wheel line
   c. 'usermod –aG wheel <username>'
Now you are set to use the Ansible scripts in this repository. 

# Example network config
Subnet: 10.0.2.0/24

TYPE=Ethernet
PROXY_METHOD=none
BROWSER_ONLY=no
BOOTPROTO=static
DEFROUTE=yes
IPV4_FAILURE_FATAL=no
IPV6INIT=yes
IPV6_AUTOCONF=yes
IPV6_DEFROUTE=yes
IPV6_FAILURE_FATAL=no
IPV6_ADDR_GEN_MODE=stable-privacy
NAME=enp0s3
UUID=f484feb5-f236-4236-89e4-a18d5bc6fc10
DEVICE=enp0s3
ONBOOT=yes
IPADDR=10.0.2.15
NETMASK=255.255.255.0
GATEWAY=10.0.2.1
DNS1=x.x.x.x
DNS2=x.x.x.x

