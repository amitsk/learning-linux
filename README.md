# Setting up a Linux desktop

A practical tutorial for **new programmers** and **CS students** who want a real Linux workstation, not a weekend of forum archaeology.

Linux is the OS that quietly runs most of the internet, most of the world's supercomputers, and that one lab machine nobody is allowed to reboot. You do not need to memorize man pages before breakfast. You do need a machine you can break, fix, and program on.

This guide walks you from "what even is a distro?" to a Linux Mint Cinnamon box with SSH, a firewall, extra users, PostgreSQL, language toolchains, and a sensible set of developer tools.

**Companion tutorial:** the command line is a skill, not a personality. Work through [amitsk/learning-shell](https://github.com/amitsk/learning-shell) alongside this guide. Whenever this tutorial says "open a terminal," that repo is the homework.

## Who this is for

- You are learning to program, or you are in a CS course that assumes you "just use Linux."
- You want a desktop you can actually live in (browser, editor, terminal, database), not a server you SSH into from a Windows laptop forever.
- You would rather follow official docs than a 47-minute YouTube video that starts with "hey guys."

You do **not** need prior Linux experience. Curiosity and a USB stick will do.

## How to use this tutorial

Read the sections in order the first time. After that, treat them as a map:

| Section | What you get |
| --- | --- |
| [1. Basics of Linux](docs/01-linux-basics.md) | Distros (Fedora, Ubuntu, Linux Mint), desktop flavors (GNOME, XFCE, Budgie, Cinnamon), and where the shell tutorial fits |
| [2. How Linux is put together](docs/02-linux-design.md) | The kernel vs the distro, userspace tooling, and diagrams of the stack |
| [3. Development workstation](docs/03-dev-workstation.md) | Linux Mint Cinnamon install, `apt`, updates, SSH, UFW, users/groups, PostgreSQL, editors and AI coding tools |
| [4. Languages and toolchains](docs/04-languages.md) | mise for Java/Python/Node/Go, uv, Cargo, Volta/nvm, GCC and Clang, VS Code extensions |
| [5. Used laptops and Linux resurrection](docs/05-used-laptops.md) | Buying second-hand hardware and bringing an old laptop back from the dead |

Prefer **links over copies**. Official installers change; this tutorial should not become a fossilized screenshot of Ubuntu 14.04.

## Suggested path for a first weekend

1. Skim [section 1](docs/01-linux-basics.md) and pick **Linux Mint Cinnamon** unless you have a good reason not to.
2. Skim [section 2](docs/02-linux-design.md) so "kernel" stops sounding like a food blog.
3. Install Mint using the official guide, then follow [section 3](docs/03-dev-workstation.md) on the new machine.
4. Install compilers and language runtimes with [section 4](docs/04-languages.md).
5. Start [Getting started with the Unix shell](https://github.com/amitsk/learning-shell/blob/main/scripts/getting_started.md).
6. If you are installing on a used box, read [section 5](docs/05-used-laptops.md) *before* you buy the laptop.

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
