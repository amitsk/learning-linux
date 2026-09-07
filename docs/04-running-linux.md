# 4. Running Linux: virtual machines and containers

[← Choosing a distribution](03-linux-distributions.md) · [Home](../README.md) · [Development workstation →](05-dev-workstation.md)

You can learn Linux before replacing your computer's operating system. A virtual machine gives you a full Linux system in a window; a container gives you an isolated environment for Linux programs. Choose based on what you want to practice.

## Choose an environment

| Approach | Good for | What to expect |
| --- | --- | --- |
| Dedicated install | Daily Linux desktop use and hardware setup | Linux controls the machine; back up existing data before installing. |
| Dual boot | Keeping another OS alongside Linux | Choose an OS at startup. Partitioning and boot setup need care and backups. |
| Virtual machine (VM) | Learning installation, desktops, services, and administration | A full guest OS with its own kernel and virtual disk, sharing the host's RAM and CPU. |
| WSL 2 on Windows | Shell tools and development alongside Windows apps | A Linux kernel in a managed VM, integrated with Windows; setup requires supported Windows and appropriate permissions. |
| Docker or Podman container | Trying command-line tools and packaging applications | Isolated processes and a user-space filesystem using a shared Linux kernel. |

For the full workstation tutorial, use a dedicated Mint installation or a Mint VM. Containers are useful for the shell exercise below, but the later desktop, boot, UFW, and systemd instructions assume a full OS.

## Install Linux in VirtualBox

Your existing OS is the **host**; Linux inside the VM is the **guest**. The VM's virtual disk is normally a file on the host. The guest installer sees that virtual disk as its installation target.

1. Install [VirtualBox](https://www.virtualbox.org/) for your host OS. Check its supported host and guest architectures. For a typical Intel/AMD PC, use an x86-64 Linux ISO. Hardware virtualization (Intel VT-x or AMD-V) may need enabling in firmware.
2. Download and verify the [Linux Mint Cinnamon ISO](https://linuxmint.com/download.php), following the [Mint verification guide](https://linuxmint-installation-guide.readthedocs.io/en/latest/verify.html). An ISO is an installer disc image; you can attach it directly to a VM without making a USB stick.
3. Create a new Linux VM and select the ISO. As a starting point on a host with at least 16 GB RAM, allocate **2 virtual CPUs, 4 GB RAM, and a 40 GB dynamically allocated virtual disk**. Leave enough resources for the host; development tools may need more disk space later.
4. Keep the default **NAT** network for initial internet access. If offered unattended installation, skip it to practice the normal Mint installer. Start the VM and follow the [Mint installation steps](https://linuxmint-installation-guide.readthedocs.io/en/latest/install.html).
5. Install onto the new virtual disk. The installer's “erase disk” option applies to that VM disk in this setup; confirm its size and do not attach host physical disks. Restart and eject the ISO if the installer boots again.
6. Log in, install updates, and shut down the guest cleanly. Take a VM snapshot so you can return to this working state. Snapshots help undo experiments; keep separate backups of important projects.

The [VirtualBox first-steps guide](https://docs.oracle.com/en/virtualization/virtualbox/7.1/user/Introduction.html) covers the wizard and snapshots. [Working with VMs](https://docs.oracle.com/en/virtualization/virtualbox/7.2/user/working-with-vms.html) covers virtual disks and networking. Guest Additions can improve resizing and desktop integration; follow the instructions for your VirtualBox version if needed.

Then continue with [chapter 5's first-boot steps](05-dev-workstation.md#52-first-boot-become-a-boring-up-to-date-machine) **inside the guest**. With NAT, another computer usually cannot connect directly to the guest's private address. For the later SSH exercise, add a VirtualBox NAT forwarding rule from host address `127.0.0.1`, host port `2222`, to guest port `22`, then connect from the host:

```bash
ssh -p 2222 youruser@127.0.0.1
```

Enable the guest's SSH service and firewall allowance first, as chapter 5 describes. Binding the forwarding rule to localhost makes this a host-to-guest exercise.

## Other VM tools and WSL

On a Linux host, [virt-manager](https://virt-manager.org/) provides a graphical interface to KVM/QEMU: create a VM, attach an ISO, allocate resources, and run the installer. On macOS, [UTM](https://mac.getutm.app/) is another option. For Apple Silicon, choose an ARM64 guest such as an appropriate Ubuntu or Debian image and UTM's virtualization mode. Emulating an Intel/AMD guest is a different, generally slower path; an x86-64 Mint ISO is not an ARM64 installer.

On supported Windows systems, [install WSL](https://learn.microsoft.com/en-us/windows/wsl/install) by opening PowerShell as administrator and running:

```powershell
wsl --install
```

Restart if prompted, then create the Linux user when the distribution launches. WSL 2 is useful for shells, compilers, and some graphical apps, though its integration differs from logging into a complete Cinnamon desktop. On a managed school or work computer, installation may require the administrator to enable it.

## Try Linux user space in Docker

A container image supplies an application's files, libraries, and possibly a distro's shell and package manager. A running container is a set of isolated processes. Unlike a VM, it does not boot its own kernel. An Ubuntu container can therefore run on a Fedora Linux host. Docker Desktop runs Linux containers through a Linux VM on macOS and Windows. See [Docker's container explanation](https://docs.docker.com/get-started/docker-concepts/the-basics/what-is-a-container/) and [Docker Desktop](https://docs.docker.com/desktop/).

Install Docker using the [official instructions](https://docs.docker.com/get-started/get-docker/) for your host, start it, and confirm `docker version` can contact the server. Then run this on the **host**:

```bash
docker run --rm -it ubuntu:24.04 bash
```

Docker downloads the image if needed and opens Bash inside a new container. `-it` gives you an interactive terminal; `--rm` removes the container when it exits. Inside it, try:

```bash
cat /etc/os-release   # Ubuntu user-space identity
uname -r             # the shared Linux kernel, not an Ubuntu kernel from the image
apt update
apt install -y curl
curl --version
exit
```

This image starts the shell as root, so the example does not use `sudo`. That differs from the regular user you create on your workstation. The installed `curl` and other container changes disappear when this disposable container exits; the downloaded image remains cached. For reusable application setup, build an image with a **Dockerfile**; for persistent data, use a [volume](https://docs.docker.com/engine/storage/volumes/).

This is a small command-line environment, with no Cinnamon desktop and usually no systemd running as PID 1. It is well suited to trying packages, builds, or a database process. [Podman](https://podman.io/docs) is an alternative container tool with a similar `podman run --rm -it ubuntu:24.04 bash` workflow once installed and configured.

## Industry context: The same container model in the cloud

*(You do **not** need a cloud account, a credit card, or a Kubernetes cluster for this tutorial. This section is just a preview of where your container knowledge travels after graduation.)*

The image you build locally can also become a cloud deployment artifact. Typically you build and test it, push it to a registry, then configure a service to pull it and run containers. The provider schedules and restarts your application; Linux remains underneath. Managed runtimes may add VM or sandbox isolation, so the exact host arrangement varies.

| Provider | Managed application containers | If you need Kubernetes |
| --- | --- | --- |
| **AWS** | [Elastic Container Service (ECS)](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/Welcome.html) orchestrates containers; with Fargate, AWS manages the compute, while EC2-backed deployments give you responsibility for the instances. | [Elastic Kubernetes Service (EKS)](https://aws.amazon.com/eks/) |
| **Azure** | [Azure Container Apps](https://learn.microsoft.com/en-us/azure/container-apps/overview) runs containerized applications with managed scaling; [Container Instances](https://learn.microsoft.com/en-us/azure/container-instances/container-instances-overview) also runs container groups without provisioning VMs. | [Azure Kubernetes Service (AKS)](https://learn.microsoft.com/en-us/azure/aks/what-is-aks) |
| **Google Cloud** | [Cloud Run](https://docs.cloud.google.com/run/docs/overview/what-is-cloud-run) runs managed container services and jobs. | [Google Kubernetes Engine (GKE)](https://docs.cloud.google.com/kubernetes-engine/docs/concepts/kubernetes-engine-overview) |

These services fill related roles; their networking, scaling, and workload constraints differ. A Linux container still supplies user space rather than a separate bootable OS. It need not use the [provider's distribution](03-linux-distributions.md#distributions-made-by-cloud-providers) as its base image. Match the image's CPU architecture and runtime requirements to the service, configure secrets and ports, and keep durable data outside disposable container filesystems.

You do not need a cloud account for this chapter's exercises. Local practice gives you the foundation for deploying later; cloud services and their storage can incur charges.

---

**Next:** [Setting up a development workstation →](05-dev-workstation.md)
