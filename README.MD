# github-auto-deploy

> Python webserver that listens for webhooks on a reposity and then does a pull to get latest code   
> 
forked from [http://logsol.github.io/Github-Auto-Deploy/](http://logsol.github.io/Github-Auto-Deploy/)   

>Requires linux, apache


## Project setup

##### required software

 - python
 - git
```bash
sudo apt-get install python git
```

#### 1.  Get initial clones of repositories to be auto-deployed
This command will get a copy of the repository that will be the base for the deployment.  Run this from your home folder, ie "/home/ubuntu"
```bash
cd /home/ubuntu
git clone https://github.com/USGS-WiM/StreamStats.git
```

#### 2.  Set up symobolic links for apache 
This creates a symbolic link between the github repository in your home folder and the apache web server home folder.  Here we can specify to only make the symbolic link from a specific folder in the github reposity, ie "/dist" in the example below.

```bash
ln -s /home/ubuntu/streamstats/dist /var/www/streamstats
```

#### 3.  Get Github Auto Deploy
Get a copy of this repo, store in "/opt".  We can't keep this in the home dir because that is encrypted and doesn't stay running after logging out
```bash
cd /opt
git clone https://github.com/USGS-WiM/Github-Auto-Deploy.git
```

#### 4.  Setup GitAutoDeploy
 Edit the file "/opt/Github-Auto-Deploy/GitAutoDeploy.conf.json"
```bash
sudo nano /opt/Github-Auto-Deploy/GitAutoDeploy.conf.json
```

#### 5.  Set up webhook on Github.com
On the Github page go to a repository, then "Admin", "Service Hooks", "Post-Receive URLs" and add the url of your machine + port (e.g. http://example.com:8001).  Specify Content type as application/json

#### 6.  Start autodeploy as a background service
This command keep the service running as a background service

```bash
 /usr/bin/nohup python /opt/Github-Auto-Deploy/GitAutoDeploy.py > /dev/null 2>&1 &
```