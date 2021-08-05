# API Usage :: Intro

The interaction with Herd-Server is realized by a set of RESTful API, some of which are authenticated through JSON Web Token (JWT) claims. This system is normally used by the Herd-View to dispatch all the tasks, but it has to be intended as a general interface suitable for interacting with the assets through the Herd-Server.

## Background

Herd-Server responds to the REST requests by using the [`JSend`](https://github.com/omniti-labs/jsend) specification, offering a consistent JSON response format which could be universally recognized and providing an easy way to consume and interact with the framework components.

In particular, CRUD operations (`create`, `read` or `retrieve`, `update`, `delete`) are performed through their corresponding HTTP verbs:

- **POST** method to `create` items;

- **GET** method to `retrieve` items;

- **PUT** method to `update` an existing item;

- **DELETE** method to `remove` items.

In addition, the execution of a module is triggered using a dedicated endpoint and a specific POST request. This behaviour expands the number of functions offered by a traditional RESTful service implementing the CRUD(E) operations set which introduces the additional `execute` verb. An entity which sends a POST request to run a module, receives a JSend response containing the `sessionid` reflected into the output flow.

The direct interaction between Herd-Server and an asset is instead based on SSH (a consolidated protocol which offers stability as well as compatibility with the majority of the available operating systems). In addition, the usage of SSH leads to the agentless implementation characterizing RedHerd. Specifically, when Herd-Server receives a task request for an asset, it initiates an SSH connection with it contextualizing and executing the commands set needed to reach the expected result. This kind of interaction overcomes the needs of a local agent waiting for a task to accomplish and allows for a lightweight computational effort asset-side.

<img src="framework_tasking.png" style="display: block; margin-left: auto; margin-right: auto; width: 95%;" alt="RedHerd">

## Specifications

A list of all the available REST API is documented in this [`datasheet`](https://docs.google.com/spreadsheets/d/1pbfyDeyFXGD8N7OqmQ6GY2Pw0ehyyIVAOf0DlusAsX4/edit?usp=sharing).

## Hands-on

The following examples serve as an overview on how to interact with RedHerd using the API and the `curl` program.

### Example 1. Authenticate

**Success**

```bash
$ curl -X POST --insecure -i -H "Content-Type: application/json" -d '{"username":"firstuser","password":"mys3cr3t"}' "https://10.10.0.3:3000/api/login"
HTTP/1.1 200 OK
X-Powered-By: Express
Content-Type: application/json; charset=utf-8
Content-Length: 490
Date: Fri, 01 Jul 1900 16:00:00 GMT

{
    "status": "success",
    "data": {
        "token":"eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2Vy [...] KDP4jvyBA"
    }
}
```

**Fail**

```bash
$ curl -X POST --insecure -i -H "Content-Type: application/json" -d '{"username":"firstuser","password":"wrongs3cr3t"}' "https://10.10.0.3:3000/api/login"
HTTP/1.1 200 OK
X-Powered-By: Express
Content-Type: application/json; charset=utf-8
Content-Length: 59
Date: Fri, 01 Jul 1900 16:00:00 GMT

{
    "status": "fail",
    "data": { 
        "reason": "Authentication failed"
    }
}
```

**Error**

```bash
$ curl -X POST --insecure -i -H "Content-Type: application/json" -d '{"username":"firstuser","password":"mys3cr3t"}' "https://10.10.0.3:3000/api/login"
HTTP/1.1 200 OK
X-Powered-By: Express
Content-Type: application/json; charset=utf-8
Content-Length: 58
Date: Fri, 01 Jul 1900 16:00:00 GMT

{
    "status": "error",
    "message": "An exception has occurred"
}
```

### Example 2. Retrieve module info 

**Success**

```bash
$ curl -X GET --insecure -i -H "Content-Type: application/json" "https://10.10.0.3:3000/api/modules/debian_ping"
HTTP/1.1 200 OK
X-Powered-By: Express
Content-Type: application/json; charset=utf-8
Content-Length: 276
Date: Fri, 01 Jul 1900 16:00:00 GMT

{
    "status": "success",
    "data": {
        "module": {
            "name": "debian_ping",
            "title": "Ping",
            "description": "A ping demo module",
            "binary": "ping",
            "author": "c4dm10 & peco602",
            "topic": "debian_misc",
            "version": "1.0",
            "params": [
                { "label": "Target", "name": "target", "type": "string" }
            ],
            "tags": [ "automatic" ]
        }
    }
}
```

**Fail**

```bash
$ curl -X GET --insecure -i -H "Content-Type: application/json" "https://10.10.0.3:3000/api/modules/wrong.module"
HTTP/1.1 200 OK
X-Powered-By: Express
Content-Type: application/json; charset=utf-8
Content-Length: 276
Date: Fri, 01 Jul 1900 16:00:00 GMT

{
    "status": "fail",
    "data": {
        "reason": "Invalid moduleName provided"
    }
}
```

**Error**

```bash
$ curl -X GET --insecure -i -H "Content-Type: application/json" "https://10.10.0.3:3000/api/modules/debian_ping"
HTTP/1.1 200 OK
X-Powered-By: Express
Content-Type: application/json; charset=utf-8
Content-Length: 58
Date: Fri, 01 Jul 1900 16:00:00 GMT

{
    "status": "error",
    "message": "An exception has occurred"
}
```

### Example 3. Execute a module

**Success**

```bash
$ curl -X POST --insecure -i -H "Content-Type: application/json" -d '{"mode":"execute","params":{"target":"www.fakesite.local"}}' "https://10.10.0.3:3000/api/assets/1/modules/debian_ping/run?t=eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2Vy [...] KDP4jvyBA"
HTTP/1.1 200 OK
X-Powered-By: Express
Content-Type: application/json; charset=utf-8
Content-Length: 101
Date: Fri, 01 Jul 1900 16:00:00 GMT

{
    "status": "success",
    "data": {
        "instance": {
            "session": "91f73ca7ff9d98359fefc137c93422ba",
            "result": null
        }
    }
}
```

**Fail**

```bash
$ curl -X POST --insecure -i -H "Content-Type: application/json" -d '{"mode":"execute","params":{"target":"www.fakesite.local"}}' "https://10.10.0.3:3000/api/assets/1/modules/debian_ping/run?t=eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2Vy [...] KDP4jvyBA"
HTTP/1.1 200 OK
X-Powered-By: Express
Content-Type: application/json; charset=utf-8
Content-Length: 58
Date: Fri, 01 Jul 1900 16:00:00 GMT

{
    "status": "fail",
    "data": {
        "reason": "Module not available"
    }
}
```

**Error**

```bash
$ curl -X POST --insecure -i -H "Content-Type: application/json" -d '{"mode":"execute","params":{"target":"www.fakesite.local"}}' "https://10.10.0.3:3000/api/assets/1/modules/debian_ping/run?t=eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2Vy [...] KDP4jvyBA"
HTTP/1.1 200 OK
X-Powered-By: Express
Content-Type: application/json; charset=utf-8
Content-Length: 58
Date: Fri, 01 Jul 1900 16:00:00 GMT

{
    "status": "error",
    "message": "An exception has occurred"
}
```

### Example 4. Create a topic

**Success**

```bash
$ curl -X POST --insecure -i -H "Content-Type: application/json" -d '{"name":"demo_topic","description":"This is a demo topic"}' "https://10.10.0.3:3000/api/topics"
HTTP/1.1 200 OK
X-Powered-By: Express
Content-Type: application/json; charset=utf-8
Content-Length: 32
Date: Fri, 01 Jul 1900 16:00:00 GMT

{
    "status": "success",
    "data": null
}
```

**Fail**

```bash
$ curl -X POST --insecure -i -H "Content-Type: application/json" -d '{"name":"wrong.topic","description":"This is a wrong topic"}' "https://10.10.0.3:3000/api/topics"
HTTP/1.1 200 OK
X-Powered-By: Express
Content-Type: application/json; charset=utf-8
Content-Length: 64
Date: Fri, 01 Jul 1900 16:00:00 GMT

{
    "status": "fail",
    "data": {
        "reason": "Invalid topicName provided"
    }
}
```

**Error**

```bash
$ curl -X POST --insecure -i -H "Content-Type: application/json" -d '{"name":"demo_topic","description":"This is a demo topic"}' "https://10.10.0.3:3000/api/topics"
HTTP/1.1 200 OK
X-Powered-By: Express
Content-Type: application/json; charset=utf-8
Content-Length: 58
Date: Fri, 01 Jul 1900 16:00:00 GMT

{
    "status": "error",
    "message": "An exception has occurred"
}
```

### Example 5. Delete a type

**Success**

```bash
$ curl -X DELETE --insecure -i "https://10.10.0.3:3000/api/types/1"
HTTP/1.1 200 OK
X-Powered-By: Express
Content-Type: application/json; charset=utf-8
Content-Length: 32
Date: Fri, 01 Jul 1900 16:00:00 GMT

{
    "status": "success",
    "data": null
}
```

**Fail**

```bash
$ curl -X DELETE --insecure -i "https://10.10.0.3:3000/api/types/wrong"
HTTP/1.1 200 OK
X-Powered-By: Express
Content-Type: application/json; charset=utf-8
Content-Length: 61
Date: Fri, 01 Jul 1900 16:00:00 GMT

{
    "status": "fail",
    "data": {
        "reason": "Invalid typeId provided"
    }
}
```

**Error**

```bash
$ curl -X DELETE --insecure -i "https://10.10.0.3:3000/api/types/1"
HTTP/1.1 200 OK
X-Powered-By: Express
Content-Type: application/json; charset=utf-8
Content-Length: 58
Date: Fri, 01 Jul 1900 16:00:00 GMT

{
    "status": "error",
    "message": "An exception has occurred"
}
```

### Example 6. Update an asset

**Success**

```bash
$ curl -X PUT --insecure -i -H "Content-Type: application/json" -d '{"description":"This is an updated description"}' "https://10.10.0.3:3000/api/assets/1"
HTTP/1.1 200 OK
X-Powered-By: Express
Content-Type: application/json; charset=utf-8
Content-Length: 32
Date: Fri, 01 Jul 1900 16:00:00 GMT

{
    "status": "success",
    "data": null
}
```

**Fail**

```bash
$ curl -X PUT --insecure -i -H "Content-Type: application/json" -d '{"description":"This is an updated description"}' "https://10.10.0.3:3000/api/assets/wrong"
HTTP/1.1 200 OK
X-Powered-By: Express
Content-Type: application/json; charset=utf-8
Content-Length: 72
Date: Fri, 01 Jul 1900 16:00:00 GMT

{
    "status": "fail",
    "data": {
        "reason": "Invalid asset identification param"
    }
}
```

**Error**

```bash
$ curl -X PUT --insecure -i -H "Content-Type: application/json" -d '{"description":"This is an updated description"}' "https://10.10.0.3:3000/api/assets/1"
HTTP/1.1 200 OK
X-Powered-By: Express
Content-Type: application/json; charset=utf-8
Content-Length: 58
Date: Fri, 01 Jul 1900 16:00:00 GMT

{
    "status": "error",
    "message": "An exception has occurred"
}
```
