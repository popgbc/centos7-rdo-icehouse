centos7-rdo-icehouse
====================

setup rdo-icehouse on centos7 files

centos7.ks  
basic configuration centos7 kickstart file  

## 1) mini install CentOS7

best mini ISO image  
  CentOS-7.0-1406-x86_64-Minimal.iso

## 2) yum update -y
  and better reboot

## 3) install rdo icehouse repository for EL7
  RDO http://openstack.redhat.com/Main_Page  
  RDO Quick Start  http://openstack.redhat.com/Quickstart  
  
    $ wget https://repos.fedorapeople.org/repos/openstack/openstack-icehouse/rdo-release-icehouse-4.noarch.rpm
    $ sudo yum install rdo-release-icehouse-4.noarch.rpm

## 4) install openstack-packstack packages
  run 
    $ sudo yum install -y openstack-packstack

## 5) get patch file from this repository
  this is work around things.  
  CentOS7 version is not 7.0 << 7.0.1406  
  bugzilla : https://bugzilla.redhat.com/show_bug.cgi?id=1117871  
  patch file  : rdo-AIO-centos7-patch-for-bug-1117871.diff  
  fix Examples)  

    - $::operatingsystemrelease < 7
    + $::operatingsystemmajrelease < 7

  run;  
  
    $ sudo su -
    # ssh-keygen -t rsa
    # cat /root/.ssh/id_rsa.pub > /root/.ssh/authorized_key
    # chmod 600 /root/.ssh/authorized_keys
    # ls -l /root/.ssh/authorized_keys
    # wget https://raw.githubusercontent.com/naototty/centos7-rdo-icehouse/master/rdo-AIO-centos7-patch-for-bug-1117871.diff
    # ls -l rdo-AIO-centos7-patch-for-bug-1117871.diff
    # yum install -y patch
    # cd /
    # cat /root/rdo-AIO-centos7-patch-for-bug-1117871.diff | patch -p1

## 6) go packstack
  start packstack install "packstack --allinone" or other options.
  
    # packstack --allinone

