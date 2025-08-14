# Terminal Commands — A Practical, Comprehensive README

A clear, useful cheat‑sheet of the most common terminal commands for Linux and macOS shells (bash/zsh). Each entry shows:

* **Command** — what you type
* **What it does** — plain‑English description
* **Example** — copy‑paste friendly

> **Notes**
>
> * Examples assume a POSIX shell (bash/zsh). macOS often ships BSD variants of tools (slightly different flags) while most Linux distros use GNU. When flags differ, I call it out.
> * ⚠️ = potentially destructive. Read before you run.
> * Use `--help` and `man <tool>` for details (e.g., `man grep`).

---

## Table of Contents

1. [Navigation & Files](#navigation--files)
2. [Viewing & Quick Editing](#viewing--quick-editing)
3. [Search & Find](#search--find)
4. [Permissions, Ownership & sudo](#permissions-ownership--sudo)
5. [Compression & Archives](#compression--archives)
6. [Processes & Jobs](#processes--jobs)
7. [System & Disk Info](#system--disk-info)
8. [Networking & Transfers](#networking--transfers)
9. [Text Processing (Power Tools)](#text-processing-power-tools)
10. [Redirection, Pipes & Command Chaining](#redirection-pipes--command-chaining)
11. [Variables, Aliases & History](#variables-aliases--history)
12. [Clipboard & “Open with default app”](#clipboard--open-with-default-app)
13. [Package Managers](#package-managers)
14. [Git Essentials (Terminal)](#git-essentials-terminal)
15. [SSH Keys (Quick Start)](#ssh-keys-quick-start)
16. [tmux (Persistent Terminals)](#tmux-persistent-terminals)
17. [Keyboard Shortcuts](#keyboard-shortcuts)
18. [Common One‑Liners](#common-one-liners)
19. [Safety Tips](#safety-tips)

---

## Navigation & Files

* **`pwd`** — Print current directory
  **Example**

  ```bash
  pwd
  ```

* **`ls`** — List files (add `-l` long, `-a` all, `-h` human sizes)
  **Example**

  ```bash
  ls -lah
  ```

* **`cd`** — Change directory (`cd -` to go back)
  **Example**

  ```bash
  cd /etc
  cd -    # back to previous
  ```

* **`tree`** — Directory tree (install first: `brew install tree` or `sudo apt install tree`)
  **Example**

  ```bash
  tree -L 2
  ```

* **`mkdir`** — Make directory (`-p` parents)
  **Example**

  ```bash
  mkdir -p src/components
  ```

* **`touch`** — Create empty file / update timestamps
  **Example**

  ```bash
  touch README.md
  ```

* **`cp`** — Copy files (`-r` recursive; `-a` archive)
  **Example**

  ```bash
  cp file.txt backup.txt
  cp -r assets/ public/assets/
  ```

* **`mv`** — Move/rename files
  **Example**

  ```bash
  mv report.md docs/report-2025-08.md
  ```

* **`rm`** ⚠️ — Remove files (`-r` recursive, `-f` force)
  **Example**

  ```bash
  rm old.log
  rm -rf build/   # ⚠️ deletes folder and its contents permanently
  ```

* **`rmdir`** — Remove *empty* directories
  **Example**

  ```bash
  rmdir tmp-empty
  ```

* **`ln`** — Links (`-s` symbolic)
  **Example**

  ```bash
  ln -s /usr/local/bin/node ~/bin/node
  ```

* **`stat`** — File metadata (size, perms, times)
  **Example**

  ```bash
  stat file.txt
  ```

* **`file`** — Guess file type
  **Example**

  ```bash
  file some-binary
  ```

---

## Viewing & Quick Editing

* **`cat`** — Print file(s) to stdout
  **Example**

  ```bash
  cat /etc/hosts
  ```

* **`less`** — Pager (scroll with arrows, `/pattern` search, `q` to quit)
  **Example**

  ```bash
  less big.log
  ```

* **`head` / `tail`** — Start/end of files (`-n` lines; `tail -f` follow)
  **Example**

  ```bash
  head -n 20 access.log
  tail -n 100 error.log
  tail -f app.log
  ```

* **`nl`** — Number lines
  **Example**

  ```bash
  nl script.sh | less
  ```

* **`nano`** — Simple terminal editor (easy)
  **Example**

  ```bash
  nano config.ini
  ```

* **`vim`** — Powerful editor (modal)
  **Example**

  ```bash
  vim main.py
  ```

---

## Search & Find

* **`grep`** — Search text (add `-R` recursive, `-n` line numbers, `-i` case‑insensitive)
  **Example**

  ```bash
  grep -Rni "TODO" src/
  ```

* **`find`** — Find files by name/type/time/size; run actions
  **Examples**

  ```bash
  find . -type f -name "*.log"
  find . -type f -name "*.tmp" -delete          # ⚠️ delete matches
  find . -type f -mtime +7 -name "*.log" -delete
  ```

* **`which` / `command -v`** — Locate a command in `PATH`
  **Example**

  ```bash
  command -v python
  ```

* **`locate`** — Instant filename search (needs `updatedb`)
  **Example**

  ```bash
  locate ssh_config
  ```

---

## Permissions, Ownership & sudo

* **`chmod`** — Change permissions (symbolic or octal)
  **Examples**

  ```bash
  chmod u+x deploy.sh         # add execute for user
  chmod 644 file.txt          # rw-r--r--
  chmod -R 755 public/        # rwxr-xr-x recursively
  ```

* **`chown`** — Change owner (and group with `:`)
  **Example**

  ```bash
  sudo chown -R user:staff /var/www
  ```

* **`chgrp`** — Change group
  **Example**

  ```bash
  sudo chgrp developers app.sock
  ```

* **`umask`** — Default permission mask
  **Example**

  ```bash
  umask 022
  ```

* **`sudo`** — Run command as another user (default root)
  **Examples**

  ```bash
  sudo systemctl restart nginx
  sudo !!   # re-run last command with sudo
  ```

* **`visudo`** — Safely edit sudoers file
  **Example**

  ```bash
  sudo visudo
  ```

---

## Compression & Archives

* **`tar`** — Pack/unpack tarballs (add `z` for gzip, `J` for xz)
  **Examples**

  ```bash
  tar -czf site.tar.gz public/
  tar -xzf site.tar.gz -C /tmp/extract
  tar -tvf site.tar.gz  # list contents
  ```

* **`zip` / `unzip`** — Zip archives
  **Examples**

  ```bash
  zip -r project.zip src/ docs/
  unzip -l project.zip
  unzip project.zip -d ./extract
  ```

* **`gzip` / `gunzip`**, **`xz` / `unxz`**, **`bzip2` / `bunzip2`** — Compress single files
  **Examples**

  ```bash
  gzip bigfile     # creates bigfile.gz
  gunzip bigfile.gz
  xz -z dataset.csv   # creates dataset.csv.xz
  ```

---

## Processes & Jobs

* **`ps`** — List processes (`aux` for all; `-ef` on some systems)
  **Example**

  ```bash
  ps aux | less
  ```

* **`top`** / **`htop`** — Live process viewer (`htop` is nicer; install it)
  **Example**

  ```bash
  htop
  ```

* **`pgrep` / `pkill`** — Find/kill by name
  **Examples**

  ```bash
  pgrep -fl node
  pkill -f "python my_server.py"   # ⚠️ kills matching processes
  ```

* **`kill`** — Send signal to PID (`-TERM` graceful, `-KILL` force)
  **Example**

  ```bash
  kill -TERM 12345
  kill -9 12345        # ⚠️ last resort
  ```

* **Job control** — Run in background & manage
  **Examples**

  ```bash
  long_task &          # start in background
  jobs                 # list jobs
  fg %1                # bring job 1 to foreground
  bg %1                # resume job 1 in background
  disown %1            # detach from shell
  nohup long_task &    # keep running after logout
  ```

---

## System & Disk Info

* **`uname -a`** — Kernel/system info
  **Example**

  ```bash
  uname -a
  ```

* **`lsb_release -a`** (Linux) / **`sw_vers`** (macOS) — OS version
  **Examples**

  ```bash
  lsb_release -a
  sw_vers
  ```

* **`uptime`** — How long the system has been running
  **Example**

  ```bash
  uptime
  ```

* **`df -h`** — Disk free by filesystem
  **Example**

  ```bash
  df -h
  ```

* **`du -sh`** — Directory sizes (`*` to see children)
  **Examples**

  ```bash
  du -sh .
  du -sh * | sort -h
  ```

* **`free -h`** (Linux) / **`vm_stat`** (macOS) — Memory usage
  **Examples**

  ```bash
  free -h
  vm_stat
  ```

* **`systemctl`** (Linux systemd) — Services
  **Examples**

  ```bash
  systemctl status nginx
  sudo systemctl enable --now nginx
  journalctl -u nginx -f
  ```

* **`dmesg`** — Kernel ring buffer (hardware/messages)
  **Example**

  ```bash
  dmesg | less
  ```

---

## Networking & Transfers

* **`ping`** — Check reachability
  **Example**

  ```bash
  ping -c 4 example.com
  ```

* **`traceroute`** (Linux/mac) — Route to host
  **Example**

  ```bash
  traceroute example.com
  ```

* **`dig`** / **`nslookup`** — DNS queries
  **Examples**

  ```bash
  dig example.com +short
  dig MX google.com
  nslookup example.com
  ```

* **`curl`** — HTTP client (download, headers, POST)
  **Examples**

  ```bash
  curl -I https://example.com                 # headers
  curl -L -O https://example.com/file.tar.gz  # follow redirects, save as filename
  curl -X POST -H "Content-Type: application/json" -d '{"ok":true}' https://httpbin.org/post
  ```

* **`wget`** — Downloader (Linux; install on mac)
  **Example**

  ```bash
  wget -c https://example.com/big.iso    # resume
  ```

* **`ssh`** — Remote shell
  **Example**

  ```bash
  ssh -i ~/.ssh/id_ed25519 user@server.example.com
  ```

* **`scp`** — Secure copy
  **Examples**

  ```bash
  scp file.txt user@server:/var/www/
  scp -r site/ user@server:/var/www/site/
  ```

* **`rsync`** — Smart sync (fast, resumable)
  **Examples**

  ```bash
  rsync -avh --progress src/ dest/
  rsync -avz --delete ./public/ user@server:/var/www/site/
  ```

* **`ss -tulpen`** (Linux) / **`lsof -i :PORT`** (mac/Linux) — Open ports
  **Examples**

  ```bash
  ss -tulpen          # Linux: listening sockets
  lsof -i :3000       # what's using port 3000
  ```

---

## Text Processing (Power Tools)

* **`wc`** — Count lines/words/chars
  **Example**

  ```bash
  wc -l access.log
  ```

* **`sort`** — Sort lines (`-n` numeric, `-h` human, `-r` reverse)
  **Example**

  ```bash
  sort -h sizes.txt
  ```

* **`uniq`** — Unique or count (`-c`) adjacent duplicates (often with `sort`)
  **Example**

  ```bash
  sort urls.txt | uniq -c | sort -nr | head
  ```

* **`cut`** — Column extractor
  **Example**

  ```bash
  cut -d, -f1,3 data.csv
  ```

* **`paste`** — Merge lines by columns
  **Example**

  ```bash
  paste file1.txt file2.txt
  ```

* **`tr`** — Translate/delete characters
  **Example**

  ```bash
  tr '[:lower:]' '[:upper:]' < names.txt
  ```

* **`sed`** — Stream editor (find/replace, ranges)
  **Examples**

  ```bash
  sed 's/foo/bar/g' input.txt > output.txt
  # In-place (GNU sed / Linux):
  sed -i 's/DEBUG=false/DEBUG=true/' .env
  # In-place (BSD sed / macOS):
  sed -i '' 's/DEBUG=false/DEBUG=true/' .env
  ```

* **`awk`** — Field-aware scripting
  **Examples**

  ```bash
  awk -F, '{print $1,$3}' data.csv
  awk '$3 > 100 {print $0}' data.tsv
  ```

* **`xargs`** — Build & run commands from stdin
  **Examples**

  ```bash
  # Safely delete null-delimited list from find:
  find . -type f -name "*.tmp" -print0 | xargs -0 rm -f
  # Parallel downloads (GNU xargs):
  cat urls.txt | xargs -n1 -P4 wget
  ```

* **`tee`** — Split output to file and screen
  **Example**

  ```bash
  make 2>&1 | tee build.log
  ```

---

## Redirection, Pipes & Command Chaining

* **Redirection**

  ```bash
  cmd > out.txt       # stdout to file (overwrite)
  cmd >> out.txt      # stdout append
  cmd 2> err.txt      # stderr to file
  cmd > all.txt 2>&1  # stdout+stderr to same file
  ```

* **Pipes**

  ```bash
  producer | filter | consumer
  ```

* **Chaining**

  ```bash
  do_this && then_this          # run second only if first succeeds
  do_this || or_else            # run if first fails
  cmd1 ; cmd2 ; cmd3            # run sequentially regardless
  ```

* **Command substitution**

  ```bash
  echo "Today is $(date)"
  FILES=$(ls *.md)
  ```

* **Here-docs**

  ```bash
  cat <<'EOF' > script.sh
  echo "hello"
  EOF
  ```

* **Brace expansion & globs**

  ```bash
  touch {a,b,c}.txt            # a.txt b.txt c.txt
  mv *.jpg images/             # glob all JPGs
  ```

---

## Variables, Aliases & History

* **Environment variables**

  ```bash
  export PORT=8080
  echo "$PORT"
  PATH="$HOME/bin:$PATH"       # prepend to PATH
  ```

* **Aliases**

  ```bash
  alias ll='ls -lah'
  unalias ll
  ```

* **History & quick recalls**

  ```bash
  history
  !!          # re-run last command
  !git        # run the last command that started with 'git'
  !?pattern   # last command containing 'pattern'
  ```

* **Shell config**

  ```bash
  # bash:  ~/.bashrc, ~/.bash_profile
  # zsh:   ~/.zshrc
  source ~/.zshrc
  ```

---

## Clipboard & “Open with default app”

* **macOS**

  ```bash
  pbcopy < file.txt            # to clipboard
  pbpaste > pasted.txt         # from clipboard
  open .                       # open folder in Finder
  open report.pdf              # open with default app
  ```

* **Linux (install one)**

  ```bash
  xclip -sel clip < file.txt
  xclip -o -sel clip > out.txt
  xdg-open .                   # open in file manager
  xdg-open report.pdf
  ```

---

## Package Managers

* **Debian/Ubuntu (APT)**

  ```bash
  sudo apt update
  sudo apt install htop
  apt search ffmpeg
  sudo apt upgrade
  sudo apt autoremove
  ```

* **Fedora/RHEL (DNF/YUM)**

  ```bash
  sudo dnf install htop
  sudo dnf update
  ```

* **Arch (pacman)**

  ```bash
  sudo pacman -Syu
  sudo pacman -S ripgrep
  sudo pacman -Rns package-name
  ```

* **openSUSE (zypper)**

  ```bash
  sudo zypper refresh
  sudo zypper install htop
  ```

* **macOS (Homebrew)**

  ```bash
  /bin/bash -c "$(curl -fsSL https://brew.sh/install.sh)"
  brew search ffmpeg
  brew install ripgrep
  brew upgrade
  brew services start postgresql
  ```

---

## Git Essentials (Terminal)

* **Setup & clone**

  ```bash
  git config --global user.name "Your Name"
  git config --global user.email "you@example.com"
  git clone https://github.com/user/repo.git
  ```

* **Daily workflow**

  ```bash
  git status
  git add -p
  git commit -m "Describe change"
  git pull --rebase
  git push
  ```

* **Branching & diff**

  ```bash
  git switch -c feature/x
  git switch main
  git merge feature/x
  git diff        # unstaged changes
  git log --oneline --graph --decorate --all
  ```

* **Stash**

  ```bash
  git stash -u
  git stash pop
  ```

---

## SSH Keys (Quick Start)

* **Generate & use**

  ```bash
  ssh-keygen -t ed25519 -C "you@example.com"
  eval "$(ssh-agent -s)"
  ssh-add ~/.ssh/id_ed25519
  cat ~/.ssh/id_ed25519.pub    # add this to Git host / server
  ```

---

## tmux (Persistent Terminals)

* **Basics**

  ```bash
  tmux new -s work
  tmux attach -t work
  # Inside tmux: Ctrl-b d   (detach)
  ```

---

## Keyboard Shortcuts

* **Ctrl‑C**: interrupt current command
* **Ctrl‑D**: end of input / logout
* **Ctrl‑Z**: suspend to background (then `bg`/`fg`)
* **Ctrl‑A / Ctrl‑E**: jump to start/end of line
* **Alt‑B / Alt‑F**: move by word
* **Ctrl‑R**: reverse search history
* **Tab**: autocomplete

---

## Common One‑Liners

* **Largest files/folders in current directory**

  ```bash
  du -sh * 2>/dev/null | sort -h | tail
  ```

* **Find files modified in last 24h**

  ```bash
  find . -type f -mtime -1 -print
  ```

* **Replace text across a codebase (GNU sed)**

  ```bash
  grep -RIl "oldName" . | xargs sed -i 's/oldName/newName/g'
  ```

  **macOS BSD sed**

  ```bash
  grep -RIl "oldName" . | xargs sed -i '' 's/oldName/newName/g'
  ```

* **Count unique visitors by IP in Nginx log**

  ```bash
  cut -d' ' -f1 access.log | sort | uniq -c | sort -nr | head
  ```

* **Who’s listening on a port**

  ```bash
  lsof -i :8080
  ```

* **Watch a command repeatedly**

  ```bash
  watch -n 2 'df -h'
  ```

* **Compute checksum**

  ```bash
  sha256sum file.iso     # Linux
  shasum -a 256 file.iso # macOS
  ```

---

## Safety Tips

* Prefer **dry runs** when available (e.g., `rsync --dry-run`).
* Be cautious with wildcards and `-delete` / `rm -rf`. Print first:

  ```bash
  find . -name "*.tmp" -print   # verify before deleting
  ```
* Quote variables to avoid word splitting:

  ```bash
  rm "$FILE"
  ```
* Use absolute paths when operating as `root`.
* Version control critical scripts; add `set -euo pipefail` in bash scripts to fail fast.

---

### How to Extend This Cheat Sheet

* Use `man <tool>` and `tool --help` to explore flags.
* Create your own aliases (e.g., `alias gs='git status'`).
* Save shell functions/aliases in `~/.bashrc` or `~/.zshrc`.

---

If you’d like, tell me your OS (Linux distro or macOS) and your daily tasks, and I’ll tailor this README to your exact setup (e.g., Docker, Kubernetes, Python/Node workflows, macOS‑specific tools).
