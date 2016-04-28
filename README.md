# node-rc

A FreeBSD rc.d script for node.js applications using forever.js.

## Purpose

The goal is to have a node project be a proper system service, starting at boot, restarting upon failure, and ready to drop into a jail.

## Installation

```bash
npm install -g forever
git clone https://github.com/rwestlund/node-rc
cp node-rc/node /usr/local/etc/rc.d/
vim /etc/rc.conf
```

In addition to `node_enable`, the following rc variables should be defined in
/etc/rc.conf:

* `node_msg` -- The name of your program, printed at start. Defaults to "node".
* `node_dir` -- The directory where your node files live. Must be defined.
* `node_logdir` -- The directory for logfiles. Defaults to `${node_dir}/logs`.
* `node_user` -- Passed to noded process as process.env.USER. Defaults to "www".
* `node_group` -- Passed to noded process as process.env.GROUP. Defaults to "www".
* `node_app` -- Application main script. Defaults to "/bin/www" (relative to `node_user`'s home
* `node_forever` -- forever binary file path. Defaults to `/usr/local/bin/forever`.
* `node_local_forever` -- use local forever binary (ie. `node_user's home/node_modules/.bin/forever`)
* `node_forever_log` -- forever log file. Defaults to /var/log/forever.log.

`node_user` and `node_group` may be used to drop node's root privileges after binding to ports.

## Notes
If you do not use mongdb, then remove the mongod dependency from the script.
