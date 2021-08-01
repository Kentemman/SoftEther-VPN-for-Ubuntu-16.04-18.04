# SoftEther VPN for Ubuntu 16.04 | 18.04

## Softether-install-for-ubuntu

### You will need to be root user for this!
First update the OS:
```
sudo apt-get update && sudo apt-get upgrade -y && sudo apt-get autoremove -y
```
Next:
```
apt-get -y install build-essential wget curl gcc make wget tzdata git libreadline-dev libncurses-dev libssl-dev zlib1g-dev
```
Download latest SoftEther with these commands:
```
wget https://github.com/SoftEtherVPN/SoftEtherVPN_Stable/releases/download/v4.36-9754-beta/softether-vpnserver-v4.36-9754-beta-2021.06.07-linux-x64-64bit.tar.gz
tar xzf softether-vpnserver-v4.36-9754-beta-2021.06.07-linux-x64-64bit.tar.gz && rm softether-vpnserver-v4.36-9754-beta-2021.06.07-linux-x64-64bit.tar.gz
```
## Configure SoftEther
```
cd vpnserver && sudo make
```
```
cd ..
sudo mv vpnserver /usr/local && cd /usr/local/vpnserver/
sudo chmod 600 *
sudo chmod 700 vpnserver vpncmd
```
```
sudo ./vpnserver start
sudo ./vpncmd
```
### Select 1 and Enter Twice

Set Password
```
ServerPasswordSet
```
### And type exit & Paste this:
```
sudo cat >> /lib/systemd/system/vpnserver.service << EOF
[Unit]
Description=SoftEther VPN Server
After=network.target

[Service]
Type=forking
ExecStart=/usr/local/vpnserver/vpnserver start
ExecStop=/usr/local/vpnserver/vpnserver stop

[Install]
WantedBy=multi-user.target
EOF
```
### Press Q and Enter:

Next Paste this:
```
echo net.ipv4.ip_forward = 1 | ${SUDO} tee -a /etc/sysctl.conf
echo net.ipv6.ip_forward = 1 | ${SUDO} tee -a /etc/sysctl.conf
```
```
systemctl enable vpnserver
systemctl start vpnserver
systemctl stop vpnserver
systemctl restart vpnserver
systemctl status vpnserver
```
And then
```
sudo ufw allow 500,4500/udp
ufw allow 443
ufw allow 1701
ufw allow 1194
ufw allow 5555
```
## Setting up server with vpncmd
To do.

## Updating SoftEther
To do.
