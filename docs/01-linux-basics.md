# 1. Basics of Linux

[← Home](../README.md) · [How Linux is put together →](02-linux-design.md)

Linux is not one product. It is a **kernel** (the bit that talks to hardware) plus a **buffet of software** that a *distribution* packages into something you can install. People say "I run Linux" the way people say "I drive a car." They usually mean a specific distro, desktop, and set of habits.

If you only remember one thing from this page: **pick a distro, install it, then learn the shell.** Distro-hopping is a hobby. Programming is the homework.

## Linux is already around you

Linux's reach extends far beyond desktop PCs. Its adaptable kernel and open-source development model let organizations build everything from small devices to large computing clusters.

- **Cloud and servers:** Linux runs web applications, databases, build systems, and container hosts across AWS, Azure, and Google Cloud. Providers even maintain their own distributions, covered in [chapter 3](03-linux-distributions.md). [Amazon Linux](https://aws.amazon.com/linux/amazon-linux-2023/) is one example.
- **Phones and tablets:** Android uses the Linux kernel beneath its own runtime, libraries, and app framework. That makes an Android phone part of the Linux ecosystem, but it does not give it the same desktop or package manager as Ubuntu. See the [Android architecture overview](https://source.android.com/docs/core/architecture).
- **Embedded devices:** Routers, appliances, industrial equipment, and in-vehicle systems can use tailored Linux systems. The [Yocto Project](https://www.yoctoproject.org/) helps manufacturers build systems for their hardware; these often have neither a desktop nor a keyboard.
- **Scientific computing:** Linux dominates large supercomputers used for simulations and research. [TOP500's Linux statistics](https://www.top500.org/statistics/details/osfam/1/) track its presence in that ranking.
- **Personal computing and learning:** Linux also powers developer workstations and small computers such as the Raspberry Pi, whose official [Raspberry Pi OS](https://www.raspberrypi.com/software/operating-systems/) is Debian-based.

There is no single useful “Linux market share” across all these categories. Desktop usage alone misses phones, cloud infrastructure, and devices. Learning processes, permissions, networking, and the shell gives you concepts you can reuse across many of them.

## Why CS students end up on Linux

- Course staff, cloud VMs, and internships assume POSIX tools: `ssh`, `git`, `make`, compilers, Python, databases.
- Linux is common on the servers you will deploy to. Developing on the same family of OS removes a whole class of "works on my machine" bugs.
- The command line is not optional in systems, networks, security, or DevOps courses. Start here: [amitsk/learning-shell](https://github.com/amitsk/learning-shell).

Windows and macOS are fine computers. Linux is the one that matches the machines you are training for.

## The vocabulary you need

The **kernel** manages hardware and processes. **User space** contains programs such as shells, compilers, and browsers. A **distribution** packages the kernel and software with installation and update tools. A **desktop environment** provides the graphical interface.

[Chapter 2](02-linux-design.md) explains how those pieces fit together. [Chapter 3](03-linux-distributions.md) helps you choose a distro and desktop, and [chapter 4](04-running-linux.md) shows how to try Linux in a VM or container.

## You still need the terminal

The GUI is for living. The shell is for *working*. CS coursework will not accept a screenshot of the file manager as a build log.

The shell tutorial's [two-hour path](https://github.com/amitsk/learning-shell#if-you-are-new) is the assignment. It ends on purpose.

1. [hello.sh](https://github.com/amitsk/learning-shell/blob/main/scripts/getting_started.md#3-writing-your-first-script) — about 30 minutes. SSH in that file can wait.
2. [nano, and how to leave Vim](https://github.com/amitsk/learning-shell/blob/main/scripts/text_editors.md#you-can-close-this-tab) — about 20 minutes. Stop when the page says you can close the tab.
3. [Bash basics, sections 1–4](https://github.com/amitsk/learning-shell/blob/main/scripts/basic_shell.md#the-light-path-ends-here) — about 45 minutes. Stop at the line that says the light path ends.

Same afternoon, if you want: [aliases](https://github.com/amitsk/learning-shell/blob/main/scripts/shell_customization.md#aliases), then the [modern tools table](https://github.com/amitsk/learning-shell/blob/main/scripts/modern_tools.md) (15 minutes, including [delta](https://github.com/amitsk/learning-shell/blob/main/scripts/modern_tools.md#using-delta-with-git) and the [alias block](https://github.com/amitsk/learning-shell/blob/main/scripts/modern_tools.md#3-aliases-for-these-tools)). [Users and groups](https://github.com/amitsk/learning-shell/blob/main/scripts/users_groups.md) is the chapter [section 5](05-dev-workstation.md) uses when you add an account. sed, awk, HTTP, and Make wait until a course names them.

### Five commands that unlock the rest

Run these after install. Meanings live in the shell tutorial; this is just the "you are not stuck" kit.

```bash
pwd          # where am I?
ls -la       # what is here, including hidden files?
cd ~         # go home
man ls       # the manual; q to quit
sudo apt update   # on Mint/Ubuntu: refresh package lists
```

On Fedora, `sudo dnf makecache --refresh` refreshes repository metadata. `sudo dnf upgrade --refresh` also installs available upgrades; it is closer to running `apt update` followed by `apt upgrade`.

## Extra reading (still beginner-friendly)

- [Linux Journey](https://linuxjourney.com/)
- [MIT Missing Semester](https://missing.csail.mit.edu/)
- [The Linux Documentation Project](https://tldp.org/guides.html)
- [DigitalOcean Linux basics](https://www.digitalocean.com/community/tags/linux-basics)

---

**Next:** [How Linux is put together →](02-linux-design.md)
