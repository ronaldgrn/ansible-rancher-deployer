
# ansible-rancher  
Ansible yaml files for configuring a single node rancher 2.0 server on Ubuntu 16.04.
  
This was only tested on Hetzner Cloud but should work anywhere.  
  
This script configures/installs the following  
  
- python2 (needed for ansible)  
- ufw  
- fail2ban  
- /etc/sysctl.conf  
  
## Deploy Instructions  
Create a hosts file and replace placeholders with your IP and (optional_ domain.  
  
```  
cp hosts.sample hosts  
```


Run  the following command to deploy
```  
ansible-playbook -i hosts deploy.yml  
```  
    
**Notes:**  
 - Leave domain as "unset" if you do not wish to register a letsencrypt certificate.
 - Rancher 2.0 uses letsencrypt so the usual ratelimits apply.

PR's welcome