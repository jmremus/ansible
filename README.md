# Jmremus's Ansible Homelab Config

## Intro
This is an Ansible setup for a homelab running under:
  - Proxmox (debian 5.13)
  - Podman
  - Guix

There are roles to set up the following services:
  - Dashy    (a configurable homepage)
  - InfluxDB (time series DB)
  - Grafana  (dashboard)
  - Radicale (CalDAV/CardDAV)
  - AgenDAV  (a calendar frontend)
  - Gitea    (git)
  - Pihole   (ad blocking)
  - Pinry    (A pinboard app)

## Instructions
As a precaution, the following roles are commented out by default:
  - Pihole (see WARNING) 
  - Podman (it replaces /etc/containers.conf to add GUIX rootless support)

Make sure you replace all lines labeled 'CHANGE_ME' with your platform-specific
config. 
Files that need to be configured:
  - inventory.yaml
  - site.yaml
  - group_vars/all
  - roles/agendav/tasks/main.yml
  - roles/pihole/files (WARNING: this will overwrite your ufw config)

Once this is done, run ./ansible.sh

**WARNING: Pihole is run as a rootless container, and listens to DNS on port 1053**
**and as part of the install, it will overwrite the system's firewall**
**config (ufw) in order to redirect port 1053 to 53. It also assumes your**
**subnet is 192.168.1.0/24.**
**Before enabling Pihole, inspect ./roles/pihole to make sure you understand**
**and accept the changes that will be made.**
**Also do not forget to install and enable ufw via apt-get beforehand**


