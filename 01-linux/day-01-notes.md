# Day 01 — Linux Fundamentals

> Phase 1 · `01-linux/day-01-notes.md`
> Goal: understand what Linux is and get comfortable running your first commands.

Directory for today:

```
01-linux/
├── setup-server.sh      # (built on Day 07)
├── permissions-lab.md   # (built on Day 04)
└── day-01-notes.md      # this file
```

---

## Part 1 — Theory

### 1. What is Linux?

Linux is an **open-source operating system** — the software layer that sits between your
hardware (CPU, memory, disk, network) and the applications you run. It manages resources,
runs programs, handles files, and controls devices.

- Created by **Linus Torvalds in 1991**; free and open source (anyone can read/modify the code).
- Technically, "Linux" is just the **kernel**. A usable system = kernel + tools + libraries = a **distribution** (see #3).
- Runs almost everything: web servers, the cloud (AWS/Azure/GCP mostly run Linux), Android phones,
  routers, smart TVs, supercomputers, Docker containers, Kubernetes nodes.

**Why DevOps uses Linux:** it's free, scriptable, stable, secure, and it's what servers and
containers run on. Nearly every DevOps tool (Docker, Kubernetes, Ansible, Terraform) is built for it.

### 2. The Linux Kernel

The **kernel** is the core of the OS — the first program that loads and the one with full control
of the hardware. It handles:

- **Process management** — deciding which program runs on the CPU and when.
- **Memory management** — allocating RAM to programs.
- **Device management** — talking to disks, network cards, USB, etc. via drivers.
- **System calls** — the controlled "API" applications use to ask the kernel to do things
  (open a file, send data over the network).

You can see your kernel version with `uname -r`. Example: `5.15.0-91-generic`
- `5` = major version, `15` = major revision, `0` = patch, `91-generic` = the distro's build.

Linux uses a **monolithic kernel** (most core services run in one kernel space), which is fast.

### 3. Linux Distributions

A **distribution ("distro")** bundles the Linux kernel with a package manager, system tools,
libraries, and default configuration to make a complete, usable OS. Major families:

| Family | Examples | Package manager |
|--------|----------|-----------------|
| **Debian** | Debian, **Ubuntu**, Linux Mint | `apt` / `.deb` |
| **Red Hat** | RHEL, Fedora, CentOS/Rocky/Alma | `dnf`/`yum` / `.rpm` |
| **SUSE** | openSUSE, SLES | `zypper` / `.rpm` |
| **Arch** | Arch, Manjaro | `pacman` |

They all share the same kernel — the differences are the tools, package format, release cycle,
and defaults. For DevOps, **Ubuntu** and **RHEL-family** are the two you'll meet most.

### 4. Ubuntu

**Ubuntu** is a Debian-based distribution and the most popular Linux for beginners and servers.

- Uses the **`apt`** package manager (`.deb` packages).
- **LTS (Long-Term Support)** releases (e.g., 20.04, 22.04, 24.04) get **5 years of support** —
  these are what you run on servers because they're stable. LTS versions come out every 2 years in April.
- Huge community and documentation, so problems are easy to google.
- This is the distro you'll install in your VM on Day 02.

### 5. Linux Server vs Desktop

| | **Desktop** | **Server** |
|--|-------------|------------|
| Interface | GUI (graphical desktop) | Usually **headless** — no GUI, just a terminal |
| Accessed via | Monitor, keyboard, mouse | **SSH** over the network (Day 19) |
| Purpose | Daily use, browsing, coding | Hosting apps, databases, websites 24/7 |
| Resources | Spends RAM/CPU on graphics | Every resource goes to the workload |

As a DevOps engineer you work almost entirely with **servers**, controlling them through the
command line over SSH. That's why mastering the CLI matters more than any GUI.

### 6. Shell vs Terminal

These are often confused — they're different things:

- **Terminal** = the *program/window* that gives you a text interface (e.g., GNOME Terminal,
  the black screen). It just displays text and takes your keystrokes. Historically it was a
  physical "terminal" device.
- **Shell** = the *program that interprets your commands*. You type a command, the shell reads
  it, runs it, and returns the output. Common shells: **bash** (default on most Linux), **zsh**, `sh`, `fish`.

Analogy: the **terminal is the phone**, the **shell is the person on the other end** who
understands and acts on what you say. Check your shell with:

```bash
echo $SHELL      # e.g. /bin/bash
```

### 7. The Root User

**root** is the **superuser** — the all-powerful administrator account.

- Its user ID is always **UID 0**.
- It can read, modify, or delete *any* file, install software, and change system settings —
  no permission checks apply to root.
- Its home directory is `/root` (not `/home/root`).
- **Danger:** because root bypasses all safety checks, a typo can wipe the system
  (the infamous `rm -rf /`). Best practice: **don't log in as root for daily work** — use a
  normal user and elevate with `sudo` only when needed (see #8).

### 8. sudo

**`sudo`** = "**s**uper**u**ser **do**". It lets a permitted normal user run a **single command**
with root privileges, instead of logging in as root full-time.

```bash
apt update           # ❌ fails: "Permission denied" (needs admin rights)
sudo apt update      # ✅ runs as root, just for this one command
```

- It asks for **your** password (not root's) the first time, then remembers for ~15 minutes.
- Who's allowed is controlled by the **`/etc/sudoers`** file and the **`sudo`** group. On Ubuntu,
  the first user you create is added to the `sudo` group automatically.
- Every `sudo` command is **logged** (in `/var/log/auth.log`), which is why it's safer and more
  auditable than sharing the root password.

---

## Part 2 — Hands-On

Run each command, read the output, and note what it tells you. Example outputs below are typical
for an Ubuntu server — yours will differ slightly.

### `uname -a` — system & kernel information

Prints kernel and system details. `-a` means "all".

```bash
$ uname -a
Linux ubuntu-server 5.15.0-91-generic #101-Ubuntu SMP Tue Nov 14 13:29:11 UTC 2023 x86_64 x86_64 x86_64 GNU/Linux
```

Field by field:

| Value | Meaning |
|-------|---------|
| `Linux` | Kernel name |
| `ubuntu-server` | Hostname (the machine's name) |
| `5.15.0-91-generic` | Kernel release/version |
| `#101-Ubuntu SMP Tue Nov 14 ...` | Build number + date; **SMP** = supports multiple CPUs |
| `x86_64` | Machine hardware (64-bit Intel/AMD) |
| `x86_64` | Processor type |
| `x86_64` | Hardware platform |
| `GNU/Linux` | Operating system |

Handy variants: `uname -r` (kernel version only), `uname -m` (architecture only).

### `hostname` — the machine's name

```bash
$ hostname
ubuntu-server
```

This is the name that identifies the machine on a network. You'll see it in your shell prompt
(`user@ubuntu-server:~$`). It can be changed with `hostnamectl set-hostname newname`.

### `whoami` — who am I logged in as?

```bash
$ whoami
devops
```

Prints your **current effective username**. Try it after `sudo` to see the difference:

```bash
$ sudo whoami
root
```

### `id` — your user, group, and all group memberships

```bash
$ id
uid=1000(devops) gid=1000(devops) groups=1000(devops),27(sudo),4(adm),24(cdrom)
```

Field by field:

| Part | Meaning |
|------|---------|
| `uid=1000(devops)` | Your **user ID** and name. Regular users start at 1000; **root is 0** |
| `gid=1000(devops)` | Your **primary group** ID and name |
| `groups=...` | **All groups** you belong to. `27(sudo)` here means you can use `sudo` |

This is the fastest way to check "can this user run sudo?" — look for `sudo` (Ubuntu) or `wheel` (RHEL) in the groups.

### `uptime` — how long the system has been running (+ load)

```bash
$ uptime
 14:32:05 up 2 days,  3:14,  2 users,  load average: 0.15, 0.10, 0.05
```

Field by field:

| Value | Meaning |
|-------|---------|
| `14:32:05` | Current time |
| `up 2 days, 3:14` | System has been running 2 days, 3 hours, 14 minutes (since last boot) |
| `2 users` | Number of users currently logged in |
| `load average: 0.15, 0.10, 0.05` | Average system load over the **last 1, 5, and 15 minutes** |

**Understanding load average** (important!): it's roughly the number of processes waiting to run.
Compare it to your **CPU core count**:
- On a **1-core** machine: `1.00` = fully busy, `2.00` = overloaded (twice the work it can handle), `0.15` = mostly idle.
- On a **4-core** machine: `4.00` = fully busy. So `0.15` here means the server is almost idle.

Rule of thumb: **load average ≈ number of cores** is "fully utilized." Above that, tasks are queuing.

### `date` — current date and time

```bash
$ date
Mon Aug 24 14:32:05 UTC 2026
```

Shows day, date, time, **timezone (UTC here)**, and year. Servers are very often set to **UTC**
so logs across regions line up. You can format it:

```bash
$ date "+%Y-%m-%d %H:%M:%S"
2026-08-24 14:32:05
```

That `+%Y-%m-%d` format is exactly what you'll use to timestamp backups on Day 13.

### `ls` — list directory contents

```bash
$ ls
Desktop  Documents  Downloads  day-01-notes.md
```

Lists files and folders in your current directory. Most-used options:

```bash
$ ls -l      # long format: permissions, owner, size, date
-rw-r--r-- 1 devops devops 1240 Aug 24 14:30 day-01-notes.md

$ ls -a      # show hidden files (those starting with a dot, like .bashrc)
$ ls -lh     # long format with human-readable sizes (1.2K, 5.4M)
$ ls -la     # combine: long + all/hidden — the everyday favorite
```

Reading the `-l` line: `permissions | links | owner | group | size | date | name`.
You'll decode the permission part (`-rw-r--r--`) fully on **Day 04**.

### `pwd` — print working directory

```bash
$ pwd
/home/devops
```

Tells you **where you are** in the filesystem — your current directory's full path. Essential
whenever you're unsure of your location. `~` is shorthand for your home directory (`/home/devops`).

---

## Key Takeaways

- Linux = open-source OS; **the kernel** is its core, a **distribution** makes it usable.
- **Ubuntu** (Debian-based, `apt`, LTS) is what you'll run.
- **Terminal** = the window; **shell** (bash) = the command interpreter.
- **root (UID 0)** is all-powerful — use a normal user + **`sudo`** instead.
- Orientation commands: `uname -a`, `hostname`, `whoami`, `id`, `uptime`, `date`, `ls`, `pwd`.
- **Load average** compares to your CPU core count to judge if a server is busy.

## Quick self-check

1. What's the difference between the Linux kernel and a Linux distribution?
2. Terminal vs shell — which one interprets your commands?
3. Your `id` shows `uid=1000` and `groups=...,27(sudo)`. Can you run `sudo`? Why?
4. `uptime` shows `load average: 3.90` on a 4-core server. Busy or idle?
5. Which command tells you your current directory path?

