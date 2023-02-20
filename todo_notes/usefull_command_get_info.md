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


- adb shell dmesg >> insert/path/to/log/where/you/want/to/store
- adb shell cat /sys/fs/pstore/console-ramoops >> insert/path
- adb logcat >> insert/path/to/filename
- adb shell cat /proc/kmsg >> insert/path/to/logfilename
- adb shell cat /proc/last_kmsg >> insert/path/to/logfilename
- dmesg >> insert/path/to/log/where/you/want/to/store 
- cat /sys/fs/pstore/console-ramoops >> insert/path

```
###############################
#                             #
#  PROPER AOSP BUG REPORTING  #
#                             #
###############################
#


Many times when using a custom ROM or kernel, you may experience an issue. The
developer may want something called a logcat or dmesg to look into this but you
may not know how to do that. There are a couple of ways to do so and that is
what I am going to explain now. This is valid for themers, ROM developers, and
kernel developers.

A logcat is useful for debugging crashes or other weird behaviors with apps or
themes. A dmesg is a kernel log, detailing what each subsystem is doing.
A ramoops is the previous dmesg, which will detail why a phone force restarted.
```

```
###################
# 1. USING AN APP #
###################

1. Getting a logcat:
    a. Download a logcat app from the Play Store (I will be using Matlog for
       the rest of this tutorial).
    b. Open the app and grant it root permissions (if you are not rooted and
       do not want to be, you will need to use ADB below).
    c. Clear the buffer but clicking the three dot menu and hitting clear.
    d. Click on the three dot menu, choose File, then Record.
    e. Duplicate your crash/issue.
    f. Go back into Matlog and hit the stop button in the lower righthand corner.
    g. Send the generated file to your developer/themer following the etiquette
       below.

2. Getting a dmesg:
    a. Either download a dmesg app and follow similar steps as above OR download
       a terminal emulator and continue on.
    b. Open your terminal emulator and type su to enter as the root user.
    c. Type dmesg > /sdcard/test.log
    d. Send the generated file (located in the head folder of your internal
       storage partition) to your developer, following the etiquette below.

3. Getting a ramoops:
    a. Open a file manager and navigate to /sys/fs/pstore and copy the file
       named console-ramoops or console-ramoops1 to your sdcard folder.
    b. Send that file to your kernel developer following the etiquette below.
```
```
##################################
# PROPER BUG REPORTING ETIQUETTE #
##################################

1.  First and foremost, understand that for the vast majority of people, this is
    a hobby, not a job. It may take some time for your issue to be resolved.
    Being a jerk or bossy is likely to get you banned or at the least have your
    issue dismissed.

2.  Write in clear, concise manner what the issue is with steps to reproduce

    Bad: My phone is broken, help!
    Good: Whenever I open YouTube after a clean flash, it force closes.

3.  Explain what you have done. A developer should not have to ask what has
    already been attempted.

4.  Provide any scenarios/ROMs where it did work (was it working in a previous
    update, etc.)

5.  If you are technically inclined, provide commits that are either the issue
    or will resolve the issue. Developers love having a solution presented for
    them.
```

```
################
# 2. USING ADB #
################

1.  Download the latest tools from Google:
    https://dl.google.com/android/repository/platform-tools-latest-linux.zip
    https://dl.google.com/android/repository/platform-tools-latest-darwin.zip
    https://dl.google.com/android/repository/platform-tools-latest-windows.zip

2.  Extract those to a folder and move into that folder:
    $ cd <folder_location>

3.  Plug in your device and accept the debugging prompt (turn on ADB in
    Settings > Developer Options if you don't see it).

4.  Verify your device is recognized.
    $ adb devices or $ ./adb devices

5.  Clear the logcat buffer.
    $ adb logcat -c or $ ./adb logcat -c

6.  Take your log:
    Logcat: $ adb logcat -d > test.log or $ ./adb logcat -d > test.log
    dmesg: $ adb shell dmesg > test.log or $ ./adb shell dmesg > test.log

7.  Give that log to the appropriate party with a proper report, following the
    etiquette below.
```