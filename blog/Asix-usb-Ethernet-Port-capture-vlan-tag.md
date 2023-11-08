Wireshark is widely used for Ethernet communication development. (My industry is power system and substation automation) I have some projects clearly require supporting the Ethernet packets with & without VLAN tag.  In this case, we need consider the following conditions for validation.  
1. The publisher send the packets with/without VLAN tag  
2. The Ethernet Switch can be setup to keep/remove the VLAN tag  
3. The subscriber may see / not see the VLAN tag depend on the OS and driver configuration.  

Typically wireshark is used as an validation tool. Here is the link from wireshark  
https://wiki.wireshark.org/CaptureSetup/VLAN  

My environment is windows + USB3 Ethernet Adapter (ASIX AX88179), there is an solution from the vendor:  


Please set the "Packet Priority & VLAN" parameter of ASIX USB to LAN Windows drivers to "Packet Priority & VLAN Disable" to capture the VLAN tagged packets on WireShark.

![image](https://user-images.githubusercontent.com/17861461/157847624-49aef5cd-306b-429c-9bac-7a65c0dde9ec.png)
