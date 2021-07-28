# Module Implementation :: Intro

The term task refers to the abstract representation of an operator intent. Each task needs a static implementation in order to be executed and this implementation is called **module** while its instance is a **process**. A set of modules carrying out similar tasks is grouped into a common **topic**, which is the representation of one or more characteristics bringing together a number of tasks and, transitively, one or more modules (e.g. scanning, spoofing, Wi-Fi, ...). Concretely, to develop a new module follow the indications below.

## Module metadata

The first step requires the generation an **.info** file containing the module metadata. These metadata ranges from simple details, such as name, title and description, to structured input parameters which are quite critical for the module execution.

**MODULE_NAME.info**
```json
{
    "name": "MODULE_NAME",                // Filename without extension
    "title": "MODULE_TITLE",              // Title
    "description": "MODULE_DESCRIPTION",  // Description
    "binary": "MODULE_BINARY",            // Binary file executed by the module (e.g. nmap, nikto)
    "author": "MODULE_AUTHOR",            // Author
    "topic": "MODULE_TOPIC",              // Topic to which the module refers 
    "version": "MODULE_VERSION",          // Version (e.g. 1.0, 1.1)
    "params": [                           // Module input parameters
            {
                "label"  : "PARAMETER 1", // Label of the input fields in the module form, 
                "name"   : "PARAMETER_1", // Name of the input parameter in the module form, 
                "type"   : "list",        // Type of the input parameter ("string" => text, "number" => number, "boolean" => checkbox, "password" => password, "list" => select),
                "values" : [              // Array of values in case of "list" type (nullable)
                    "VALUE_1", 
                    "VALUE_2", 
                    "VALUE_3"
                    ] 
            },
            {
                "label"  : "PARAMETER 2", // Label of the input fields in the module form, 
                "name"   : "PARAMETER_2", // Name of the input parameter in the module form, 
                "type"   : "string",      // Type of the input parameter ("string" => text, "number" => number, "boolean" => checkbox, "password" => password, "list" => select),
            },       
        ],
    "tags": [
        "automatic"                       // "automatic", "interactive" or "pivotable" according to the module execution mode
    ]
}
```

A metadata file, as shown in the previous code snippet, has the *info* extension and essentially consists of `json-formatted` data which must be filled as explained hereafter: 

- *name* is the module name, it must match the metadata filename and should be chosen according the following convention *operatingsystem_binary*. As an example, some module names are `android_ping`, `debian_ping`, `windows_ping` and `macos_ping`;

- *title* and *description* are two informative fields which could be fundamental to understand what actions a module is able to performs;

- *binary* is the executable launched by the module (e.g. ping, nmap, nikto, ...). It must assume an atomic value, i.e. only one binary for each module;

- *author* is the module developer or its group of developers;

- *topic* is a sort of group which the module is associated to. This association is related to its target operating system and scope. The list of available topics is presented in the following table, where *os* must be replaced with `debian`, `android`, `windows` or `macos`:

| Topic | Description |
| --- | --- |
| os_service | Service modules |
| os_misc | Generic modules |
| os_reconnaissance | Gather target information |
| os_weaponization | Exploit a target |
| os_delivery | Deliver a payload to a target |
| os_installation | Install a malicious software on a target |
| os_lateral_movement | Laterally move to other systems |
| os_command_and_control | Establish a command and control channel on a target |
| os_execution | Produce an effect on a target |

- *version* is the module version;

- *params* is crucial to properly render the Herd-View module GUI and is an array of json objects, where each of them corresponds to an input parameter:
    - `label` is the label associated to the specific control in the Herd-View GUI;
    - `name` is the name of the parameter associated to the control in the Herd-View GUI. This parameter is also used to reference the module at run time;
    - `type` is the GUI control type ("string" => text, "number" => number, "boolean" => checkbox, "password" => password, "list" => select);
    - `values` is an array of strings containing all possible values assignable to the Herd-View GUI control. This parameter is used when *type* has been set to *list*.

- *tags* is an array of strings which will be helpful in future framework developments. Currently it can assume the following values:
    - `automatic`, if the module performs the task autonomously without any additional user interaction (e.g. ping, nmap);
    - `interactive`, if the module requires user interaction via console (e.g. airgeddon, metasploit);
    - `pivotable`, if the module requires user interaction but it needs a redirection to an external destination (e.g. a third-party website). In this scenario Herd-Server acts as a pivot.

## Module logic

The module execution logic is coded in a **.js** JavaScript file. In order to allow a rapid development, the framework provides a set of JavaScript built-in modules containing specific base classes. These classes are implemented for each compatible operating system, e.g., Windows (`WindowsModule`) and Linux (`LinuxModule`), and can be used to inherit all the required properties and methods needed to interact with the assets:

```js
const WindowsModule = require('../base/rdhd-mod-base_windows_module');

class ModuleName extends WindowsModule
{
    /* Module logic */
}
```

```js
const LinuxModule = require('../base/rdhd-mod-base_linux_module');

class ModuleName extends LinuxModule
{
    /* Module logic */
}
```

In practice, by complying with the provided interface, it is extremely easy to extend and/or enhance RedHerd capabilities. The following snippet provides a business code implementation of a sample Linux module.

**MODULE_NAME.js**
```js
'use strict';

const LinuxModule = require('../base/rdhd-mod-base_linux_module');

class ModuleName extends LinuxModule
{
    constructor(asset, context, session, wsServer, token)
    {
        super(asset, "MODULE_NAME", session, wsServer, token);

        /* Input parameters */
        this.parameter_1 = context.parameter_1;
        this.parameter_2 = context.parameter_2;
    }

    configure(whatIf = false)
    {
        /* Command to be executed to configure the asset for module execution */
        let task = "sudo apt update; sudo apt install MODULE_BINARY -y";
        this.do(task, "cmd_res", false, whatIf);
    }

    /** To be implemented only if the module is "automatic" **/
    run(whatIf = false)
    {
        if (this.validate())
        {
            /* Command to be executed */
            let task = "sudo MODULE_BINARY -p1 " + this.parameter_1 + " -p2 " + this.parameter_2;
            this.do(task, "cmd_res", false, whatIf);
        }
        else
        {
            this.reportAndExit(this.buildErrorMessage("Invalid input provided"));
        }
    }
    
    /** To be implemented only if the module is "interactive" **/
    interact(whatIf = false)
    {
        let axios = require('axios');
        let https = require("https");
        let deasync = require('deasync');
        let response = false;

        if (this.validate())
        {
            let agent = new https.Agent({ rejectUnauthorized: false });
            let op;

            if (this.operation.toUpperCase() == "START")
            {
                /* Command to be executed */
                let task = "sudo MODULE_BINARY -p1 " + this.parameter_1 + " -p2 " + this.parameter_2;
                op = "enable";

                axios.post(this.url,
                { 
                    operation: op,
                    service: {
                        type: 'TERMINAL',
                        params: {
                            command: task
                        }
                    }
                },
                {
                    httpsAgent: agent,
                    auth: this.auth
                })
                .then((res) => {
                    response = res.data.data.service;
                })
                .catch((err) => {
                    response = err.message;
                });
                deasync.loopWhile(() => !response);
            }
            else
            {
                op = "disable";

                axios.post(this.url,
                { 
                    operation: op,
                    service: {
                        type: 'TERMINAL'
                    }
                },
                {
                    httpsAgent: agent,
                    auth: this.auth
                })
                .then((res) => {
                    response = res.data.data.service;
                })
                .catch((err) => {
                    response = err.message;
                });
                deasync.loopWhile(() => !response);

                this.reportAndExit(this.buildInfoMessage("Operation started"));
            }
        }
        else
        {
            this.reportAndExit(this.buildErrorMessage("Invalid input provided"));
        }
        return response;
    }

    /** To be implemented only if the module is "pivot" **/
    pivot(whatIf = false)
    {
        let axios = require('axios');
        let https = require("https");
        let deasync = require('deasync');
        let response = false;
        let feedback;

        if (this.validate())
        {
            let agent = new https.Agent({ rejectUnauthorized: false });
            let task;
            let op;
            let port;

            if (this.operation.toUpperCase() == "START")
            {
                /* Command to be executed */
                task = "sudo MODULE_BINARY";
                op = "enable";

                //  Spawn a Web proxy
                // ******************************
                axios.post(this.url,
                { 
                    operation: op,
                    service: {
                        type: "HTTP_PROXY",
                        params: {
                            rport: 8081
                        }
                    }
                },
                {
                    httpsAgent: agent,
                    auth: this.auth
                })
                .then((res) => {
                    response = true;
                    port = res.data.data.service.ports.port;

                })
                .catch((err) => {
                    response = err.message;
                });
                deasync.loopWhile(() => !response);

                //  Async execution
                // ******************************
                this.do(task, "cmd_res", false, whatIf);

                feedback = this.buildWarnMessage("Connect to https://10.10.0.3:" + port + "?t=" + this.token);
            } 
            else 
            {
                task = "sudo killall -9 MODULE_BINARY";
                op = "disable";

                //  Destroy the Web Proxy
                // ******************************
                axios.post(this.url,
                { 
                    operation: op,
                    service: {
                        type: "HTTP_PROXY"
                    }
                },
                {
                    httpsAgent: agent,
                    auth: this.auth
                })
                .then((res) => {
                    response = true;
                })
                .catch((err) => {
                    response = err.message;
                });

                deasync.loopWhile(() => !response);

                //  Async execution
                // ******************************
                this.do(task, "cmd_res", false, whatIf);
    
                feedback = this.buildInfoMessage("Operation started");
            }
        }
        else
        {
            this.reportAndExit(this.buildErrorMessage("Invalid input provided"));
        }
        this.reportAndExit(feedback);
    }

    validate()
    {
        if (/* parameters validation logic */)
        {
            return true;
        }
        return false;
    }
}
```

Each module class, deriving from one of the base classes, must have a *constructor* and must expose at least three methods: *run* (or its alternative *interact* and *pivotable*), *configure* and *validate*:

- the *constructor* is responsible for specifying the *MODULE_NAME*, according to the one inserted into the *.info* file, and retrieving the input parameters from a specialized object named *context*, again as specified in the metadata file:

        this.parameter_1 = context.parameter_1;
        this.parameter_2 = context.parameter_2;

- the *configure* method is responsible for implementing all the preliminary activities, such as installing the binary and all its dependencies (e.g. via `apt install`) and performing required configurations.

- the *run*, *interact* or *pivot* methods are mutually exclusive and are responsible for module execution. They must be implemented if the module is tagged as *automatic*, *interactive* or *pivotable*, respectively. All of them need the task variable populated with the required command line, i.e. binary and arguments. The only difference is that *interact* automatically spawns a terminal session to Herd-View, while *pivot* launches a proxy service (see the table below) and displays the endpoint which connect to.

| Service | Description |
| --- | --- |
| TCP_PROXY | Proxies the TCP traffic from an operator machine to an asset, and vice-versa, through Herd-Server |
| UDP_PROXY | Proxies the UDP traffic from an operator machine to an asset, and vice-versa, through Herd-Server |
| HTTP_PROXY | Proxies the HTTP traffic from an operator machine to an asset, and vice-versa, through Herd-Server |
| RTSP_REDIRECTOR | Redirects the RTSP video stream from an asset to an operator machine through Herd-Server |


- The *validate* method verifies (if necessary) the parameters passed to the module in order to check for incorrect input data. Validation logic can be completely custom or leverage the helper functions exposed by the *Validator* class:

| Validation Function | Example |
| --- | --- |
| Validator.validateNumber(value) | 10 |
| Validator.validateBinaryNumber(value) | 1010 |
| Validator.validateFileName(value) | test-file.exe |
| Validator.validateIp(value) | 192.168.1.1 |
| Validator.validateIpRange(value) | 192.168.1.1-255 |
| Validator.validateCIDR(value) | 192.168.1.1/24 |
| Validator.validateHostname(value) | test.target.local |
| Validator.validateHost(value) | hostname or IP |
| Validator.validateURL(value) | http[s]://www.example.com |
| Validator.validateTcpUdpPort(value) | 8080 |
| Validator.validateTcpUdpPortRange(value) | 8080-8088 |
| Validator.validateTcpUdpPortSubset(value) | 1-1024,3000,5000-8080 | 
| Validator.validateWindowsPath(value) | c:\path\to\file |
| Validator.validateLinuxPath(value) | /path/to/file |
| Validator.validateBool(value) | true |
| Validator.validatePositiveBool(value) | true |
| Validator.validateNegativeBool(value) | false |
| Validator.validateSSID(value) | WLAN SSID |

!!! note
    Both **.info** and **.js** files must be placed in the path `herd-server/bin/module/collection` to make the module available.

!!! note
    Modules can be created/updated while the framework is active. It is just necessary to add/modify module files and then restart the Herd-Server:
    ```
    $ sudo herd-cli server -r
    ```

## Hands-on

Hereafter, we provide some examples of modules implementation:

### Example 1. Android Ping

**android_ping.info**
```json
{
    "name": "android_ping",
    "title": "Android Ping",
    "description": "Android ping demo module",
    "binary": "ping",
    "author": "c4dm10 & peco602",
    "topic": "android_misc",
    "version": "1.0",
    "params": [{"label": "Target", "name": "target", "type": "string"}],
    "tags": ["automatic"]
}
```

**android_ping.js**
```js
'use strict';

const LinuxModule = require('../base/rdhd-mod-base_linux_module');

// moduleCode: android_ping
class AndroidPing extends LinuxModule
{
    // ************************************************************
    //  AndroidPing module
    // ************************************************************
    // target   :   IP address or FQDN to ping
    // ************************************************************

    constructor(asset, context, session, wsServer, token)
    {
        super(asset, "android_ping", session, wsServer, token);

        //  POST parameters
        // ******************************
        this.target = context.target;
    }

    run(whatIf = false)
    {
        if (this.validate())
        {
            let task = "ping -c 4 " + this.target;

            //  Async execution
            // ******************************
            this.do(task, "cmd_res", false, whatIf);
        }
        else
        {
            this.reportAndExit(this.buildErrorMessage("Invalid input provided"));
        }
    }

    validate()
    {
        if ((this.target) && Validator.validateHost(this.target))
        {
            return true;
        }
        return false;
    }
}

module.exports = AndroidPing
```

### Example 2. Debian TCP Port scanning

**debian_nmap_tcp.info**
```json
{
  "name": "debian_nmap_tcp",
  "title": "Nmap TCP Scan",
  "description": "Nmap module to scan TCP ports",
  "binary": "nmap",
  "author": "c4dm10 & peco602",
  "topic": "debian_reconnaissance",
  "version": "1.0",
  "params": 
    [
      {"label": "Target range", "name": "target", "type": "string"},
      {"label": "Port range", "name": "ports", "type": "string"}
    ],
  "tags": ["automatic"]
}
```

**debian_nmap_tcp.js**
```js
class DebianNmapTCP extends LinuxModule
{
    constructor(asset, context, session, wsServer, token)
    {
        super(asset, "debian_nmap_tcp", session, wsServer, token);
        this.target = context.target;
        this.ports = context.ports;
    }

    configure(whatIf = false)
    {
        let task = "sudo apt update; sudo apt install nmap -y";
        this.do(task, "cmd_res", false, whatIf);
    }

    run(whatIf = false)
    {
        if (this.validate())
        {
            let task = "sudo nmap -Pn -p" + this.ports + " " + this.target;
            this.do(task, "cmd_res", false, whatIf);
        }
        else
        {
            this.reportAndExit(this.buildErrorMessage("Invalid input provided"));
        }
    }
    
    validate()
    {
        if (((this.target) && (Validator.validateHost(this.target) || Validator.validateIp(this.target) || Validator.validateCIDR(this.target) || Validator.validateIpRange(this.target))) && ((this.ports) && (Validator.validateTcpUdpPortSubset(this.ports))))
        {
            return true;
        }
        return false;
    }
}
```

### Example 3. Debian Airgeddon

**debian_airgeddon.info**
```json
{
    "name": "debian_airgeddon",
    "title": "Airgeddon WiFi Attack Suite",
    "description": "Airgeddon WiFi Attack Suite",
    "binary": "airgeddon",
    "author": "c4dm10 & peco602",
    "topic": "debian_delivery",
    "version": "1.0",
    "params": [{"label": "Operation", "name": "operation", "type": "list", "values": ["start", "stop"]}],
    "tags": ["interactive"]
}
```

**debian_airgeddon.js**
```js
'use strict';

const LinuxModule = require('../base/rdhd-mod-base_linux_module');

// moduleCode: debian_airgeddon
class DebianAirgeddon extends LinuxModule
{
    // ************************************************************
    //  Airgeddon module
    // ************************************************************
    // https://github.com/wifiphisher/wifiphisher
    // https://en.kali.tools/?p=90
    //
    // operation       :   [start/stop]
    // ************************************************************

    constructor(asset, context, session, wsServer, token)
    {
        super(asset, "debian_airgeddon", session, wsServer, token);

        //  POST parameters
        // ******************************
        this.auth = { username: context.username, password: context.password };
        this.operation = context.operation;

        //  Local fields
        // ******************************
        this.url = "https://127.0.0.1:3000/api/assets/" + this.asset.id + "/service" + this.urlReadyToken;
    }

    configure(whatIf = false)
    {
        let task = "sudo apt update; \
                    sudo apt install git iw aircrack-ng tmux -y && \
                    sudo rm -rf airgeddon && \
                    git clone --depth 1 https://github.com/v1s1t0r1sh3r3/airgeddon.git && \
                    cd airgeddon && \
                    sudo sed -i 's/AIRGEDDON_WINDOWS_HANDLING=xterm/AIRGEDDON_WINDOWS_HANDLING=tmux/g' .airgeddonrc";

        //  Async execution
        // ******************************
        this.do(task, "cmd_res", false, whatIf);
    }

    interact(whatIf = false)
    {
        let axios = require('axios');
        let https = require("https");
        let deasync = require('deasync');
        let response = false;

        if (this.validate())
        {
            let agent = new https.Agent({ rejectUnauthorized: false });
            let op;

            if (this.operation.toUpperCase() == "START")
            {
                let task = "cd airgeddon && sudo /bin/bash airgeddon.sh";
                op = "enable";

                axios.post(this.url,
                { 
                    operation: op,
                    service: {
                        type: 'TERMINAL',
                        params: {
                            command: task
                        }
                    }
                },
                {
                    httpsAgent: agent,
                    auth: this.auth
                })
                .then((res) => {
                    response = res.data.data.service;
                })
                .catch((err) => {
                    response = err.message;
                });
                deasync.loopWhile(() => !response);
            }
            else
            {
                op = "disable";

                axios.post(this.url,
                { 
                    operation: op,
                    service: {
                        type: 'TERMINAL'
                    }
                },
                {
                    httpsAgent: agent,
                    auth: this.auth
                })
                .then((res) => {
                    response = res.data.data.service;
                })
                .catch((err) => {
                    response = err.message;
                });
                deasync.loopWhile(() => !response);

                feedback = this.buildInfoMessage("Operation started");
            }
        }
        else
        {
            this.reportAndExit(this.buildErrorMessage("Invalid input provided"));
        }
        return response;
    }

    validate()
    {
        let result = false;
        if ((this.operation.toUpperCase() == "START") || (this.operation.toUpperCase() == "STOP"))
        {
            result = true;
        }
        return result;
    }
}

module.exports = DebianAirgeddon
```

### Example 4. Debian Motion Camera

**debian_motion_cam.info**
```json
{
    "name": "debian_motion_cam",
    "title": "Motion Remote Cam Access",
    "description": "Motion Remote Cam Access",
    "binary": "motion",
    "author": "c4dm10 & peco602",
    "topic": "debian_video",
    "version": "1.1",
    "params": [{"label": "Operation", "name": "operation", "type": "list", "values": ["start", "stop"]}],
    "tags": ["pivotable"]
}
```

**debian_motion_cam.js**
```js
'use strict';

const LinuxModule = require('../base/rdhd-mod-base_linux_module');

// moduleCode: debian_motion_cam
class DebianMotionCam extends LinuxModule
{
    // ************************************************************
    //  MotionCam module
    // ************************************************************
    //
    // operation       :   [start/stop]
    // ************************************************************

    constructor(asset, context, session, wsServer, token)
    {
        super(asset, "debian_motion_cam", session, wsServer, token);

        //  POST parameters
        // ******************************
        this.auth = { username: context.username, password: context.password };
        this.operation = context.operation;

        //  Local fields
        // ******************************
        this.url = "https://127.0.0.1:3000/api/assets/" + this.asset.id + "/service"  + this.urlReadyToken;
    }

    configure(whatIf = false)
    {
        let task = "sudo apt update; \
                    sudo apt install motion -y && \
                    sudo sed -i 's/stream_localhost\ on/stream_localhost\ off/g' /etc/motion/motion.conf; \
                    sudo sed -i 's/width\ 320/width\ 640/g' /etc/motion/motion.conf; \
                    sudo sed -i 's/height\ 240/height\ 480/g' /etc/motion/motion.conf";

        //  Async execution
        // ******************************
        this.do(task, "cmd_res", false, whatIf);
    }

    pivot(whatIf = false)
    {
        let axios = require('axios');
        let https = require("https");
        let deasync = require('deasync');
        let response = false;
        let feedback;

        if (this.validate())
        {
            let agent = new https.Agent({ rejectUnauthorized: false });
            let task;
            let op;
            let port;

            if (this.operation.toUpperCase() == "START")
            {
                task = "sudo motion";
                op = "enable";

                //  Spawn a Cam proxy
                // ******************************
                axios.post(this.url,
                { 
                    operation: op,
                    service: {
                        type: "HTTP_PROXY",
                        params: {
                            rport: 8081
                        }
                    }
                },
                {
                    httpsAgent: agent,
                    auth: this.auth
                })
                .then((res) => {
                    response = true;
                    port = res.data.data.service.ports.port;

                })
                .catch((err) => {
                    response = err.message;
                });
                deasync.loopWhile(() => !response);

                //  Async execution
                // ******************************
                this.do(task, "cmd_res", false, whatIf);

                feedback = this.buildWarnMessage("Connect to https://10.10.0.3:" + port + "?t=" + this.token);
            } 
            else 
            {
                task = "sudo killall -9 motion";
                op = "disable";

                //  Destroy a Cam proxy
                // ******************************
                axios.post(this.url,
                { 
                    operation: op,
                    service: {
                        type: "HTTP_PROXY"
                    }
                },
                {
                    httpsAgent: agent,
                    auth: this.auth
                })
                .then((res) => {
                    response = true;
                })
                .catch((err) => {
                    response = err.message;
                });

                deasync.loopWhile(() => !response);

                //  Async execution
                // ******************************
                this.do(task, "cmd_res", false, whatIf);
    
                feedback = this.buildInfoMessage("Operation started");
            }
        }
        else
        {
            feedback = this.buildErrorMessage("Invalid input provided");
        }
        this.reportAndExit(feedback);
    }

    validate()
    {
        let result = false;
        if ((this.operation.toUpperCase() == "START") || (this.operation.toUpperCase() == "STOP"))
        {
            result = true;
        }
        return result;
    }
}

module.exports = DebianMotionCam

```
