---
created_at: '2025-11-30T00:34:14Z'
tags:
- ssh
- howto
---

!!! prerequisite
     -   Have an [active account and project.](../../Getting_Started/Accessing_eRI/Creating_an_eRI_Account.md)
     -   Using standard Linux/Mac terminal *or* [Windows Subsystem for Linux](../../Scientific_Computing/Terminal_Setup/Windows_Subsystem_for_Linux_WSL.md)
         with [Ubuntu terminal](../../Scientific_Computing/Terminal_Setup/Ubuntu_LTS_terminal_Windows.md).

## First time setup

The login process can be simplified significantly with a few easy
configurations.

1. In a new local terminal run; `mkdir -p ~/.ssh/sockets` this will
    create a hidden file in your home directory to store socket
    configurations.

2. Open your ssh config file with `nano ~/.ssh/config` and add the
    following (replacing **`username`** with your username):

    ```sh
    Host login-0
        HostName login-0.eri.agresearch.co.nz
        User <USERID>@agresearch.co.nz     # eg blogsj@agresearch.co.nz
        GSSAPIAuthentication yes

    Host login-1
        HostName login-1.eri.agresearch.co.nz
        User <USERID>@agresearch.co.nz     # eg blogsj@agresearch.co.nz
        GSSAPIAuthentication yes
    ```

    Close and save with ctrl x, y, Enter

3. Ensure the permissions are correct by
    running `chmod 600 ~/.ssh/config`.

## Usage

Assuming you have followed the setup above you will be able to connect
to the clusters directly using;

```sh
ssh login-0
```

or

```sh
ssh login-1
```

Subsequent local terminals opened will be able to `scp` files without
having to re-enter authentication e.g.

```sh
scp <path/filename> login-0:~/
```

For more info visit [data transfer](../../Getting_Started/Next_Steps/Moving_files_to_and_from_the_cluster.md).

!!! prerequisite "What Next?"
     -   [Moving files to/from a cluster.](../../Getting_Started/Next_Steps/Moving_files_to_and_from_the_cluster.md)
     -   Setting up an [X-Server](../../Scientific_Computing/Terminal_Setup/X11_on_NeSI.md) (optional).
