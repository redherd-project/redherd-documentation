# Asset Tasking :: Intro

This section describes the steps required to access the framework GUI and assign tasks to assets.

## 1. Herd-View login

Connect to Herd-View at `https://10.10.0.5` and fill the login page with your user credentials.

<img src="login.png" style="display: block; margin-left: auto; margin-right: auto; width: 95%; border: 2px solid #000;" alt="RedHerd">

## 2. Asset interaction

Once you are logged in, you will be able to interact with the list of all the assets which have already joined the framework. For each asset you will find:

- Name
- IP address
- Status (`online`/`offline`)
- User
- Description

<img src="asset-list.png" style="display: block; margin-left: auto; margin-right: auto; width: 95%; border: 2px solid #000;" alt="RedHerd">

You can directly interact with the asset by opening a terminal:

<img src="asset-terminal.png" style="display: block; margin-left: auto; margin-right: auto; width: 95%; border: 2px solid #000;" alt="RedHerd">

or you can configure the asset to perform tasks:

<img src="asset-config.png" style="display: block; margin-left: auto; margin-right: auto; width: 95%; border: 2px solid #000;" alt="RedHerd">


## 3. Topics attachement

First, it is necessary to associate some topics to the asset in relation to the type of tasks to perform (e.g. reconnaissance).

<img src="asset-topics-adding.png" style="display: block; margin-left: auto; margin-right: auto; width: 95%; border: 2px solid #000;" alt="RedHerd">


## 4. Module selection

Once you have associated a topic to an assets, all the related module will be available to it and could be potentially used against targets.

<img src="asset-modules.png" style="display: block; margin-left: auto; margin-right: auto; width: 95%; border: 2px solid #000;" alt="RedHerd">

## 5. Module configuration

Before executing a module it is necessary to install all its dependencies on the selected `asset` by clicking on the *gear* button.

<img src="module-configure.png" style="display: block; margin-left: auto; margin-right: auto; width: 95%; border: 2px solid #000;" alt="RedHerd">

## 6. Module execution

You must insert the required parameters:

<img src="module-start.png" style="display: block; margin-left: auto; margin-right: auto; width: 95%; border: 2px solid #000;" alt="RedHerd">

and then you can easily interact with the asset to perform the desired task by pressing the *play* button.

<img src="module-interact.png" style="display: block; margin-left: auto; margin-right: auto; width: 95%; border: 2px solid #000;" alt="RedHerd">


## Hands-on

<iframe width="560" height="315" src="https://www.youtube.com/embed/_jDor_CCcC4" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" style="margin-bottom: 30px;" allowfullscreen></iframe>
