# Kali Purple USB Installation Guide

> **Date:** December 31, 2025 - January 1, 2026  
> **Hardware:** 128GB SanDisk Extreme Go USB 3.2  
> **Desktop Environment:** Xfce (for performance on USB)  
> **Status:** ✅ Successfully completed

---

## 📋 Overview

This guide documents the complete installation of Kali Purple on a USB drive for a portable security lab. Includes all troubleshooting steps, BIOS configurations, and lessons learned.

---

## 🎯 Goal

Create a bootable, persistent Kali Purple installation on USB that can:
- Boot on any PC
- Save changes permanently
- Include all defensive security tools
- Be portable for on-site work

---

## 🛠️ Hardware Requirements

### What I Used:

**USB Drives:**
- **Target USB:** 128GB SanDisk Extreme Go USB 3.2 (for Kali Purple system)
- **Installer USB:** 32GB SanDisk USB 3.0 (for the installer only)

**PC Specs:**
- **Motherboard:** B650 GAMING (AMD)
- **CPU:** AMD Ryzen 5
- **RAM:** 32GB DDR4
- **BIOS Mode:** CSM/UEFI compatible

**Why Two USB Sticks?**
- First attempt with one USB failed (kernel panic when booting from same USB being installed to)
- Solution: Use separate installer USB and target USB

---

## 📥 Download & Preparation

### 1. Download Kali Purple Installer

**Source:** https://www.kali.org/get-kali/

**Which Image:**
- Installer Images → **Kali Purple Installer**
- NOT the Live image!
- File: `kali-linux-2024.X-installer-purple-amd64.iso`

### 2. Create Bootable Installer USB

**Tool:** Rufus (https://rufus.ie)

**Settings:**
```
Device: 32GB USB (installer stick)
Boot selection: kali-linux-xxx-installer-purple-amd64.iso
Partition scheme: MBR
Target system: BIOS or UEFI
File system: FAT32
```

**IMPORTANT:** Use "DD Image mode" when Rufus asks!

---

## 🔧 Installation Process

### Step 1: BIOS Configuration

**Access BIOS:**
- Restart PC
- Press **Del** or **F2** during boot
- Enter BIOS Setup

**Settings to Check/Change:**

1. **Boot Mode:**
   - Set to **CSM** (Compatibility Support Module)
   - OR: CSM/UEFI Mixed mode
   - Pure UEFI may cause issues with USB boot

2. **Secure Boot:**
   - **Disable** Secure Boot
   - Required for Linux USB boot

3. **Boot Priority:**
   - USB drive first
   - Or use Boot Menu (F11/F12) during startup

**Save & Exit BIOS**

---

### Step 2: Boot from Installer USB

**Hardware Setup:**
1. Insert **32GB installer USB**
2. Insert **128GB target USB** (where Kali will be installed)
3. Restart PC
4. Press **F11** or **F12** for Boot Menu
5. Select the **32GB USB** (installer)

**Kali Installer Starts!** ✅

---

### Step 3: Installation Wizard

#### 3.1 Welcome Screen
- Select: **Graphical Install**

#### 3.2 Language & Location
- Language: English
- Location: Germany (or your country)
- Keyboard: German (or your layout)

#### 3.3 Network Configuration
- Hostname: `kali-purple`
- Domain name: Leave blank (remove fritz.box if pre-filled)

#### 3.4 User Account
- Full name: Your name
- Username: `mrthirteen` (or your preferred username)
- Password: [Strong password - write it down!]

#### 3.5 Partition Disks - CRITICAL!

**⚠️ VERY IMPORTANT - Choose the RIGHT disk!**

**Partitioning method:**
- Select: **Guided - use entire disk**

**Select disk to partition:**
- **IMPORTANT:** Choose the **128GB USB** (SCSI device, usually `/dev/sdb`)
- **NOT** your internal SSD/HDD!
- Look at size: ~129.2 GB = your USB stick

**Partition scheme:**
- Select: **All files in one partition (recommended for new users)**

**Partitions will be:**
- 1 GB - EFI System Partition (ESP)
- ~121 GB - Root partition (/) - ext4
- ~7 GB - Swap area

**Confirm:** Write changes to disk? → **Yes**

**⚡ Installation starts - takes 1-2 hours!**

---

### Step 4: Software Selection

**Desktop Environment:**
- Select: **Xfce** (recommended for USB - lightweight!)
- Deselect: GNOME (too heavy for USB)

**Kali Purple Tools:**
- Keep all checked ✅
- Includes: NIST CSF domains (Identify, Protect, Detect, Respond, Recover)

**Major packages installed:**
- Defensive security tools
- Ghidra, Metasploit, Wireshark
- Python3, Wine, ZAP
- And many more...

**⏱️ This takes time - be patient!**

---

### Step 5: GRUB Bootloader

**Install GRUB to:** Automatic (installer chooses `/dev/sdb`)

**⚠️ GRUB installation may appear frozen for 10+ minutes - this is NORMAL!**
- Don't panic
- Don't force-restart
- Just wait!

**When done:** Installation complete!

---

### Step 6: First Boot

**Hardware changes:**
1. **Remove** the 32GB installer USB
2. **Keep** the 128GB Kali USB plugged in
3. Restart PC

**Boot sequence:**
- If USB not visible in BIOS → Change to CSM mode
- Set 128GB USB as first boot device
- Boot!

**🎉 Kali Purple desktop appears!**

---

## 🚨 Troubleshooting

### Issue 1: Kernel Panic on Boot

**Problem:**
- Trying to boot from the same USB being installed to
- Error: "Kernel panic - not syncing"

**Solution:**
- Use TWO USB sticks:
  - 32GB for installer
  - 128GB for Kali system
- Boot from installer USB, install to target USB

---

### Issue 2: USB Not Visible in BIOS

**Problem:**
- BIOS doesn't show USB drive in boot options

**Solution:**
- Change BIOS mode from UEFI to **CSM**
- Or use CSM/UEFI mixed mode
- USB should appear as "USB Hard Disk: SanDisk"

---

### Issue 3: GRUB Installation Freezes

**Problem:**
- GRUB installation appears stuck for 10+ minutes

**Solution:**
- **WAIT!** This is normal for USB installations
- Do NOT force restart
- It WILL complete eventually

---

### Issue 4: "Reboot and Select Proper Boot Device"

**Problem:**
- After installation, system won't boot from USB

**Solution:**
1. Check BIOS boot priority
2. Ensure CSM mode is enabled
3. Try different USB port (USB 3.0 vs 2.0)
4. May need to reinstall GRUB manually

---

## ✅ Post-Installation

### First Login

**Credentials:**
- Username: `max` (or what you set)
- Password: [your password]

### Initial Setup

**1. Update system:**
```bash
sudo apt update
sudo apt upgrade -y
```

**2. Install Timeshift (for snapshots):**
```bash
sudo apt install timeshift
```

**3. Create first snapshot:**
```bash
sudo timeshift --create --comments "Fresh install"
```

---

## 🎨 Customization

### Enable Dark Mode

**Settings → Appearance → Style:**
- Select: **Kali-Dark** or **Adwaita-dark**

**Terminal dark mode:**
- Terminal → Edit → Preferences → Colors
- Select dark color scheme

---

## 📊 Performance Notes

### USB Speed Considerations

**USB 3.0/3.2 Performance:**
- Read: ~400 MB/s
- Write: ~300 MB/s
- **Much slower than internal SSD!**

**Expected behavior:**
- First program launch: Slow (10-20 seconds)
- After caching: Faster
- Large programs (Firefox, Burp): Always slower

**Tips:**
- Use lightweight apps when possible
- Let programs cache in RAM
- Be patient on first boot

---

## 💾 Backup Strategy

### Image Backup (Golden Image)

**Attempted with:**
- Win32 Disk Imager → Failed (CRC errors)
- USB Image Tool → Failed (CRC errors)

**Note:** USB stick had defective sectors that prevented full image backup. System works fine for booting/using, but backup failed.

**Alternative:** Use Timeshift within Kali for system snapshots

### Timeshift Snapshots

**Setup:**
```bash
sudo apt install timeshift
sudo timeshift --create
```

**Snapshot strategy:**
- Keep 5 snapshots maximum
- Create before major changes
- Automatic cleanup of old snapshots

---

## 📝 Lessons Learned

### What Worked

✅ Two USB stick method (separate installer and target)
✅ CSM boot mode instead of pure UEFI
✅ Xfce desktop for better USB performance
✅ Patience during GRUB installation
✅ Using blue USB 3.0 ports for better speed

### What Didn't Work

❌ Single USB stick installation (kernel panic)
❌ Pure UEFI mode (USB not recognized)
❌ External image backup (CRC errors)
❌ Front panel USB 2.0 ports (too slow)

### Best Practices

**For future installations:**
1. Always use two USB sticks
2. Enable CSM in BIOS
3. Disable Secure Boot
4. Choose Xfce for lightweight desktop
5. Use rear USB 3.0 ports for better performance
6. Don't panic during GRUB installation
7. Create Timeshift snapshots instead of external images

---

## 🎯 Use Cases

**What this USB is for:**
- Portable pentesting lab
- Security assessments on-site
- Learning defensive security
- Testing in different environments
- Forensics work
- Emergency recovery tool

**What it's NOT for:**
- Daily driver (too slow)
- Production work
- Gaming
- Heavy development (use VM instead)

---

## 🔗 Resources

**Official Documentation:**
- https://www.kali.org/docs/installation/hard-disk-install/
- https://www.kali.org/docs/usb/kali-linux-live-usb-install/

**Tools Used:**
- Rufus: https://rufus.ie
- Kali Linux: https://www.kali.org

**Community:**
- Kali Forums: https://forums.kali.org
- r/Kali on Reddit

---

## 📅 Timeline

**Total time:** ~3 hours

**Breakdown:**
- Download ISO: 30 min
- Create installer USB: 10 min
- BIOS configuration: 10 min
- Installation: 2 hours
- First boot & testing: 30 min
- Troubleshooting: Additional time

---

## ✨ Final Thoughts

Despite the challenges (two-USB requirement, slow speeds, backup issues), having a portable Kali Purple system is incredibly valuable for learning and real-world security work. The persistence means all changes, tools, and configurations are saved - making it a true portable security lab.

**Worth it?** Absolutely! 💪

---

**Last Updated:** January 1, 2025  
**Author:** Michael (mrthirteen)  
**Status:** Complete & Working ✅
