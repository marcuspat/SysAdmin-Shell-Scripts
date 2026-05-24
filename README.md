# System Administration Shell Scripts

Collection of bash shell scripts for common system administration tasks, focusing on disk management, RAID monitoring, and system maintenance.

## 🎯 Overview

This repository contains practical shell scripts used by system administrators for:
- **RAID monitoring and information gathering**
- **Disk partitioning and management**
- **System maintenance automation**
- **Hardware health checks**

## 📁 Contents

### raidinfo.sh
Comprehensive RAID information script that provides detailed status and configuration:
- **RAID array status monitoring** - Check health of all RAID devices
- **Disk information** - Show detailed disk usage and partition data
- **RAID level detection** - Identify RAID 0, 1, 5, 10 configurations
- **Fault tolerance status** - Show degraded or failed arrays
- **Automated reporting** - Generate human-readable status reports

### parted.sh
Disk partitioning automation script:
- **Partition creation** - Automated disk partitioning
- **Filesystem setup** - Create filesystems on new partitions
- **Mount point management** - Automate mount point configuration
- **Disk validation** - Verify disk health before partitioning

## 🚀 Usage

### RAID Information Script
```bash
# Check all RAID arrays
sudo ./raidinfo.sh

# Check specific RAID device
sudo ./raidinfo.sh /dev/md0

# Detailed output with all information
sudo ./raidinfo.sh --verbose

# Check only degraded arrays
sudo ./raidinfo.sh --degraded-only
```

### Partition Script
```bash
# List available disks
sudo ./parted.sh --list-disks

# Create new partition on disk
sudo ./parted.sh --create /dev/sdb

# Create partition with specific size
sudo ./parted.sh --create /dev/sdb --size 100G

# Create filesystem and mount
sudo ./parted.sh --setup /dev/sdb1 /mnt/data
```

## 🔧 Requirements

### System Requirements
- **Linux operating system** (tested on CentOS/RHEL, Ubuntu, Debian)
- **Root/sudo access** required for disk operations
- **mdadm** installed for RAID management
- **parted** utility for partition management

### Installing Dependencies
```bash
# CentOS/RHEL
sudo yum install mdadm parted util-linux

# Ubuntu/Debian
sudo apt-get install mdadm parted util-linux

# Verify installation
mdadm --version
parted --version
```

## 📋 Script Features

### raidinfo.sh Features
- **Auto-detection**: Finds all RAID devices automatically
- **Health monitoring**: Checks array status and identifies issues
- **Detailed information**: Shows RAID level, devices, and status
- **Error reporting**: Highlights degraded or failed arrays
- **Log generation**: Creates timestamped reports

### parted.sh Features
- **Safe operations**: Validates inputs before making changes
- **Interactive mode**: Confirms dangerous operations
- **Partition alignment**: Ensures proper partition alignment
- **Filesystem support**: Supports ext4, xfs, btrfs
- **Mount management**: Handles fstab updates

## 🛠️ Examples

### Check RAID Health
```bash
# Quick health check
sudo ./raidinfo.sh

# Detailed RAID information
sudo ./raidinfo.sh | grep -E "Status|Level|Devices"

# Monitor RAID status (watch mode)
watch -n 5 'sudo ./raidinfo.sh'
```

### Disk Partitioning
```bash
# Create new data partition
sudo ./parted.sh --create /dev/sdb --size 500G
sudo mkfs.ext4 /dev/sdb1
sudo mkdir /mnt/data
sudo mount /dev/sdb1 /mnt/data

# Add to fstab for persistence
echo "/dev/sdb1 /mnt/data ext4 defaults 0 0" | sudo tee -a /etc/fstab
```

### System Maintenance
```bash
# Check all disk health
sudo ./raidinfo.sh
df -h
lsblk

# Partition new storage drive
sudo ./parted.sh --list-disks
sudo ./parted.sh --create /dev/sdc
```

## ⚠️ Safety Notes

### Important Warnings
- **Always backup data** before partitioning or modifying RAID
- **Test scripts** in non-production environments first
- **Use with caution** - these scripts modify disk configurations
- **Review script contents** before running on production systems

### Risk Mitigation
- Scripts include confirmation prompts for destructive operations
- Read operations are safe and can be run without concern
- Write operations should be tested on non-critical systems first

## 🔍 Troubleshooting

### Common Issues

**Permission Denied**
```bash
# Solution: Run with sudo
sudo ./raidinfo.sh
```

**mdadm Not Found**
```bash
# Solution: Install mdadm
sudo apt-get install mdadm  # Ubuntu/Debian
sudo yum install mdadm      # CentOS/RHEL
```

**RAID Shows Degraded**
```bash
# Solution: Check RAID status and replace failed drives
sudo ./raidinfo.sh --degraded-only
cat /proc/mdstat
```

## 📚 Related Resources

- **Misc_Ansible_Playbooks**: Ansible automation for system administration
- **dns-bash-scripts**: DNS management shell scripts
- **aws_python_sdk**: AWS infrastructure scripts

## 🤝 Contributing

Contributions welcome! Please:
1. Test scripts thoroughly before submitting
2. Include error handling and validation
3. Add usage examples for new features
4. Document any system requirements

## 📝 License

System administration utilities - Free to use and modify.

---

**System Administration Shell Scripts** - Simplifying RAID management and disk maintenance with reliable automation.
