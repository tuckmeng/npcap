This are the examples from the Npcap SDK compiled to run on windows. The Npcap SDK is from https://npcap.com which is a standardised packet capture library implementing the pcap API for all platforms. To try them out, install the npcap installer on Windows and then run the exe files. There are challenges building the files in Windows, so I've created them here.
The files are as follows:

a. basic_dump.exe - Captures the number of bytes flowing through the network interface.

b. basic_dump_ex.exe - Does the same thing as (a) but using another network interface.

c. pf.exe - Generic Packet Filter where you specify a network source string and a packet filter string, eg pf -s source -o output_file_name -f filter_string -l snaplen .  Read the format of the packet filter from the website.

d. pktdump_ex.exe - Prints the packets from the network , eg pktdump_ex -s \\Device\\NPF_{C8736017-F3C3-4373-94AC-9A34B7DAD998}

e. readfile.exe - Reads the packets from the file, eg readfile filename

f. readfile_ex.exe - Reads the packets from the file using another interface

g. savedump.exe - Dumps the packets from network interface to file in pcap format, eg savedump filename. Remember to rename it as .pcap extension.

h. sendpack.exe - Sends test packets to the network interface

i. udpdump.exe - Captures incoming UDP packets to network interface
