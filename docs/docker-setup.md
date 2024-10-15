## Docker on Open Media Vault

### Install Docker
1. Navigate to the `System -> Plugins` tab and search and install the `openmediavault-compose` plugin. Refresh the page after the installation.

2. Navigate to the `Services -> Compose -> Settings` tab. Then scroll down to the bottom and click `Reinstall Docker` to install Docker.

### Moving Docker Storage
1. Install `openmediavault-compose` plugin by logging into the NAS with SSH and execute the following:

```sh
$ sudo apt update
$ sudo apt install -y openmediavault-compose
```

2. Afterwards, refresh the page and navigate to the `Storage -> Shared Folders` and click on the `=` icon to create three folders:

```
docker            -> The Docker data directory, defined in /etc/docker/daemon.json
docker-compose    -> Location of compose files
docker-data       -> Location of persistent container data
docker-app        -> For personal use, storing Dockerfiles and data
```

3. Navigate to the `Services -> Compose` tab and enter the `Settings` interface. Configure the `Shared folder` for `Compose Files` and `Data`.

4. Access the SSH session again and execute the following to move Docker data to the shared folder, where `/src/dev-disk-by-uuid-XXYYZZ/docker` represents the absolute path of the shared folder. This can be obtained from the `Storage -> Shared Folders` list on the web interface:

```sh
$ su root
$ systemctl stop docker.socket docker.service
$ mv /var/lib/docker/* /srv/dev-disk-by-uuid-XXYYZZ/docker/
```

5. On the web interface, set the `Docker storage` to the absolute path of the `docker` shared folder. Save the settings and apply. Reboot the system.

The final value filled on the GUI:
```
Compose Files's Shared folder  -> on /dev/md0, docker-compose
Data's Shared folder           -> on /dev/md0, docker-data
Docker's Docker storage        -> on /srv/dev-disk-by-uuid-XXYYZZ/docker/
```

6. Guide for `Nextcloud with Docker`, `Jellyfin with Docker`, and `Portainer with Docker` eventually will be made.