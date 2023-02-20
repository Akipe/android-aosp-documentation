# Usefull command get info

- <http://newandroidbook.com/ddb/>

* `cat /proc/cpuinfo`: To get the CPU architecture and details
* `cat /proc/version`: To get the running kernel version
* `cat /proc/partitions`: To get the partition map (might need root)
* `mount` and `df`: To get the mounted partitions stats
* `ls -l /dev`: To get a list of all device nodes (useful for determining standard Linux, AOSP and vendor/BSP additions)
* `ls -l /dev/block/platform/*/*/by-name`: To get the partition names (might require root. As of Android 10, /dev/block/by-name can be used)
* `dumpsys`: For a dump of all services
* `getprop`: To get all the properties set on the device
* `getevent`: To get a list of input devices (after which you can press CTRL-C)
* `service list`: To get a list of all binder services
* `ps -Zefw`: To get a list of all processes and kernel threads on your device (w = boundless width)
* `ls -l /sys/module`: To get a list of all modules, compiled in or loaded. lsmod would also be appreciated if you have loaded modules.
* `lshal` - to list HW HALs
* Rooted devices only - this is the most helpful - get [bindump tool](http://newandroidbook.com/tools/bindump.html) And run `bindump users all` and `bindump vndbinder users all`.
* Rooted only - [`jpt .... list`](http://newandroidbook.com/tools/jpt.html) to dump the GPT partition table
* Rooted only - `lsof` - this really helps
* Rooted only - `ls -lR /` root (otherwise all the good stuff is denied..). This will be a huge file of O(60M), so please gzip before submitting.

The easiest way to get all this output is by running "script" on your MacOS or Linux host before "adb". this logs everything you do (until you type "exit") into a file called "typescript" - which is what I need. Thank you!

If your device identifies as a known chipset listed here, it probably doesn't make sense to list it here unless the outputs of the above commands greatly differ (e.g. `service list`) or are from some esoteric brand.