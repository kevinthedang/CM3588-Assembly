## Setup Users

The following users should be apart of the distribution.

| Username | Password | has sudo? |
|----------|----------|-----------|
| pi       | pi       | Yes       |
| root     | fa       | No        |
|          |          |           |

### Remove the Default User
1. Log in as `root` through your given IP.
  * If you can't find this. Plug in your board into a monitor using hdmi and login as root. Run `ip a` for your IP so you can ssh anywhere in your network.

2. Remove the default `pi` user.

```sh
deluser pi
```

### Create the New User

3. Create a new user with whatever name you want.
    * `useradd` will do no prompts and create the user.
    * `adduser` will provide a prompt for password and create the user.

```sh
$ useradd <name of user>
$ passwd <name of user>
```

OR

```sh
$ adduser <name of user>
```

4. Add your new user to the sudo group.

```sh
$ usermod -aG sudo <name of user>
```

### SSH Configuration
For security, we can disable root ssh access and enable access to our new user.

5. Edit the `sshd_config`. You should have a group for your user. For example if a user was named `sample` then the group should be `sample`. You can change it like below (usually Line 24).

```sh
$ vim /etc/ssh/sshd_config

...

AllowGroups _ssh sample
```

6. Now that you have your user set to log in, restart the `ssh` daemon and exit. You can also do `CTRL+D` to logout.

```sh
$ systemctl restart sshd
$ exit
```

7. Now you can ssh into the nas using your new user!

```sh
$ ssh <user>@<ip_address>
```
