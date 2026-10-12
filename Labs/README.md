# DevOps

Coursework repository for DevOps.

## Student Information

| Field | Details |
|---|---|
| Name | Eman Fatima |
| Registration Number | 2023-BCS-025 |
| Course Code | <COURSE CODE> |
| Section | A |
| GitHub Username | Eman-Fatima-7125 |

## Lab 01: Installing Ubuntu Server on VMware Workstation Pro and Connecting with SSH

### Objective
Install Ubuntu Server 26.04.1 LTS inside a VMware Workstation Pro virtual machine, create a user account that matches my GitHub username, identify the server's IPv4 address, and connect to the server from Windows over SSH.

### Environment

| Item | Value |
|---|---|
| Host operating system | Windows |
| Virtualization software | VMware Workstation 16 Pro |
| Guest operating system | Ubuntu Server 26.04.1 LTS (amd64) |
| Virtual disk | 20 GB, LVM |
| Server name | `ubuntu` |
| Ubuntu username | `eman-fatima-7125` |
| Network interface | `ens33` (DHCP) |
| Server IPv4 address | `192.168.82.131` |
| Local prompt | `eman-fatima-7125@ubuntu` |

### Tasks Completed

| Task | Description | Evidence |
|---|---|---|
| 1 | Check available host storage | `available_storage.png` |
| 2 | GitHub profile with actual name | `github_actual_name.png` |
| 3 | Student Marks Portal sign-in and enrollment | `portal_login_page.png`, `portal_github_profile.png`, `portal_enrollment_submitted.png` |
| 4 | Download the Ubuntu Server ISO | `ubuntu_server_iso.png` |
| 5 | Open VMware Workstation Pro | `vmware_workstation.png` |
| 6 | Start the New Virtual Machine Wizard | `vm_creation_wizard.png`, `vm_typical_configuration.png` |
| 7 | Select the Ubuntu ISO | `vm_ubuntu_iso_selected.png` |
| 8 | Installer language selection | `ubuntu_language.png` |
| 9 | Keyboard configuration | `ubuntu_keyboard_layout.png`, `ubuntu_keyboard_variant.png` |
| 10 | Choose the installation type | `ubuntu_installation_type.png` |
| 11 | Network configuration | `ubuntu_installer_network.png`, `ubuntu_network_interface.png` |
| 12 | Proxy and mirror configuration | `ProxyConfiguratuin.png`, `Mirror Configuration.png` |
| 13 | Guided storage configuration | `ubuntu_guided_storage.png`, `vm_configuration_summary.png` |
| 14 | Storage summary and confirmation | `ubuntu_storage_configuration.png`, `ubuntu_partition_layout.png`, `ubuntu_selected_disk.png`, `ubuntu_disk_details.png`, `ubuntu_storage_warning.png`, `ubuntu_storage_confirmed.png` |
| 15 | Profile setup: name, server name and username | `ubuntu_profile_setup.png`, `ubuntu_actual_name.png`, `ubuntu_server_name.png`, `ubuntu_username.png` |
| 16 | Ubuntu Pro, SSH, snaps and installation | `ubuntu_pro.png`, `SSH_Configuration.png`, `server_snap.png`, `ubuntu_installation_progress.png`, `ubuntu_installer_boot.png`, `ubuntu_identity_verified.png` |
| 17 | Find the IP address and connect over SSH | `ubuntu_ip_address.png`, `windows_ssh_command.png`, `windows_ssh_fingerprint.png`, `windows_ssh_login.png`, `windows_ssh_identity.png` |

### SSH Connection

```
ssh eman-fatima-7125@192.168.82.131
```

On the first connection the host key fingerprint is accepted by typing `yes`. After logging in, the remote prompt shows `eman-fatima-7125@ubuntu`.

### Repository Structure

```
DevOps/
├── README.md
└── Labs/
    └── Lab01/
        ├── README.md                  (instructor-provided lab instructions)
        ├── Lab1_Solution.pdf          (full lab report with captions)
        ├── images/
        │   └── install-ubuntu-server/ (instructor-provided examples)
        └── screenshots/               (original evidence screenshots)
```

### Submission Checklist

- [x] Repository is named `DevOps`
- [x] Work is stored under `Labs/Lab01`
- [x] Evidence screenshots are in `Labs/Lab01/screenshots/`
- [x] `Lab1_Solution.pdf` is in `Labs/Lab01/`
- [x] Ubuntu username matches my GitHub username
- [x] Server name is `ubuntu`
- [x] No passwords, tokens, or private keys are visible
- [x] All files are committed and pushed to GitHub
