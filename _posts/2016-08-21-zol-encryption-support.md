---
layout: post
title: "ZFS on Linux encryption support"
date: 2014-08-22 16:25:06 -0700
comments: false
---

```
root@debtest5:~# uname -a
Linux debtest5 4.6.0-1-amd64 #1 SMP Debian 4.6.4-1 (2016-07-18) x86_64 GNU/Linux
root@debtest5:~# cd zfs/
root@debtest5:~/zfs# git rev-parse HEAD
7d5190d2868b1eeea49583247a7aa4992b7941a8
root@debtest5:~/zfs# ./scripts/zfs.sh -v
Loading spl (/root/spl/module/spl/spl.ko)
Loading splat (/root/spl/module/splat/splat.ko)
Loading zavl (/root/zfs/module/avl/zavl.ko)
Loading znvpair (/root/zfs/module/nvpair/znvpair.ko)
Loading zunicode (/root/zfs/module/unicode/zunicode.ko)
Loading zcommon (/root/zfs/module/zcommon/zcommon.ko)
Loading icp (/root/zfs/module/icp/icp.ko)
Loading zfs (/root/zfs/module/zfs/zfs.ko)
Successfully loaded ZFS module stack
root@debtest5:~/zfs# openssl rand 32 > /root/test-key
root@debtest5:~/zfs# fallocate -l 6G /root/file1.img 
root@debtest5:~/zfs# fallocate -l 6G /root/file2.img 
root@debtest5:~/zfs# ./cmd/zpool/zpool create -O encryption=aes-256-ccm -O  keysource=raw,file:///root/test-key -f tank mirror /root/file{1,2}.img
root@debtest5:~/zfs# ./cmd/zfs/zfs create  tank/dataset1
root@debtest5:~/zfs# 
```

