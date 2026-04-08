SECTION 1: Installing Debian 13 with LVM and Disk Encryption
1.1 Installation Process
To carry out the installation process of the Debian 13 Virtual Machine (VM) in this project, the Oracle VirtualBox application was used.

Initial Setup and VM Creation
ISO Acquisition: The first step involved downloading the Debian 13 ISO, specifically the netinst.iso version.

VM Configuration: The VM was created by defining the name, location, ISO image, and operating system details.

Resource Allocation: Specific hardware resources (CPU, RAM) were assigned to ensure optimal performance.

System Summary: A final review of the debian-C2 VM configuration was performed before launching the installer.

Installation Steps
Network and Hostname: Configuration of the network settings and system hostname to identify the VM within the local network.

User Accounts: Setup of administrative (root) and user accounts, implementing strong password policies from the start.

Partitioning Method: Selection of the Guided Partitioning method using the entire disk with Encrypted LVM for maximum security.

Logical Volume Structure: Final review of the structure, including separate partitions for root, home, and swap.

Encryption: Creation of the LUKS encryption passphrase to protect data at the disk level.

Package Management: Configuration of the APT package manager and selection of a local mirror for efficient updates.

Desktop Environment: Selection of GNOME and essential system utilities.

Bootloader: Installation of the GRUB bootloader on the primary drive.

Verification and System Commands
Upon the first boot, the system requires the LUKS passphrase to unlock the encrypted partition. The following commands were used to verify the system structure:

lsblk: Lists information about all available block devices.

pvs: Displays information about the Physical Volumes.

vgs: Provides volume group information, displaying one line per group.

lvs: Shows logical volume information.

cryptsetup status: Reports the current status of an active encrypted device.

1.2 Research Questions
1. What is LUKS and how does it relate to dm-crypt?
LUKS (Linux Unified Key Setup) is a standard for block device encryption that defines how encrypted data is stored and how access keys are managed. Its main objective is to provide a secure and standardized way to protect disks, allowing multiple passwords and robust key management.

Relationship: LUKS acts as a management layer over dm-crypt, which is the Linux kernel component responsible for the actual encryption and decryption. The device mapper infrastructure allows the creation of virtual devices, acting as an intermediary between the file system and the hardware to apply transformations transparently.

2. Difference between Full-Disk Encryption (FDE) and Filesystem-level Encryption
Full Disk Encryption (FDE): Encrypts all data on a device (OS, temp files, free space).

Advantages: Comprehensive protection; transparent to the user once unlocked.

Limitations: Does not protect data while the system is running/unlocked; lack of flexibility in selecting specific files.

Filesystem-level Encryption: Protects only specific files or directories.

Advantages: Greater user control; allows selective protection of sensitive data.

Limitations: Possible exposure of metadata; requires more complex manual configuration.

3. LVM and its Abstraction Layers
The Logical Volume Manager (LVM) is a framework that allows flexible space assignment on storage devices. Its three layers are:

Physical Volume (PV): The actual physical disk or partition tagged for LVM.

Volume Group (VG): A pool of space created by combining multiple Physical Volumes.

Logical Volume (LV): The functional partition created from the Volume Group, equivalent to a standard disk partition.

Advantages: LVM provides dynamic storage management, allowing partitions to be resized or moved easily, which is crucial for server environments.

4. The Boot Process with LUKS+LVM
Booting a system with LUKS+LVM requires unlocking encryption before the OS can mount.

GRUB loads the kernel and initramfs.

The system prompts for the LUKS passphrase to open the encrypted container via dm-crypt.

Once opened, LVM scans for logical volumes.

The system mounts the root partition and transfers control to the operating system.

1.3 Bibliography
IBM. (2026). Considerations for encrypting data partitions using LUKS. IBM Documentation.

Karthick. (2022). LVM Linux commands. OSTechNix.

Kerrisk, M. (Ed.). (2026). lsblk(8) — Linux manual page. man7.org.

Linux Kernel Organization. (2024). dm-crypt documentation.

Red Hat, Inc. (2026). Displaying Volume Groups / Logical Volumes. Red Hat Customer Portal.

Red Hat. (2023). Encrypting block devices using dm-crypt/LUKS.

Santos, J. A., & Santos, J. A. (2025). ¿Qué es LVM y cómo funciona en Linux? Profile Software Services.

Tutorials Point. (2026). UNIX Commands - pvs.
