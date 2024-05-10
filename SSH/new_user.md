# guide

## add new user for ssh login

```sh
adduser <username>
```

### create .ssh in new user directory and copy authorized keys

```sh
cd /home/user
mkdir .ssh
cp /root/.ssh/authorized_keys .ssh/
```

### set appropriate file permissions

```sh
sudo chmod 700 /home/user/.ssh

sudo chmod 600 /home/user/.ssh/authorized_keys

sudo chown username:username /home/username/.ssh -
```

### change Public Key

```sh
vi .ssh/authorized_keys
```

### allow user for ssh

```sh
sudo vi /etc/ssh/sshd_config
```

- search for :ALLowUsers and add your user

  example: AllowUsers user1 user2 user3

restart sshd

```sh
systemctl restart sshd
```
