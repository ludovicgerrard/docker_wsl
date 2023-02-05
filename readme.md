to install docker engine used this instructions (https://docs.docker.com/engine/install/ubuntu/)

after installing docker engine if service not working,  follow this article (https://crapts.org/2022/05/15/install-docker-in-wsl2-with-ubuntu-22-04-lts/)

This article relate about this

When installing Docker in WSL2 with Ubuntu 20.04 LTS, you can install Docker by following the official instructions. After installing Docker, you can start Docker by simply running sudo service docker start.

However, when you install Docker in WSL2 with the latest Ubuntu 22.04 LTS, you will notice that Docker will not start after running sudo service docker start. You will receive errors when starting a container, and sudo service docker status will tell you Docker is not running.

The reason this errors occurs is because Ubuntu 22.04 LTS uses iptables-nft by default. You need to switch to iptables-legacy so that Docker will work again:

Run sudo update-alternatives --config iptables
Enter 1 to select iptables-legacy
Now run sudo service docker start, and Docker will start as expected!
