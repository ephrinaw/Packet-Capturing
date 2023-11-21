# Packet-Capturing



As a security analyst, it’s important to know how to capture and filter network traffic in a Linux environment using tools such as TCPDUMP. Also needs to know the basic concepts associated with network interfaces. Below we’ll perform tasks associated with using tcpdump to capture network traffic data in a packet capture (p-cap) file and then examine the contents of the captured packet data to focus on specific types of traffic.<br>
Installation : <br>
![image](https://github.com/ephrinaw/Packet-Capturing/assets/39829776/791fb2ba-f93d-40ff-8ca2-c9990e77797c)

 
Use ifconfig to identify the interfaces that are available:
![image](https://github.com/ephrinaw/Packet-Capturing/assets/39829776/52d9722d-471d-4376-acfd-d0101c144616)

sudo tcpdump -D command identify the interface options available for packet capture.
This may be useful on systems that do not include the ifconfig command.
![image](https://github.com/ephrinaw/Packet-Capturing/assets/39829776/38040623-f4d3-491f-828b-dd95e8eb1a11)
 

Filter live network packet data from the eth0 interface with tcpdump:
sudo tcpdump -i eth0 -v -c5
This command will run tcpdump with the following options:<br>
•	-i eth0: Capture data specifically from the eth0 interface.<br>
•	-v: Display detailed packet data.<br>
•	-c5: Capture 5 packets of data.
![image](https://github.com/ephrinaw/Packet-Capturing/assets/39829776/63631ab6-02d4-4a8c-9f5d-4ccf18a41a2f)
 
Capture packet data into a file called capture.pcap:
sudo tcpdump -i eth0 -nn -c9 port 80 -w capture.pcap &
This command will run tcpdump in the background with the following options:
•	-i eth0: Capture data from the eth0 interface.<br>
•	-nn: Do not attempt to resolve IP addresses or ports to names. This is best practice from a security perspective, as the lookup data may not be valid. It also prevents malicious actors from being alerted to an investigation.<br>
•	-c9: Capture 9 packets of data and then exit.<br>
•	port 80: Filter only port 80 traffic. This is the default HTTP port.<br>
•	-w capture.pcap: Save the captured data to the named file.<br>
•	&: This is an instruction to the Bash shell to run the command in the background.
![image](https://github.com/ephrinaw/Packet-Capturing/assets/39829776/f217a01f-c42a-4021-ae83-169b0db1413a)

 

Using curl to generate some HTTP (port 80) traffic:
curl opensource.google.com
When the curl command is used like this to open a website, it generates some HTTP (TCP port 80) traffic that can be captured.
![image](https://github.com/ephrinaw/Packet-Capturing/assets/39829776/05d08454-293e-4bc2-ae60-a20b733ea07a)
 
Verify that packet data has been captured:
![image](https://github.com/ephrinaw/Packet-Capturing/assets/39829776/6d0dacb8-716c-4f3a-ab56-b363136662af)
 
Use the tcpdump command to filter the packet header data from the capture.pcap:
sudo tcpdump -nn -r capture.pcap -v
This command will run tcpdump with the following options:<br>
•	-nn: Disable port and protocol name lookup.<br>
•	-r: Read capture data from the named file.<br>
•	-v: Display detailed packet data.
![image](https://github.com/ephrinaw/Packet-Capturing/assets/39829776/1f46202d-fbd4-4bf5-b429-4b0dfa105216)
 
Use the tcpdump command to filter the extended packet data from the capture.pcap  file:
sudo tcpdump -nn -r capture.pcap -X
This command will run tcpdump with the following options:<br>
•	-nn: Disable port and protocol name lookup.<br>
•	-r: Read capture data from the named file.<br>
•	-X: Display the hexadecimal and ASCII output format packet data. We can analyze hexadecimal and ASCII output to detect patterns or anomalies during malware analysis or forensic analysis.
![image](https://github.com/ephrinaw/Packet-Capturing/assets/39829776/c7d92410-b559-432d-8672-b7f5130989fd)

 









