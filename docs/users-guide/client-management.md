# Client Management :: Intro

As for the asset also for the client we have tried to provide high flexibility and reduced interaction. Again, a one-line script interacts with Distribution-Server, downloads the user-related `OpenVPN` configuration file and initiates the VPN encrypted channel.

!!! note
    For the first client we have used the credentials of the user with id 1 (`-i 1`).

!!! note
    The one-liner is not needed in case you want a direct control of the framework from the machine on which it is hosted.

!!! warning
    There could be VPN connection issues if the `client` device and `Herd-Server` are not time synchronized.

## Docker

The dockerized client case is the most simple. The one-liner provided locally by the Herd-CLI creates an Ubuntu container that joins the infrastructure and allows the host machine to act as a client: 

```bash
$ herd-cli endpoint -s 172.23.16.16 -o docker -m client -i 1

                                                                                        
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
                                                                                        

sudo docker run -d --rm --cap-add=NET_ADMIN --device /dev/net/tun -e DSTRSRV_PUBLIC_ADDRESS="172.23.16.16" -e USERNAME="USER_001" -e PASSWORD="l9tcuv6GKUDBYtcyt2fyEcktDE578cs1" --network host -v $(pwd)/redherd-certificates:/usr/local/share/ca-certificates --name redherd-client redherd/client
```

## Debian

It is just required to run the Herd-CLI one-liner on the Debian host:

```bash
$ herd-cli endpoint -s 172.23.16.16 -o debian -m client -i 1

                                                                                        
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
                                                                                        

sudo bash -c "apt update && apt install openvpn -y && curl -k -u USER_001:l9tcuv6GKUDBYtcyt2fyEcktDE578cs1 https://172.23.16.16:8443/f6865d8c51bb7a1ba155bdfbeb3f686e/config.ovpn > ./redherd.ovpn && /usr/sbin/openvpn ./redherd.ovpn
```

## Windows

Download and install the [`OpenVPN-Client`](https://openvpn.net/client-connect-vpn-for-windows/), then use the `PowerShell` one-liner to download the `OpenVPN` configuration.

```bash
$ herd-cli endpoint -s 172.23.16.16 -o windows -m client -i 1

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
[Net.ServicePointManager]::ServerCertificateValidationCallback = {$true}; $webclient = New-Object System.Net.WebClient; $basic = [System.Convert]::ToBase64String([System.Text.Encoding]::ASCII.GetBytes("USER_001" + ":" + "l9tcuv6GKUDBYtcyt2fyEcktDE578cs1"));$webclient.Headers["Authorization"] = "Basic ";
$webclient.DownloadFile("https://172.23.16.16:8443/f6865d8c51bb7a1ba155bdfbeb3f686e/config.ovpn", "redherd.ovpn")
}; powershell -ep bypass -nop -c $block

 [!] Manually run OpenVPN with downloaded redherd.ovpn config file 
```

## Android

Download and install the [`OpenVPN-Client`](https://play.google.com/store/apps/details?id=net.openvpn.openvpn&hl=it&gl=US), then download the `OpenVPN` configuration from the provided link.

```bash
$ herd-cli endpoint -s 172.23.16.16 -o android -m client -i 1

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
                                                                                        


 [!] Manually download the OpenVPN config file: 
 [!] Url: https://172.23.16.16:8443/f6865d8c51bb7a1ba155bdfbeb3f686e/config.ovpn 
 [!] Username: USER_001 
 [!] Password: l9tcuv6GKUDBYtcyt2fyEcktDE578cs1 
```

## MacOS

Download and install the [`OpenVPN-Client`](https://openvpn.net/client-connect-vpn-for-mac-os/), then use the `Zsh` one-liner to download the `OpenVPN` configuration.

```bash
$ herd-cli endpoint -s 172.23.16.16 -o macos -m client -i 1

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
                                                                                        

curl -k -u USER_001:l9tcuv6GKUDBYtcyt2fyEcktDE578cs1 https://172.23.16.16:8443/f6865d8c51bb7a1ba155bdfbeb3f686e/config.ovpn > ./redherd.ovpn

 [!] Manually run OpenVPN with the downloaded `redherd.ovpn` config file 
```

## Herd-View Access

!!! warning
    In order to access Herd-View it is mandatory to download and install RedHerd Certification Authority certificate.

After successfully joined the framework VPN, connect to Herd-View using a browser and visiting the URL `https://10.10.0.5`, then download the RedHerd Certification Authority certificate clicking on the upper-left button and install it in your system. Alternatively, you can obtain this certificate directly from `https://10.10.0.3:3000/ca.crt`.

<img src="download-ca.png" style="display: block; margin-left: auto; margin-right: auto; width: 95%; border: 2px solid #000;" alt="RedHerd">

<img src="download-ca-detail.png" style="display: block; margin-left: auto; margin-right: auto; width: 95%; border: 2px solid #000;" alt="RedHerd">

Once the certificate has been trusted, it is possible to fill the login page with your user credentials.h

<img src="login.png" style="display: block; margin-left: auto; margin-right: auto; width: 95%; border: 2px solid #000;" alt="RedHerd">
