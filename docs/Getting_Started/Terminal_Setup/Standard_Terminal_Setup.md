---
created_at: '2025-11-30T00:34:14Z'
tags:
- ssh
- howto
---

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

For more info visit [data transfer](../../File_Systems/File_Transfer.md).

1473709      bash                 2024-proxy_development_methane biltont@agresea RUNN      26:00    7:34:00 compute-0 2 16G (null)
srun --nodelist=compute-0 --pty bash mem=16G
