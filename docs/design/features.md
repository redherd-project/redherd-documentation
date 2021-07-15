<h1>Features</h1>

RedHerd has several overwhelming features that characterize it with strong orchestration capabilities:

* **Intuitive Interface**: it provides, through Herd-View, an intuitive web application to easily interact with the assets;
* **Multi-Platform**: it is able to orchestrate a wide range of devices, offering joining and tasking procedures for different operating systems (`Windows`, `Linux`, `MacOS` and `Android`);
* **Multi-User**: it supports multi-user collaboration. The teamwork has become crucial for effective operations. In relation to this, joining RedHerd many users can task the same asset or operate independently;
* **Agentless**: it overcomes the requirement of a local agent waiting for a task to accomplish. Specifically, during the task warmup Herd-Server receives a job for an asset and initiates an SSH connection with it. Subsequently, it specializes and executes the set of commands needed to reach the expected result, allowing a lightweight computational effort asset-side;
* **Easily Deployable**: it is cross platform and can be deployed both on premise and in a Cloud-based environment. In order to grant this feature, a bash script has been proposed to automate the framework deployment process on a Debian-based distro. Taking into account the design choice to use docker-enabled containerization, an equivalent script could be easily developed allowing RedHerd to be hosted on a different operating system;
* **Easily Expandable**: it provides developer ready JavaScript specifications, offering an easy way to expand the product features by writing custom modules and accomplishing an uncountable number of tasks;
* **API Driven**: it is driven by an extensive set of REST API which enables third party application to easily interact with and make use of the framework features.
