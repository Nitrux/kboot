# Kernel Boot (`kboot`) | [![License](https://img.shields.io/badge/License-BSD_3--Clause-blue.svg)](https://opensource.org/licenses/BSD-3-Clause)

<p align="center">
  <img width="128" height="128" src="https://raw.githubusercontent.com/Nitrux/luv-icon-theme/master/Luv/mimetypes/64/application-x-executable.svg">
</p>


# Introduction

The Kernel Boot (`kboot`) utility using [kexec](https://en.wikipedia.org/wiki/Kexec) and is designed for [Nitrux OS](https://nxos.org/) to provide a solution to make it easier to load other Linux kernels on the fly.

> _⚠️ Important: `kboot` is intended to work exclusively in Nitrux OS, and using this utility in other distributions is not supported at all. Please do not open issues regarding this use case; they will be closed._

# Overview

`kboot` is designed for a particular purpose, make it easier to allow for a faster transition from the currently running kernel to a new kernel, avoiding the time-consuming hardware initialization and bootloader stages.

> _♦ Information: `kboot` is included by default starting with Nitrux 2.9.1._

---

### What `kboot` is

- Minimalistic, focusing on necessary functionality.
- A CLI utility.
- [100% Free and Open Source Software](#licensing) written entirely in [POSIX-compliant scripting language](https://en.wikipedia.org/wiki/Shell_script#Typical_POSIX_scripting_languages).

### What `kboot` is not

- A bootloader.
  - `kboot` uses a mechanism for loading and executing a new kernel within an already running system, bypassing the complete boot process. In comparison, a bootloader such as GRUB is a full-featured bootloader responsible for the initial bootstrapping of the operating system. GRUB provides a menu to select the desired operating system or kernel loads the selected kernel into memory, and transfers control to it.
- An init.
  - `kboot` does not function as an init or replace an init. The init process is responsible for initializing the system, starting essential system services and daemons, and bringing up the user space environment. `kboot` does not perform these functions, `kboot` only loads a new kernel image.
- A container, virtual machine, Live USB creator, Linux distribution, Live/Recovery/Rescue/Emergency environment, system installer, desktop environment, firmware, or "proprietary software."
  - _**Note**: We don't know why anyone would think that, but one can never know, so let's clarify that._

----

### Requeriments

- Nitrux 2.9.0+.

### Support for Previous Releases

`kboot` can work with previous releases that include [kexec](https://en.wikipedia.org/wiki/Kexec), such as Nitrux 2.9.0.

**Using `kboot` on Previous Releases**

For releases of Nitrux where `kboot` is not available by default, do the following.

```
git clone --depth=1 https://github.com/Nitrux/kboot.git $HOME/kboot
sudo cp $HOME/kboot/usr/bin/kboot /usr/bin
sudo cp $HOME/kboot/etc/kboot.conf /etc
```

# Usage

`kboot` is designed to be highly autonomous.

### Commands:

**Switch**: `sudo kboot switch debian` or `sudo kboot switch liquorix`
- Switches the kernel using the settings in the specified configuration file, e.g `debian` or `liquorix`.
> _⚠️ Important: This process involves stopping the currently running kernel and starting the new kernel from scratch. All running processes, including the graphical session, are terminated during this transition._

### Configuration:

`kboot` uses the files in the  directory `/etc/kboot.conf.d` to load kernels.
>_⚠️ Important: The files in this directory must refer to a valid kernel (vmlinuz) and initram images (initrd.img) within the filesystem. Nitrux OS puts kernel images other than the default kernel, like the signed Debian kernel, and initrd in the directory `/kboot` for better organization. In addition, to prevent polluting the GRUB when the boot menu is generated._

### Options:

- `sudo kboot -h`: Displays the help of `kboot`.
- `sudo kboot -d`: Runs `kboot` in verbose mode.
- `sudo kboot -v`: Displays the version of `kboot`.

# Licensing

The repository and its contents are licensed under **BSD-3-Clause**.

# Issues
If any problems are encountered, users can create an issue.

©2023 Nitrux Latinoamericana S.C.
