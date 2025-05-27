
# ansible-rancher  
Ansible playbook for securing, installing and upgrading a single node rancher 2.X server on Ubuntu.

This playbook is compatible with Ubuntu 22.04 & 24.04.
  
This was tested on Hetzner Cloud and DigitalOcean but should work anywhere.
  
This script does the following:
  
- installs python3 (needed for ansible)
- installs fail2ban (uses default config)
- disables ssh password authentication
- hardens networking with sysctl
- (optionally) secures ports with ufw
- installs the specified version of docker
- starts a container with the image: rancher/rancher:stable

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

The `ufw` role is commented out by default as we recommend using your providers firewall. Uncomment this from deploy.yml to configure ufw to only allow the ports rancher needs to work.


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