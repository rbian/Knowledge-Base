DM-Multipathing (DM-MPIO) provides input-output (I/O) fail-over and load-balancing within Linux for block devices.[1][2][3] By utilizing device-mapper, multipathd provides the host-side logic to use multiple paths of a redundant network to provide continuous availability and higher bandwidth connectivity between the host server and the block-level device.[4] DM-MPIO handles the rerouting of block I/O to an alternate path in the event of a path failure. DM-MPIO can also balance the I/O load across all of the available paths that are typically utilized in Fibre Channel (FC) and iSCSI SAN environments.[5] DM-MPIO is based on the device mapper, which provides the basic framework that maps one block device onto another.

[Linux_DM_Multipath - wiki](https://en.wikipedia.org/wiki/Linux_DM_Multipath)

[Setting Up DM-Multipath] (https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6-Beta/html-single/DM_Multipath/index.html#setup_procedure)

[multipath(8) - Linux man page] (http://linux.die.net/man/8/multipath)
