# TIPS and TRICKS was collected

## CSF knownledge base

- Basic command for csf

```bash
    csf -e      | enables csf
    csf -x      | disables csf
    csf -f      | flush all rule
    csf -r      | restart csf (the connection will be lost)
    csf -g IP   | search IP or CIDR
    csf -a IP   | allow IP
    csf -tr IP  | remove IP from temporary blacklist
    csf -tr     | flush all IP from temporary blacklist
    csf -d IP   | add IP to file /etc/csf/csf.deny to block IP
    csf -dr     | flush all IP form /etc/csf/csf.deny
```

- Open port in csf

  - Open the configuration file :

    ```bash
        vi /etc/csf/csf.conf
    ```

  - In this file , add port you want to allow.

    ```bash
        # Allow incoming TCP ports
        TCP_IN = “20,21,22,25,26,53,80,110,143,443,465,587,993,995,2077”

        # Allow outgoing TCP ports
        TCP_OUT = “20,21,22,25,26,37,43,53,80,110,113,443,465,873,2087”
    ```

  - Restart csf

    ```bash
        csf -r
    ```
  
## Snap error when using proxy

- Error is :

```bash
    error: cannot install "core": Post
    https://api.snapcraft.io/v2/snaps/refresh: Method Not Allowed
```

- Fix : comment 2 line in file `/etc/systemd/system/snapd.service.d/snap_proxy.conf`.

```bash
    #Enviroment="HTTP_PROXY=http://archive.ubuntu.com/ubuntu"
    #Enviroment="HTTPS_PROXY=https://archive.ubuntu.com/ubuntu"
```

- Run to reload snap service:

```bash
    systemctl daemon-reload
    systemctl restart snapd
```

## ERROR Failed to compile PHP extension on Centos

```bash
    make: *** [src/core/ext/filters/client_channel/lb_policy/grpclb/grpclb.lo] Error 1
    ERROR: `make' failed
```

- Fist you should check GCC version, gRPC require GCC version 4.9+, if GCC version in your OS is 4.8 you should upgrade it.

- On Centos OS.

```bash
    sudo yum install centos-release-scl
    sudo yum install devtoolset-7-gcc*
    scl enable devtoolset-7 bash
    pecl install grcp
```

- On Ubuntu

```bash
    sudo apt update
    sudo apt install build-essential
    sudo apt-get install manpages-dev
    pecl install grcp
```