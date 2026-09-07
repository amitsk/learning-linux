# Setting up a Linux desktop

A practical tutorial for **new programmers** and **CS students** who want a real Linux workstation, not a weekend of forum archaeology.

Linux powers cloud servers, Android devices, embedded systems, supercomputers, and developer desktops. You do not need to memorize man pages before breakfast. You do need a machine you can break, fix, and program on.

This guide walks you from "what even is a distro?" to a Linux Mint Cinnamon box with SSH, a firewall, extra users, PostgreSQL, language toolchains, and a sensible set of developer tools.

**Companion tutorial:** the command line is a skill, not a personality. Work through [amitsk/learning-shell](https://github.com/amitsk/learning-shell) alongside this guide. Whenever this tutorial says "open a terminal," that repo is the homework.

## Who this is for

- You are learning to program, or you are in a CS course that assumes you "just use Linux."
- You want a desktop you can actually live in (browser, editor, terminal, database), not a server you SSH into from a Windows laptop forever.
- You would rather follow official docs than a 47-minute YouTube video that starts with "hey guys."

You do **not** need prior Linux experience. Curiosity and a computer that can run a Linux VM will do. A USB stick is useful if you choose a hardware install.

## How to use this tutorial

Read the sections in order the first time. After that, treat them as a map:

| Section | What you get |
| --- | --- |
| [1. Basics of Linux](docs/01-linux-basics.md) | Where Linux is used, essential vocabulary, and where the shell tutorial fits |
| [2. How Linux is put together](docs/02-linux-design.md) | The kernel vs the distro, userspace tooling, and diagrams of the stack |
| [3. Choosing a Linux distribution](docs/03-linux-distributions.md) | Debian, Ubuntu, Mint, Fedora, desktop choices, cloud-provider distros, and Omarchy |
| [4. Running Linux: virtual machines and containers](docs/04-running-linux.md) | VirtualBox and alternatives, WSL, Docker, and cloud container services |
| [5. Development workstation](docs/05-dev-workstation.md) | Linux Mint Cinnamon install, `apt`, updates, SSH, UFW, users/groups, PostgreSQL, editors and AI coding tools |
| [6. Languages and toolchains](docs/06-languages.md) | mise for Java/Python/Node/Go, uv, Cargo, Volta/nvm, GCC and Clang, VS Code extensions |
| [7. Used laptops and Linux resurrection](docs/07-used-laptops.md) | Buying second-hand hardware and bringing an old laptop back from the dead |

Prefer **links over copies**. Official installers change; this tutorial should not become a fossilized screenshot of Ubuntu 14.04.

## Suggested path for a first weekend

1. Read [basics](docs/01-linux-basics.md) and [Linux design](docs/02-linux-design.md) for the vocabulary.
2. Pick a distro in [chapter 3](docs/03-linux-distributions.md); this tutorial uses **Linux Mint Cinnamon**.
3. Choose a VM or hardware install in [chapter 4](docs/04-running-linux.md). If buying a used laptop, read [chapter 7](docs/07-used-laptops.md) before shopping.
4. Follow [workstation setup](docs/05-dev-workstation.md) on your installed Linux system, then add [language toolchains](docs/06-languages.md).
5. Work through [Getting started with the Unix shell](https://github.com/amitsk/learning-shell/blob/main/scripts/getting_started.md) alongside those steps.

## What you will have at the end

- A Linux desktop with Cinnamon, updates, and basic CLI tools
- An SSH server behind UFW, with extra users and groups for practice
- A local PostgreSQL server you created yourself
- Links to VS Code, IntelliJ IDEA, Codex, Grok Build, and Claude Code
- Compilers (GCC/Clang) and runtimes via mise (Java, Python, Node, Go), plus uv and Cargo
- Enough mental model of Linux to not panic when a CS assignment says "use the terminal"

## License and contributions

This is a living tutorial. If a distro moves a download page, open a PR. If a joke is too dad-tier, also open a PR. We can negotiate.

---

**Next:** [Basics of Linux →](docs/01-linux-basics.md)
