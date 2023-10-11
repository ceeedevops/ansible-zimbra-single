## Installing Zimbra on a Single Server Using Ansible

The role `ansible-zimbra-single` automates the installation of single-server Zimbra Open Source Edition `v8.8.15` and `v9.0.0` on `CentOS 7`, CentOS `8`, Rocky Linux `8`, Ubuntu `18.04`, and Ubuntu `20.04`.

## Installation Prerequisites

1. Must be a fresh CentOS `7`, CentOS `8`, Rocky Linux `8`, Ubuntu `18.04`, or Ubuntu `20.04` minimal installation.
2. Static network configuration must be already set.
3. Ansible control node must have the `netaddr` Python module installed.

Installing Ansible and  `netaddr` module using `pip`

```bash
sudo apt install python3-pip
sudo python3 -m pip install ansible
sudo python3 -m pip install netaddr
```
## Clone The Repository

```bash
git clone https://github.com/ceeedevops/ansible-zimbra-single.git
```

##  Example Playbook

> [!IMPORTANT] 
> Ansible managed node tested to run as `root` user only!

Create playbook similar to  below:

```bssh
nano site.yml
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

```bash
zimbra_timezone: Asia/Colombo
zimbra_fqdn: mail.c-eee.org
zimbra_admin_password: ChangeMe@1
```
## Modify the hosts file in the repository root directory

```bash
sudo nano ansible-zimbra-single/hosts
```
- Modify the `ip` address of your zimbra server  as per your setup

```bash
[zimbra]
10.10.0.25
```

- Then run as follows:

```bash
ansible-playbook -i ansible-zimbra-single/hosts site.yml --tags install
```

- If you want to setup Zimbra 9 instead:

```bash
ansible-playbook -i ansible-zimbra-single/hosts site.yml --tags zimbra9
```

## Other Features

The job also installs Fail2Ban, which is preconfigured with jails and filters. They can be found in the /etc/fail2ban directory.

```bash
fail2ban-client status
```
- Output:

```bash
Status
  |- Number of jail:	4
    `- Jail list:	sshd, zimbra-admin, zimbra-smtp, zimbra-webmail
```

## License

MIT License

## Credits to Original Author

Dear Jan: We could not have done this so easily without your excellent effort and contributions to the community. 

- Author: Jan Cubillan
- GitHub: https://github.com/jancubillan
