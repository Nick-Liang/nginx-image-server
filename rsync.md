#1

yum -y install xinetd

vi /etc/xinetd.d/rsync

service rsync
{

disable = no #yes -> no

socket_type = stream

wait = no

user = root

server = /usr/bin/rsync

server_args = –daemon

log_on_failure += USERID

}

#2
service xinetd restart

#3
create /etc/rsyncd.conf

#4
script：

pid file = /var/run/rsyncd.pid
motd file = /etc/rsyncd/rsyncd.motd
log file = /usr/local/rsync/log/rsyncd.log
log format = %t %a %m %f %b
syslog facility = local3
timeout = 300
port = 873
address = 10.28.6.153
uid = root
gid = root
use chroot = yes
read only = no
max connections = 5
[image]
path=/
comment = Image Transfer
ignore errors
read only = not
list = false
auth users = root
secrets file = /etc/rsyncd/rsyncd.secrets
hosts allow = 10.28.6.154
hosts deny = *

