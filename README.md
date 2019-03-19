# How-to-create-custom-script-to-run-automatically-during-boot-in-RHEL-CentOS-7

Linux : How to configure a custom script in systemd to run during boot in RHEL/CentOS-7


# vi /var/tmp/myscript.sh
#!/bin/bash
echo "`date` : This is a sample script to test auto run during boot" > /var/tmp/script.out


chmod +x /var/tmp/myscript.sh


# vi /etc/systemd/system/sample.service
[Unit]
Description=Description for sample script goes here
After=network.target

[Service]
Type=simple
ExecStart=/var/tmp/myscript.sh
TimeoutStartSec=0

[Install]
WantedBy=default.target



After= : If the script needs any other system facilities (networking, etc), modify the [Unit] section to include appropriate After=, Wants=, or Requires= directives.

Type= : Switch Type=simple for Type=idle in the [Service] section to delay execution of the script until all other jobs are dispatched

WantedBy= : target to run the sample script in


systemctl daemon-reload

systemctl enable sample.service

systemctl start sample.service

systemctl reboot
