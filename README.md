# FPOracle

**A little documentation to make a server multi-function with Oracle Free Tier.**

It contains :
- DuckDNS to have a free domain name (and subdomains)
- Portainer to manage and deploy stack and containers with Docker
- Nginx Proxy Manager to implement reverse proxy
- MCSManager to host and manage Minecraft servers on a web interface
- Jellyfin to host and manage a media server to watch your movies, series etc..
- Wireguard to host a VPN (for me, hosted in Marseille, France)

## Table of contents

- [FPOracle](#fporacle)
  - [Table of contents](#table-of-contents)
  - [Server creation on Oracle \& First config](#server-creation-on-oracle--first-config)
  - [DuckDNS](#duckdns)
  - [Portainer](#portainer)
  - [Nginx Proxy Manager](#nginx-proxy-manager)
  - [Wireguard VPN](#wireguard-vpn)
  - [MCSManager](#mcsmanager)
  - [Jellyfin](#jellyfin)

## Server creation on Oracle & First config

All begins with an account creation on [Oracle Cloud Free Tier](https://www.oracle.com/fr/cloud/free/), with a real credit card (no money will be taken, it's just for verification). Lydia or  online bank is not allowed.

Then, you can create a new instance (in Compute tab) with the max configuration for free :
- ***Image*** : Canonical Ubuntu 22.04 Minimal aarch64
- ***Arm-based processor*** : Ampere A1 Compute (VM.Standard.A1.Flex)
- ***OCPU*** : 4 core equivalent 
- ***RAM*** : 24 GB
- ***Boot volume size*** : 200 GB

**DO NOT FORGET TO SAVE THE SSH PRIVATE KEY, YOU MUST IT TO CONNECT TO YOUR SERVER FOR THE FIRST TIME. If you forget it, you must redo all the procedure of instance creation.**

> If the following error appears : `Error: Out of capacity...` you must wait and retry the instance creation (this can take hours or days before Oracle re-allocate some un-used machines).
<br />Some scripts are available to check the availability of the machines. You can find them [here](https://github.com/hitrov/oci-arm-host-capacity). (not tested)

When the instance is created, you can connect to it with the public IP and the private key. You can find the public IP in the instance details.

```bash
ssh -i /path/to/private/key ubuntu@public_ip
```
ubuntu user has not password, to create it :
```bash
sudo passwd ubuntu
```
and to enable ssh connection with password :
```bash
sudo nano /etc/ssh/sshd_config
```
and change the line `PasswordAuthentication no` to `PasswordAuthentication yes`. Then, restart sshd service :
```bash
sudo systemctl restart sshd
```
You can even do a config file to connect to the server :
```bash
nano ~/.ssh/config
```
and adding the following lines :
```bash
Host oracle-server
    HostName 'your-public-ip'
    User ubuntu
```
To connect to the server without password and private key explicitly, you can copy your public key to the server :
```bash
ssk-keygen
ssh-copy-id oracle-server
```
Before beginning to install all the services, you must update and upgrade the server :
```bash
sudo apt update && sudo apt upgrade -y
```

## DuckDNS

## Portainer

## Nginx Proxy Manager

## Wireguard VPN

## MCSManager

## Jellyfin