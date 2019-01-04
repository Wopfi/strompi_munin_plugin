# strompi_munin_plugin
## What it does

A Munin plugin for monitoring the [StromPi 3](https://strompi.joy-it.net/)

This plugin fetches the voltages and battery capacity and visualizes them in munin graphs.

## How to install

First you should clone the repository with
`git clone https://github.com/Wopfi/strompi_munin_plugin.git`
You'll end up with directory called strompi_munin_plugin containing this file and the plugin Python script named `strompi_`
For the plugin to work you'll need python and a working serial connection to the StromPi 3 board.

The Plugin needs to be copied into the munin plugin directory which should be
`/usr/share/munin/plugins/`
on the Raspberry Pi.

Also the plugin's configuration needs to be added to
`/etc/munin/plugin-conf.d/munin-node`
```
[strompi*]
user root
group root
```

This plugin is enabled for automatic installation by munin-node-configure so after you followed the above steps you just need to run
`sudo munin-node-configure --shell` to get the shell code for creating the needed symlinks. Or you can just pipe that output directly to the shell by running
`sudo /usr/sbin/munin-node-configure --shell | sudo sh` in the `/etc/munin/plugins` directory.

Either way you should end up with this additional symlinks:
```
lrwxrwxrwx 1 root root 30 Apr 17 14:03 strompi_battery -> /usr/share/munin/plugins/strompi_
lrwxrwxrwx 1 root root 30 Apr 17 14:03 strompi_voltages -> /usr/share/munin/plugins/strompi_
```
Now you just need to restart the munin-node by typing
`sudo service munin-node restart`
and the graphs should start showing up in the next cycle.
