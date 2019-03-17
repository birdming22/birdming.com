

# Data Recovery

first thing is to detach file system

    sudo unmount -l /dev/sda1

## debugfs
* ref. [Debug a file system](http://users.nccs.gov/~fwang2/linux/lk_debugfs.html)
* ref. [debugfs Command Examples](http://www.cs.montana.edu/courses/309/topics/4-disks/debugfs_example.html)

Find inode of file

    % ls -li testfile
    5505914 -rw-rw-r-- 1 k100 k100 0  5月 19 10:42 testfile

If inode is available, use **cat** or **dump** to dump file

    % sudo debugfs /dev/sdb1
    debugfs 1.42.9 (4-Feb-2014)
    debugfs:  cat <5505914>
    debugfs:  dump <5505914> /tmp/testfile

Use grep to find data block, and find inode from data block by **icheck**

    % grep --only-matching --byte-offset --binary --text --perl-regexp "\x51\x46\x49" /dev/sda1
    25165824:QFI
    222100898:QFI

    % sudo debugfs /dev/sdb1
    debugfs 1.42.9 (4-Feb-2014)
    debugfs:  icheck 25165824

Use lsdel to undelete file

ref. [Linux debugfs Hack: Undelete Files](http://www.cyberciti.biz/tips/linux-ext3-ext4-deleted-files-recovery-howto.html)

Recover **Overwritten** files ?

ref. [Can overwritten files be recovered?](http://unix.stackexchange.com/questions/149342/can-overwritten-files-be-recovered)

In ref url, block size is 512, recently ext4 block size is 4096.

    grep -a -b "text in the deleted file" /dev/sda1
    13813610612:this is some text in the deleted file
    
    dd if=/dev/sda1 bs=512 count=1 skip=$(expr 13813610612 / 512)

if file is large, data blocks of file could not be continuous and hard to recover. use filegrag (e2fsprogs) to get layout information.

    # filefrag -v bitnami-reviewboard.qcow2 
    Filesystem type is: ef53
    File size of bitnami-reviewboard.qcow2 is 15547367424 (3795744 blocks, blocksize 4096)
     ext logical  physical  expected length flags
       0       0 278986752            32768 
       1   32768 279019520            32768 
     168 3727360 338982912 325736448   2048 
     169 3729408 339019776 338984960   2048 
     170 3731456 788815872 339021824   4096 
     171 3735552 979961856 788819968   2048 
     172 3737600 979970048 979963904   4096 
     173 3741696 980002816 979974144   2048 
     174 3743744 980015104 980004864   4096 
     175 3747840 980285440 980019200   2048 
     176 3749888 980889600 980287488   8192 
     177 3758080 981530624 980897792   2048 
     178 3760128 981565440 981532672   6144 
     179 3766272 981573632 981571584  29472 eof

block size

    sudo dumpe2fs -h /dev/sda1

## e2fsck
use backup journal block to recover file system

    sudo e2fsck -f -b 32768 /dev/nbd1p1

## Ext4magic

* [Official Site](http://ext4magic.sourceforge.net/ext4magic_en.html)
* Based on ext3grep and extundelete
* example: [ext4 recover deleted files (undelete) using ext4magic on CentOS 6](http://source.kohlerville.com/2013/02/ext4-recover-deleted-files-undelete-using-ext4magic-on-centos-6/)

## photorec
[PhotoRec](http://www.cgsecurity.org/wiki/PhotoRec) is file data recovery software designed to recover lost files.

### How PhotoRec works

PhotoRec identifies a JPEG file when a block begins with:

    0xff, 0xd8, 0xff, 0xe0
    0xff, 0xd8, 0xff, 0xe1
    or 0xff, 0xd8, 0xff, 0xfe

## Reference

* [深入理解ext4（一）----extent區段](http://blog.csdn.net/sara4321/article/details/8609610)
* [EXT4介紹與分析](http://blog.csdn.net/robinlovesnow/article/details/7567037)
* [如何恢復 Linux 上刪除的文件，第 5 部分：ext4](https://www.ibm.com/developerworks/cn/linux/l-cn-filesrc5/)
