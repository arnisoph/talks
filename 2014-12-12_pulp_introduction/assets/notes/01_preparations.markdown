# Setup CentOS 7

```
systemctl mask firewalld; systemctl stop firewalld
timedatectl set-timezone Europe/Berlin
yum install git net-tools htop vim wget

wget https://repos.fedorapeople.org/repos/pulp/pulp/rhel-pulp.repo -O /etc/yum.repos.d/rhel-pulp.repo

cd /var/tmp
wget https://dl.fedoraproject.org/pub/epel/7/x86_64/e/epel-release-7-2.noarch.rpm
rpm --install epel-release-7-2.noarch.rpm
```

Verify list:
```
yum repolist
```
