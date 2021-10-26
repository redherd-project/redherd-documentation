# Multiple Asset Tasking :: Intro

This section describes the steps required to task multiple assets at the same time.

## 1. Module list

Once you are logged in, you will see the list of all the assets which have already joined the framework.

<img src="asset-list.png" style="display: block; margin-left: auto; margin-right: auto; width: 95%; border: 2px solid #000;" alt="RedHerd">

If you click the module button in the sidebar, you will access to the list of all the available modules:

<img src="module-list.png" style="display: block; margin-left: auto; margin-right: auto; width: 95%; border: 2px solid #000;" alt="RedHerd">

## 2. Module selection

You can use the filter function to search for the specific module that you are looking for:

<img src="module-selection.png" style="display: block; margin-left: auto; margin-right: auto; width: 95%; border: 2px solid #000;" alt="RedHerd">

## 3. Assets selection

Once the module has been selected, it is possible to choose the assets that must execute it:

<img src="asset-selection.png" style="display: block; margin-left: auto; margin-right: auto; width: 95%; border: 2px solid #000;" alt="RedHerd">

## 4. Module configuration

The selected module must be properly configured to be executed. In particular, in this screenshot an IP address is necessary to perform the Ping Flood simulation:

<img src="module-configuration.png" style="display: block; margin-left: auto; margin-right: auto; width: 95%; border: 2px solid #000;" alt="RedHerd">

## 5. Module execution

It is necessary to install all the required dependencies by clicking on the *gear* button and then on *play* to execute the module.

!!! warning
    The module will not be executed by an asset if the related topic has not been previously attached to it. See [`Topics attachment`](https://redherd.readthedocs.io/en/latest/users-guide/single-asset-tasking/#3-topics-attachement) for details.

<img src="module-execution.png" style="display: block; margin-left: auto; margin-right: auto; width: 95%; border: 2px solid #000;" alt="RedHerd">

If the module has been correctly started, you will see a green tick in the *Launched* column.

## 6. Process list

For each asset a new process is spawned, interacting with it an operator could consume the module output or terminate its execution clicking the *kill* button.

<img src="process-list.png" style="display: block; margin-left: auto; margin-right: auto; width: 95%; border: 2px solid #000;" alt="RedHerd">
