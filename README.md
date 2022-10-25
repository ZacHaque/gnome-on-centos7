# gnome-on-centos7
 
Run following command to install GNOME on the Centos7

Install xrdp
```
sudo yum install -y epel-release
sudo yum install -y xrdp tigervnc-server
sudo systemctl enable xrdp
sudo systemctl start xrdp
```

Change file permission
```
sudo chcon --type=bin_t /usr/sbin/xrdp
sudo chcon --type=bin_t /usr/sbin/xrdp-sesman
```

Open firewall ports
```
sudo firewall-cmd --add-port=3350/tcp --permanent
sudo firewall-cmd --add-port=3389/tcp --permanent
sudo firewall-cmd --reload
```

How to Install GNOME Desktop Environment
```
sudo yum update -y
sudo yum groupinstall "GNOME DESKTOP" "Graphical Administration Tools" -y
echo "gnome-session" > ~/.Xclients
chmod +x ~/.Xclients
sudo systemctl restart xrdp.service
```

Setting GUI target

Since VPS are mostly with the command line interface you will need to set GUI as a boot target so that every time you restart the VPS the OS should boot in GUI environment:

`sudo systemctl get-default`

if the output says multi-user.target than you will need to run below command:

`sudo systemctl set-default graphical.target`

and than reboot by below command

`reboot`

Now we should be able to RDP in to the GNOME
