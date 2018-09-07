Installing MariDB-Galera Cluster inside PVE Centos 7 containers (LXC) 
===

UPD:
---

the Centos 7 template has no ssh-server, so after install, you have to `pct exec CONTAINER-ID /bin/bash` and install sshd and allow remote root login

```shell
$ yum -y update && yum -y upgrade && yum -y install openssh-server && echo "PermitRootLogin yes" >> /etc/ssh/sshd_config && systemctl restart sshd
```
UPD 2:
---
For clean install Maria-DB-Galera cluster run `galera_all_in_one.yaml`
```shell
$ ansible-playbook galera_all_in_one.yaml
```

Don't forget to type your values in inventory `[galera_cluster:vars]`
* mysql_root_password=`<Password for MySQL root user>`
* repl_user=`<User for replication>`
* repl_password=`<Password for replication user>`
* wsrep_cluster_address=`<IP addresses of MariaDB nodes>`

1. After fresh install
---

* Updating system
* Installing packages:
    + `nano`
    + `bash-completion`
    + `mc`
    + `yum-utils`
* Allowing remote root for `ssh`
* Adding additional repo

2. Installing MariaDB-Galera cluster
---

* Adding MariaDB repo
* Installing:
    + `MariaDB-server`
    + `MariaDB-client`
    + `rsync`
    + `galera`
    + `MySQL-python`

3. Initial setting
---

* Analog ```mysql_secure_installation```

4. Configuring MariaDB-Galera cluster
---

* Creating & adding credintials to ~/.my.cnf (for using root password to ansible)
* Add user for replication
* Editing conf
