# Kernel Boot (`kboot`) | [![License](https://img.shields.io/badge/License-BSD_3--Clause-blue.svg)](https://opensource.org/licenses/BSD-3-Clause)

<p align="center">
  <img width="128" height="128" src="https://raw.githubusercontent.com/Nitrux/luv-icon-theme/master/Luv/mimetypes/64/application-x-executable.svg">
</p>


# Introduction

The Kernel Boot (`kboot`) utility uses [kexec](https://en.wikipedia.org/wiki/Kexec), and we designed it for [Nitrux OS](https://nxos.org/) to make it easier to load other Linux kernels on the fly.

> [!WARNING]
> `kboot` is intended to work exclusively in Nitrux OS, and using this utility in other distributions is not supported. Please do not open issues regarding this use case; they will be closed.

# Overview

Kernel Boot is designed for a particular purpose, making it easier to transition from the currently running kernel to a new kernel and avoiding the time-consuming hardware initialization and bootloader stages. It performs the following steps:

1. Reads the settings in the specified configuration file.
2. Then, use `kexec` to load the selected kernel using the parameters from the configuration file.

> [!TIP]
> Kernel Boot is included by default, starting with Nitrux 2.9.1.

---

### What `kboot` is

- Minimalistic, focusing on necessary functionality.
- A CLI utility.
- [100% Free and Open Source Software](#licensing) written entirely in [POSIX-compliant scripting language](https://en.wikipedia.org/wiki/Shell_script#Typical_POSIX_scripting_languages).

### What `kboot` is not

- A bootloader.
  - Kernel Boot uses a mechanism for loading and executing a new kernel within an already running system, bypassing the complete boot process. In comparison, a bootloader such as GRUB is a full-featured bootloader responsible for the initial bootstrapping of the operating system. GRUB provides a menu to select the desired operating system or kernel.
- An init or service manager.
 Kernel Boot does not function as an init or replace an init. The init process is responsible for initializing the system, starting essential system services and daemons, and bringing up the user-space environment. Kernel Boot does not perform these functions; It only loads a new kernel image.
- An initrd or initram generator.
  - Kernel Boot does not replace or modify the existing initramfs generator. The initram generator tools like dracut or initramfs-tools are responsible for identifying and including the necessary modules, drivers, and scripts to correctly set up the root filesystem and handle any unique configurations (e.g., encrypted root, LVM, RAID, etc.). Kernel Boot loads a kernel and an existing initram, then transfers control to it.
- A container, virtual machine, Live USB creator, Linux distribution, Live/Recovery/Rescue/Emergency environment, system installer, desktop environment, firmware, or "proprietary software."

> [!NOTE]
> We don't know why anyone would think that, but one can never know, so let's clarify that.

----

### Requirements

- Nitrux 2.9.0+.

### Support for Previous Releases

Kernel Boot can work with previous releases that include [kexec](https://en.wikipedia.org/wiki/Kexec), such as [Nitrux 2.9.0](https://nxos.org/changelog/release-announcement-nitrux-2-9-0/).

**Using `kboot` on Previous Releases**

For Nitrux releases where `kboot` is not available by default, do the following:

```
git clone --depth=1 https://github.com/Nitrux/kboot.git $HOME/kboot
sudo cp $HOME/kboot/usr/bin/kboot /usr/bin
sudo cp -r $HOME/kboot/etc/kboot.d /etc
```

# Usage

Kernel Boot is designed to be highly autonomous.

### Commands:

**Switch**: `sudo kboot switch <config_file>`

- Switches the kernel using the settings in the specified configuration file, e.g., `/etc/kboot.d/debian` or `/etc/kboot.d/liquorix`.

> [!WARNING]
> This process involves stopping the currently running kernel and starting the new kernel from scratch. All running processes, including the graphical session, are terminated during this transition. For users of NVIDIA GPUs, using Kernel Boot is not a viable option due to how the NVIDIA proprietary driver works with the Linux kernel.

### Configuration:

Kernel Boot uses the directory `/etc/kboot.d` files to load kernels.

> [!WARNING]
> The files in this directory must refer to a valid kernel (vmlinuz) and initram images (initrd.img) within the filesystem. We recommend placing kernel images other than the default kernel and initrd in the/kboot directory for better organization. In addition, to prevent polluting the GRUB menu.

### Options:

```
-h or --help        Show this help.
-v or --version     Show the version.
-d or --debug       Enable verbose output.

```
# Licensing

The repository and its contents are licensed under **BSD-3-Clause**.

# Issues

If any problems are encountered, users can create an issue.

©2023 Nitrux Latinoamericana S.C.
