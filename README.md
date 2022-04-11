# centos7_master
Configuration of my Centos7 master VM

# Initial setup
1. Download and install virtualbox
2. Download and install/configure the latest centos7 image
3. Configure the network in Virtual box to be a 'bridged network'
   a. curl a website to check if internet access is working
4. Install git (any version will do)
   a. 'yum install git' (easiest)
   b. Check the version of git: git --version
5. Install wget
   a. 'yum install wget'
6. Install Ansible
   a. yum install epel-release
   b. yum install ansible (latest version)
   c. TO BE DONE. FIND A WAY TO INSTALL ANY ANSIBLE VERSION ON MASTER
   d. All epel Ansible versions: https://releases.ansible.com/ansible/rpm/release/epel-7-x86_64/

Now you are set to use the Ansible scripts in this repository. 
