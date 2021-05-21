# Tinystatus Systemd service

This is a systemd service for tinystatus. Tinystatus is a status page generator made with shell
script.

For information about tinystatus itself, visit [tinystatus repo](https://github.com/bderenzo/tinystatus).

## Setup

To install tinystatus:

* Clone the repository and go to the created directory
* Edit the checks file `checks.csv`
* To add incidents or maintenance, edit `incidents.txt`
* Generate status page `./tinystatus > index.html`
* Serve the page with your favorite web server

To install service:

* Put `tinystatus` and `tinystatus-runner` scripts in `/usr/bin`
* Put `tinystatus.service` in `/etc/systemd/system` and run `systemctl daemon-reload` as root
* Put `checks.csv` and `incidents.txt` in `/etc/tinystatus`
* Enable and start systemd service
* Status page will be generated in `/var/www/tinystatus/index.html`

Service will restart (generate status page) every 5 minutes.

## Configuration file

The syntax of `checks.csv` file is:
```
Command, Expected Code, Status Text, Host to check
```

Command can be:
* `http` - Check http status
* `ping` - Check ping status 
* `port` - Check open port status

There are also `http4`, `http6`, `ping4`, `ping6`, `port4`, `port6` for IPv4 or IPv6 only check.
Note: `port4` and `port6` require OpenBSD `nc` binary.
