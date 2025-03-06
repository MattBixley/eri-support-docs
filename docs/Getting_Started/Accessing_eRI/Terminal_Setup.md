---
created_at: '2018-11-30T00:34:14Z'
tags:
- ssh
- howto
description: How to setup your ssh config file in order to connect to the NeSI cluster.
---

!!! prerequisite
     -   Have an [active account and project.](../../Getting_Started/Accounts-Projects_and_Allocations/Creating_a_NeSI_Account_Profile.md)
     -   Set up your [Linux Password.](../../Getting_Started/Accessing_the_HPCs/Setting_Up_and_Resetting_Your_Password.md)
     -   Set up [Second Factor Authentication.](../../Getting_Started/Accessing_the_HPCs/Setting_Up_Two_Factor_Authentication.md)
     -   Have one of:
         - Built in Linux/Mac terminal
         - [Windows Subsystem for Linux](../../Scientific_Computing/Terminal_Setup/Windows_Subsystem_for_Linux_WSL.md)
         - [VSCode](../../Scientific_Computing/Terminal_Setup/VSCode.md)

## First time setup

The login process can be simplified significantly with a few easy
configurations.

1. In a new local terminal run; `mkdir -p ~/.ssh/sockets` this will
    create a subdirectory in your home directory to store socket
    configurations.

2. Open your ssh config file (e.g. `nano ~/.ssh/config` to open with the text editor `nano`) and add the
    following (replacing **`username`** with your username):

```sh
Host ssh.agresearch.co.nz
    HostName ssh.agresearch.co.nz
    User bixleym
    IdentitiesOnly yes
    IdentityFile ~/.ssh/agr.rsa
    ForwardX11 yes
    ForwardX11Trusted yes
    ServerAliveInterval 300
    ServerAliveCountMax 2

Host inscrutable.agresearch.co.nz
    HostName inscrutable.agresearch.co.nz
    ProxyJump bixleym@ssh.agresearch.co.nz
    User bixleym
    IdentitiesOnly yes
    IdentityFile ~/.ssh/agr.rsa
    ForwardX11 yes
    ForwardX11Trusted yes
    ServerAliveInterval 300
    ServerAliveCountMax 2

Host *
    ControlMaster auto
    ControlPath ~/.ssh/sockets/ssh_mux_%h_%p_%r
    ControlPersist 1
```

3. Ensure the permissions are correct by
    running `chmod 600 ~/.ssh/config`.

## Usage

Assuming you have followed the setup above you will be able to connect
to the clusters directly using;

```sh
ssh eri
```

!!! prerequisite "What Next?"
     -   [Moving files to/from a cluster.](../../Getting_Started/Next_Steps/Moving_files_to_and_from_the_cluster.md)
     -   Setting up an [X-Server](../../Scientific_Computing/Terminal_Setup/X11_on_NeSI.md) (optional).
