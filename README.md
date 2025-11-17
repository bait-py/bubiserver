# BUBI Server Installation and Configuration 🏠

Welcome to the **BUBI Server** repository. Here you will find everything you need to set up and customize your own home server, following the same structure we use in BUBI.

![Final Result](https://raw.githubusercontent.com/bait-py/bubiserver/main/BUBIServerResult1.jpg)
![Final Result 2](https://raw.githubusercontent.com/bait-py/bubiserver/main/BUBIServerResult2.jpg)

---

## Prerequisites

* **Hardware:**

  * Raspberry Pi 4
  * NAS or preferred storage system
* **Software:**

  * USB drive with Ubuntu Server installed
  * Remote management tools (SSH, VNC, etc.)

---

## Installation

### 1. Operating System

Install Ubuntu Server on the Raspberry Pi 4 to begin the setup process.

### 2. Network Configuration

* Assign a static IP address to your server for easier access.
* Install and configure SSH if it is not already enabled.

### 3. NAS Configuration and Pairing

The configuration may vary depending on the OS used on your NAS. Below is the process using **Rockstor**:

* Assign a static IP address to the NAS and install Rockstor.
* From the Rockstor web interface:

  * Go to **Disks** and format all drives, ensuring no previous file systems remain.
  * In **Pools**, create a new pool with the disks you want to use.
  * Select the RAID level (RAID 0 recommended when using disks of different sizes/brands).
  * In **File Sharing**, enable NFS and create a new share with default permissions, adding your server’s IP.
* On the server, edit `/etc/fstab` to auto-mount the NAS share:

  ```
  IPOfNAS:/export/ShareName  /MountPoint  nfs  defaults  0  0
  ```
* Run:

  ```
  mount -a
  ```

  to mount the share.

### 4. Installing Docker and Portainer

* Update the system:

  ```bash
  sudo apt update && sudo apt upgrade -y
  ```
* Install Docker:

  ```bash
  sudo apt install docker.io
  sudo systemctl enable docker
  sudo systemctl start docker
  sudo systemctl status docker
  ```
* Install Portainer using Docker:

  ```bash
  sudo docker run -d -p 8000:8000 -p 9000:9000 --name=portainer --restart=always \
  -v /var/run/docker.sock:/var/run/docker.sock -v /bubiapps/portainer:/data \
  portainer/portainer
  ```
* Access the Portainer interface:

  ```
  http://ServerIP:9000/
  ```

### 5. Initial Portainer Setup

* On your first login, create the administrator account.
* Set up your first environment — in this case, the local environment.

### 6. Installing the First Service (Homepage)

* Inside Portainer, open your environment and go to **Stacks**.
* Click **+ Add Stack**.
* Paste the Homepage compose file into the Web Editor:
  [Homepage Compose 🔗](https://github.com/bait-py/bubiserver/blob/main/portainer%20docker%20compose/homepage.yaml)
* Deploy the stack.
* Access the dashboard:

  ```
  http://ServerIP:7200
  ```
* If you want the same configuration as BUBI Server, use the files here:
  [Homepage Config 🔗](https://github.com/bait-py/bubiserver/tree/main/homepage%20config)

---

## Installing Additional Services & Extra Information ⚙

You can find more Docker Compose files for additional services in this repository:
[Docker Compose Files 🔗](https://github.com/bait-py/bubiserver/tree/main/portainer%20docker%20compose)

You can also explore additional services here:

* [Docker Hub](https://hub.docker.com/search?q=linuxserver)
* [linuxserver.io](https://docs.linuxserver.io/)

---

## Contributions 🎉

We welcome suggestions, improvements, and new features. Feel free to contribute!

---

## License 📝

This project is licensed under Creative Commons:
**BUBI Server © 2024 by BUBI — CC BY 4.0**

---

Thank you for using BUBI Server. Enjoy building your own local cloud environment! 🚀
