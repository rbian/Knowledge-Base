LVM is a Device Mapper target which provides logical volume management for the Linux systems. Heinz Mauelshagen wrote the original code in 1998, taking its primary design guidelines from the HP-UX's volume manager.[3] The installers for the most modern distributions are LVM-aware enough to be able to have the root filesystem be on a logical volume

[LVM how-to](http://tldp.org/HOWTO/LVM-HOWTO/)

#Initializing disks or disk partitions

 Before you can use a disk or disk partition as a physical volume you will have to initialize it:

 Run pvcreate on the disk:

`# pvcreate /dev/hdb`

#Activating a volume group

After rebooting the system or running vgchange -an, you will not be able to access your VGs and LVs. To reactivate the volume group, run:

`# vgchange -a y my_volume_group`

#Removing a volume group

 Make sure that no logical volumes are present in the volume group, see later section for how to do this.

 Deactivate the volume group:

 `# vgchange -a n my_volume_group`
        
 Now you actually remove the volume group:

 `# vgremove my_volume_group`
 
#Adding physical volumes to a volume group

 Use 'vgextend' to add an initialized physical volume to an existing volume group.

 `# vgextend my_volume_group /dev/hdc1`
 
#Removing physical volumes from a volume group

 Make sure that the physical volume isn't used by any logical volumes by using then 'pvdisplay' command:

`# pvdisplay /dev/hda1`

`--- Physical volume ---`
`PV Name               /dev/hda1`
`VG Name               myvg`
`PV Size               1.95 GB / NOT usable 4 MB [LVM: 122 KB]`
`PV#                   1`
`PV Status             available`
`Allocatable           yes (but full)`
`Cur LV                1`
`PE Size (KByte)       4096`
`Total PE              499`
`Free PE               0`
`Allocated PE          499`
`PV UUID               Sd44tK-9IRw-SrMC-MOkn-76iP-iftz-OVSen7`

        
 If the physical volume is still used you will have to migrate the data to another physical volume using pvmove.

 Then use 'vgreduce' to remove the physical volume:

 `# vgreduce my_volume_group /dev/hda1`
 
#Creating a logical volume

 To create a 1500MB linear LV named 'testlv' and its block device special '/dev/testvg/testlv':

 `# lvcreate -L1500 -ntestlv testvg`
        
 To create a 100 LE large logical volume with 2 stripes and stripe size 4 KB.

 `# lvcreate -i2 -I4 -l100 -nanothertestlv testvg`
        
 If you want to create an LV that uses the entire VG, use vgdisplay to find the "Total PE" size, then use that when running lvcreate.

 `# vgdisplay testvg | grep "Total PE"`
 `Total PE              10230`
 `# lvcreate -l 10230 testvg -n mylv`
        
This will create an LV called mylv filling the testvg VG.

 If you want the logical volume to be allocated from a specific physical volume in the volume group, specify the PV or PVs at the end of the lvcreate command line.

 `# lvcreate -L 1500 -ntestlv testvg /dev/sdg`
 
#Removing a logical volume

 A logical volume must be closed before it can be removed:

 `# umount /dev/myvg/homevol`
 `# lvremove /dev/myvg/homevol`
 `lvremove -- do you really want to remove "/dev/myvg/homevol"? [y/n]: y`
 `lvremove -- doing automatic backup of volume group "myvg"`
 `lvremove -- logical volume "/dev/myvg/homevol" successfully removed`
        
