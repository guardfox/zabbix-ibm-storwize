This Zabbix Template was tested on Zabbix v. 3.0.9 on 23Nov 2017.

Zabbix user should have  public key authentication enabled against IBM v3700 with Monitoring  privilege assigned.

For SAN node please configure following macros: 
${STORWIZEADDR}="10.0.0.1"
Zabbix scripts as external scripts will use this address for ssh access to IBM Storwize v3700.

Place scripts under /usr/local/sbin
Validate that your zabbix proxy is having SSH key defined in zabbix proxy config:
example:
SSHKeyLocation=/etc/zabbix/.ssh

As well make sure that zabbix can store temp files under : /etc/zabbix/scripts/repo for Items Discovery.

Create a new rsa ssh key for zabbix:

ssh-keygen -t rsa -b 2048 -f /etc/zabbix/.ssh/id_ibm
Generating public/private rsa key pair.
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /etc/zabbix/.ssh/id_ibm.
Your public key has been saved in /etc/zabbix/.ssh/id_ibm.pub.
The key fingerprint is:
78:ae:59:5e:a1:75:73:1c:7d:fa:eb:27:80:32:aa:ce root@zbx-proxy01
The key's randomart image is:
+---[RSA 2048]----+
|                 |
|               . |
|              . o|
|       .     . o.|
|      . S o.o +  |
|       ooo.o.o . |
|       .+o.  .  .|
|   .  .= .    . o|
|   .E.o .     .+.|
+-----------------+

Configure zabbix user in IBM Storwize v3700 with public key authentication using /etc/zabbix/.ssh/id_ibm.pub.

Import template in your zabbix server and make sure that script are installed on your zabbix-proxy.

As well tested with IBM storwize v7000g2 2076-524.
