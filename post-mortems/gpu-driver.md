# Postmortem: GPU Driver Crashed the Kubernetes Master Node

## General Information
- **Date of Incident:** 2025-03-03 14:15:34
- **Owner(s):** Barush Mendez barush1203@gmail.com
- **Shared With:** @Repo_viewers
- **Status:** Final

---

## Executive Summary
**Impact:**
- All services were unresponsive, and the Kube-API was down for **6 days**, making Kubernetes management impossible.

**Root Cause:**
- A broken **Nvidia GPU driver** on the K8s master node caused a **Kernel Panic** during boot. The issue had been present for weeks but only became apparent after a power outage forced a reboot, preventing the system from booting properly.

**Resolution:**
- The issue was resolved by booting into a previous kernel version, removing broken packages, reinstalling necessary dependencies, and updating the system.

---

## Problem Summary
- **Duration:** Main outage: Mon, March 3, 14:15:34 to Sun, March 9, 19:45:21
- **Affected Services/Products:**
  - **V-Rising Server**
  - **Kube-API**
  - **Grafana**
  - **Jellyfin**
  - **Linkding**
- **Scope:** 100% of hosted services were unavailable.
- **User Impact:** All applications hosted on Kubernetes were **inaccessible for 6 days**, and Kubernetes management was not possible due to the **Kube-API outage**.
- **Revenue Impact:** Since this is a **homelab**, there was no financial impact.

---

## Detection
- **How It Was Detected:** The issue was detected manually when trying to access services.
- **Time to Detection:** 3 hours.

---

## Root Causes and Trigger

The **Kubernetes master node** is equipped with an **Nvidia GPU** to provide **hardware acceleration** for the **Jellyfin** service. During the installation of the `nvidia-dkms-390` driver, it failed to build properly with the existing kernel version. As a result, **kernel headers and other dependencies also failed to configure**. This issue was left unattended, and the system remained operational until a **power outage forced a reboot**.

Upon reboot, the system encountered a **Kernel Panic**, rendering the master node **unbootable**. Since this node was the **only master node in the cluster**, its failure resulted in:
- **Total cluster downtime** (no Kubernetes management available).
- **All hosted applications becoming inaccessible** since services relied on the master node’s private IP.

This incident highlights the **risks of a single-point-of-failure architecture** and the need for a **high-availability (HA) cluster setup**.

---

## Resolution
- **Steps Taken:**
  1. Since remote access was impossible, a **monitor was connected** to review boot logs, revealing the **Kernel Panic**.
  2. Booted using a **previous kernel version**, which restored system functionality.
  3. Attempted to update the server with `sudo apt update && sudo apt upgrade`, but this **failed due to broken packages**.
  4. Removed the broken packages using `sudo apt-get remove --purge '^nvidia-.*'`, then ran `sudo dpkg --configure -a` to fix package configuration issues.
  5. Executed `dpkg -l | grep -v ^ii` to identify any remaining broken packages and manually removed them with `sudo apt-get remove --purge <package_name>`.
  6. Ran `sudo apt-get install -f` to **fix missing dependencies** and executed `sudo apt-get install --reinstall linux-headers-$(uname -r)` to ensure the kernel was properly configured.
  7. Rebooted the machine and **confirmed that the Kernel Panic was resolved**.
- **Time to Resolution:** 6 days.

---

## Lessons Learned
### **What Went Well**
- The issue was relatively simple to resolve **once identified**.
- No data loss occurred.

### **What Went Poorly**
- There were **no automated alerts** indicating the outage.
- **Resolution time was too long** due to a lack of monitoring and immediate detection.
- **Single-node master architecture** resulted in **complete cluster downtime**.

### **Where We Got Lucky**
- **No luck here**—this was a full failure scenario.

---

## Action Items
### **Prevention Measures**
- **Ensure GPU driver installations are fully successful** or immediately revert changes if errors occur.
- **Migrate cluster to a high-availability (HA) setup** to prevent a single point of failure.
- **Expose the Kube-API through a load balancer** in an HA setup to improve reliability.

### **Emergency Response Improvements**
- **Set up a ticketing system** to document incidents and track resolutions.
- **Improve response times** for homelab issues by creating predefined troubleshooting workflows.

### **Monitoring & Alerting Enhancements**
- **Implement infrastructure monitoring** (e.g., Prometheus + Grafana) to detect issues proactively.
- **Set up blackbox monitoring** to detect failures **outside the Kubernetes cluster** (e.g., HTTP/TCP checks for critical services).

---
