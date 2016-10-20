---
title: "Make Larger Volume For Cinder To Use In Devstack"
layout: post
---

I needed to move the location of the volume backing file from
`/opt/stack/data` to `/mnt` but this can apply also if you just want to
make the volume size larger without rerunning devstack.

Look at the list of currently used files and where they are attached.
Then create a new volume backing file in the location of your choosing
and mount it to the next `loopX` device.

    sudo losetup -a
    export CINDER_VOLUME_LOCATION=/opt/stack/data/cinder-volumes
    dd if=/dev/zero of=$CINDER_VOLUME_LOCATION bs=1 count=0 seek=30G
    sudo losetup $CINDER_VOLUME_LOCATION /dev/loop3
    sudo fdisk /dev/loop3

Use the following keys for fdisk to create a linux vm parition and save
it.

    n
    p
    1
    ENTER
    ENTER
    t
    8e
    w

The next step because devstack modified the lvm config is to edit the
`/etc/lvm/lvm.conf` file and add to the filter.

    sudo emacs /etc/lvm/lvm.conf

    + global_filter = [ "a|loop1|", "a|loop2|", "a|loop3|", "r|.*|" ]  # from devstack

Notice i added `"a|loop3|"` to the global filter. Save this change and
then create the volume.

    sudo pvcreate /dev/loop3
    sudo vgs

With vgs we can see the volume groups available.

    stack-volumes-default
    stack-volumes-lvmdriver-1

The volume group stack-volumes-default is for the snapshots and the
`stack-volumes-lvmdriver-1` volume group is for cinder. So we can now
extend the cinder group knowing this information.

    sudo vgextend stack-volumes  /dev/loop3
    sudo vgs

Now you should see a larger volume size. Its pretty easy.

References:

\[1\] https://udaraliyanage.wordpress.com/2014/05/23/openstack-increase-volume-capacity/

