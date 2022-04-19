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
      * More information about the proxy I used you can find below.
5. Install Ansible
   a. Add an Ansible repository
      * Example config below
   b. yum install ansible-x.x.x (e.g ansible-2.9.17)
6. Install git (any version will do)
   a. 'yum install git' (easiest)
   b. Check the version of git: git --version
7. Clone this repository to you linux machine
8. Create an SSH key and copy it to bitbucket
9. Connect your development environment to the 
	
	You are all set to run Ansible and the environment will be set up for you
 

4. Connect your IDE to the VM
   
   
   
   

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

# Example proxy config
1. On your windows host make sure Golang and Git are installed.
2. Clone the gontlm to a local folder and change directory to the cloned folder
   * https://github.com/bdwyertech/gontlm-proxy
3. Command: "go install"
4. Update /etc/yum.conf file with the proxy settings
   * proxy=http://10.0.2.2:3128/
5. Update ~/.bashrc file
   * See below:
export http_proxy="http://10.0.2.2:3128/"
export https_proxy=${http_proxy}
export no_proxy="localhost,10.0.2.2,127.0.0.0/8,::1"
export HTTPS_PROXY=${http_proxy}
export HTTP_PROXY=${http_proxy}
export NO_PROXY=${no_proxy}
export _JAVA_OPTIONS='-Dhttp.proxyHost=10.0.2.2 -Dhttp.proxyPort=3128 -Dhttps.proxyHost=10.0.2.2 -Dhttps.proxyPort=3128 -DsocksProxyHost=10.0.2.2 -DsocksProxyPort=8010 -Dhttp.nonProxyHosts="localhost"'
   
NOTE: I am using a NAT network on Virtualbox. 10.0.2.2 is the Gateway of my specific NAT network. Port 3128 is the default port used by gontlm
   
6. You can create a powershell script to run gontlm in the background and run it when you need the proxy:

   function GoNTLM-Enable {
	Remove-Job -Name GoNTLM-Proxy -Force -ErrorAction SilentlyContinue
	Start-Job -Name GoNTLM-Proxy -ScriptBlock {C:\Users\tvannor\go\bin\gontlm-proxy.exe }
	$env:http_proxy='http://127.0.0.1:3128'
}

GoNTLM-Enable
   
# Example Yum repo config
[tnorden@centos7master ~]$ cat /etc/yum.repos.d/ansible.repo
[ansible]
name=Extra Ansible package versions
baseurl=https://releases.ansible.com/ansible/rpm/release/epel-7-x86_64/
enabled=1
gpgcheck=0

   
