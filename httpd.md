#### Install Htttpd
```sh
$ yum update
$ yum -y install httpd
```

#### Allow Apache Through the Firewall
*Allow the default HTTP and HTTPS port, ports 80 and 443, through firewalld:*
```sh
$ sudo firewall-cmd --permanent --add-port=80/tcp
sucsess
$ sudo firewall-cmd --permanent --add-port=443/tcp
success
```
*And reload the firewall:*
```sh
$ sudo firewall-cmd --reload
success
```
*Configure apache on  boot:*
```sh
$ systemctl start httpd
$ systemctl enable httpd
$ systemctl restart httpd 
```
*Check this ip server:*
```sh
$ ip addr
2: enp0s3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP group default qlen 1000
    link/ether 08:00:27:2a:3d:f4 brd ff:ff:ff:ff:ff:ff
    inet 192.168.100.195/24. (This here.)
```
*Access your browser: 192.168.100.195 and this page ![enter image description here](https://lh3.googleusercontent.com/f_zm9FRNnmC86WA6pZyJFuOEzrmEFlaH0FVAzPDep_cZv3YoI0bm7d0BXZep2acSAecTNbDcdJgH=s500 "screenshot-web-server")*
