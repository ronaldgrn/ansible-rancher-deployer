
# ansible-rancher  
Ansible yaml files for configuring a single node rancher 2.0 server on Ubuntu 16.04.
  
This was only tested on Hetzner Cloud but should work anywhere.
  
This script does the following:
  
- installs python2 (needed for ansible)
- secures ports with ufw
- installs fail2ban (uses default config)
- disables ssh password authentication
- hardens networking with sysctl
- installs docker 17.03.2
- starts a container with the image: rancher/rancher:latest

*Requirements:*
- ansible
- ssh-key for target server (password auth will be disabled)

The rancher data is persisted in `/opt/rancher` and remains across multiple runs.
  
## Deploy Instructions  
Copy `hosts.sample` to `hosts` and replace placeholders with your IP and (optional) domain.
  
```  
cp hosts.sample hosts  
```

If you need a specific version of rancher, change `rancher_tag` to the desired version.


Run  the following command to deploy
```  
ansible-playbook -i hosts deploy.yml  
```

## Update Instructions
To update a rancher deploy created using this script, simply re-run the deploy command. 
It is **highly recommended** to backup your datastore (/opt/rancher) in case of any errors.


## Important Notes 
 - Leave domain as "unset" if you do not wish to register a letsencrypt certificate. (ideal for testing)
 - The ssl certificate is issued using letsencrypt so the usual ratelimits apply.
 - Re-running this script is _potentially_ destructive. While your data persists in `/opt/rancher` the container _will_ be recreated each run.


PR's welcome