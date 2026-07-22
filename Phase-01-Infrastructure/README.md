# Phase 01 - Infrastructure Setup

## Objective

Build a stable virtualization environment that will serve as the foundation for the DuceTech SOC Home Lab.

---

## Environment

- VMware Workstation Pro 26H1
- Windows 11
- AMD Ryzen 5 5600X
- 16 GB RAM
- External SSD
- Windows Virtual Machine

---

## Tasks Completed

- Installed VMware Workstation Pro
- Enabled AMD-V (SVM Mode) in BIOS
- Created CyberSecurity-Lab folder structure
- Created first Windows 11 virtual machine
- Configured TPM support
- Installed Windows 11
- Installed VMware Tools
- Created "Fresh Windows Install" snapshot
- Renamed workstation to DuceTech

---

## Challenges

### Problem

VMware would not launch the virtual machine.

### Cause

AMD-V virtualization was disabled inside the BIOS.

### Resolution

Entered ASUS BIOS, enabled SVM Mode, rebooted host computer, and verified virtualization was enabled in Windows.

---

## Skills Learned

- VMware Administration
- Windows Installation
- BIOS Configuration
- Virtual Machine Management
- Snapshot Management
- Event Viewer Basics

---

## Next Phase

Windows Administration Bootcamp

Topics:

- Event Viewer
- Services
- PowerShell
- Local Security Policy
- Windows Registry
