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

#### 1.  Get initial clones of repositories
This command will get a copy of the repository that will be the base for the deployment.  Run this from your home folder, ie "/home/ubuntu"
```bash
git clone https://github.com/USGS-WiM/StreamStats.git
```

#### 2.  Setup GitAutoDeploy
To set it up, do the following:

 - enter the matching for your project(s) in the GitAutoDeploy.conf.json file
 - start the server by typing "python GitAutoDeploy.py" 
to run it as a daemon add "--daemon-mode"
 - On the Github page go to a repository, then "Admin", "Service Hooks", 
"Post-Receive URLs" and add the url of your machine + port (e.g. http://example.com:8001).  Specify Content type as application/json

#### 2.  Set up symobolic links to apache 
This creates a symbolic link between the github repository in your home folder and the apache web server home folder.  Here we can specify to only make the symbolic link from a specific folder in the github reposity, ie "/dist" in the example below.

```bash
ln -s /home/ubuntu/streamstats/dist /var/www/streamstats
```