irs-nonprofit
=============

Non-profit 990 data collected by PublicResource.org

#!/bin/bash
# usage: extract_tiff.sh [iso name without .iso] [subdir name]
# run this from the new_data directory.
# assume each month is in subdir. Inside of subdir are a set of iso files.

# example:
# sudo bash ./extract_tiff.sh 2012_08_T_01 2012_08_T

ISO=$1
SUB=$2

/sbin/mdconfig -a -t vnode -u 99 -f ./$SUB/$ISO.iso
/bin/mkdir -p /mnt/$ISO.mount
/sbin/mount -t cd9660 /dev/md99 /mnt/$ISO.mount/

/bin/cp -r /mnt/$ISO.mount $SUB/$ISO

/sbin/umount /mnt/$ISO.mount
/bin/rmdir /mnt/$ISO.mount
/sbin/mdconfig -d -u 99