# CyberDefenders HawkEye Lab – Investigation Report

## Introduction

In this lab, I analysed a network capture file to investigate suspicious activity and identify information related to a malware infection. I used Wireshark to inspect network packets and other analysis tools to investigate files, IP addresses, domains and email activity.

## Investigation Steps

### 1. Finding the total number of packets

I opened the capture file in Wireshark and checked the status bar at the bottom of the window. It displayed the total number of packets in the capture.

### 2. Finding the time of the first packet

I opened **Statistics → Capture File Properties** in Wireshark. I checked the capture information to find the time of the first packet.

### 3. Finding the capture duration

I used **Statistics → Capture File Properties** to check the start and end times of the capture and determine its duration.

### 4. Finding the most active computer

I opened **Statistics → Conversations** and selected the Ethernet tab. I reviewed the conversations and compared the traffic to identify the most active computer.

### 5. Identifying the MAC address manufacturer

I checked the MAC address of the device and used a MAC address lookup service to identify its manufacturer.

### 6. Finding the manufacturer's headquarters

After identifying the manufacturer, I searched for the company online to find the location of its headquarters.

### 7. Finding the number of computers in the organisation

I opened **Statistics → Conversations** and checked the IPv4 tab. I reviewed the internal IP addresses in the network to identify the organisation's computers.

### 8. Finding the most active computer name

I used the Wireshark display filter:

`ip.src == 10.4.10.132 && dns`

I inspected the DNS traffic to identify the computer name associated with the IP address.

### 9. Identifying the DNS server

I inspected DNS request packets and checked their destination IP addresses to identify the DNS server being used.

### 10. Finding the domain requested in packet 204

I selected packet number 204 in Wireshark and inspected its DNS information to find the requested domain name.

### 11. Finding the IP address of the domain

I followed the relevant UDP stream in Wireshark and inspected the DNS communication to identify the IP address associated with the domain.

### 12. Finding the country of the IP address

I used a GeoIP lookup service, such as MaxMind GeoIP, to identify the country associated with the IP address.

### 13. Identifying the victim's operating system

I inspected HTTP traffic and followed the relevant TCP stream. I checked the **User-Agent** information in the HTTP request to identify the operating system.

### 14. Identifying the downloaded malicious file

I used the Wireshark display filter:

`http.request.method == "GET"`

I inspected the HTTP requests to locate the file downloaded from the suspicious website.

### 15. Finding the MD5 hash of the downloaded file

I exported the malicious file from Wireshark by going to **File → Export Objects → HTTP**.

After exporting the file, I opened PowerShell and calculated its MD5 hash using:

`Get-FileHash <filename> -Algorithm MD5`

The MD5 hash was:

`71826ba081e303866ce2a2534491a2f7`

### 16. Identifying the web server software

I inspected the HTTP response headers related to the malicious file download in Wireshark. I checked the **Server** header, which showed that the web server was running **LiteSpeed**.

### 17. Finding the public IP address of the victim's computer

I examined packets where the victim's internal IP address (`10.4.10.132`) communicated with external IP addresses. I opened **packet 3166** and checked the **Line-based text data** field.

The victim's public IP address was:

`173.66.146.112`

### 18. Finding the country of the email server

I used the SMTP display filter in Wireshark to locate email-related traffic. I checked the email server's IP address and used a GeoIP lookup to identify its country.

### 19. Identifying the email server software

I followed the relevant SMTP TCP stream and inspected the server response information to identify the email server software.

### 20. Finding the destination email account

I inspected the SMTP communication and checked the email headers to identify the destination email address used by the malware.

### 21. Finding the password used by the malware to send the email

I inspected the SMTP authentication information in the relevant packet stream. Where the authentication data was Base64 encoded, I decoded it using CyberChef to examine the information.

### 22. Identifying the malware variant

I inspected the relevant SMTP and email data. I used CyberChef to decode the encoded content and examine the information that helped identify the malware variant.

### 23. Finding the Bank of America credentials

I examined the decoded email content to locate the Bank of America credentials mentioned in the captured communication. I kept the credential information private rather than publishing it in this report.

### 24. Finding the interval between data transmissions

I compared the timestamps of the SMTP email packets in Wireshark. By checking the time difference between the messages, I identified the interval between the data transmissions.

## Tools Used

- **Wireshark:** Network traffic and packet analysis.
- **CyberChef:** Decoding encoded data.
- **VirusTotal:** File and malware analysis.
- **Brim:** Network traffic investigation.
- **WHOIS lookup:** Domain and registration information.
- **A-Packets:** Network packet analysis.
- **MaxMind GeoIP:** IP address location lookup.

## Conclusion

This lab helped me practise analysing network traffic, investigating suspicious downloads, examining DNS and SMTP communication, and identifying information related to a malware infection. It also improved my understanding of how network analysis tools can help during a security investigation.
