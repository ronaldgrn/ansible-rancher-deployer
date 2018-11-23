
# ansible-rancher  
Ansible yaml files for configuring a single node rancher 2.0 server on Ubuntu 16.04.
  
This was only tested on Hetzner Cloud but should work anywhere.  
  
This script configures/installs the following  
  
- python2 (needed for ansible)  
- ufw  
- fail2ban  
- /etc/sysctl.conf
- rancher/rancher:latest

The rancher data is persisted in `/opt/rancher` and remains across multiple runs.
  
## Deploy Instructions  
Create a hosts file and replace placeholders with your IP and (optional) domain.
  
```  
cp hosts.sample hosts  
```


Run  the following command to deploy
```  
ansible-playbook -i hosts deploy.yml  
```  
    
**Notes:**  
 - Leave domain as "unset" if you do not wish to register a letsencrypt certificate. (ideal for testing)
 - The ssl certificate is issued using letsencrypt so the usual ratelimits apply.
 - Script is _potentially_ destructive. While your data persists in `/opt/rancher` the container _will_ be recreated each run.


PR's welcome