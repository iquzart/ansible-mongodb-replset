Ansible MongoDB Replica set
=========

Ansible role for MongoDB Replicaset configuration

Role Variables
--------------

```
# Repository 
mongodb_enable_yum_repository: true
mongodb_install_version_major: 4
mongodb_install_version_minor: 4
mongodb_install_version_patch: "*"
mongodb_install_package_lock: true

# SELinux Configuration
configure_selinux: True

# MongoDB Configuration
mongodb_conf_file: /etc/mongodb/mongod.conf            
mongodb_conf_db_dir: /data/mongo-data
mongodb_conf_log_dir: /var/log/mongodb                 
mongodb_conf_dbEngine: wiredTiger                      
mongodb_conf_auth: true                                
mongodb_conf_bindIp: "0.0.0.0"                       
mongodb_conf_journal: true                             
mongodb_conf_maxConns: 1000                           
mongodb_conf_port: 27017                               
mongodb_conf_oplogSize: 1024
mongodb_conf_cloudmonitoring: "off"

# Systemd Units
mongodb_daemon_unitfile: /etc/systemd/system/mongod.service 

# Replicset configuration 
mongodb_replication_enabled: true
mongodb_replication_key_file: /etc/mongodb/repl.key
mongodb_replication_set_name: rs01

# PyMongo Configuration
mongodb_pymongo_from_pip: true                  
mongodb_pymongo_pip_version: 3.7.1

# Account configuration
mongodb_root_account: root
mongodb_root_password: "p@ssw0rd"

mongodb_admin_account: dbadmin
mongodb_admin_password: "p@ssw0rd"

mongodb_backup_account: backupadmin
mongodb_backup_password: "p@ssw0rd"
```

Example Playbook
----------------

```
  - name: Mongo DB Setup 
    hosts: mongo
    remote_user: root
    become: yes

    roles:
      - mongodb-replicaset
```

Optional Requirement
--------------------
-  CentOS Baseline - [CentOS-Baseline Ansible Role](https://github.com/iquzart/ansible-centos-baseline/blob/master/README.md)

License
-------

MIT

To-DO
-------
1. Ubuntu Support
2. Standalone installation