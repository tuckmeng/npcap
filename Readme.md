# What this is all about

This are the examples from the Npcap SDK compiled to run on windows. The Npcap SDK is from https://npcap.com which is a standardised packet capture library implementing the pcap API for all platforms. The same feature in Unix is available if you install tcpdump.To try them out, install the npcap installer on Windows and then run the exe files. There are challenges building the files in Windows, so I've created them here. 

# Why Would You Do This
In Linux, it's easy to see what's going on under the hood and on the network, however, the visibility is not really there in Windows. If you can see the stuff coming in on your wifi or network, it'll be so much easier to tell if your machines are getting hit or sending some weird requests. You can actually pipe the data to alert you on the status of your network, be it abnormal bandwidth utilisation on your network or abnormal calls to/from your machines.

# Running the files under Linux

Interestingly if you run the command wine exename.exe on Linux, the exe files actually can pick up the network interface name and prompt you to choose them, but are not able to get them to capture the packets. Believe it's just a dll name referencing issue and you just need a stub windows dll that maps the npcap lib functions to the linux pcap functions. But that's an exercise for another day.

# What The Files Do

The files are as follows:

a. basic_dump.exe - Captures the number of bytes flowing through the network interface.

b. basic_dump_ex.exe - Does the same thing as (a) but using another network interface.

c. pf.exe - Generic Packet Filter where you specify a network source string and a packet filter string, eg pf -s source -o output_file_name -f filter_string -l snaplen .  Read the format of the packet filter from the website. Use doublequotes to specify the filter string. For example pf -s \Device\NPF_{B2205B19A-EA24-4965-A789-EFA330ACA725} -o CON -f "port 53" allows you to see your DNS traffic. Replace the device name in the -s parameter with the one you see in iflist.exe

d. pktdump_ex.exe - Prints the packets from the network , eg pktdump_ex -s \\Device\\NPF_{C8736017-F3C3-4373-94AC-9A34B7DAD998}

e. readfile.exe - Reads the packets from the file, eg readfile filename

f. readfile_ex.exe - Reads the packets from the file using another interface

g. savedump.exe - Dumps the packets from network interface to file in pcap format, eg savedump filename. Remember to rename it as .pcap extension.

h. sendpack.exe - Sends test packets to the network interface

i. udpdump.exe - Captures incoming UDP packets to network interface

# Packet Capture Filter Rule and Viewing Data on the Screen
Packet capture filter rule  examples are the same as wireshark, so read https://gitlab.com/wireshark/wireshark/-/wikis/CaptureFilters or https://www.wireshark.org/docs/wsug_html_chunked/ChCapCaptureFilterSection.html . If you want to view the data on the screen instead of saving it to a file, just use the filename CON. This is a special filename in Windows allowing you to pipe data to the screen for further processing or viewing in real time.

# Compiling the Files
The files are basically in C or C++. I've modified the GNUmakefiles to compile under MINGW-64 in Windows. Although there is a cross-compiler in Linux that produces Windows executables, I've had some problems with the linker linking to invalid files. So I've used the Windows version. I've gotten the windows compiler from https://github.com/skeeto/w64devkit/releases/tag/v1.16.1 from a gentleman Christopher Wellons whose website is here: https://nullprogram.com/tools/ . The website has some interesting articles and other tools which you may be interested to compile and use.
