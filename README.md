# PCPPReader

EXCERCISE
We would like you to develop a small command line software that will allow to filter/convert pcap files. 
Technologies
The software must be developed using the following technologies:
 - C++ language. You can use any version (we are using C++11)
 - PcapPlusPlus library (we are using latest stable)
Platform
The software must run on the following platform specs:
 - GNU/Linux x86_64. You can use any flavor/version (we are using Ubuntu Server 18.04)
 - Since software operates on files, you can use either real HW or a virtualized/dockerized environment
Description
The software must read packets from an input pcap file, and create and output pcap file. For each input 
packet, the following rules must be followed before writting it to the output file.
1. If packet comes from a different VLAN ID than the one specified by --vlan option, it must be 
dropped
2. If packet DataLink layer protocol is not ETHERNET, it must be dropped
3. If packet Network layer protocol doesn't match the one specified by --ip-version option (IPv4 or 
IPv6), it must be dropped
4. If packet Network layer protocol is IPv4 or IPv6, TTL must be decreased by the amount specified by
--ttl option. If TTL is lower or equal than the option, packet must be dropped
5. If packet Transport layer protocol is ICMP, it must be dropped
6. If packet Transport layer protocol is UDP, and contains a DNS layer, the server address and port 
fields must be replaced by --dns-addr and --dns-port options
Input
- Required parameters:
 -i: path of the input pcap file 
 -o: path of the input pcap file
- Optional parameters:
 --vlan: Value to be used for rule #1
 --ip-version: Value to be used for rule #3
 --ttl: Value to be used for rule #4
 --dns-addr: Value to be used for rule #6
 --dns-port: Value to be used for rule #6
Output
- The software must write the output file in the path specified, even if it contains zero packets.
- It also must display the following packet stats in the standard output:
 - Total bytes & packets processed
 - Total bytes & packets dropped
 - Total bytes & packets written
 - Total DNS packets modified
Considerations
- There is no need to validate the provided options (is outside of the scope of the exercise)
- If an option is not present, then the corresponding rule should not be applied
- Output pcap file should be valid and readable in Wireshark without displaying errors of any kind
Example usage
Consider the following command
pcap-convert --vlan 5 -ip-version 4 --ttl 2 --dns-addr 10.0.0.1 --dns-port 5353 -i input.pcap -o output.pcap
This will result in output.pcap containing only packets from input.pcap that are tagged as vlan 5, contain 
IPv4 layer with ttl>2 and contain no ICMP layer. All written packets will have TTL decreased by 2, and DNS
packets will have the server address and port replaced by 10.0.0.1:5353
PcapPlusPlus resources
• Github repository
• Homepage
• Docs
• Tutorials
• Examples
PcapPlusPlus example code to use as base for the exercise
• Example of pcap file reading/writting
• Example of reading command line arguments
