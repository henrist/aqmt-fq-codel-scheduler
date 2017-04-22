# fq_codel scheduler for aqmt

This repository contains the fq_codel scheduler from Linux patched so
it can be used with https://github.com/henrist/aqmt

New commits in Linux should be cherry-picked to the `kernel-reference`
branch and merged to master. This way the `kernel-reference` should
be a 1-to-1 match to the implementation in Linux.

## Using

Before building you have to symlink `common/testbed.h` from the aqmt project
so it is available in this folder.

Building:

```
make
```

Loading kernel module:

```
sudo make load
```

The scheduler will now be available as a qdisc with the name `fq_codel`.
Note that if you had `fq_codel` available already this will shadow that
module, so this will be used instead.

Unloading:

```
sudo make unload
```
