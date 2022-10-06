# Ton demo

## Todo

- [ ]  Provision
    - [x]  RockyLinux/8 has a problem with Virtualbox Guest Extensions. Trying generic/rocky8 works fine.
    
    [https://github.com/EnterpriseDB/postgres-deployment/issues/339](https://github.com/EnterpriseDB/postgres-deployment/issues/339)
    
- [ ]  

---

# Description

## Github [https://github.com/ToontjeM/tondemo](https://github.com/ToontjeM/tondemo)

# Reference Architectures

![EDB-RA-1.png](Ton%20demo%2055ab5b3500e046d1ad2e0a96146af8a8/EDB-RA-1.png)

![EDB-RA-2.png](Ton%20demo%2055ab5b3500e046d1ad2e0a96146af8a8/EDB-RA-2.png)

![EDB-RA-3.png](Ton%20demo%2055ab5b3500e046d1ad2e0a96146af8a8/EDB-RA-3.png)

---

# edb-deployment

### Configure

Creates files to provision the project environment

`source ~/.edb_repo_user && edb-deployment virtualbox configure tondemo -u $USER:$PASSWORD -m 2048 -c 2 -k $HOME/.ssh/id_rsa_personal.pub -K $HOME/.ssh/id_rsa_personal`

### Provision

Provisions the environment according to project configured using configure. `edb-deployment provision tondemo`

Provision creates a Vagrantfile in `~/.edb-deployment/virtualbox/tondemo/`. The IMAGE_NAME needs to be changed from `RockyLinux/8` to `generic/rocky8`. RockyLinux/8 doesn't have the VirtualBox Guest Extensions installed and is therefor a false image for VirtualBox.

See:  ‣ 

Looks like `mwedb/rockylinux8` is a possibility as well.

⚠️ **Before provisioning, change ~/.edb-deployment/virtualbox/tondemo/Vagrantfile to reference the right box.**

Then `edb-deployment virtualbox provision tondemo`

### Deploy

Deploys EDB software into the project

To deploy using edb-deployment's ansible `sshpass` needs to be installed on the local machine. `brew install hudochenkov/sshpass/sshpass`

Make sure the 192.168.81.* range is removed from ˜/.ssh/known_hosts

### Destroy

Destroys instances

`edb-deployment virtualbox destroy tondemo`

### Remove

---

## Logs / passwords

Ansible logs in `.edb-deployment/log/virtualbox/tondemo.log`

All password are stored in `~/.edb-deployment/baremetal/test/.edbpass`

```
(virtualbox) ? ~/postgresdemo **ls ~/.edb-deployment/baremetal/test/.edbpass**                                    [ton.machielsen@MAC-C02G44RZMD6R]
barman_pass        enterprisedb_pass  pemadmin_pass      pgpool_pass
efm_pass           pcpadmin_pass      pemagent_pass      repuser_pass
(virtualbox) √ ~/postgresdemo **cat ~/.edb-deployment/baremetal/test/.edbpass/barman_pass**                       [ton.machielsen@MAC-C02G44RZMD6R]
LTtJFadehGnxXWrjcdQI
```

## Servers

At the end of the provisioning script you will get the server IP's (or by using `edb-deployment virtualbox display tondemo`)

```
PEM Server: https://192.168.81.100:8443/pem
PEM User: pemadmin
PEM Password: IgWYZpZVhciPkFBwOngs

    Name        Public IP          SSH User   Private IP
============================================================
     barman1    192.168.81.101     vagrant    192.168.81.101
        pem1    192.168.81.100     vagrant    192.168.81.100
    primary1    192.168.81.102     vagrant    192.168.81.102
```

ssh using `edb-deployment virtualbox ssh tondemo primary1`  vagrant / vagrant

### Demo flow

- 
- 

---

## Links

[Virtualbox Deployment Guide](https://docs.google.com/document/d/1cuzc6ggXWg0qk2oBZevMqfRoDsz52NVd9EqBpt-en1E/edit)

[https://github.com/ToontjeM/postgresdemo](https://github.com/ToontjeM/postgresdemo)