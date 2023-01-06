# AWS Traffic Monitor

This monitor is based in aws cli v2, and it can simply check the usage of the traffic by calling in cli.  
When the usage reached the limit you set, the tool can execute the cmd you pre-defined.

# Requirement

- aws cli v2

if you are not installed currently you may go to
this [Refer](https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2-linux.html) for more details.

# Usage

- -c Path to config file [json]
- -l Interval for loop [second]

## Config Example

```text
[{"Name":"Ubuntu-1","Limit":{"Unit":"GB","Value":1000},"Command":["sudo poweroff"]}]
```

## Service

```
# /etc/systemd/system/traffic_monitor.service
[Unit]
Description=AWS Traffic Monitor
Documentation=https://xnozo.com
After=network.target network-online.target
Requires=network-online.target

[Service]
User=root
Group=root
WorkingDirectory=/root/AWS_Traffic_Monitor/
ExecStart=/root/AWS_Traffic_Monitor/TrafficMonitor -c config.json -l 60

[Install]
WantedBy=multi-user.target
```

# Limitation

The monitor now only support the **lightsail**.

# Author

Made by starx and under **GNU GPLv3** LICENCE.
