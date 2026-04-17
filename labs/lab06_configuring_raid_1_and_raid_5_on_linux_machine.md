# Lab 6: Configuring RAID 1 and RAID 5 on a Linux Machine

## Objective
Configure and manage RAID 1 (mirroring) and RAID 5 (striping with parity) arrays on a Linux system. This lab focuses on understanding RAID concepts, disk redundancy, fault tolerance, and storage management.

## Prerequisites
- Kali Linux virtual machine (VMware Player or VirtualBox)
- Root/sudo access
- Basic understanding of Linux disk management
- Familiarity with command-line operations

## Background
RAID (Redundant Array of Independent Disks) provides data redundancy and performance improvements. RAID 1 mirrors data across disks for redundancy, while RAID 5 uses striping with parity for both performance and fault tolerance.

## Part 1: Preparing the Environment

### Step 1: System Setup
Update your Linux distribution:

```bash
sudo apt update && sudo apt upgrade -y
```

### Step 2: Install mdadm
```bash
sudo apt install mdadm -y
```

### Step 3: Examine Current Disks
```bash
lsblk
```

Identify the disks available for RAID (e.g., sdb, sdc, sdd).

### Step 4: Add Disks
Add virtual disks to your VM:
- [VMware Player Guide](https://docs.vmware.com/en/VMware-Workstation-Player-for-Windows/17.0/com.vmware.player.win.using.doc/GUID-FB6F0D1B-6517-4F27-9AB5-93BF834D684D.html)
- [VirtualBox Guide](https://www.techrepublic.com/article/how-to-add-new-drives-to-a-virtualbox-virtual-machine/)

Add at least 3 disks of 500MiB each.

## Part 2: Configuring RAID 1

### Step 1: Create RAID 1 Array
Using two disks (sdb and sdc):
```bash
sudo mdadm --create --verbose /dev/md0 --level=1 --raid-devices=2 /dev/sdb /dev/sdc
```

### Step 2: Format and Mount the RAID Array
```bash
sudo mkfs.ext4 /dev/md0
sudo mkdir /mnt/raid1
sudo mount /dev/md0 /mnt/raid1
```

### Step 3: Update mdadm Configuration
```bash
sudo mdadm --detail --scan | sudo tee -a /etc/mdadm/mdadm.conf
sudo update-initramfs -u
```

**Screenshot Required #1**: Output of `sudo mdadm --detail /dev/md0` showing:
- State: clean
- Active Devices: 2
- Working Devices: 2
- Device table showing both disks as active sync

## Part 3: Configuring RAID 5

### Step 1: Create RAID 5 Array
Using three disks (sdd, sde, sdf):
```bash
sudo mdadm --create --verbose /dev/md1 --level=5 --raid-devices=3 /dev/sdd /dev/sde /dev/sdf
```

### Step 2: Format and Mount the RAID Array
```bash
sudo mkfs.ext4 /dev/md1
sudo mkdir /mnt/raid5
sudo mount /dev/md1 /mnt/raid5
```

## Part 4: Monitoring and Managing RAID Arrays

### Step 1: Testing Fault Tolerance

**Simulate disk failure:**
```bash
sudo mdadm /dev/md0 --fail /dev/sdb
```

**Screenshot Required #2**: Output of `sudo mdadm --detail /dev/md0` after failure showing:
- State: clean, degraded
- Active Devices: 1
- Failed Devices: 1
- Device table showing one disk marked as faulty

**Replace the failed disk:**
```bash
sudo mdadm /dev/md0 --remove /dev/sdb
sudo mdadm /dev/md0 --add /dev/sdb
```

**Screenshot Required #3**: Output of `sudo mdadm --detail /dev/md0` after rebuild showing:
- State: clean
- Active Devices: 2
- Working Devices: 2
- Device table showing both disks as active sync (rebuild complete)

## Deliverables

Submit a **PDF file** containing:

**Required Content:**
1. **Cover Page**: Name, Student ID, Section, Lab Title
2. **Three Required Screenshots** with captions:
   - Screenshot #1: RAID 1 healthy state (`mdadm --detail /dev/md0`)
   - Screenshot #2: RAID 1 degraded state after disk failure
   - Screenshot #3: RAID 1 recovered state after rebuild
3. **Analysis Section** (1-2 pages):
   - Compare RAID 1 vs RAID 5 (redundancy, capacity, performance)
   - Explain what happened during fault tolerance testing and why the array remained operational

**File naming convention**:
`CSCI61-[Section]-[StudentID]-[LastName]-Lab06.pdf`

## Grading

**Total: 100 points**

- RAID 1 configuration and verification (30 points)
- RAID 5 configuration and verification (30 points)
- Fault tolerance testing (25 points)
- Documentation quality and analysis (15 points)

### Deduction Criteria
- Missing required screenshots: -10 points each
- Unclear or unreadable screenshots: -5 points each
- Missing or inadequate analysis section: -10 points
- Incorrect file naming: -5 points
- Incomplete fault tolerance testing: -15 points
- Late submission: As per course policy

## Hints
- Ensure disks are not mounted before creating RAID arrays
- Use `lsblk` frequently to verify disk states
- RAID rebuild can take time; monitor with `cat /proc/mdstat`
- Save your work frequently; VM snapshots are recommended
- Test commands in order; skipping steps may cause failures
- Make sure terminal text is readable in screenshots (adjust font size if needed)
- The three screenshots are the proof that your RAID arrays are working correctly
