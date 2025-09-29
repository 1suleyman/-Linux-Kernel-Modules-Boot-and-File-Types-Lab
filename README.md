# 🐧 Linux Kernel Modules, Boot, and File Types Lab

In this lab, I learned how to:

* Identify the **init process** used by the Linux system
* Check the **default system target** and change it
* Determine **file types** for system files
* Understand **recommended directories** for third-party software
* Identify **hardware information** such as Ethernet controllers

All tasks were completed using standard Linux terminal commands, and `sudo` was required for several administrative actions.

---

## 📋 Lab Overview

**Goal:**

* Explore the Linux boot process and init system
* Investigate system targets and default runlevels
* Inspect file types and locations of system files
* Learn recommended conventions for installing third-party software
* Query hardware details using built-in Linux tools

**Learning Outcomes:**

* Understand Linux init systems (systemd vs SysV)
* Work with system targets and runlevels
* Use `file` to check file types
* Locate system directories and block device info
* Identify hardware vendors with `lspci`

---

## 🛠 Step-by-Step Journey

### Step 1: Check the Init Process

**Task:** Determine which init system the system uses.

**Command:**

```bash
ls -ln /sbin/init
```

* Output shows symbolic link: `/sbin/init -> /lib/systemd/systemd`
* **Conclusion:** The system uses **systemd** as the init process.

💡 **Tip:** `systemd` is the default init system in most modern Linux distributions.

---

### Step 2: Check & Change Default System Target

**Task:** Find and change the default system target (runlevel).

**Commands:**

```bash
systemctl get-default               # Shows current default target (e.g., graphical.target)
sudo systemctl set-default multi-user.target  # Changes default to multi-user.target
```

💡 **Tip:** You need `sudo` to change the default target for all users.

---

### Step 3: Identify File Types

**Task:** Determine the type of various system files.

**Commands:**

```bash
sudo file /root/firefox.db        # Output: Debian binary package file
sudo file /root/sample_script.sh  # Output: Bourne-Again shell script (bash)
```

💡 **Tip:** `file` analyzes content to determine file type, not just the extension.

---

### Step 4: Recommended Directory for Third-Party Software

**Observation:**

* Third-party IDEs or software packages are typically installed in `/opt`
* Using `/opt` avoids conflicts with system-managed directories (`/usr/bin`, `/usr/lib`)

---

### Step 5: Locate Block Device Information

**Task:** Identify the directory containing block device info.

**Command:**

```bash
lsblk
```

* Output shows all block devices
* Metadata is located under `/sys/block`

💡 **Tip:** Use `lsblk` to visualize disks, partitions, and mount points.

---

### Step 6: Identify Ethernet Controller Vendor

**Task:** Find the Ethernet controller vendor in the system.

**Command:**

```bash
lspci | grep -i ethernet
```

* Output shows the vendor name (e.g., Red Hat Virtual Network Device)

💡 **Tip:** `lspci` lists all PCI devices, useful for identifying network and storage controllers.

---

## ✅ Verification

* Init process: `/sbin/init -> /lib/systemd/systemd`
* Default system target: `graphical.target` → changed to `multi-user.target`
* File types verified with `file` command
* Third-party software installation directory: `/opt`
* Block devices and partitions listed via `lsblk`
* Ethernet controller vendor identified with `lspci`

---

## 📌 Key Notes

| Feature               | Command / Path                   | Description                         |                                 |
| --------------------- | -------------------------------- | ----------------------------------- | ------------------------------- |
| Init process          | `ls -ln /sbin/init`              | Shows which init system is used     |                                 |
| Default system target | `systemctl get-default`          | Shows current target/runlevel       |                                 |
| Change system target  | `sudo systemctl set-default ...` | Changes default target/runlevel     |                                 |
| File types            | `sudo file <filepath>`           | Determines type of a file           |                                 |
| Third-party software  | `/opt`                           | Recommended installation directory  |                                 |
| Block devices         | `lsblk`                          | Lists physical disks and partitions |                                 |
| Ethernet vendor       | `lspci                           | grep -i ethernet`                   | Shows network controller vendor |

---

## 💡 Tips / Takeaways

* Always use `sudo` for administrative tasks.
* `systemctl` replaces legacy runlevel management commands (`init`, `telinit`).
* Use absolute paths when checking or moving files in system directories.
* `lsblk` and `/sys/block` help understand storage topology.
* `lspci` is invaluable for hardware inspection.

---

## ✅ References

* [Linux `ls` Manual](https://man7.org/linux/man-pages/man1/ls.1.html)
* [Linux `file` Manual](https://man7.org/linux/man-pages/man1/file.1.html)
* [systemd Targets Documentation](https://www.freedesktop.org/software/systemd/man/systemd.target.html)
* [lsblk Documentation](https://man7.org/linux/man-pages/man8/lsblk.8.html)
* [lspci Documentation](https://man7.org/linux/man-pages/man8/lspci.8.html)
