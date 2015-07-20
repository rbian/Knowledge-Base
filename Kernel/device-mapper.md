The device mapper is Linux kernel's framework for mapping physical block devices onto higher-level virtual block devices. It forms the foundation of LVM2, software RAIDs and dm-crypt disk encryption, and offers additional features such as file system snapshots.

Device mapper works by passing data from a virtual block device, which is provided by the device mapper itself, to another block device. Data can be also modified in transition, which is performed, for example, in the case of device mapper providing disk encryption or simulation of unreliable hardware behavior.

#Device Mapper Arch
![](/home/rbian/Downloads/image002.gif)

#[Dmsetup commands](https://wiki.gentoo.org/wiki/Device-mapper)

*Create*

The create command activates a new device mapper device. It appears in /dev/mapper. In addition, if the target has metadata, it reads it, or if this its first use, it initializes the metadata devices. Note the prior device mapper devices can be passed as parameters (if the target takes a device), thus it is possible to "stack" them. The syntax is: `dmsetup create <new device name> --tables <start sector> <end sector> <target name> <target parmaters>`

*Remove*

The remove command deactivates a device mapper device. It removes it from /dev/mapper. Syntax is `dmsetup remove [-f] <device name>` Note is not possible to remove a device that's in use. The -f option may be passed the replace the target with one that fails all I/O, hopefully allowing the reference count to drop to 0.

*Message*

The message command send a message to the device. What message are supported depend on the target Syntax is: `dmsetup message <sector number> <device name> <target message>` The <sector number> tends not to be used and is almost always 0.

*Suspend*

The suspend command stops any NEW I/O. Existing I/O will still be completed. This can be used to quiesce a device. Syntax is: `dmsetup message suspend <device name>`

*Resume*

The resume command allows I/O to be submitted to a previously suspended device. Syntax is: `dmsetup message suspend <device name>`

*Reload*

The reload command replaces an existing device, possible with new targets and/or parameters. It may be necessary to suspend the target first. Some targets are immutable and can't be replaced with this command. Syntax is the same as create
