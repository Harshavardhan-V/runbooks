# 📘 **RUNBOOK: Daily Linux Commands for SRE/Support (With Full Flag/Letter Explanation)**

This is ordered **from most-used → moderately used → rarely used** for real SRE workflows.

---

# ----------------------------------------------------

# **SECTION 1 — Primary Daily Commands (Top SRE Usage)**

# ----------------------------------------------------

## **1.1 List Files With Details & Hidden Files**

### **Command**

```bash
ls -la
```

### Explanation

| Part | Meaning                                      |
| ---- | -------------------------------------------- |
| `ls` | List directory contents                      |
| `-l` | Long format (permissions, owner, size, date) |
| `-a` | Show all files including hidden (`.` files)  |



---

## **1.2 Search Inside Files (Logs, Errors)**

### **Command**

```bash
grep -r --text "reboot" /var/log/
```

### Explanation

| Part        | Meaning                              |
| ----------- | ------------------------------------ |
| `grep`      | Search for patterns inside files     |
| `-r`        | Recursive search through directories |
| `--text`    | Treat binary files as text           |
| `"reboot"`  | Pattern to search                    |
| `/var/log/` | Directory containing logs            |



---

## **1.3 View Running Processes**

### **Command**

```bash
ps lax
```

### Explanation

| Part | Meaning                                    |
| ---- | ------------------------------------------ |
| `ps` | Process status                             |
| `l`  | Long format                                |
| `a`  | Show processes of all users                |
| `x`  | Include processes not attached to terminal |



---

## **1.4 Check System Resource Usage**

### **Command**

```bash
free --mega
```

### Explanation

| Part     | Meaning              |
| -------- | -------------------- |
| `free`   | Show RAM usage       |
| `--mega` | Display values in MB |



---

## **1.5 Check Disk Usage**

### **Command**

```bash
df /
```

### Explanation

| Part | Meaning               |
| ---- | --------------------- |
| `df` | Disk filesystem usage |
| `/`  | Root partition        |



---

## **1.6 Directory Size Summary**

### **Command**

```bash
du -sh /bin/
```

### Explanation

| Part    | Meaning          |
| ------- | ---------------- |
| `du`    | Disk usage       |
| `-s`    | Summary only     |
| `-h`    | Human readable   |
| `/bin/` | Target directory |



---

## **1.7 Networking — Check interfaces**

### **Command**

```bash
ip a
```

### Explanation

| Part | Meaning                              |
| ---- | ------------------------------------ |
| `ip` | Linux network utility                |
| `a`  | Address (show IPs of all interfaces) |



---

## **1.8 Show Listening Ports**

### **Command**

```bash
ss -tunlp
```

### Explanation

| Part | Meaning                       |
| ---- | ----------------------------- |
| `ss` | Socket statistics             |
| `-t` | TCP ports                     |
| `-u` | UDP ports                     |
| `-n` | Do not resolve names → faster |
| `-l` | Show *listening* ports        |
| `-p` | Show process using port       |



---

## **1.9 Search Installed Packages (Ubuntu/Debian)**

### **Command**

```bash
apt search "apache"
```

### Explanation

| Part       | Meaning                  |
| ---------- | ------------------------ |
| `apt`      | Package manager frontend |
| `search`   | Search for package       |
| `"apache"` | Query text               |



---

## **1.10 View File Permissions (ACL)**

### **Command**

```bash
getfacl archive
```

### Explanation

| Part      | Meaning                       |
| --------- | ----------------------------- |
| `getfacl` | Get ACL permissions of a file |
| `archive` | Filename                      |



---

## **1.11 Git Daily Commands**

### **Add Files**

```bash
git add *.cpp
```

| Part    | Meaning          |
| ------- | ---------------- |
| `git`   | Version control  |
| `add`   | Stage files      |
| `*.cpp` | All `.cpp` files |

### **Commit**

```bash
git commit -m "Message"
```

| Part     | Meaning                |
| -------- | ---------------------- |
| `commit` | Save staged snapshot   |
| `-m`     | Commit message follows |

### **Clone**

```bash
git clone <repo-url>
```

Clones remote repo locally.



---

# ----------------------------------------------------

# **SECTION 2 — Frequent Weekly Commands**

# ----------------------------------------------------

## **2.1 Check System Boot Target**

### **Command**

```bash
systemctl get-default
```

### Explanation

| Part          | Meaning                  |
| ------------- | ------------------------ |
| `systemctl`   | Systemd control          |
| `get-default` | Show default boot target |



---

## **2.2 Reload Systemd Daemon**

### **Command**

```bash
systemctl daemon-reload
```

### Explanation

| Part            | Meaning                       |
| --------------- | ----------------------------- |
| `daemon-reload` | Reload systemd configurations |



---

## **2.3 View CPU Info**

### **Command**

```bash
lscpu
```

### Explanation

| Part  | Meaning         |
| ----- | --------------- |
| `ls`  | list            |
| `cpu` | CPU information |



---

## **2.4 View Time Zone**

```bash
timedatectl
```

| `timedatectl` | Manage time/date settings |

Modify timezone:

```bash
timedatectl set-timezone America/New_York
```



---

## **2.5 Package Info (Debian)**

### **Find which package provides a file**

```bash
dpkg --search /bin/ls
```

| `dpkg` | Debian package manager |
| `--search` | Search for file ownership |



---

# ----------------------------------------------------

# **SECTION 3 — Administrative / Support Commands**

# ----------------------------------------------------

## **3.1 Add User to Group**

### **Command**

```bash
usermod -a -G developers jane
```

### Explanation

| Letter       | Meaning              |
| ------------ | -------------------- |
| `usermod`    | Modify a user        |
| `-a`         | Append to group list |
| `-G`         | Secondary group(s)   |
| `developers` | Group                |
| `jane`       | User                 |



---

## **3.2 Lock User Account**

### **Command**

```bash
usermod -L sam
```

| `-L` | Lock account |



---

## **3.3 Check Mount Options**

### **Command**

```bash
findmnt /dev/vda1
```

| `findmnt` | Find mounted filesystem |
| `/dev/vda1` | Device |



---

## **3.4 Mount Disk Read-Only**

### **Command**

```bash
mount -o ro,noexec,nosuid /dev/vdb1 /mnt
```

| Part        | Meaning                  |
| ----------- | ------------------------ |
| `mount`     | Attach filesystem        |
| `-o`        | Options                  |
| `ro`        | Read-only                |
| `noexec`    | Do not allow executables |
| `nosuid`    | Ignore SUID bits         |
| `/dev/vdb1` | Device                   |
| `/mnt`      | Mount point              |



---

## **3.5 View Block Devices**

### **Command**

```bash
lsblk
```

| `ls` | List |
| `blk` | Block devices |



---

## **3.6 Swap Commands**

```bash
swapon --show
swapoff /dev/vdb2
```

| Part      | Meaning             |
| --------- | ------------------- |
| `swapon`  | Enable swap         |
| `--show`  | Display active swap |
| `swapoff` | Disable swap        |



---

# ----------------------------------------------------

# **SECTION 4 — Advanced / Occasional SRE Commands**

# ----------------------------------------------------

These are used occasionally during escalations or infra work.

---

## **4.1 OpenSSL Certificate CSR**

### **Command**

```bash
openssl req -newkey rsa:4096 -keyout priv.key -out cert.csr
```

### Explanation

| Part       | Meaning                    |
| ---------- | -------------------------- |
| `openssl`  | Crypto utility             |
| `req`      | Create certificate request |
| `-newkey`  | Generate new keypair       |
| `rsa:4096` | Algorithm & key size       |
| `-keyout`  | Output private key path    |
| `-out`     | Output CSR filename        |



---

## **4.2 SELinux Commands**

Examples:

### Change File SELinux Context

```bash
chcon -t httpd_sys_content_t /var/index.html
```

| Part                  | Meaning        |
| --------------------- | -------------- |
| `chcon`               | Change context |
| `-t`                  | Type           |
| `httpd_sys_content_t` | Context type   |



---

## **4.3 LVM Commands**

### Create a Physical Volume

```bash
pvcreate /dev/vdb
```

| `pvcreate` | Create Physical Volume |

### List PVs

```bash
pvs
```

### Create Volume Group

```bash
vgcreate volume1 /dev/vdb
```

### Create LV

```bash
lvcreate <options>
```



---

# ----------------------------------------------------

# **SECTION 5 — Least-used but included (per file)**

# ----------------------------------------------------

These are seen rarely in day-to-day SRE operational workflows.

Examples:

### RAID

```bash
mdadm --create /dev/md0 --level=1 --raid-devices=2 /dev/vdb /dev/vdc
```

### XFS Repair

```bash
xfs_repair /dev/vdb
```

### ACL Set

```bash
setfacl --modify user:john:rw file
```