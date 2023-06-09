# Ansible Starter

This is the most basic Ansible template I did after I figured it out how to even get started. From this point it should be very simple to use. It is not advanced (yet) but it should get you up and running in no time. I will be using it myself to start a project and will improve it as necessary.

- IDE used: Visual Studio Code.
- Fully linted.
- No bloat.

## Prerequisites

- A computer.
- Another computer as server such as raspberry pi.
- Basic Linux computer skills.

## Setup

- Install ansible on your machine. `brew install ansible`, `apt install ansible`, etc. It will install ansible and ansible
- SSH Key
  - Option 1 (recommended): Setup ssh key on the server so you could connect securely without inputing password.
  - Option 2: Use username and password. Add password in the inventory: `ansible_password = *******` just under `ansible_username` line.
- Adjust ever so slightly the inventory and maybe the playbook
- ???
- Profit!

### (Option 1) SSH Key

```sh
ssh-keygen -t ed25519 -o -a 100 -C "ansible"
ssh-copy-id -i ansible -s [host]
# - -s means it is secured already with a other.
# - use -n to do a dry run.
# - change [host] to server host or ip where you want to send the key.
```

### (Option 2) Password

- You many need to install sshpass. The way I got it working on mac is:

 ```sh
 curl -L https://raw.githubusercontent.com/kadwanev/bigboybrew/master/Library/Formula/sshpass.rb > sshpass.rb && brew install sshpass.rb && rm sshpass.rb\n
 ```

Your milage may vary.

### Ad-hoc command examples

- Run sudo apt update on inventory all with module apt with sudo: `ansible all -m apt -a update_cache=true --become --ask-become-pass`
- Install whatever package you want using apt with sudo on inventory pi with sudo ansible pi -m apt -a name=[some package] --become --ask-become-pass

### Playbook

- Does whatever is defined in the file: `ansible-playbook playbooks/misc.yml`
- Use `--become --ask-become-pass` if have password or ssh key with password.

### SSH Agent (Optional)

```sh
# Agent will enter password for you :)
# Look up how to do it if it doesn't work...
ssh-add eval "$(ssh-agent -s)"
ssh-add ~/.ssh/ansible
```
