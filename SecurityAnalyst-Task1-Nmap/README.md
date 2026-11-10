## Basic Network Scanning with Nmap ##

**Oasis Infobyte - Security Analyst Internship**
_________________________________________________________________


1. Project Overview
___________________

For this task, I used Nmap to scan a local Ubuntu Server virtual machine and identify its open ports and running services.

Nmap (Network Mapper) is an open-source tool used to discover devices and examine open ports and services on a network.

Network scanning is important because it helps identify reachable services, understand network exposure, and find services that may need further security review.

I performed the scans from Kali Linux using Oracle VirtualBox. The purpose was to understand how network scanning works and how to collect basic information about a target machine.

2. Lab Environment
_____________________

______________________________________________
| Component      | Details                   |
|----------------|---------------------------|
| Scanner        | Kali Linux                |
| Target         | Ubuntu Server 26.04.1 LTS |
| Scanner IP     | 192.168.56.101            |
| Target IP      | 192.168.56.104            |
| Nmap Version   | 7.991                     |
| Virtualization | Oracle VirtualBox         |
| Network        | Host-only Adapter         |
----------------------------------------------

Both machines were connected through a private virtual network.

3. Tools Used
_____________

- Kali Linux: Used as the scanning machine.
- Nmap: Used to discover open ports and running services.
- Ubuntu Server: Used as the target machine.
- Oracle VirtualBox: Used to run both virtual machines.

4. Nmap Installation and Verification
_____________________________________

Nmap was already available in my Kali Linux installation, so I first checked that it was installed correctly.

Command:

"nmap --version"

The installed version was 7.991.

If Nmap is not available on another Kali or Debian-based system, it can be installed using:


"sudo apt install nmap"`

5. Scanning Methodology
______________________

5.1 Initial Basic Scan
______________________

I started with a basic scan while SSH was not running on the target.


"nmap 192.168.56.104"

The target was online, but all 1000 scanned TCP ports were closed.

5.2 Basic Scan After Starting SSH
_________________________________

After installing and starting OpenSSH on Ubuntu, I repeated the same scan.

This time, port 22 appeared as open.

5.3 Service Version Detection
_____________________________

I used the following commands to identify the running service and its version:


"nmap -sV -p 22 192.168.56.104"


I also performed a full default service version scan:


"nmap -sV 192.168.56.104"


Both scans identified OpenSSH 10.2p1 Ubuntu 2ubuntu3.8 on port 22.

5.4 Operating System Detection

I attempted to identify the operating system using:


"sudo nmap -O 192.168.56.104"


Nmap did not return an exact operating system match.

The target was known to be Ubuntu Server 26.04.1 from my own lab setup, but the scan itself did not confirm an exact OS match.

6. Results and Findings:
_______________________

The main result was one open TCP port.

| Port | Protocol | State | Service | Version |
|---|---|---|---|---|
| 22 | TCP | Open | SSH | OpenSSH 10.2p1 Ubuntu 2ubuntu3.8 |

The first scan showed no open ports. After starting SSH, port 22 appeared as open.

The other 999 scanned TCP ports were closed.

7. Basic Security Analysis
__________________________

SSH is used for remote access and administration of Linux systems.

An open SSH port is not automatically a security vulnerability, but it should be configured properly.

Some possible risks include weak passwords, unauthorized login attempts, and allowing connections from untrusted devices.

Recommended measures include:

- Using strong authentication or SSH keys.
- Keeping OpenSSH updated.
- Restricting access to trusted devices.
- Monitoring SSH authentication logs.

No exploitable vulnerability was confirmed during this project.

8. Project Files
________________

The project contains the following files:

SecurityAnalyst-Task1-Nmap/
│
├── README.md
├── nmap_scan_results.txt
│
├── evidence/
│   ├── basic_scan.txt
│   ├── basic_scan_after_ssh.txt
│   ├── ssh_version_scan.txt
│   ├── service_version_full.txt
│   └── os_detection.txt
│
└── screenshots/
    ├── basic_scan.png
    ├── basic_scan_after_ssh.png
    ├── ssh_version_scan.png
    ├── service_version_full.png
    ├── os_detection.png
    ├── ssh_installation.png
    └── ssh_service_status.png


9. Ethical Considerations
_________________________

All scans were performed on my own local Ubuntu Server virtual machine.

Network scanning should only be performed on systems that you own or have explicit permission to test.

No external or production systems were scanned.

10. References
______________

- Nmap Official Documentation: https://nmap.org/docs.html
- Nmap Service Version Detection: https://nmap.org/book/man-version-detection.html
- Nmap OS Detection: https://nmap.org/book/man-os-detection.html
- Ubuntu Server Documentation: https://documentation.ubuntu.com/server/
