---
created_at: '2018-11-30T00:34:14Z'
tags:
- ssh
- howto
description: How to setup your ssh config file in order to connect to the eRI cluster.
---


## First time setup

The login process can be simplified significantly with a few easy
configurations.

1. In a new local terminal run; `mkdir -p ~/.ssh/sockets` this will
    create a subdirectory in your home directory to store socket
    configurations.

2. Open your ssh config file (e.g. `nano ~/.ssh/config` to open with the text editor `nano`) and add the
    following (replacing **`username`** with your username):

```sh
ControlPath ~/.ssh/control/%C
ControlMaster auto
Host login-0
   User <userid>@agresearch.co.nz
   Hostname 10.29.107.20
   ProxyCommand ssh -YW %h:%p login-0
   ServerAliveInterval 300
   ServerAliveCountMax 2
   ForwardX11 yes
   ForwardX11Trusted yes

ControlPath ~/.ssh/control/%C
ControlMaster auto
Host login-1
   User <userid>@agresearch.co.nz
   Hostname 10.29.107.20
   ProxyCommand ssh -YW %h:%p login-1
   ServerAliveInterval 300
   ServerAliveCountMax 2
   ForwardX11 yes
   ForwardX11Trusted yes
```

3. Ensure the permissions are correct by
    running `chmod 600 ~/.ssh/config`.

## Usage

Assuming you have followed the setup above you will be able to connect
to the clusters directly using;

```sh
ssh login-0
```

!!! prerequisite "What Next?"
     -   [Moving files to/from a cluster.](../../File_Systems/File_Trnsfer.md)

