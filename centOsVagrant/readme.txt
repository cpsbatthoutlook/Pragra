#VirtualBox 
#https://blogs.oracle.com/wim/running-virtualbox-inside-a-vm-instance-in-oracle-cloud-infrastructure
	#https://wiki.centos.org/HowTos/Virtualization/VirtualBox

cd /etc/yum.repos.d
wget http://download.virtualbox.org/virtualbox/rpm/rhel/virtualbox.repo
yum --enablerepo=epel install dkms

yum -y groupinstall "Development Tools"
yum -y install kernel-devel
yum install -y kernel-uek-devel-`uname -r` gcc
yum -y  install VirtualBox-5.2
wget https://download.virtualbox.org/virtualbox/5.2.8/Oracle_VM_VirtualBox_Extension_Pack-5.2.8.vbox-extpack
vboxmanage extpack install Oracle_VM_VirtualBox_Extension_Pack-5.2.8.vbox-extpack
##Didn't work 
## Alternative below didn't work either
#https://stackoverflow.com/questions/49203548/centos-7-virtualbox-is-complaining-that-the-kernel-module-is-not-loaded
wget https://linuxsoft.cern.ch/cern/centos/7/updates/x86_64/Packages/kernel-devel-3.10.0-957.10.1.el7.x86_64.rpm
yum localinstall kernel-devel-3.10.0-957.10.1.el7.x86_64.rpm -y
 /sbin/vboxconfig

usermod -a -G vboxusers opc

#Create 1st VM
# vboxmanage createvm --name oci-test --ostype oracle_64 --register
# vboxmanage modifyvm oci-test --memory 4096 --vram 128 --ioapic on
# vboxmanage modifyvm oci-test --boot1 dvd --boot2 disk --boot3 none --boot4 none
# vboxmanage modifyvm oci-test --vrde on
#Create 40GB VDI / ISO as DVD image
# vboxmanage createhd --filename oci-test.vdi --size 40960
# vboxmanage storagectl oci-test --name "SATA Controller" --add sata --controller IntelAHCI
# vboxmanage storageattach oci-test --storagectl "SATA Controller" --port 0 --device 0 --type hdd --medium oci-test.vdi
# vboxmanage storagectl oci-test --name "IDE Controller" --add ide
# vboxmanage storageattach oci-test --storagectl "IDE Controller" --port 0 --device 0 --type dvddrive --medium /home/opc/OracleLinux-R7-U5-BETA-Server-x86_64-dvd.iso


##VAGRANT install
#https://www.vagrantup.com/downloads.html
wget https://releases.hashicorp.com/vagrant/2.2.6/vagrant_2.2.6_x86_64.rpm
yum install vagrant_2.2.6_x86_64.rpm
cd /centOSVagrant/
vagrant init
#Copy Vagrant file from k8s site



##ANSIBLE
##https://www.digitalocean.com/community/tutorials/how-to-install-and-configure-ansible-on-centos-7
yum -y install epel-release
yum -y install ansible


