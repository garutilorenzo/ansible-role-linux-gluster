[![GitHub issues](https://img.shields.io/github/issues/garutilorenzo/ansible-role-linux-gluster)](https://github.com/garutilorenzo/ansible-role-linux-gluster/issues)
![GitHub](https://img.shields.io/github/license/garutilorenzo/ansible-role-linux-gluster)
[![GitHub forks](https://img.shields.io/github/forks/garutilorenzo/ansible-role-linux-gluster)](https://github.com/garutilorenzo/ansible-role-linux-gluster/network)
[![GitHub stars](https://img.shields.io/github/stars/garutilorenzo/ansible-role-linux-gluster)](https://github.com/garutilorenzo/ansible-role-linux-gluster/stargazers)

# Install and configure gluster in HA mode

Ansible role used to install and configure gluster, NFS ganesha and pacemaker for HA

## Requirements

Install ansible, ipaddr and netaddr:

```
pip install -r requirements.txt
```

Download the role form GitHub:

```
ansible-galaxy install git+https://github.com/garutilorenzo/ansible-role-linux-gluster.git
```

Your inventory file must have the following groups:

* gluster

## Role Variables

**NOTE:** only replicated volume supported at the moment 

This role accept this variables:

| Var   | Required |  Default | Desc |
| ------- | ------- | ----------- |  ----------- |
| `gluster_vip_ip`       | `yes`       | `dns`       | Gluster VIP ip used for HA. Must be in the network subnet where gluster and pacemaker daemon are listening |
| `hacluster_password`       | `yes`       | `dns`       | Secrets used for hacluster user |
| `gluster_subnet`       | `no`       | ``       | If the server have multiple network interfaces, specify the subnet where the gluster and pacemaker daemon are listening. |
| `gluster_resolv_mode`       | `no`       | `dns`       | Determinate how nodes will be resolved, used for local testing purposes where dns is not available. |
| `gluster_volume`       | `no`       | `example`       | The name of the NFS volume exposed by NFS ganesha |
| `gluster_path`       | `no`       | `/tank/`       | Gluster local storage directory |
| `gluster_volume_type`       | `no`       | `replica`       | Gluster volume type `stripe | replica | disperse`. For more detail see [here](https://docs.gluster.org/en/v3/Administrator%20Guide/Setting%20Up%20Volumes/) |
| `gluster_volume_replica_count_type`       | `no`       | `3`       | Gluster local storage directory |

## Example playbook

Here one example playbook:

```yaml
- hosts: gluster
  become: yes
  remote_user: vagrant
  roles: 
    - role: ansible-role-linux-gluster
```

## TODO

* Support for striped and disperse volume
* Create the FS not only the directory