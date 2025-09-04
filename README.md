# Home Security Operations Center (SOC) Lab

## Overview
This repository documents a **Home Security Operations Center (SOC) Lab**, a virtualized environment built to simulate enterprise-grade cybersecurity operations. The lab enables hands-on practice in threat detection, incident response, network monitoring, and defensive techniques using free and open-source tools. It replicates a professional SOC setup, including log collection, SIEM, endpoint monitoring, and simulated attacks, making it ideal for cybersecurity enthusiasts and aspiring SOC analysts.

## Objectives
- Simulate realistic network traffic and cyber attacks.
- Collect, aggregate, and analyze security logs.
- Detect and respond to incidents using industry-standard tools.
- Develop practical skills in cybersecurity operations.

## Lab Architecture
The lab is built on a virtualized network using VirtualBox, with the following components:
- **pfSense Firewall**: Manages network segmentation and routing (NAT, Internal, optional DMZ).
- **Windows Server 2022**: Hosts Active Directory for a domain environment (e.g., lab.local).
- **Windows 10/11 Endpoint**: Simulates user systems, joined to the domain, with Sysmon for monitoring.
- **Ubuntu Server**: Runs the ELK Stack (Elasticsearch, Logstash, Kibana) or Splunk for SIEM capabilities.
- **Kali Linux**: Acts as the attacker system for simulating threats.

### Network Topology

[Internet] <--> [pfSense (NAT + LAN)] <--> [Internal Network]
|
+--> [Ubuntu SIEM (192.168.1.10)]
+--> [Windows Server (192.168.1.20)]
+--> [Windows Endpoint]
+--> [Kali Attacker (Isolated)]

- **LAN**: 192.168.1.0/24 (pfSense LAN IP: 192.168.1.1).
- **Isolation**: Internal network ensures lab traffic is contained.

## Setup Instructions
### Prerequisites
- **Hardware**: 16+ GB RAM, multi-core CPU with virtualization support, 500+ GB SSD.
- **Software**: VirtualBox, ISOs for pfSense, Ubuntu Server, Windows Server 2022, Windows 10/11, Kali Linux.
- **Skills**: Basic networking, VM management, command-line familiarity.

### Installation Steps
1. **Virtualization Setup**:
   - Install VirtualBox and create NAT and Internal networks.
2. **pfSense Firewall**:
   - VM: 2-4 GB RAM, 2 CPUs, 20 GB disk.
   - Configure WAN (NAT) and LAN (192.168.1.1/24).
   - Enable DHCP and basic firewall rules.
3. **Windows Server (Active Directory)**:
   - VM: 4 GB RAM, 60 GB disk.
   - Install Windows Server 2022, promote to Domain Controller (lab.local).
   - Use BadBlood script to populate with users/groups.
4. **Windows Endpoint**:
   - VM: 4-8 GB RAM, 50 GB disk.
   - Join domain, install Sysmon with a modular config.
5. **Ubuntu SIEM**:
   - VM: 8 GB RAM, 100 GB disk.
   - Install ELK Stack or Splunk, configure log forwarding (Winlogbeat, Filebeat).
   - Access Kibana at `http://192.168.1.10:5601`.
6. **Kali Linux**:
   - VM: 4 GB RAM, 40 GB disk.
   - Install Metasploit, Sliver, and other attack tools.

### Tool Configurations
- **Log Forwarding**: Winlogbeat (Windows) and Filebeat (Linux) to SIEM.
- **Network Monitoring**: Snort on pfSense or Ubuntu for IDS/IPS.
- **EDR**: Wazuh or LimaCharlie on endpoints.
- **Dashboards**: Create SIEM visualizations for processes, network activity, and alerts.
- **Detection Rules**: Set rules for LSASS access, ransomware behaviors (e.g., shadow copy deletion).

## Simulated Scenarios
Practice the following to build SOC skills:
1. **Malware Execution**:
   - Generate payload with `msfvenom` on Kali, execute on Windows.
   - Monitor in SIEM for malicious processes.
2. **Command and Control (C2)**:
   - Use Sliver to establish a session, run commands.
   - Detect via EDR/SIEM telemetry.
3. **Credential Dumping**:
   - Simulate LSASS access, trigger SIEM alerts.
4. **Vulnerability Scanning**:
   - Run `nmap -sV` from Kali, analyze results.
5. **Incident Response**:
   - Use TheHive to document and respond to incidents.

**Tip**: Take VM snapshots before simulations for easy rollback.

## Best Practices
- **Isolation**: Keep lab network isolated from production networks.
- **Snapshots**: Save VM states regularly.
- **Updates**: Keep tools and VMs updated.
- **Documentation**: Log configurations and findings.

## Troubleshooting
- **Network Issues**: Verify IPs, gateways, and firewall rules.
- **SIEM Failures**: Check log forwarder configs and open ports (e.g., 514 for syslog).
- **Performance**: Allocate sufficient RAM/CPU, use SSD storage.

## Resources
- **Guides**: [LetsDefend](https://letsdefend.io/), Elastic documentation.
- **Repos**: [SOC-Home-Lab-Attack-Defense-Simulation](https://github.com/xAHIINX00/SOC-Home-Lab-Attack-Defense-Simulation), [SOC_Home_Lab](https://github.com/soriesesay1/SOC_Home_Lab).
- **Communities**: r/homelab, cybersecurity forums.

## License
This project is for educational purposes and uses open-source tools under their respective licenses.
