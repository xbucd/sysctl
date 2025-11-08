# 🛡️ Hardened Linux Kernel Sysctl Configuration

Hardened Linux Kernel Parameters for optimal **security** and **performance**.

---

## ⚠️ Important Notice ⚠️

⚠️ **This configuration can change system behavior and may break certain applications if misapplied.** 

⚠️**Read before applying. Use at your own risk. 
You are fully responsible for any changes to your system.**  



---

## 📚 References
- [Sysctl Explorer](https://sysctl-explorer.net/) – explore and understand kernel parameters  
- [Linux Kernel Documentation](https://www.kernel.org/doc/Documentation/sysctl/) – official kernel documentation  

---

## 📝 Notes
This configuration aims for a balanced approach to security and usability.  
You can modify any option according to your system's needs.  
Recommended for:  
- **64-bit Linux systems**  
- Stable environments (wired or controlled networks)

  > This repository provides a secure baseline for Linux kernel hardening while maintaining stability and compatibility with VMs, containers, and standard network setups.

---

## 🗂 Configuration Basics
Linux `sysctl` configs are usually loaded from `/etc/sysctl.d`.  
Files are read in **lexicographic order**, so later files override earlier ones.
> Later files (like 99-custom.conf) override settings in earlier files (like 20-default.conf)

Example:

```bash
$ cat /etc/sysctl.d/20-default.conf
net.ipv4.ip_forward = 0

$ cat /etc/sysctl.d/99-custom.conf
net.ipv4.ip_forward = 1

$ sysctl net.ipv4.ip_forward
net.ipv4.ip_forward = 1
```

Other common load paths:

- /run/sysctl.d

- /usr/local/lib/sysctl.d

- /usr/lib/sysctl.d

- /lib/sysctl.d

To see which files are loaded on a systemd-based system:
```bash
systemd-analyze cat-config sysctl
```

---

## 🚀 Recommended Deployment
1. **Clone or download** the repository:
```bash
git clone https://github.com/xbucd/sysctl
cd sysctl
```
OR
use curl for fast deployment (recommend):
```bash
   sudo curl https://raw.githubusercontent.com/xbucd/sysctl/refs/heads/main/99-hardening.conf -o /etc/sysctl.d/99-hardening.conf
   # this command will download 99-hardening.conf to /etc/sysctl.d/
```
skip step 3
2. **Review the configuration** carefully:
```bash
less 99-hardening.conf
# or open in text editor
```
> ⚠️ Read and understand all options before applying. Adjust settings to your needs.

3. **Copy the configuration** to `/etc/sysctl.d/`:
```bash
sudo cp 99-hardening.conf /etc/sysctl.d/ 
```

4. **Load and Apply Configuration**
```bash
# Apply all sysctl configurations
sudo sysctl --system
```

5. **Verify applied settings (example):**
```bash
# Example: check IP forwarding
sysctl net.ipv4.ip_forward

# Check kernel pointer restrictions
sysctl kernel.kptr_restrict
```
---
⚡ Tips

- Optional or advanced settings should be commented out until you fully understand their impact

- Use this configuration as a baseline and tweak for your environment

- Consider keeping a backup of your current sysctl settings



