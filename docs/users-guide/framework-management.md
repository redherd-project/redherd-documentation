# Framework Management :: Intro

This section provides a deeper insight on how to fully manage the framework deployment process and all its features.

## Destroy

The deploy script can also be used to take the framework down:

```bash
$ sudo ./deploy.sh -d

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
                                                                                        

 [*] Docker environment cleanup 
ovpnsrv
Untagged: ovpnsrv:latest
Deleted: sha256:91e78a2d4ce5fb45970d261909f113d0062109702f8ec0ec757b2a7858ff5d23
Deleted: sha256:5693be9dc0dc0f0ecf136f37475a4b9adf31c0a72894b687822690db7e1f1e8c
Deleted: sha256:852d8501542f54dbe5754f7fd73d807c4203f66d62ff54d99c119419a02bca2b
Deleted: sha256:869c88433db452ed79c7162582047dcfbaf47b209317ec1fa6b71a9c40b96ecd
Deleted: sha256:6b07e4131caa0156ed54f2b2ce27f0c03a3d50e03cc3cc6767d1b69cf4a7205e
Deleted: sha256:0e459de7b327a61e34e29b6a07c06ea38797c5202e5e3819eee5f8a23553ca08
Deleted: sha256:b7404afcdd25a8b70ad5873c4094d13f1975a58acf81885e7d88de7288365c11
Deleted: sha256:b43b3ed5d13e7f800a5ec9e6d3072d32ece187eb182be07245910f95787f5093
Deleted: sha256:be6ba2aa03790eb8336b8464eb14cdcb34270e6cdb22d83a0e11b20919181214
Deleted: sha256:07fc7232db98106e694a0234a0ab7ba19286133832192a299a70ecec4dce5682
Deleted: sha256:e1c5528f18db384fa8373d701f3e61af0e2c1656733af27959ae587a83b457d4
Deleted: sha256:8f1cece9330a25a1cf795ba78562059f326138fbea5e2749d64dd5a3d70f4050
Deleted: sha256:9bfcecbeeb774e41e9561e686a4afb7f5012316ef7e271ab017082692b182298
Deleted: sha256:bfa09c8289fbcc8791c8a174d545cea0fa5f4617c26aa30f1b07ff494b010ad0
Deleted: sha256:45ba11e8699b99fec50b655797907112cc6246280f146774f42a33cca8cc8408
Deleted: sha256:36fcb8e0144e44d9c85aadb569122350252c74320b619dbf4cc458da3173cae4
Deleted: sha256:6ce35068dce464cfd49e7bfa8f0cb9ac384e687732d7d26074873ba63388b915
herdsrv
Untagged: herdsrv:latest
Deleted: sha256:58d8b77f4eaa2252921cd77d5cfd496f29cd6fe6d23463b28ae8233d65e2731a
Deleted: sha256:116de39c14160d43d2a3fb24aed18b9c9b2228ae0d8e5cec533990c01548cf95
Deleted: sha256:b042ec9beedfd8aaa9b070900a080385ea705003a97633b2a3710b3a25c90740
Deleted: sha256:e68cb0e1bd2b8346e2de7dde87ae5d2b7dba3b1497cb30b954bebd6fe86edb52
Deleted: sha256:e17cca51ca5993a778056672511ae01f4b5231a14add9ea7dd7145a8cf24c9a9
Deleted: sha256:ecf85fbbcde4f995c90ad19b7da82314fd0bcacf8bc085c296e7dba33edf7551
Deleted: sha256:96797af7230236fe1eae96e3bea3ad38453c277f36c8a298d4ecc27cb1892eee
Deleted: sha256:693d0d723aced0e2121968489f25c1e8a206c7c170893777c251af498cedff6e
Deleted: sha256:4ea4c8116ce073d39f6b95fe774ad873ea072c171d2c78dd9e5e130bc6b2ff7a
Deleted: sha256:8bbf0fdc143fdc22558d4c2f120e59a655146f3f285775e071cc2e1f79b92339
Deleted: sha256:308cccf6a89553f19e45a79c043ac83025181ca1b3c00268ae765ec228626b2f
Deleted: sha256:4ca64ce92227b399e4749a970027b149b7e0ba167186f3822fae0c9c9e1391dc
Deleted: sha256:17d8b36dd94c4ddfbfe4784bdd20d9b6b5769f4eca6e4efdb43d01d5d6f0cfd4
Deleted: sha256:2e9271591c173b6ab793635240a224e830a8cc36cad9b21d7f1e772d95e8143d
Deleted: sha256:5c62079596e97e4221a3b510558e8853fa6fc1dae3549e8785b6777215984a46
Deleted: sha256:34631d73d29e214ffda5cda7e1660769a7dd3ca5736582bcc63a232f4d42cc7f
Deleted: sha256:5bf2516c48fa1fee5522ad761de3f8a4329b50fd8178b252e39cab3bc7db9b77
Deleted: sha256:81f6727d260bf8f8ba3c26e316c88e20673f294bc06e60ff28861f43d976493e
Deleted: sha256:1119f1e7303603bc416e90ae0c6b4124b23bfa9b2aafec1af4273782449c5914
ftpsrv
Untagged: ftpsrv:latest
Deleted: sha256:42f92a4ddd6dc98221542a9e28982ce9674bac081636edfcf8e86a5e04cc3af1
Deleted: sha256:d159c5cb39cc834e02e833c3ddb6bb6a9c80a4a6a9b653251c56d0284342cb1d
herdview
Untagged: herdview:latest
Deleted: sha256:8b351a7109b26167045ace8118ebd63fabb35db531973c664c9a103cc673a4db
Deleted: sha256:2c67a03feece34a56f65a77b37d345f3abfece9b97cf1f2631c4ea571148d5ce
dstrsrv
Untagged: dstrsrv:latest
Total reclaimed space: 0B
internal
ovpn-data-server
```

Once the script has completed, you can verify that no RedHerd dockers are up:

```bash
$ sudo docker ps

CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
```

## Quick-deploy

Select the external IP address to which all `assets`/`clients` will connect:

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

Deploy the framework for the desired number of `assets`/`client` (e.g. `-a 10`):

```bash
$ cd redherd-framework
$ sudo ./deploy.sh -s 172.23.163.163 -a 10

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
[!] INIT DB: FALSE
[!] GENERATE CA: FALSE
[!] GENERATE CERTS: FALSE
[!] GENERATE KEYS: FALSE
[!] GENERATE USERS: FALSE
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
!!! note
    Use destroy and quick-deploy if you want temporary deactivate the framework.

!!! note
    Assets are able to automatically re-join after a framework destroy or quick-deploy.


## Database re-initialization

Deploy the framework and re-initialize the local database:

```bash
$ cd redherd-framework
$ sudo ./deploy.sh -s 172.23.163.163 -a 10 -db

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
[!] GENERATE CA: FALSE
[!] GENERATE CERTS: FALSE
[!] GENERATE KEYS: FALSE
[!] GENERATE USERS: FALSE
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

## Certification Authority regeneration

Deploy the framework and regenerate the Certification Authority:

```bash
$ cd redherd-framework
$ sudo ./deploy.sh -s 172.23.163.163 -a 10 -ca

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
[!] INIT DB: FALSE
[!] GENERATE CA: TRUE
[!] GENERATE CERTS: TRUE
[!] GENERATE KEYS: FALSE
[!] GENERATE USERS: FALSE
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

!!! note
    Re-initialize the Certification Authority if you want to cut-off all assets. 

!!! warning
    Assets will not be able to automatically re-join the framework since SSL certificates are not trusted anymore.

!!! danger
    Please note that distribution server credentials are still valid so this will not save you against *kidnapped* assets.


## Distribution-Server credentials regeneration

Deploy the framework and regenerate all credentials relative to Distribution-Server:

```bash
$ cd redherd-framework
$ sudo ./deploy.sh -s 172.23.163.163 -a 10 -u

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
[!] INIT DB: FALSE
[!] GENERATE CA: FALSE
[!] GENERATE CERTS: FALSE
[!] GENERATE KEYS: FALSE
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

!!! note
    Re-initialize the Certification Authority if you want to definitely cut-off all assets. 

!!! danger
    Assets will not be able to automatically re-join the framework since SSL certificates are not trusted anymore.
