Ansible MongoDB 
=========

Ansible role for MongoDB configuration with Replicaset support.


Features
-----------
```
    - CentOS and Ubuntu Support
    - Standalone and Replicaset configuration
    - Configures SELinux on CentOS
    - Configures Firewalld 
    - MongoDB config file location can be changed to custome directory
    - Custome Database and Log directories
    - Enable/Disable Authentication (enable by default and recommended)
    - Create Users - Root, DBAdmin, Backup Admin
    - Replica priority can be configured
    - SCARM Authentication
```

Support Matrix
--------------

| Destro | MongoDB 4.4 | MongoDB 4.3 |
| --- | --- | --- |
| CentOS 8 | Supported (Tested) | Supported (Not Tested) |
| CentOS 7 | Supported (Tested) | Supported (Not Tested) |
| Ubuntu 20.04 LTS | Supported (Tested) | Supported (Not Tested) |
| Ubuntu 19.04 LTS | Supported (Tested) | Supported (Not Tested) |


Role Variables
--------------

```

# MongoDB Version
mongodb_install_version_major: 4
mongodb_install_version_minor: 4
mongodb_install_version_patch: "*"

# CentOS
mongodb_enable_yum_repository: true
mongodb_install_package_lock: true

# Ubuntu
mongodb_enable_apt_repository: true


# SELinux Configuration (only on CentOS)
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
mongodb_replication_enabled: true   #false will create a standalone MongoDB instance
mongodb_replication_key_file: /etc/mongodb/repl.key
mongodb_replication_set_name: rs01


# PyMongo Configuration                 
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
Host Inventory
-----------
```
all:
    hosts:
    children:
        mongo:
            hosts:
                mongo-01.example.com:
                    host_name: mongodb-01
                    host_ip: "192.168.122.201"
                mongo-02.example.com:
                    host_name: mongodb-02
                    host_ip: "192.168.122.202"
                mongo-03.example.com:
                    host_name: mongodb-03
                    host_ip: "192.168.122.203"
        master:
            hosts:
                mongo-01.example.com:
        replicas:
            hosts:
                mongo-02.example.com:
                    priority: 1
                mongo-03.example.com:
                    priority: 1
        arbiter:
            hosts:
#                mongo-03.example.com:
#                    priority: 0


```


Optional Requirement
--------------------
-  CentOS Baseline - [Ansible Role](https://github.com/iquzart/ansible-centos-baseline/blob/master/README.md)

License
-------
MIT

To-DO
-------
1. TLS support
2. x509 Auth Support


Author Information
------------------

Muhammed Iqbal <iquzart@hotmail.com>