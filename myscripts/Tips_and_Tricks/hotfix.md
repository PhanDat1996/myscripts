# TIPS and TRICKS was collected

## snap error when using proxy

- error is :

```bash
    error: cannot install "core": Post
    https://api.snapcraft.io/v2/snaps/refresh: Method Not Allowed
```

- fix :

comment 2 line:
`#Enviroment="HTTP_PROXY=http://archive.ubuntu.com/ubuntu"`
`#Enviroment="HTTPS_PROXY=https://archive.ubuntu.com/ubuntu"`

in file `/etc/systemd/system/snapd.service.d/snap_proxy.conf`

- then run :

```bash
    systemctl daemon-reload
    systemctl restart snapd
```
