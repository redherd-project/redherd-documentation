# Setup :: Intro

The entire solution is cross platform and can be deployed both on premise and in a Cloud-based environment. The released implementation focuses on a `Debian` host machine tested both locally and remotely.

## System requirements

Following are some recommended and tested specifications for the host machine:

- Ubuntu >= 18.04
- 8+ GB RAM
- 50+ GB HDD
- 2+ CPUs

## 1. Obtain

The first step involves to obtain the latest release of the framework cloning it from the official GitHub [`repository`](https://github.com/redherd-project/redherd-framework):

```bash
$ git clone https://github.com/redherd-project/redherd-framework.git
```

## 2. Deploy

The second step includes the deploy of RedHerd on the host machine. It could be performed running the specifically developed `deploy.sh` bash script which implements a manually triggered but fully automated procedure on a Debian-based device.

### 2.1 Select the public interface

Select the external IP address which all `assets`/`clients` will connect to:

```bash
$ ip a

1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host 
       valid_lft forever preferred_lft forever
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc mq state UP group default qlen 1000
    link/ether 00:15:5d:01:84:00 brd ff:ff:ff:ff:ff:ff
    inet 172.23.163.163/20 brd 172.23.175.255 scope global dynamic noprefixroute eth0
       valid_lft 82990sec preferred_lft 82990sec
    inet6 fe80::ab6c:c19c:6d33:aff1/64 scope link noprefixroute 
       valid_lft forever preferred_lft forever
```

### 2.2 Install Docker

Before going further, Docker installation is necessary to deploy and launch the RedHerd framework:

```bash
$ cd redherd-framework
$ sudo ./redherd-framework/utils/install_docker.sh
```

<iframe width="560" height="315" src="https://www.youtube.com/embed/APJO3MQloLQ" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" style="margin-bottom: 30px;" allowfullscreen></iframe>

### 2.3 Launch the deploy script

Using the command line provided below, the deploy script will initialize the database (`-db`), generate the Certification Authority (CA) (`-ca`), the SSH keys (`-k`), the `Distribution-Server` credentials (`-u`) and the OpenVPN configurations for 10 (`-a 10`) endpoints (`assets`/`clients`). You can join to the framework up to `256` endpoints.

```bash
$ cd redherd-framework
$ sudo ./deploy.sh -s 172.23.163.163 -db -ca -k -u -a 10

  *                                          #                                          
 **                                          (#                                         
 **                                          ((#                                        
 ***                                        #((#                                        
  ****(         (*****    ((((((          #((((                                         
   *******************   ((((((((((((((((((((#                                          
     *****************   ((((((((((((((((((                                             
          ***********       (((((((((((                                                 
              *******      (((((((#                                                     
                  (*****   (((   ______ _______ ______  _     _ _______  ______ ______  
                   *****  (((   |_____/ |______ |     \ |_____| |______ |_____/ |     \ 
                    ****  ((    |    \_ |______ |_____/ |     | |______ |    \_ |_____/ 
                     *** ((#                                                            
                     *** (((                                                            
                                                                                        

[*] DETECTED PARAMETERS:
====================================================
[!] INIT DB: TRUE
[!] GENERATE CA: TRUE
[!] GENERATE CERTS: TRUE
[!] GENERATE KEYS: TRUE
[!] GENERATE USERS: TRUE
[!] PUBLIC HOSTNAME: 172.23.163.163
[!] ASSETS COUNT: 10
[!] VPN NET CIDR: 10.11.0.0/16
[!] DOCKER OVPNSRV NAME: ovpnsrv
[!] DOCKER OVPNSRV ADDRESS: 10.10.0.2
[!] DOCKER HERDSRV NAME: herdsrv
[!] DOCKER HERDSRV ADDRESS: 10.10.0.3
[!] DOCKER HERDVIEW NAME: herdview
[!] DOCKER HERDVIEW ADDRESS: 10.10.0.5
[!] DOCKER FTPSRV NAME: ftpsrv
[!] DOCKER FTPSRV ADDRESS: 10.10.0.4
[!] DOCKER DSTRSRV NAME: dstrsrv
====================================================
Continue? [y/N]: y

```

### 2.4 Check framework status

Once the deploy procedure has completed, check all dockers are up and running:

```bash
$ sudo docker ps

CONTAINER ID   IMAGE             COMMAND                  CREATED              STATUS              PORTS                                             NAMES
07839fcaec7e   dstrsrv:latest    "/docker-entrypoint.…"   About a minute ago   Up About a minute   80/tcp, 0.0.0.0:8443->443/tcp, :::8443->443/tcp   dstrsrv
48beb5cb7eb8   herdview:latest   "/docker-entrypoint.…"   About a minute ago   Up About a minute   80/tcp                                            herdview
f3fec616f317   ftpsrv:latest     "/bin/sh -c '/run.sh…"   4 minutes ago        Up 4 minutes        21/tcp, 30000-30009/tcp                           ftpsrv
e12362fa5dca   herdsrv:latest    "docker-entrypoint.s…"   4 minutes ago        Up 4 minutes        3000-3001/tcp                                     herdsrv
4b5fe465f217   ovpnsrv:latest    "ovpn_run"               7 minutes ago        Up 7 minutes        0.0.0.0:1194->1194/udp, :::1194->1194/udp         ovpnsrv
```

## 3. Initialize

Finally, the first user, aka the **System User**, has to be generated in order to initialize the framework:

```bash
$ sudo herd-cli user -a firstuser
New User Password: 

 [-] Attempting to create the new user 
 [!] Operation successfully completed 
```

<iframe width="560" height="315" src="https://www.youtube.com/embed/lYqn-kMNVWs" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" style="margin-bottom: 30px;" allowfullscreen></iframe>
