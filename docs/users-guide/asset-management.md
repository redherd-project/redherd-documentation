# Asset Management :: Intro

One of the aspects which is particularly relevant is the asset setup and join procedure. The implementation of this feature has been ruled by two design drivers: high **flexibility** and **low user interaction**. The former characteristic is needed in order to grant a remarkable level of compatibility with different operating systems, while the latter is fundamental to minimize failures and reduce the skills required to add a new asset to RedHerd. The result is a manually triggered yet fully automated procedure that involves only the execution of a `one-line` script which is different for each compatible platform: `Bash` for Android and Linux, `PowerShell` for Windows and `Zsh` for MacOS.

This one-liner interacts with Distribution-Server and acts as a dropper downloading the full setup script and the related `OpenVPN` configuration file. The second stage fully configures the device in order to fulfill the framework requirements, i.e., dependencies management, certificate trusting, firewall and SSH daemon set up. Then, the VPN connection is initiated and the API are used to interact with Herd-Server and insert the new asset into the framework database. At this point, the asset is effectively part of the framework and so it is completely accessible by the operators.

!!! warning
    The asset joining procedure is more complex than the client one since additional steps are required (e.g. new user and shared folder creation, certification authority trusting, ...).

!!! warning
    There could be VPN connection issues if the `client` device and `Herd-Server` are not time synchronized.

!!! note
    As an example, credentials corresponding to the user with id 2 (`-i 2`) have been considered.


## Docker

!!! note
    Only one docker asset is allowed per machine.


### Add

```bash
$ herd-cli endpoint -s 172.23.16.16 -o docker -m install -i 2

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
                     *** ((#    Command-line Interface                                  
                     *** (((                                                            
                                                                                        

sudo docker run -d --rm --cap-add=NET_ADMIN --device /dev/net/tun -e DSTRSRV_PUBLIC_ADDRESS="172.23.16.16" -e USERNAME="78l8zUBjpm" -e PASSWORD="2GHDUWvZxtbn18LeiVoEv4UmhGv0rUrY" --privileged=true --network host --name redherd-asset redherd/asset
```

### Remove

```bash
$ herd-cli endpoint -s 172.23.16.16 -o docker -m remove -i 2

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
                     *** ((#    Command-line Interface                                  
                     *** (((                                                            
                                                                                        

sudo docker stop redherd-asset
```


## Debian

### Add

```bash
$ herd-cli endpoint -s 172.23.16.16 -o debian -m install -i 2

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
                     *** ((#    Command-line Interface                                  
                     *** (((                                                            
                                                                                        

sudo bash -c "curl -k -u 78l8zUBjpm:2GHDUWvZxtbn18LeiVoEv4UmhGv0rUrY https://172.23.16.16:8443/50f3331a80894d85bcda8c4b404a919c/debian_asset_setup.sh > /tmp/script.sh && chmod +x /tmp/script.sh && /tmp/script.sh install && rm -rf /tmp/script.sh"
```

### Remove

```bash
$ herd-cli endpoint -s 172.23.16.16 -o debian -m remove -i 2

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
                     *** ((#    Command-line Interface                                  
                     *** (((                                                            
                                                                                        

sudo bash -c "curl -k -u 78l8zUBjpm:2GHDUWvZxtbn18LeiVoEv4UmhGv0rUrY https://172.23.16.16:8443/50f3331a80894d85bcda8c4b404a919c/debian_asset_setup.sh > /tmp/script.sh && chmod +x /tmp/script.sh && /tmp/script.sh remove && rm -rf /tmp/script.sh"
```

## CentOS

### Add

```bash
$ herd-cli endpoint -s 172.23.16.16 -o centos -m install -i 2

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
                     *** ((#    Command-line Interface                                  
                     *** (((                                                            
                                                                                        

sudo bash -c "curl -k -u 78l8zUBjpm:2GHDUWvZxtbn18LeiVoEv4UmhGv0rUrY https://172.23.16.16:8443/50f3331a80894d85bcda8c4b404a919c/debian_asset_setup.sh > /tmp/script.sh && chmod +x /tmp/script.sh && /tmp/script.sh install && rm -rf /tmp/script.sh"
```

### Remove

```bash
$ herd-cli endpoint -s 172.23.16.16 -o centos -m remove -i 2

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
                     *** ((#    Command-line Interface                                  
                     *** (((                                                            
                                                                                        

sudo bash -c "curl -k -u 78l8zUBjpm:2GHDUWvZxtbn18LeiVoEv4UmhGv0rUrY https://172.23.16.16:8443/50f3331a80894d85bcda8c4b404a919c/debian_asset_setup.sh > /tmp/script.sh && chmod +x /tmp/script.sh && /tmp/script.sh remove && rm -rf /tmp/script.sh"
```

## Windows

### Add

```bash
$ herd-cli endpoint -s 172.23.16.16 -o windows -m install -i 2

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
                     *** ((#    Command-line Interface                                  
                     *** (((                                                            
                                                                                        

$block = {
[Net.ServicePointManager]::ServerCertificateValidationCallback = {$true}; $webclient = New-Object System.Net.WebClient; $basic = [System.Convert]::ToBase64String([System.Text.Encoding]::ASCII.GetBytes("78l8zUBjpm" + ":" + "2GHDUWvZxtbn18LeiVoEv4UmhGv0rUrY"));$webclient.Headers["Authorization"] = "Basic ";
$webclient.DownloadFile("https://172.23.16.16:8443/50f3331a80894d85bcda8c4b404a919c/windows_asset_setup.psm1", "script.psm1")
Import-Module .\script.psm1; Add-Asset; Remove-Item .\script.psm1;
}; powershell -ep bypass -nop -c $block
```

### Remove

```bash
$ herd-cli endpoint -s 172.23.16.16 -o windows -m remove -i 2

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
                     *** ((#    Command-line Interface                                  
                     *** (((                                                            
                                                                                        

$block = {
[Net.ServicePointManager]::ServerCertificateValidationCallback = {$true}; $webclient = New-Object System.Net.WebClient; $basic = [System.Convert]::ToBase64String([System.Text.Encoding]::ASCII.GetBytes("78l8zUBjpm" + ":" + "2GHDUWvZxtbn18LeiVoEv4UmhGv0rUrY"));$webclient.Headers["Authorization"] = "Basic ";
$webclient.DownloadFile("https://172.23.16.16:8443/50f3331a80894d85bcda8c4b404a919c/windows_asset_setup.psm1", "script.psm1")
Import-Module .\script.psm1; Remove-Asset; Remove-Item .\script.psm1;
}; powershell -ep bypass -nop -c $block
```

## Android

!!! warning
    You must have **root privileges** on the Android device to use it as a RedHerd asset.

In order to join an Android device it is necessary to install:

- `Termux` [[`Google Play`](https://play.google.com/store/apps/details?id=com.termux&hl=it&gl=US),[`GitHub`](https://github.com/termux/termux-app)]
- `Termux:Boot` [[`Google Play`](https://play.google.com/store/apps/details?id=com.termux.boot&hl=it&gl=US),[`GitHub`](https://github.com/termux/termux-boot)]
- `Termux:API` [[`Google Play`](https://play.google.com/store/apps/details?id=com.termux.api&hl=it&gl=US),[`GitHub`](https://github.com/termux/termux-api)]

The one-liners must be executed in a Termux session.

### Add

```bash
$ herd-cli endpoint -s 172.23.16.16 -o android -m install -i 2

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
                     *** ((#    Command-line Interface                                  
                     *** (((                                                            
                                                                                        

 [!] Install Termux, Termux:Boot and Termux:API from Google Play 

pkg install curl -y && curl -k -u 78l8zUBjpm:2GHDUWvZxtbn18LeiVoEv4UmhGv0rUrY https://172.23.16.16:8443/50f3331a80894d85bcda8c4b404a919c/android_asset_setup.sh > /home/user/script.sh && chmod +x /home/user/script.sh && /home/user/script.sh install && rm -rf /home/user/script.sh
```

### Remove

```bash
$ herd-cli endpoint -s 172.23.16.16 -o android -m remove -i 2

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
                     *** ((#    Command-line Interface                                  
                     *** (((                                                            
                                                                                        

 [!] Install Termux, Termux:Boot and Termux:API from Google Play 

pkg install curl -y && curl -k -u 78l8zUBjpm:2GHDUWvZxtbn18LeiVoEv4UmhGv0rUrY https://172.23.16.16:8443/50f3331a80894d85bcda8c4b404a919c/android_asset_setup.sh > /home/user/script.sh && chmod +x /home/user/script.sh && /home/user/script.sh remove && rm -rf /home/user/script.sh
```

## MacOS

!!! note
    Full disk access for `Terminal` application is required.
    
### Add

```bash
$ herd-cli endpoint -s 172.23.16.16 -o macos -m install -i 2

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
                     *** ((#    Command-line Interface                                  
                     *** (((                                                            
                                                                                        

sudo zsh -c "curl -k -u 78l8zUBjpm:2GHDUWvZxtbn18LeiVoEv4UmhGv0rUrY https://172.23.16.16:8443/50f3331a80894d85bcda8c4b404a919c/macos_asset_setup.sh > /tmp/script.sh && chmod +x /tmp/script.sh && /tmp/script.sh install && rm -rf /tmp/script.sh"
```

### Remove

```bash
$ herd-cli endpoint -s 172.23.16.16 -o macos -m remove -i 2

                                                                                        
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
                     *** ((#    Command-line Interface                                  
                     *** (((                                                            
                                                                                        

sudo zsh -c "curl -k -u 78l8zUBjpm:2GHDUWvZxtbn18LeiVoEv4UmhGv0rUrY https://172.23.16.16:8443/50f3331a80894d85bcda8c4b404a919c/macos_asset_setup.sh > /tmp/script.sh && chmod +x /tmp/script.sh && /tmp/script.sh remove && rm -rf /tmp/script.sh"
```

## Asset Ban

During the RedHerd Framework lifecycle it is possible that some assets have to be excluded from the operative network due to *kidnapping* or simply for administrative reasons. This scenario could involve mainly two actions: **Full Asset Ban** and **Single Asset Ban**.

### Full Asset Ban

In this situation the quickest method is to [`regenerate`](https://redherd.readthedocs.io/en/latest/users-guide/framework-management/#certification-authority-regeneration) the RedHerd Certification Authority, this action cuts off all assets contemporary.

### Single Asset Ban

In this case Herd-CLI offers an administrative command which allows to revoke the VPN certificate assigned to a specific asset. This command is part of the *asset* realm and requires the asset name.

```bash
$ sudo herd-cli asset -b vVDNDUUGjb
 [-] Attempting to revoke client certificate
 [!] Certificate successfully revoked
```
