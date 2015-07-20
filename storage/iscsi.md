In computing, iSCSI is an acronym for Internet Small Computer System Interface, an Internet Protocol (IP)-based storage networking standard for linking data storage facilities.

By carrying SCSI commands over IP networks, iSCSI is used to facilitate data transfers over intranets and to manage storage over long distances. iSCSI can be used to transmit data over local area networks (LANs), wide area networks (WANs), or the Internet and can enable location-independent data storage and retrieval.

The protocol allows clients (called initiators) to send SCSI commands (CDBs) to SCSI storage devices (targets) on remote servers. It is a storage area network (SAN) protocol, allowing organizations to consolidate storage into data center storage arrays while providing hosts (such as database and web servers) with the illusion of locally attached disks.[1]

Unlike traditional Fibre Channel, which usually requires dedicated cabling,[a] iSCSI can be run over long distances using existing network infrastructure.[2] iSCSI was pioneered by IBM and Cisco in 1998 and submitted as draft standard in March 2000.

[wiki](https://en.wikipedia.org/wiki/ISCSI)

[Configuring iSCSI target using 'targetcli'](https://wiki.rvijay.in/index.php/Configuring_iSCSI_target_using_'targetcli')

#Logging In to an iSCSI Target
the iSCSI service must be running in order to discover or log into targets. To start the iSCSI service, run:
`service iscsi start`
When this command is executed, the iSCSI init scripts will automatically log into targets where the node.startup setting is configured as automatic. This is the default value of node.startup for all targets.
To prevent automatic login to a target, set node.startup to manual. To do this, run the following command:
`iscsiadm -m node --targetname proper_target_name -p target_IP:port -o update -n node.startup -v manual`
Deleting the entire record will also prevent automatic login. To do this, run:
`iscsiadm -m node --targetname proper_target_name -p target_IP:port -o delete`
To automatically mount a file system from an iSCSI device on the network, add a partition entry for the mount in /etc/fstab with the _netdev option. For example, to automatically mount the iSCSI device sdb to /mount/iscsi during startup, add the following line to /etc/fstab:
`/dev/sdb /mnt/iscsi ext3 _netdev 0 0`
To manually log in to an iSCSI target, use the following command:
`iscsiadm -m node --targetname proper_target_name -p target_IP:port -l`
