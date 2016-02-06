+++
date = "2016-02-02T22:00:02Z"
description = ""
draft = false
tags = []
title = "Stop 0x0000007B Error on Booting Windows 7"
topics = ["Work"]

+++

## Upgrading from Windows 7 to Windows 10

It was Monday morning. I attempted to upgrade my work PC to Windows 10. My colleagues were able to upgrade to Windows 10 very easily so I thought it'd be a piece of cake.

Unfortunately it wasn't an easy and smooth process for me and took a few hours to complete. 

The upgrade failed with the following error:

```
We couldn't update the system reserved partition.
```

This error appeared to be common and I found a few possible things to try to fix it.

I followed the instructions from this [blog post](//blogs.msdn.microsoft.com/buckh/2015/08/10/fix-windows-10-upgrade-couldnt-update-the-system-reserved-partition/). My system reserved partition was 100 MB and full like the author of the blog.

## Steps

1. Install [MiniTool Partition Wizard Free Edition](//www.minitool.com/partition-manager/partition-wizard-home.html)
2. Reduce the OS partion by 200 MB
3. Increase the system reserved partition by 200 MB
4. Hit Apply and restart my PC

## Results

After step 4, I was met with the following blue screen...

{{% fluid_img "/img/post/stop-0x0000007b-error.jpg" %}}

```
*** STOP: 0x0000007B (0xFFFFF880009A97E8, 0xFFFFFFFFC0000034, 0x000000000000, 0x000000000000)
```

0x0000007B corresponds to **INACCESSIBLE_BOOT_DEVICE**.

At this point, I wasn't able to boot my PC in safe mode at all.

Startup Repair couldn't do anything either. I couldn't blame it because it found no OS so didn't know what to repair! 

## Fix (which worked for me)

1. Boot from Windows recovery disk
2. System Recovery Options -> Command Prompt
3. Run the following command (x is the drive letter where Windows is installed):

```
chkdsk x: /r
```

4. Wait, wait and wait
5. Restart and hope for the best

And this did the trick for me :)

I'm now on Windows 10 and so far so good!