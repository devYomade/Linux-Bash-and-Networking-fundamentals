# Task:
- Review the CIS benchmark for ubuntu, and try to implement at least 10 of the recommendations that we made within the benchmark.

# Instructions:
- N/A

# Steps Taken:

## To ensure permissions on /etc/passwd are configured, meaning that the /etc/passwd file is protected from unauthorized write access.
- I ran the following command to verify `uid` and `gid` are booth `0/root` and `Access` is `644`:
<br>

![stat 1](https://user-images.githubusercontent.com/105651785/192492750-42467ac1-9936-4c4a-a3da-09ef96d08ccf.png)
## Ensure permissions on /etc/passwd- are configured (Automated)
- It is critical to ensure that the /etc/passwd- file is protected from unauthorized access. 
Although it is protected by default, the file permissions could be changed either 
inadvertently or through malicious actions.
- So i ran the command `stat /etc/passwd-` to make sure that `uid` and `gid` are booth `0/root` and Access is `644 or more ristrictive.
<br>

![stat 2](https://user-images.githubusercontent.com/105651785/192494841-b724bfc4-6c42-4220-9e4f-ef2a0f9651eb.png)
##  Ensure default group for the root account is GID 0 (Automated)
-The usermod command can be used to specify which group the root user belongs to. This 
affects permissions of files that are created by the root user.
- Using GID 0 for the root account helps prevent root -owned files from accidentally 
becoming accessible to non-privileged users.
- So i ran the command `grep "^root:" /etc/passwd | cut -f4 -d:` to verify the result is 0.
<br> 

![stat 3](https://user-images.githubusercontent.com/105651785/192497032-1f1f4838-4284-4b28-b90a-dd91853cffe8.png)
##  Disable Automounting (Automated)
- autofs allows automatic mounting of devices, typically including CD/DVDs and USB drives.
- So i ran the following command to make sure it is not installed ` dpkg -s autofs` 
<br>

![stat 4](https://user-images.githubusercontent.com/105651785/192502971-b2cad7cc-4864-4050-9254-1412f46fa577.png)
## Ensure Avahi Server is not installed (Automated)
- Avahi is a free zeroconf implementation, including a system for multicast DNS/DNS-SD 
service discovery. Avahi allows programs to publish and discover services and hosts 
running on a local network with no specific configuration. For example, a user can plug a 
computer into a network and Avahi automatically finds printers to print to, files to look at 
and people to talk to, as well as network services running on the machine.
- Avahi is a free zeroconf implementation, including a system for multicast DNS/DNS-SD 
service discovery. Avahi allows programs to publish and discover services and hosts 
running on a local network with no specific configuration. For example, a user can plug a 
computer into a network and Avahi automatically finds printers to print to, files to look at 
and people to talk to, as well as network services running on the machine.
- So i ran the following command to verify `avahi-daemon` is not installed ` dpkg -s avahi-daemon | grep -E '(Status:|not installed)'`
<br>

![Stat 5](https://user-images.githubusercontent.com/105651785/192512668-ed76fa9e-bff0-4e09-8edd-4226bb9057de.png).
## Ensure CUPS is not installed (Automated)
-The Common Unix Print System (CUPS) provides the ability to print to both local and 
network printers. A system running CUPS can also accept print jobs from remote systems 
and print them to local printers. It also provides a web based remote administration 
capability.
- If the system does not need to print jobs or accept print jobs from other systems, it is 
recommended that CUPS be removed to reduce the potential attack surface.
- So i ran the command the following command  to verify `cups` is not Installed:  `dpkg -s cups | grep -E '(Status:|not installed)'`
<br>

![Stat 6](https://user-images.githubusercontent.com/105651785/192515442-b1a7d183-b82c-41d2-863b-319c0f1eaa48.png)
##  Ensure DHCP Server is not installed (Automated)
-  The Dynamic Host Configuration Protocol (DHCP) is a service that allows machines to be 
dynamically assigned IP addresses.
- Unless a system is specifically set up to act as a DHCP server, it is recommended that this 
package be removed to reduce the potential attack surface.
- So i ran the following command  to verify `isc-dhcp-server` is not installed:  `dpkg -s isc-dhcp-server | grep -E '(Status:|not installed)'`
<br>

![stat 7](https://user-images.githubusercontent.com/105651785/192518204-9b77d897-a4dc-4781-8d30-cd2d03aadad0.png)
## Ensure TCP SYN Cookies is enabled (Automated)
- When tcp_syncookies is set, the kernel will handle TCP SYN packets normally until the 
half-open connection queue is full, at which time, the SYN cookie functionality kicks in. SYN 
cookies work by not using the SYN queue at all. Instead, the kernel simply replies to the 
SYN with a SYN|ACK, but will include a specially crafted TCP sequence number that 
encodes the source and destination IP address and port number and the time the packet 
was sent. A legitimate connection would send the ACK packet of the three way handshake 
with the specially crafted sequence number. This allows the system to verify that it has 
received a valid response to a SYN cookie and allow the connection, even though there is no 
corresponding SYN in the queue.
- Attackers use SYN flood attacks to perform a denial of service attacked on a system by 
sending many SYN packets without completing the three way handshake. This will quickly 
use up slots in the kernel's half-open connection queue and prevent legitimate connections 
from succeeding. SYN cookies allow the system to keep accepting valid connections, even if 
under a denial of service attack.
- So i ran the following command to verify .
<br>

![stat 8](https://user-images.githubusercontent.com/105651785/192531861-e685c8f5-e3c5-40fe-a946-be9c07ca6e45.png)
## Ensure rsyslog is installed (Automated).
- The rsyslog software is a recommended replacement to the original syslogd daemon 
which provide improvements over syslogd, such as connection-oriented (i.e. TCP) 
transmission of logs, the option to log to database formats, and the encryption of log data 
en route to a central logging server.
- The security enhancements of rsyslog such as connection-oriented (i.e. TCP) transmission 
of logs, the option to log to database formats, and the encryption of log data en route to a 
central logging server) justify installing and configuring the package.
- So i ran the following command to Verify either `rsyslog` or `syslog-ng` is installed: ` dpkg -s rsyslog`
<br>

![stat 9](https://user-images.githubusercontent.com/105651785/192533030-71ba4813-6b9f-4e39-82f2-1bc85ed4ef09.png)
## Ensure rsyslog Service is enabled (Automated)
- Once the rsyslog package is installed it needs to be activated.
- If the rsyslog service is not activated the system may default to the syslogd service or lack 
logging instead.
- So i ran the following command to  verify `rsyslog` is enabled:  `systemctl is-enabled rsylog`
<br>

![stat 10](https://user-images.githubusercontent.com/105651785/192534196-68480d4c-2094-464c-9785-bb72a3ff6a9a.png)





