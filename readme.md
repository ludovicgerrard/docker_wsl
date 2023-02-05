to install docker engine used this instructions (https://docs.docker.com/engine/install/ubuntu/)

after installing docker engine if service not working,  follow this article (https://crapts.org/2022/05/15/install-docker-in-wsl2-with-ubuntu-22-04-lts/)

This article relate about this

When installing Docker in WSL2 with Ubuntu 20.04 LTS, you can install Docker by following the official instructions. After installing Docker, you can start Docker by simply running sudo service docker start.

However, when you install Docker in WSL2 with the latest Ubuntu 22.04 LTS, you will notice that Docker will not start after running sudo service docker start. You will receive errors when starting a container, and sudo service docker status will tell you Docker is not running.

The reason this errors occurs is because Ubuntu 22.04 LTS uses iptables-nft by default. You need to switch to iptables-legacy so that Docker will work again:

Run sudo update-alternatives --config iptables
Enter 1 to select iptables-legacy
Now run sudo service docker start, and Docker will start as expected!

For network issu follow this step (https://github.com/docker/for-linux/issues/1105) detailled below
If you run Debian try:
sudo update-alternatives --set iptables /usr/sbin/iptables-legacy

ensure that /etc/sysctl.conf includes:
net.ipv4.ip_forward = 1

Third guess: Are you using openvpn?
If so, create the bridge yourself:
`sudo apt-get install bridge-utils

sudo brctl addbr docker0

sudo ip addr add 10.1.0.1/24 dev docker0

sudo ip link set dev docker0 up

ip addr show docker0

sudo systemctl restart docker

sudo iptables -t nat -L -n`
