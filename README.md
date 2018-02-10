# Example Project Virtuozzo 7.0
This is an example setup and configuration of an virtuozzo host over ansible.

## Requirements

### Vagrant
Vagrant Version: 2.0.2

```
vagrant plugin install ansible
vagrant plugin install vagrant-reload
```

## Usage

```
vagrant up
vagrant ssh
sudo vztmpl-dl --gpg-check --list-remote
sudo vzctl create 101 --ostemplate ubuntu-14.04-x86-minimal
sudo vzctl set 101 --ipadd 10.1.2.3 --save
sudo vzctl set 101 --nameserver 10.0.2.1 --save
sudo vzctl start 101
sudo vzlist
```

