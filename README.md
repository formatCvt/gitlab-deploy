# Gitlab deploy daemon

Gitlab post-receive webhook receiver

## Install

* Copy config file to /etc/gitlab-deploy.json


    sudo cp config.example.json /etc/gitlab-deploy.json


* Edit config file

* Copy init script

    sudo cp extra/debian/gitlab-deploy.init /etc/init.d/gitlab-deploy # debian style
    sudo cp extra/centos/gitlab-deploy.init /etc/init.d/gitlab-deploy # redhat style

    sudo chmod +x /etc/init.d/gitlab-deploy

* Start deamon

    sudo /etc/init.d/gitlab-deamon start


* Add to run level
    
    sudo update-rc.d gitlab-deploy defaults # debian style
    sudo /sbin/chkconfig --add gitlab-deploy # redhat style


## Config file

Config file is JSON


    {
        "port": 8001,
        "allow_hosts" : ["207.97.227.253", "50.57.128.197", "108.171.174.178", "50.57.231.61"],
        "repositories":
        [{
            "url": "https://gitlab.com/litmisty/gitlab-deploy",
            "path": "/home/jung/tmp/gitlab-deploy",
            "branch": "master",
            "command": "echo deploying"
        }]
    }


### port

The service port

### allow_hosts

IPs of gitlab servers

### repositories

Target local repositories.

Daemon will check Url and branch, and checkout source from gitlab to target 'path'

Make sure to check the **url**. 

**Do not enter the git repository url, use the gitlab project url**

'command' will execute after checkout ended

