#### server
apt-get install nfs-kernel-server
apt-get install nfs-common

vim /etc/exports

<目录>(如/nfs) *(rw,sync,no_root_squash)     # * 表示允许任何网段 IP 的系统访问该 NFS 目录

chmod -R 777 /nfs

chown root:root /nfs/ -R

/etc/init.d/nfs-kernel-server start

#### client
apt install -y nfs-common
showmount -e + 主机IP
mount -t nfs -o nolock 远端ip:目录 本地目录

如

mount -t nfs -o nolock 10.0.0.10:/nfs /mnt/nfs