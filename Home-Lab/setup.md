# Home Lab Setup Guide

> **Purpose:** Learning environment for IT Security & System Administration  
> **Investment:** ~€700 hardware + ongoing software/services  
> **Status:** ✅ Active & Expanding

---

## 🎯 Goals

**Primary objectives for this home lab:**

1. **Hands-on Learning**
   - Practice system administration
   - Test security tools
   - Break things safely
   - Learn from failures

2. **Certification Preparation**
   - Azure AZ-104 practice environment
   - Linux administration practice
   - Windows Server skills
   - Networking fundamentals

3. **Project Development**
   - NodeWatch21 development
   - Bitcoin node operation
   - Security tool testing
   - Automation scripts

4. **Career Preparation**
   - Portfolio building
   - Real-world experience
   - Interview demonstrations
   - Skill validation

---

## 🖥️ Hardware

### Main Workstation

**Specifications:**
- **Motherboard:** B650 GAMING (AMD)
- **CPU:** AMD Ryzen 5
- **RAM:** 32GB DDR4
- **Storage:** 1TB NVMe SSD
- **GPU:** Integrated graphics
- **OS:** Windows 11 Pro

**Primary uses:**
- Daily work
- VirtualBox/VMware host
- Development environment
- Documentation

**Why these specs:**
- 32GB RAM → Run multiple VMs simultaneously
- Fast NVMe → Quick VM operations
- Ryzen 5 → Good multi-core for VMs
- Windows 11 Pro → Hyper-V support

**Cost:** Existing hardware

---

### MiniPC (Lab Server)

**Specifications:**
- **Model:** [Brand/Model TBD]
- **CPU:** AMD Ryzen 5
- **RAM:** 32GB DDR4
- **Storage:** 2TB NVMe SSD
- **Network:** Gigabit Ethernet
- **Power:** Low power consumption
- **OS:** Ubuntu Server / Windows Server (dual-boot planned)

**Primary uses:**
- Bitcoin full node
- Lightning Network node
- NodeWatch21 development server
- Always-on services
- Testing environment

**Why MiniPC over Raspberry Pi:**
- ✅ 2TB SSD → Full Bitcoin blockchain + space
- ✅ 32GB RAM → Multiple services
- ✅ Future-proof for 5+ years
- ✅ Can run VMs if needed
- ✅ Professional development environment

**Cost:** ~€700

**Purchase Decision:**
- Raspberry Pi: ~€200 (limited, 8GB RAM max)
- MiniPC: ~€700 (powerful, expandable)
- **Chose MiniPC** → Investment in career & learning

---

### Portable Lab

**Kali Purple USB:**
- **Device:** 128GB SanDisk Extreme Go USB 3.2
- **OS:** Kali Purple (Xfce)
- **Purpose:** Portable security lab
- **Cost:** ~€30

**Additional USB Sticks:**
- 5x 32GB SanDisk USB 3.0
- Uses:
  - Kali installer
  - Hiren's Boot CD
  - Other Linux distros
  - Backup tools
- **Cost:** ~€40 (5-pack)

---

### Network Equipment

**Current:**
- Fritz!Box router (ISP provided)
- Gigabit Ethernet
- Wi-Fi 6

**Planned upgrades:**
- Managed switch for VLAN practice
- Dedicated firewall (OPNsense/pfSense)
- Network tap for traffic analysis

---
### Bitcoin Hardware Wallets

**Security Setup:**
- Purpose: Cold storage & backup
- Security: PIN + passphrase protection
- Cost: ~€150 (multiple devices)

*Note: Specific hardware wallet models not disclosed for security reasons*


## 💿 Software & Virtualization

### Hypervisors

**VirtualBox (Primary):**
- **Why:** Free, easy, good for learning
- **Uses:** Most VMs, testing, development
- **VMs:**
  - Ubuntu Server
  - Ubuntu Desktop
  - Linux Mint
  - Kali Linux
  - Windows Server 2022

**VMware Workstation:**
- **Why:** Professional features, better performance
- **Uses:** Complex networking scenarios
- **Note:** Caused network issues on main PC (disabled for now)

---

### Operating Systems

**Linux Distributions:**

**1. Ubuntu Server 24.04 LTS**
- Purpose: Server administration practice
- Uses: Docker host, web servers, databases
- Why: Industry standard, LTS support

**2. Ubuntu Desktop**
- Purpose: Linux desktop experience
- Uses: Daily Linux tasks, learning GUI tools

**3. Linux Mint**
- Purpose: Windows-like Linux experience
- Uses: Easy transition from Windows
- Why chosen: Familiar interface, beginner-friendly

**4. Kali Purple**
- Purpose: Defensive security
- Uses: Blue team tools, SOC practice
- Environment: Both VM and USB

**5. Kali Linux (offensive)**
- Purpose: Pentesting practice (later)
- Uses: Red team tools, CTF challenges

**Windows:**

**1. Windows 11 Pro (Host)**
- Purpose: Main OS, development
- Uses: Everything, Hyper-V

**2. Windows Server 2022 (VM)**
- Purpose: Server administration
- Uses: Active Directory, Group Policy, PowerShell

---

### Development Tools

**IDEs & Editors:**
- Visual Studio Code
- PyCharm (for Python)
- Notepad++

**Version Control:**
- Git
- GitHub Desktop
- GitHub CLI

**Languages:**
- Python (primary)
- PowerShell
- Bash scripting
- JavaScript/Node.js (for NodeWatch21)

---

### Security Tools

**Installed/Available:**
- Kali Purple tool suite (hundreds of tools)
- Wireshark
- Nmap
- Burp Suite
- Metasploit Framework
- John the Ripper
- Hashcat

**Planned:**
- SIEM (Security Information and Event Management)
- IDS/IPS (Intrusion Detection/Prevention)
- Vulnerability scanners

---

### Cloud Platforms

**Azure:**
- Purpose: AZ-104 certification preparation
- Services used:
  - Virtual Machines
  - Storage
  - Networking
  - Sentinel (SIEM)
- Cost: Free tier + student credits

**Cloudflare:**
- Purpose: Website hosting, DNS
- Services:
  - Pages (static hosting)
  - DNS management
  - DDoS protection
- Cost: Free tier

---

### Password Management

**Bitwarden:**
- Purpose: All credentials management
- Why: Open source, secure
- Features:
  - 2FA storage
  - Secure notes
  - Password generator
- Cost: Free (self-host planned)

---

## 🌐 Network Architecture

### Current Setup

```
Internet
    |
Fritz!Box Router
    |
    ├── Main Workstation (Ethernet)
    ├── MiniPC (Ethernet - when setup)
    └── WiFi devices
```

**IP Scheme:**
- Network: 192.168.x.0/24 (standard home network)
- Router: Gateway IP
- DHCP Range: Standard allocation
- Static assignments: Configured for critical services

---

### Planned Improvements

**Future network:**
```
Internet
    |
Firewall (OPNsense)
    |
Managed Switch
    |
    ├── VLAN 10: Management
    ├── VLAN 20: Lab/Testing
    ├── VLAN 30: Production
    └── VLAN 40: IoT/Guest
```

---

## 🔐 Security Measures

### Physical Security
- Lab in locked room
- Hardware wallets in safe
- Backup encryption keys stored separately

### Network Security
- Router firewall enabled
- VPN for remote access (planned)
- Network segmentation (future)
- Guest network isolated

### Access Control
- Bitwarden for password management
- 2FA on all critical accounts
- SSH keys for server access
- Regular password rotation

### Backup Strategy
- **Local backups:** External HDD (weekly)
- **Cloud backups:** Encrypted (monthly)
- **VM snapshots:** Before major changes
- **GitHub:** All documentation & code

---

## 💰 Cost Breakdown

### Initial Investment

| Item | Cost | Notes |
|------|------|-------|
| MiniPC | €700 | Main investment |
| Kali USB (128GB) | €30 | SanDisk Extreme Go |
| USB Sticks (5x 32GB) | €40 | Multi-pack |
| Trezor Safe 3 | €90 | Bitcoin security |
| Tangem Wallet | €60 | Backup wallet |
| **Total Hardware** | **€920** | One-time |

### Ongoing Costs

| Service | Cost | Frequency |
|---------|------|-----------|
| Internet | €40/month | ISP |
| Domain (nodewatch21.io) | €12/year | Cloudflare |
| Electricity (MiniPC) | ~€5/month | Estimate |
| **Total Monthly** | **~€45** | Ongoing |

### Free Tier Services
- Azure (student credits)
- GitHub (public repos)
- Cloudflare Pages (hosting)
- VirtualBox (hypervisor)

---

## 📚 Learning Resources

### Online Platforms
- Microsoft Learn (Azure)
- YouTube (NetworkChuck, John Hammond)
- TryHackMe (hands-on labs)
- HackTheBox (CTF challenges)

### Documentation
- Official docs (Linux, Windows, Azure)
- ArchWiki (excellent technical reference)
- Man pages (Linux commands)
- PowerShell docs

### Communities
- r/homelab
- r/sysadmin
- r/cybersecurity
- Bitcoin/Lightning communities

---

## 🎯 Use Cases

### What I Practice

**System Administration:**
- User management
- Service configuration
- Backup & recovery
- Performance tuning
- Log analysis

**Networking:**
- IP addressing & subnetting
- DNS configuration
- Firewall rules
- VPN setup
- Traffic analysis

**Security:**
- Vulnerability scanning
- Log monitoring
- Incident response
- Hardening systems
- Security policies

**Cloud:**
- Azure resource management
- Infrastructure as Code
- Cost optimization
- Security best practices

**Development:**
- Python scripting
- PowerShell automation
- Web development
- API integration
- CI/CD pipelines

---

## 🚀 Future Expansion Plans

### Short Term (2026)
- [ ] Bitcoin full node on MiniPC
- [ ] Lightning Network node
- [ ] Managed network switch
- [ ] OPNsense firewall
- [ ] Proper VLAN setup

### Medium Term (2027)
- [ ] SIEM implementation
- [ ] IDS/IPS deployment
- [ ] Dedicated backup server
- [ ] Network attached storage (NAS)
- [ ] Dedicated development server

### Long Term (2028+)
- [ ] Small rack setup
- [ ] Enterprise-grade equipment
- [ ] Advanced monitoring
- [ ] High availability setup
- [ ] Professional lab environment

---

## 📊 Lessons Learned

### Hardware Decisions

**✅ What Worked:**
- Investing in MiniPC over Raspberry Pi
- 32GB RAM on both workstation and MiniPC
- 2TB storage for future-proofing
- SanDisk Extreme Go for Kali (fast USB)

**❌ What Didn't Work:**
- VMware causing network issues (disabled)
- USB 2.0 ports for Kali (too slow)
- Trying to run everything on one machine

### Software Decisions

**✅ What Worked:**
- VirtualBox for most VMs
- Linux Mint for easy Linux transition
- Kali Purple for defensive security
- Bitwarden for password management

**❌ What Didn't Work:**
- Too many VMs running simultaneously (RAM)
- Not taking snapshots before changes
- Using Windows Subsystem for Linux instead of full VM

---

## 🎓 Skills Developed

**From this home lab, I've learned:**

**Technical:**
- Linux command line proficiency
- Windows Server administration
- Virtualization management
- Network troubleshooting
- Security tool usage
- PowerShell scripting
- Cloud service deployment

**Soft Skills:**
- Problem-solving under pressure
- Documentation habits
- Time management
- Self-directed learning
- Project planning
- Troubleshooting methodology

---

## 📝 Maintenance Schedule

**Daily:**
- Check running services
- Review logs (when relevant)
- Backup important changes

**Weekly:**
- Update systems (apt update/upgrade)
- Review disk space
- Test backups

**Monthly:**
- Full system updates
- Security audit
- Review resource usage
- Clean up old VMs/snapshots

**Quarterly:**
- Hardware inspection
- Cable management
- Dust cleaning
- Performance review

---

## 🔗 Related Documentation

- [Kali Purple Installation](../Kali-Purple/installation.md)
- [Azure Training Notes](../Azure-Training/)
- [PowerShell Scripts](../PowerShell/)
- [Network Diagrams](./network-diagrams/)

---

**Last Updated:** January 1, 2026  
**Status:** Active & Expanding  
**Next Review:** April 2026 (after Bitcoin node setup)
