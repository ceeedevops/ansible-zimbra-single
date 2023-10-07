## Installing Zimbra on a Single Server Using Ansible

The role `ansible-zimbra-single` automates the installation of single-server Zimbra Open Source Edition `v8.8.15` and `v9.0.0` on `CentOS 7`, CentOS `8`, Rocky Linux `8`, Ubuntu `18.04`, and Ubuntu `20.04`.

## Installation Prerequisites

1. Must be a fresh CentOS `7`, CentOS `8`, Rocky Linux `8`, Ubuntu `18.04`, or Ubuntu `20.04` minimal installation.
2. Static network configuration must be already set.
3. Ansible control node must have the `netaddr` Python module installed.

Installing Ansible and  `netaddr` module using `pip`

```
apt install python3-pip
python3 -m pip install ansible
python3 -m pip install netaddr
```
## Clone The Repository

```
git clone https://github.com/ceeedevops/ansible-zimbra-single.git
```

##  Example Playbook

> [!IMPORTANT] 
> Ansible managed node tested to run as `root` user only!

Create playbook similar to  below:

```bssh
vi site.yml
```

```yaml
--- 
- hosts: zimbra
  vars:
    zimbra_timezone: Asia/Colombo
    zimbra_fqdn: mail.c-eee.org
    zimbra_admin_password: ChangeMe@1
  roles:
    - ansible-zimbra-single
```

> [!IMPORTANT]
> Change the following roles variables to suit your needs in your play book

```
zimbra_timezone: Asia/Colombo
zimbra_fqdn: mail.c-eee.org
zimbra_admin_password: ChangeMe@1
```


Then run as follows:

    # ansible-playbook site.yml --tags install

If you want to setup Zimbra 9 instead:

    # ansible-playbook site.yml --tags zimbra9

Other Features
--------------

The role also installs Fail2Ban configured with predetermined jails and filters. You can view them in /etc/fail2ban directory.

    # fail2ban-client status
      Status
      |- Number of jail:	4
      `- Jail list:	sshd, zimbra-admin, zimbra-smtp, zimbra-webmail

License
-------

MIT License

Author Information
------------------

- Author: Jan Cubillan
- GitHub: https://github.com/jancubillan
