#What is it ?
netcf is

*a library for configuring network interfaces

*a command line tool (ncftool) to do the same from the command line

*distribution-agnostic and supports multiple distributions and operating systems (well, soon, anyway)

*sets up Ethernet interfaces, bridges, and bonds

Both ​libvirt and ​NetworkManager need this functionality - netcf implements what is common to both of them.

#How does it work ?
The API for netcf accepts an XML description of the overall interface you want. For a simple bridge, this is

`<interface type="bridge" name="br0">`
`  <start mode="onboot"/>`
`  <mtu size="1500"/>`
`  <dhcp/>`
`  <bridge stp="off">`
`    <interface type="ethernet" name="eth0">`
`      <mac address="ab:bb:cc:dd:ee:ff"/>`
`    </interface>`
`  </bridge>`
`</interface>`

A call to ncf_define with the above XML will make the necessary changes to your system's network configuration scripts to set up a bridge br0 with the ethernet interface eth0 enslaved to it.

This goes both ways: you can also retrieve the XML description for any network interface on your system with ncf_if_xml_desc. The important point is that netcf uses your distribution's 'native' network configuration mechanisms directly. That makes it possible to hand-edit those scripts, or modify them with other programs, without confusing netcf.
