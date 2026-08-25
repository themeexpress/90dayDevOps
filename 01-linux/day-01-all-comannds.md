## Day 01 — Hands-On Commands & Example Output

> Run inside your Ubuntu VM (`multipass shell devops`).
> Example outputs below are from an Apple Silicon (M2) Ubuntu 22.04 VM — note the
> `aarch64` architecture and the Multipass defaults (`ubuntu` user, `devops` hostname).
> Yours may differ slightly.

### 1. `uname -a` — system & kernel information

```bash
$ uname -a
Linux devops 5.15.0-91-generic #101-Ubuntu SMP Tue Nov 14 13:29:11 UTC 2023 aarch64 aarch64 aarch64 GNU/Linux
```

`aarch64` = 64-bit ARM (Apple Silicon). On an Intel machine this would read `x86_64`.

### 2. `hostname` — the machine's name

```bash
$ hostname
devops
```

### 3. `whoami` — current effective user

```bash
$ whoami
ubuntu
```

```bash
$ sudo whoami
root
```

### 4. `id` — user ID, group ID, and group memberships

```bash
$ id
uid=1000(ubuntu) gid=1000(ubuntu) groups=1000(ubuntu),4(adm),20(dialout),24(cdrom),27(sudo),100(users)
```

`27(sudo)` in the groups means this user is allowed to run `sudo`.

### 5. `uptime` — how long the system has run (+ load average)

```bash
$ uptime
 14:32:05 up 12 min,  1 user,  load average: 0.08, 0.12, 0.09
```

Load average = average number of processes waiting to run, over the last 1 / 5 / 15 minutes.
Compare it to your CPU core count (this VM has 2 cores, so ~2.00 = fully busy).

### 6. `date` — current date and time

```bash
$ date
Mon Aug 24 14:32:05 UTC 2026
```

```bash
$ date "+%Y-%m-%d %H:%M:%S"
2026-08-24 14:32:05
```

Servers usually run in UTC so logs line up across regions.

### 7. `ls` — list directory contents

```bash
$ ls
```

(A fresh VM home is empty, so this prints nothing. After you create today's notes:)

```bash
$ ls
day-01-notes.md

$ ls -lh
total 4.0K
-rw-rw-r-- 1 ubuntu ubuntu 1.2K Aug 24 14:30 day-01-notes.md
```

Common options: `-l` long format · `-a` show hidden files · `-h` human-readable sizes · `-la` combine.

### 8. `pwd` — print working directory

```bash
$ pwd
/home/ubuntu
```

`~` is shorthand for this home directory.

---

### Quick reference

| Command | What it tells you |
|---------|-------------------|
| `uname -a` | Kernel + architecture (`aarch64` on M2) |
| `hostname` | The machine's name |
| `whoami` | Your current username |
| `id` | Your UID, GID, and groups (check for `sudo`) |
| `uptime` | Boot time, logged-in users, load average |
| `date` | Current date/time (usually UTC on servers) |
| `ls` | List files (`-la` for all + details) |
| `pwd` | Your current directory path |
