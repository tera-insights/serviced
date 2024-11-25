#
# This container is used to run the script which changes the version an RPM package for serviced
#
FROM centos:centos7
MAINTAINER Zenoss <dev@zenoss.com>

RUN <<EOT
set -eux
# Add a new repository to replace CentOS 7 mirrorlist
tee /etc/yum.repos.d/CentOS-Base.repo << EOM
[CentOS-Base]
name=CentOS-Base
baseurl=http://vault.centos.org/7.9.2009/os/x86_64/
enabled=1
gpgcheck=0
EOM

# Add the docker repo
tee /etc/yum.repos.d/docker-ce.repo << EOM
[docker-ce-stable]
name=Docker CE Stable - x86_64
baseurl=https://download.docker.com/linux/centos/7/x86_64/stable
enabled=1
gpgcheck=1
gpgkey=https://download.docker.com/linux/centos/gpg
EOM
# Clear yum cache and update system
yum clean all
yum update -y
yum makecache fast
yum install -y wget rpm-build

# Install the rpmrebuild tool
wget "http://downloads.sourceforge.net/project/rpmrebuild/rpmrebuild/2.11/rpmrebuild-2.11-1.noarch.rpm?r=http%3A%2F%2Fsourceforge.net%2Fprojects%2Frpmrebuild%2Ffiles%2Frpmrebuild%2F2.11%2F&ts=1421178242&use_mirror=hivelocity" \
	-O rpmrebuild-2.11-1.noarch.rpm

rpm -Uvh rpmrebuild-2.11-1.noarch.rpm
rpm -ivh http://get.zenoss.io/yum/zenoss-repo-1-1.x86_64.rpm
EOT
