# 5b. Omarchy: a keyboard-first workstation

[← Development workstation](05-dev-workstation.md) · [Home](../README.md) · [Languages →](06-languages.md)

Chapter 5a built a Mint box you operate with a menu and a mouse. This chapter is the other personality: **[Omarchy](https://omarchy.org/)**, an opinionated Arch Linux desktop that would rather you hit `Super + Space` than hunt for a start button.

This is a *client-software* chapter. We will not install a PostgreSQL server here. Databases, if you need them locally, can live in Docker later; the point of this page is the desktop, the package manager, SSH, the firewall, users, editors, and the same client tools from 5a.

Omarchy ships a lot. It does not ship *everything*, and it does not replace its own manual. When a section below is a pointer instead of a recipe, that is on purpose.

## Start here, then steal from the manual

| What | Link |
| --- | --- |
| Homepage | [omarchy.org](https://omarchy.org/) |
| Manual (read this) | [Omarchy Manual](https://omarchy.org/manual/) |
| Install / first boot | [Getting Started](https://omarchy.org/manual/getting-started/) |
| How it feels if you came from Windows or a Mac | [Coming From Mac or Windows](https://omarchy.org/manual/coming-from-mac-or-windows/) |
| Moving around | [Navigation](https://omarchy.org/manual/navigation/) · [Hotkeys](https://omarchy.org/manual/hotkeys/) |
| Packages | [Other Packages](https://omarchy.org/manual/other-packages/) |
| Editors, mise, Docker, `gh` | [Development Tools](https://omarchy.org/manual/development-tools/) |
| Coding agents | [AI](https://omarchy.org/manual/ai/) |
| Updates and snapshots | [Updates](https://omarchy.org/manual/updates/) · [System snapshots](https://omarchy.org/manual/system-snapshots/) |
| Firewall, SSH, encryption | [Security](https://omarchy.org/manual/security/) |
| ISO / source | [Download](https://omarchy.org/#install) · [GitHub: omacom/omarchy](https://github.com/omacom/omarchy) |

If this chapter and the manual disagree, the manual wins. Distros move; this tutorial should not become a fossilized screenshot of someone else's bar.

## Why Omarchy Quattro

Use **Omarchy Quattro** (Omarchy 4). That is the current line of ISOs, not a nostalgic 3.x image you would upgrade on day one anyway.

Quattro is the release that stopped being "Hyprland plus a pile of excellent-but-separate bars, launchers, and lock screens" and became one shell. Status bar, launcher, notifications, lock screen, and system menus live together. New machines should start there. Install from [omarchy.org](https://omarchy.org/#install) and follow [Getting Started](https://omarchy.org/manual/getting-started/).

Chapter 3 called Omarchy a winter-break curiosity. That warning still has a point — this is not the "CS 101 laptop on Monday" default — but the ISO is no longer a ricing kit you debug at midnight. It is a finished desktop with opinions. Mint remains the safer first semester. Omarchy is the "I want the keyboard to be the UI" semester.

## How this is not chapter 5a

Same goal: a computer you can program on. Different animal.

| | **Linux Mint (5a)** | **Omarchy Quattro (5b)** |
| --- | --- | --- |
| Family | Debian → Ubuntu → Mint | [Arch Linux](https://archlinux.org/) (rolling) |
| Packages | `apt` / `.deb` | `pacman`, plus the Omarchy menu / `omarchy pkg` (AUR via *Install → AUR*) |
| Desktop | [Cinnamon](https://github.com/linuxmint/cinnamon) **desktop environment** | [Hyprland](https://hypr.land/) **tiling window manager** + [Quickshell](https://quickshell.org/) |
| Hands | Mouse, application menu, windows you drag | Keyboard first. The mouse is a guest |
| Windows | Overlap, minimize, hunt | Tile. Open two things and they split the screen |
| Updates | Conservative, Ubuntu-LTS-shaped | Rolling; one *Update → Omarchy* path |
| Snapshots | Timeshift | Snapper + Limine; [system snapshots](https://omarchy.org/manual/system-snapshots/) |
| Who picked the apps | You, after a few `apt install`s | The chef. "Omakase" means you eat what they plated, then customize |

Arch vs Debian in one sentence: Mint would rather be the same computer in May that it was in September. Omarchy would rather be current. That is a feature until an upgrade lands on a homework night — which is why snapshots exist.

Keyboard vs mouse in one sentence: on Mint you click Menu → Terminal. On Omarchy you hit `Super + Return`, and until you learn that, the desktop looks like it forgot to ship a UI. It did not. Read [navigation](https://omarchy.org/manual/navigation/) before you declare it broken.

Window manager vs desktop environment: Cinnamon is a whole house (panel, menu, settings, file manager conventions). Hyprland is the person who decides where the furniture goes. Omarchy then furnishes the house so you are not writing a `hyprland.conf` from a wiki at 1 a.m.

## 5b.1 Install Omarchy Quattro

Use the official documents. This paragraph is not an installer.

| Step | Official link |
| --- | --- |
| Read the pitch | [omarchy.org](https://omarchy.org/) |
| Write USB, boot, answer a handful of questions | [Getting Started](https://omarchy.org/manual/getting-started/) |
| Dual-boot next to Windows | [Dual Boot Install](https://omarchy.org/manual/dual-boot-install/) (BitLocker off first) |
| Try in a VM first | [Try on Mac](https://github.com/omacom/try-omarchy) · [Try on Windows](https://github.com/omacom/try-omarchy-windows). On Linux, the ISO is the way in; chapter 4's VirtualBox notes still apply, with an Omarchy ISO instead of Mint |

Practical notes the installer will also tell you, because they are the kind that ruin an evening:

- Turn **Secure Boot** (and TPM, if the manual still says so) off. Omarchy is not a Microsoft-affiliated distro; the firmware handshake is not on your side.
- Full-disk encryption is the default. Bring a **wired or 2.4 GHz keyboard**. Bluetooth will not type the LUKS password at boot.
- Full-disk install **wipes the selected drive**. Dual-boot is the free-space path, not bravery. Backup first.
- After install, the [manual](https://omarchy.org/manual/) is the user guide. This chapter is the CS-workstation overlay.

## 5b.2 First boot: learn Super, then become boring

1. Decrypt the disk, log in. There is no Cinnamon menu waiting for you.
2. Hit **`Super + Space`**. That is Spotlight, the Start menu, Software Manager, and half of Settings. Type to filter. This is how you install software, change themes, and update the machine.
3. Open a terminal with **`Super + Return`**. The default is [Foot](https://codeberg.org/dnkl/foot); Ghostty, Kitty, and Alacritty are a menu pick away — [Terminal](https://omarchy.org/manual/terminal/).
4. Confirm you can sudo, then do the shell homework from 5a:

```bash
whoami
sudo -v
```

Then [Getting started with the Unix shell](https://github.com/amitsk/learning-shell/blob/main/scripts/getting_started.md) until `nano` saves without a search query.

Give tiling a day before you start floating every window (`Super + T` toggles that, if you must). [Coming From Mac or Windows](https://omarchy.org/manual/coming-from-mac-or-windows/) is the translation table: `Super` is Cmd/Win, `Super + K` lists every hotkey, and there is no dock to click.

Run **Update → Omarchy** from the menu before you customize anything. Rolling distros are only "always patched" if you actually update. Snapshots happen as part of that path; see [updates](https://omarchy.org/manual/updates/).

## 5b.3 Packages: the grocery store, but it is pacman

On Mint, software is `apt`. On Omarchy, the grocery store is **pacman**, with a polite front door.

- Everyday install: Omarchy menu → **Install → Package**, or `omarchy pkg add some-package`. Guide: [Other Packages](https://omarchy.org/manual/other-packages/).
- AUR: **Install → AUR**. The AUR is "anyone can upload," closer to npm than to Ubuntu Main. Fun; not sacred.
- Raw pacman, when you want it: [ArchWiki: pacman](https://wiki.archlinux.org/title/Pacman).

The loop, translated from chapter 5a:

```bash
# Do not casually run pacman -Syu / yay -Syu.
# Omarchy wants Update → Omarchy (or `omarchy update`) so snapshots
# and migrations ride along. The guard will scold you. Listen to it.
omarchy update

omarchy pkg add git curl wget
omarchy pkg drop some-package
```

`omarchy pkg add` is "install this." *Update → Omarchy* is "eat everything new, and take a save point first." Skipping the Omarchy updater to feel more Arch is how you miss a migration and then write a Discord message.

The [Omarchy CLI](https://omarchy.org/manual/omarchy-cli/) (`omarchy`, then tab-complete) is the same system the menu drives. Agents can call it. That is not an accident.

**Mint users:** there is no `apt search` habit to unlearn so much as a new front-end. The package still has a name. You still should not mix random third-party repos like trading cards. Omarchy's own repos plus Arch core/extra/multilib are the blessed path; AUR is opt-in.

## 5b.4 Basic tools, git, and gh

A stock Omarchy install is already a developer box: git, a terminal, Neovim, Docker pieces, lazygit, a GitHub CLI stub, mise, a firewall. You are not starting from a blank Mint ISO.

Still configure git as yourself:

```bash
git --version
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
```

### GitHub CLI

[GitHub CLI](https://cli.github.com/) (`gh`) is how you talk to GitHub without opening a browser. On Omarchy it is wired as a lazy-loading stub: the first `gh` installs it. Then:

```bash
gh auth login
gh --version
```

Official: [Development Tools → GitHub CLI](https://omarchy.org/manual/development-tools/#github-cli) · [gh manual](https://cli.github.com/manual/).

Same pitch as [chapter 5a](05-dev-workstation.md#git-and-the-github-cli), only more so: this desktop is built for agents, and agents are much better at `gh` than at a GitHub tab. Stable flags, `--json`, `gh pr create`, `gh run view`. [Lazygit](https://omarchy.org/manual/tuis/#lazygit) is there if *you* want a TUI. `gh` is there so the harness can open the pull request.

### Terminals

`Super + Return` is "open a terminal," the way `Ctrl+Alt+T` was on Mint. Foot is the light default. This author still likes [Ghostty](https://ghostty.org/) when the GPU is willing — *Install → Terminal*, then *Setup → Defaults → Terminal*. Details: [Omarchy terminal](https://omarchy.org/manual/terminal/).

Optional, already in the neighborhood: [shell tools](https://omarchy.org/manual/shell-tools/) (fzf, zoxide, ripgrep), [starship](https://starship.rs/) if you want the prompt from the shell tutorial, tmux via `Super + Alt + Return`.

## 5b.5 SSH server: off until you ask

Mint needed `apt install openssh-server`. Omarchy already has OpenSSH; the *service* is off, and the firewall does not expose 22 until you turn SSH on.

Enable it from **Setup → Security → SSHD** (that opens port 22, rate-limited). Docs: [Security](https://omarchy.org/manual/security/). Background: [ArchWiki: OpenSSH](https://wiki.archlinux.org/title/OpenSSH).

```bash
ip -brief addr
# from the other computer:
ssh youruser@192.168.1.42
```

Then keys, same as 5a: [learning-shell: Using SSH](https://github.com/amitsk/learning-shell/blob/main/scripts/getting_started.md#6-using-ssh-to-connect-to-a-remote-server). Do not disable passwords until a key login has worked twice. Keep it on the LAN unless you enjoy being scanned.

## 5b.6 Firewall: already on, please do not "fix" it

[UFW](https://wiki.archlinux.org/title/Uncomplicated_Firewall) is enabled by default. Incoming is blocked except [LocalSend](https://localsend.org/). SSH stays closed until the previous section. Docker is locked down with [ufw-docker](https://github.com/chaifeng/ufw-docker) so a container does not accidentally become a public server. Again: [Security](https://omarchy.org/manual/security/).

```bash
sudo ufw status verbose
```

You should see a firewall that is already doing the job 5a made you type by hand. Do not `ufw disable` because a blog said Linux is safe on the inside. Do not `ufw allow 5432` unless you *intend* other machines to talk to a database you have not even installed in this chapter.

## 5b.7 Users and groups

Same reasons as 5a: homework vs admin, practicing permissions, not inflating the main account. Concepts: [learning-shell: User and Group Management](https://github.com/amitsk/learning-shell/blob/main/scripts/users_groups.md). Arch reference: [ArchWiki: Users and groups](https://wiki.archlinux.org/title/Users_and_groups).

Debian's `adduser` is a friendly script. Arch's native tool is `useradd`. Sudo lives on the **`wheel`** group, not a group named `sudo`.

```bash
sudo useradd -m -s /bin/bash student
sudo passwd student
sudo groupadd cs101
sudo usermod -aG cs101 student
# sudo for that user (think twice):
sudo usermod -aG wheel student
id student
```

The `-a` in `-aG` is still "append." Forget it and you replace their supplementary groups with just the one you named. That rite of passage is distro-independent.

```bash
su - student
pwd
exit
```

Omarchy also has *Setup → Reset Computer* for handing a machine to someone else, and a first-boot "installing for another owner" path. Those are not homework accounts; they are [security](https://omarchy.org/manual/security/) features. Use `useradd` for the CS-101 dummy user.

## 5b.8 Database clients (no server in this chapter)

**No PostgreSQL server install here.** 5a walked through `apt install postgresql` as a host service. On Omarchy, if you need a local engine, prefer **Install → Development → Docker DB** from the menu and read [Development Tools → Docker](https://omarchy.org/manual/development-tools/#docker). This section is clients: things that *connect*.

GUI:

- **[DBeaver](https://dbeaver.io/)** — [download](https://dbeaver.io/download/). Install via *Install → Package* / AUR, or follow their Linux instructions.

Terminal:

- **[pgcli](https://www.pgcli.com/)** — [dbcli/pgcli](https://github.com/dbcli/pgcli)
- **[mycli](https://www.mycli.net/)** — [dbcli/mycli](https://github.com/dbcli/mycli)
- **[usql](https://github.com/xo/usql)** — one CLI, many SQL dialects

Utility, not a client:

- **[sq](https://sq.io/)** — jq-shaped queries against databases and files. [Overview](https://sq.io/docs/overview/) · [install](https://sq.io/docs/install/). Use it to wrangle; use DBeaver or pgcli to browse.

Arch does not ship a tiny `postgresql-client` package the way Debian does; `psql` lives with the server package. Prefer pgcli/usql/DBeaver, or talk to a database in Docker. Point clients at that container, a course server, or a cloud instance. Do not UFW-open 5432 for fun.

## 5b.9 REST clients

Same set as 5a, Arch-shaped installs. Prefer the project docs over a pacman line copied from a blog.

### GUIs

- **[Insomnia](https://insomnia.rest/)** — [docs](https://developer.konghq.com/insomnia/)
- **[Postman](https://www.postman.com/)** — [docs](https://learning.postman.com/docs/introduction/overview/)
- **[Bruno](https://www.usebruno.com/)** — collections as files in git. [docs](https://docs.usebruno.com/)

*Install → Package* or *Install → AUR* as needed. One GUI is enough.

### curl, HTTPie, xh

[curl](https://curl.se/) is already there. Learn it from the source, not from a Slack screenshot:

- [HTTP scripting with curl](https://curl.se/docs/httpscripting.html)
- [Everything curl](https://everything.curl.dev/) (the [HTTP](https://everything.curl.dev/http) chapters)
- [learning-shell](https://github.com/amitsk/learning-shell) once you want this in a pipeline

```bash
curl -I https://example.com
```

Friendlier CLIs: **[HTTPie](https://httpie.io/docs/cli)** and its Rust clone **[xh](https://github.com/ducaale/xh)**. `xh` is a package on Arch (`omarchy pkg add xh`). Agents will still paste `curl`. You can type `xh`.

## 5b.10 jq and yq

JSON from APIs, YAML from Compose and every GitHub Action you will ever debug.

- **[jq](https://jqlang.org/)** — [tutorial](https://jqlang.org/tutorial/) · [manual](https://jqlang.org/manual/). `omarchy pkg add jq`
- **[yq](https://mikefarah.gitbook.io/yq/)** — [mikefarah/yq](https://github.com/mikefarah/yq), the Go one. Confirm the binary before you trust a filter; the Python project of the same name is a different animal.

```bash
curl -s https://httpbin.org/get | jq '.headers'
```

`curl` fetches, `jq` picks. Same story as 5a; different grocery store.

## 5b.11 Editors and coding agents

Omarchy's default editor is **[Neovim](https://omarchy.org/manual/neovim/)**. If that is not this semester's personality, *Install → Editor* offers VS Code, Cursor, Zed, Sublime, Helix, Vim, Emacs. Set the default under *Setup → Defaults → Editor*. Details: [Development Tools](https://omarchy.org/manual/development-tools/).

VS Code Linux background, if you pick it: [Visual Studio Code on Linux](https://code.visualstudio.com/docs/setup/linux). Language extensions still wait for [section 6](06-languages.md#vs-code-extensions).

IntelliJ: [install guide](https://www.jetbrains.com/help/idea/installation-guide.html) · [Toolbox](https://www.jetbrains.com/toolbox-app/). Arch/AUR if you want it in pacman; Toolbox if you want JetBrains to update itself.

### AI coding CLIs

This is one of the places Omarchy is not "Mint plus different wallpaper." Agents are first-class: lazy-loaded launchers, a default-agent picker, crash dumps that can go to the agent, a skill for editing the desktop itself. Read **[AI](https://omarchy.org/manual/ai/)** instead of pasting install scripts. The table of `claude`, `codex`, `grok`, and friends lives there and will outlive this sentence.

The same syllabus warning as 5a still applies: check the course AI policy before an agent invents a Fibonacci heap. Use them to learn, debug, and build personal projects.

*Setup → Security → Passwordless Sudo* exists because agents hate password prompts. It is a timed hole in `sudo`. Know what you are turning on: [Security](https://omarchy.org/manual/security/).

## 5b.12 Staying updated without superstition

Do not `pacman -Syu` for the full system because you saw it on the ArchWiki. Use **Update → Omarchy** or `omarchy update`. That path takes a snapshot, updates Omarchy packages, runs migrations, then updates the rest. Direct upgrades are how you skip the save point. [Updates](https://omarchy.org/manual/updates/).

If an update goes sideways, boot a snapshot from Limine and restore: [System snapshots](https://omarchy.org/manual/system-snapshots/). That rewinds `/`, not `~/`. Git remotes still matter.

```bash
hostnamectl
cat /etc/os-release
uname -r
```

Stay on the **stable** channel unless you enjoy edge. Firmware has its own menu entry (*Update → Firmware*).

## 5b.13 A reasonable "done" checklist

```bash
# You can move
# Super + Space opens the menu; Super + Return opens a terminal

# Packages / identity
git --version
gh --version            # first run may install the stub

# SSH and firewall
systemctl is-active sshd    # only after you enabled SSHD
sudo ufw status

# Practice user
id
id student

# Clients, not a local postgres unit
jq --version            # if you installed jq
# dbeaver / pgcli / xh: whatever you actually added

# Editor
nvim --version          # default
# code --version        # if you installed VS Code
```

There is no `systemctl is-active postgresql` on this list. That is the point of a client-only chapter. If those succeed, you have an Omarchy workstation. Everything else is ricing, and the manual is better at ricing than we are.

## 5b.14 Extra, still useful

- **Languages and compilers:** same as Mint — [section 6](06-languages.md). Omarchy already likes [mise](https://mise.jdx.dev/); *Install → Development* in the menu is the shortcut. Distro packages are still `pacman`/`omarchy pkg add`, not `apt`.
- **Docker:** already part of the desktop. [Development Tools → Docker](https://omarchy.org/manual/development-tools/#docker). The `docker` group is still nearly root; Omarchy leaves you out of it until you opt in.
- **Backups:** snapshots for the *system*; copy `~/` (projects, `.ssh`, `.gitconfig`) separately. A root rollback does not restore the homework you deleted in `~/Work`.
- **Shell fluency:** [learning-shell](https://github.com/amitsk/learning-shell) plus Omarchy's own [shell tools](https://omarchy.org/manual/shell-tools/).
- **When this chapter is silent:** [the Omarchy Manual](https://omarchy.org/manual/). Themes, bar, monitors, NVIDIA, Mac hardware, Windows VM, gaming — all real, none of them a CS-workstation prerequisite.

Mint is still the default first desktop in this tutorial. Omarchy is the one you pick when the menu-and-mouse path feels like someone else's computer. Either way, [section 6](06-languages.md) is where the machine starts compiling homework.

---

**Next:** [Languages and toolchains →](06-languages.md)
