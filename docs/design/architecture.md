<h1>Architecture</h1>

RedHerd uses some specialized Docker containers in order to integrate many community acclaimed open-source products with a custom application layer, implemented for interoperability purposes. These containers have been designed to compartmentalise features and to allow horizontal scaling if needed. The described architecture offers a high level of automation by allowing minimized user interaction during the asset setup process and is bounded by a Virtual Private Network (VPN) granting Operations Security (OPSEC) by design.

<img src="framework_architecture.png" style="display: block; margin-left: auto; margin-right: auto; width: 90%;" alt="RedHerd Logo">

The main elements of the RedHerd framework are listed hereafter:

- **Assets**: multi-platform devices (`Windows`, `Debian-like`, `RHEL-like`, `MacOS` and `Android`) that can be orchestrated to perform cyber operations;
- **Herd-Server**: the Node.js core of the framework which is responsible for interacting with the assets. It receives and multiplexes all the inputs from the operators thanks to an extended set of Application Programming Interfaces (API) and dispatches the output received from the assets via a Socket.IO channel;
- **File-Server**: an FTPS-based server, which allows secure file transfer among operators and assets;
- **OVPN-Server**: the OpenVPN gateway for all entities interacting with the framework;
- **Distribution-Server**: the only component publicly accessible outside the VPN edge, which represents an Nginx web server that distributes, after authentication, all the configuration files needed by an entity attempting to join the framework;
- **Herd-View**: a Progressive Web Application (PWA) written in Angular that provides a user-friendly interface to monitor and task all the assets in real-time;
- **Client**: the device used by an operator to interct with the framework components.

Last but not least, **Herd-CLI** represents the administrative application for managing the entire framework.
