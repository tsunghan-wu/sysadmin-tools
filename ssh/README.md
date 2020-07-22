# SSH Common Usages

Here are some SSH commands that I commonly use.

## A. Basic

### 0. SSH

```
ssh remote-host                     # login remote server
ssh remote-host <remote command>    # execute remote command
```

### 1. SSH commands options

```
ssh -p <ssh port>
ssh -l <login-account>
ssh -D port ... (local dynamic application-level port forwarding -> See section B.) 
ssh -L, ssh -R ... (port forwarding -> See section B.)
ssh -N (Do not execute remote command -> Useful for just port forwarding)
ssh -f (make ssh background)
```

### 2. SSH Config Example

```
Host intern
    Hostname <dest-host>
    Port 22
    ProxyJump <proxy jump server>
    User patrickwu2
```

Thus, one can only type `ssh intern` to login the dest-host.

### 3. ssh key-gen & ssh-copy-id

- Too easy, skip.

### 4. Useful SSH Applications

- scp
- rsync (ex:`rsync -az /home/testuser/data remoteserver:backup/`)
- Edit files with VIM over ssh
    - ex: `vim scp://<remote-host>/<path>`
- VNC + ssh tunnel [simple-tutorial](https://wslab.csie.ntu.edu.tw/using_VNC.html)

## B. Advanced

### 1. ssh proxy server

> Local Machine port \<port\> -> remote-host
> Common usage : proxy server (internal network browser)

```
ssh -NfD <port> <remote-host>
```

### 2. SSH Tunnel

> Local access Remote
> Bind 127.0.0.1's local-port <-> remote-host's remote-port

```
ssh -L <local-port>:127.0.0.1:<remote-port> <remote-host>
```

### 3. SSH Reverse Tunnel

> Remote-host's remote-port can access local's \<local-port\>

```
ssh -R <remote-port>:127.0.0.1:<local-port> <remote-host>
```

### 4. SSHFS

```
sshfs <remote-host>:<remote abs path> <local mount points>
```

### Reference

- https://hackertarget.com/ssh-examples-tunnels/
- Linux man page
