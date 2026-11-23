# 4. Running Linux: virtual machines and containers

[← Choosing a distribution](03-linux-distributions.md) · [Home](../README.md) · [Development workstation →](05-dev-workstation.md)

You do not have to wipe your laptop to try Linux. A **virtual machine (VM)** gives you a whole Linux computer inside a window; a **container** gives you an isolated Linux command line without booting a second kernel. Pick the level of commitment you are ready for today.

## Choose an environment

| Approach | Good for | What to expect |
| --- | --- | --- |
| Dedicated install | Daily driver & real hardware | Linux owns the disk. Back up your files first, not after. |
| Dual boot | Keeping Windows/macOS around | Pick an OS at boot. Partitioning requires backups, not bravery. |
| Virtual machine (VM) | Practicing installs, desktops, services | Full guest OS in a window; mistakes are one snapshot away from never happening. |
| [WSL 2](https://learn.microsoft.com/en-us/windows/wsl/) on Windows | Shell & dev tools beside Windows apps | Managed Linux VM integrated into Windows (school/work laptops may need IT approval). |
| [Docker](https://docs.docker.com/get-started/docker-concepts/the-basics/what-is-a-container/) or [Podman](https://podman.io/docs) | Trying CLI tools & packaging apps | Lightweight, disposable user space sharing a Linux kernel — no Cinnamon desktop. |

For the full workstation walkthrough in [chapter 5a](05-dev-workstation.md), use a dedicated Mint install or a Mint VM. Containers are great for shell practice, but UFW, boot troubleshooting, and Cinnamon expect a full OS.

## Install Linux in VirtualBox

Your real computer is the **host**; Linux inside the window is the **guest**. Its "hard drive" is just a file on your host, so clicking "Erase disk" inside the guest installer only erases that fake disk — still double-check the size so your pulse stays normal.

1. Install [VirtualBox](https://www.virtualbox.org/) (enable Intel VT-x / AMD-V in firmware if it complains).
2. Download and verify the [Linux Mint Cinnamon ISO](https://linuxmint.com/download.php) ([verification guide](https://linuxmint-installation-guide.readthedocs.io/en/latest/verify.html)) — no USB stick needed for a VM.
3. Create a Linux VM with **2 vCPUs, 4 GB RAM, and a 40 GB dynamically allocated disk** (assuming a 16 GB+ host; leave room for the host to breathe), attach the ISO, keep **NAT** networking, and skip unattended install so you see the real installer.
4. Follow the [Mint install steps](https://linuxmint-installation-guide.readthedocs.io/en/latest/install.html), reboot, eject the ISO, install updates, shut down cleanly, and **take a VM snapshot**. Snapshots are your undo button (still keep real backups of homework).

Full wizard, snapshot, and Guest Additions (better resizing/clipboard) details live in the [VirtualBox 7.2 User Guide](https://docs.oracle.com/en/virtualization/virtualbox/7.2/user/Introduction.html) and [Working with VMs](https://docs.oracle.com/en/virtualization/virtualbox/7.2/user/working-with-vms.html).

Next, jump to [chapter 5a's first-boot steps](05-dev-workstation.md#52-first-boot-become-a-boring-up-to-date-machine) **inside the guest** (or [chapter 5b](05b-omarchy.md#5b2-first-boot-learn-super-then-become-boring) for an Omarchy ISO). For the later SSH exercise over NAT, add a VirtualBox port-forwarding rule from host `127.0.0.1:2222` to guest port `22`, enable SSH + firewall in the guest ([5a](05-dev-workstation.md#55-ssh-server-so-the-machine-can-be-a-machine) / [5b](05b-omarchy.md#5b5-ssh-server-off-until-you-ask)), and connect from the host:

```bash
ssh -p 2222 youruser@127.0.0.1
```

## Other VM tools and WSL

- **Linux host:** [virt-manager](https://virt-manager.org/) puts a friendly GUI on KVM/QEMU.
- **macOS:** [UTM](https://mac.getutm.app/). On Apple Silicon, pick an **ARM64** Ubuntu or Debian ISO in virtualization mode — emulating x86-64 Mint is possible the way paddling a cruise ship is possible.
- **Windows:** Follow [Install WSL](https://learn.microsoft.com/en-us/windows/wsl/install) in an administrator PowerShell:

```powershell
wsl --install
```

Restart if prompted and create your Linux user. WSL 2 is great for shells, compilers, and code; it just isn't a full Cinnamon desktop.

## Try Linux user space in Docker

A container is isolated processes plus a distro's files and libraries, sharing a Linux kernel instead of booting its own (so an Ubuntu container happily runs on a Fedora host; on macOS/Windows, [Docker Desktop](https://docs.docker.com/desktop/) hides a tiny Linux VM underneath).

Install Docker via the [official instructions](https://docs.docker.com/get-started/get-docker/), confirm `docker version` works, then launch a disposable Ubuntu shell from your **host**:

```bash
docker run --rm -it ubuntu:26.04 bash
```

`-it` gives you an interactive terminal; `--rm` sweeps up the container when you exit. Inside it:

```bash
cat /etc/os-release   # Ubuntu user space
uname -r              # the shared Linux kernel, not Ubuntu's
apt update && apt install -y curl
curl --version
exit
```

Notice there's no `sudo` — the default container shell drops you in as root, unlike your workstation user. Everything you installed vanishes on `exit` (the base image stays cached). For repeatable setups, write a [Dockerfile](https://docs.docker.com/reference/dockerfile/); for files that survive exit, use a [volume](https://docs.docker.com/engine/storage/volumes/).

No Cinnamon desktop and usually no systemd PID 1 here, which makes containers ideal for testing packages, builds, or a quick database. [Podman](https://podman.io/docs) works the same way (`podman run --rm -it ubuntu:26.04 bash`) if you prefer a daemonless alternative.

## Industry context: The same container model in the cloud

> **No credit card required:** You do **not** need a cloud account or a Kubernetes cluster for this tutorial. This is just a map of where your local container skills go after graduation.

The same image you run locally is what teams push to a registry and deploy in the cloud. The provider schedules and restarts your containers; Linux is still doing the heavy lifting underneath.

| Provider | Managed app containers | If you need Kubernetes |
| --- | --- | --- |
| **AWS** | [ECS](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/Welcome.html) (Fargate for managed compute, or EC2 if you want to babysit VMs) | [EKS](https://aws.amazon.com/eks/) |
| **Azure** | [Azure Container Apps](https://learn.microsoft.com/en-us/azure/container-apps/overview) · [Container Instances](https://learn.microsoft.com/en-us/azure/container-instances/container-instances-overview) | [AKS](https://learn.microsoft.com/en-us/azure/aks/what-is-aks) |
| **Google Cloud** | [Cloud Run](https://docs.cloud.google.com/run/docs/overview/what-is-cloud-run) | [GKE](https://docs.cloud.google.com/kubernetes-engine/docs/concepts/kubernetes-engine-overview) |

Your container image doesn't have to match the [cloud provider's host distro](03-linux-distributions.md#industry-context-distributions-made-by-cloud-providers) — just match the CPU architecture, keep secrets out of the image, and store durable data outside disposable container disks.

---

**Next:** [5a. Setting up a development workstation →](05-dev-workstation.md)
