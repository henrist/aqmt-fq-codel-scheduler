# fq_codel scheduler for aqmt

This repository contains the fq_codel scheduler from Linux patched so
it can be used with https://github.com/henrist/aqmt

## Using

When building, we need to add the `common` directory of the `aqmt`
repository to the inclusion path.

Building:

```bash
CPATH=/path/to/aqmt/common make
```

Loading kernel module:

```bash
sudo make load
```

The scheduler will now be available as a qdisc with the name `fq_codel`.
Note that if you had `fq_codel` available already this will shadow that
module, so this will be used instead.

Unloading:

```bash
sudo make unload
```

## Keeping up-to-date with kernel changes

The branch `kernel-reference` contains copies of commits from
the Linux kernel. This is merged into master to produce the latest
patched version.

To update:

```bash
# produce patches
cd path-to-linux-tree
cd net/sched
# modify the range to fit
git format-patch -o /tmp/sched 47ec5303d7..HEAD -- sch_fq_codel.c
```

```bash
# update this repo
git checkout kernel-reference
git am -p3 /tmp/sched/*.patch
git checkout master
git merge kernel-reference
```

Push both branches after reviewing.
