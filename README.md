# cachy-sec-setup 🐟💀

> *"I use Arch, btw."*  
> Yeah but does your Arch have **BlackArch**, 100+ sec tools, kernel hardening, and fish aliases that make your terminal feel like a weapon?  
> Didn't think so.

---

## What is this

A single bash script that turns a fresh CachyOS install into a proper offensive security workstation.  
It does the boring stuff so you can get straight to the fun stuff — like legally testing systems you totally own.

No bloat. No GUI wizard. No asking you to "click next". Just `./cachy-sec-setup.sh --all` and go make coffee.

---

## What it actually does

```
✔  Verifies BlackArch strap.sh by SHA1 before running it
✔  Writes a proper mirror list (EU / US / Asia — pick your latency)
✔  Full system update before anything else
✔  Installs yay if you don't have an AUR helper yet
✔  100+ tools across 12 categories (details below)
✔  Python CLI tools via pipx — isolated envs, no venv activation needed
✔  Python library venv at ~/.venvs/sec — for things you import in scripts
✔  sysctl kernel hardening — because default Linux trusts everyone too much
✔  ~/sec/ workspace with a sensible directory structure
✔  Fish abbreviations & functions — no shell change, just new powers
✔  Enables tor and docker as services
✔  Global failure summary — know exactly what didn't install and why
```

---

## Requirements

| Thing         | Requirement                        |
|---------------|------------------------------------|
| OS            | CachyOS / any Arch-based distro    |
| Shell         | Run the script in bash; fish stays as your interactive shell |
| Privileges    | Regular user with sudo              |
| Internet      | Yes, obviously                     |
| Disk space    | ~20 GB for full install            |
| Coffee        | Strongly recommended               |

---

## Install

```bash
git clone https://github.com/cybermaksx/CachyOs_for_CyberSec
cd CachyOs_for_CyberSec
chmod +x cachy-sec-setup.sh
./cachy-sec-setup.sh --all
```

> **Do NOT run as root.** The script calls sudo itself where needed.  
> Running it as root is like giving yourself admin on a box you're testing — technically works, definitely wrong.

Open a new fish session after it finishes and everything will be there.

---

## Usage

```bash
./cachy-sec-setup.sh [option]
```

| Option | What it installs |
|--------|-----------------|
| `--all` | Everything. Nuke and pave. (default) |
| `--mirrors` | BlackArch repo + mirrors only |
| `--recon` | Recon & OSINT tools |
| `--web` | Web app testing tools |
| `--network` | Network / MITM tools |
| `--exploitation` | Exploitation & reversing |
| `--passwords` | Password cracking tools |
| `--wireless` | Wi-Fi audit tools |
| `--forensics` | Forensics & DFIR |
| `--crypto` | Crypto & steganography |
| `--se` | Social engineering tools |
| `--cloud` | Cloud & container security |
| `--osint` | OSINT tools |
| `--utils` | Dev utilities |
| `--python` | Python library venv only |
| `--pipx` | Python CLI tools via pipx only |
| `--harden` | sysctl kernel hardening only |
| `--workspace` | Create ~/sec directory structure only |
| `--fish` | Fish aliases only |
| `--help` | You're reading the wrong thing |

---

## Tools installed

### 🔍 Recon
`nmap` `masscan` `rustscan` `amass` `subfinder` `httprobe` `whatweb` `theharvester` `shodan` `dnsrecon` `dnsx` `fierce` `netdiscover` `arp-scan`

### 🌐 Web Application
`burpsuite` `zaproxy` `sqlmap` `nikto` `gobuster` `ffuf` `wfuzz` `dirsearch` `nuclei` `wafw00f` `arjun` `xsstrike` `commix` `wpscan`

### 🔗 Network / MITM
`wireshark` `tshark` `tcpdump` `bettercap` `mitmproxy` `responder` `ettercap` `netcat` `socat` `hping` `scapy` `proxychains-ng` `tor` `openvpn` `wireguard-tools`

### 💥 Exploitation
`metasploit` `exploitdb` `gdb` `pwndbg` `pwntools` `ropper` `radare2` `ghidra` `jadx` `checksec` `ltrace` `strace`

### 🔑 Passwords
`hashcat` `john` `hydra` `medusa` `crunch` `cewl` `wordlistctl`  
Also downloads **rockyou.txt** into `~/sec/passwords/wordlists/`

### 📡 Wireless
`aircrack-ng` `hcxtools` `hcxdumptool` `kismet` `bluez` `bluez-utils`

### 🔬 Forensics
`autopsy` `sleuthkit` `volatility3` `foremost` `binwalk` `hexedit` `exiftool` `bulk-extractor` `dc3dd` `guymager`

### 🔐 Crypto & Stego
`openssl` `gnupg` `hashdeep` `steghide` `zsteg` `testssl.sh`

### 🎭 Social Engineering
`set` `gophish`

### ☁️ Cloud & Containers
`docker` `docker-compose` `kubectl` `trivy` `trufflehog` `gitleaks` `aws-cli`

### 🕵️ OSINT
`spiderfoot` `recon-ng` `sherlock` `maltego` `photon`

---

## Python tools

### 🐍 Via pipx (CLI tools — globally available, zero activation needed)

> Each tool gets its own isolated environment. Like solitary confinement, but for Python.  
> `pipx upgrade-all` keeps your inmate list current.

| Tool | What it does |
|------|-------------|
| `impacket` | SMB/AD attack scripts: `secretsdump`, `GetUserSPNs`, `smbclient`… |
| `pwntools` | CTF exploit framework + `pwn` CLI |
| `frida-tools` | Dynamic instrumentation — hook anything at runtime |
| `shodan` | Query Shodan from your terminal |
| `censys` | Query Censys internet-wide scan data |
| `netexec` | Network attack Swiss-army knife (CrackMapExec's successor) |

```fish
pipx list           # see your tools
pipx upgrade-all    # upgrade everything
```

### 📚 Via venv (importable libraries — `~/.venvs/sec`)

`requests` `httpx` `scapy` `paramiko` `cryptography` `pyOpenSSL` `dnspython` `ldap3` `netifaces` `yara-python`

```fish
secenv      # activate the venv in fish
deactivate  # exit when done
```

---

## Fish abbreviations

After install, open a new fish session. These are ready:

```fish
# Navigation
sec          → cd ~/sec
recon        → cd ~/sec/recon
ctf          → cd ~/sec/ctf

# Network
myip         → curl -s ifconfig.me
localip      → ip -br a
listening    → ss -tlnp
sniff        → sudo tcpdump -i any -nn -v

# Nmap
nmap-quick   → nmap -T4 -F
nmap-full    → nmap -T4 -p- -sV -sC -O
nmap-vuln    → nmap --script=vuln -T4
nmap-stealth → sudo nmap -sS -T2 -p-
nmap-udp     → sudo nmap -sU -T4 --top-ports 200

# Encoding / decoding
b64d / b64e       base64 decode / encode
urld / urle       URL decode / encode
hex2text / text2hex
extract-ips       grep IPv4 from stdin
extract-urls      grep URLs from stdin
extract-emails    grep emails from stdin

# Tools
msfgo        → msfconsole -q
secenv       → activate Python library venv
gdb          → gdb -q
pchain       → proxychains4 -q
tor-check    → check if you're routing through Tor

# Updates
update       → sudo pacman -Syyu
aur-update   → yay -Syyu
pipx-upgrade → pipx upgrade-all
```

> Fish abbreviations expand when you press Space or Enter — you see exactly what runs. No magic black-box aliases.

---

## Workspace structure

```
~/sec/
├── recon/
├── web/
├── network/
├── exploitation/
├── passwords/
│   └── wordlists/
│       └── rockyou.txt
├── wireless/
├── forensics/
├── malware/
├── reports/
├── ctf/
└── tools/
    └── custom/
```

---

## Kernel hardening

Applied to `/etc/sysctl.d/99-cachy-sec.conf`:

```
SYN flood protection          tcp_syncookies = 1
Anti-spoofing                 rp_filter = 1
No ICMP redirects             accept_redirects = 0
No source routing             accept_source_route = 0
Hide kernel pointers          kptr_restrict = 2
Restrict dmesg                dmesg_restrict = 1
Restrict ptrace               yama.ptrace_scope = 1
No SUID core dumps            suid_dumpable = 0
Full ASLR                     randomize_va_space = 2
TCP time-wait protection      tcp_rfc1337 = 1
Log martian packets           log_martians = 1
```

---

## BlackArch mirrors

`/etc/pacman.d/blackarch-mirrorlist`:

| Mirror | Region |
|--------|--------|
| mirror.blackarch.org | Global CDN |
| ftp.gwdg.de | Germany |
| ftp.halifax.rwth-aachen.de | Germany |
| mirrors.ocf.berkeley.edu | USA |
| mirrors.tuna.tsinghua.edu.cn | Asia |
| blackarch.unixpeople.org | Europe |

The strap.sh is verified by SHA1 before execution. If the checksum doesn't match, the script exits and touches nothing.  
If BlackArch releases an updated strap.sh and the hash changes, the script will print the expected vs actual hash and a link to the official downloads page.

---

## FAQ

**Q: Why yay instead of paru?**  
A: paru was archived and is no longer maintained. yay is the community's actively maintained AUR helper. Same vibes, same flags, still Rust under the hood.

**Q: Why pipx for Python tools?**  
A: A shared venv means one broken dependency breaks everything. With pipx, each tool gets its own isolated environment. `impacket`'s deps can't fight with `frida`'s deps because they never meet. Run `pipx upgrade-all` and move on with your life.

**Q: Does this change my shell to zsh or bash?**  
A: No. Your fish stays. The script is a bash script (because that's what you run installers in) but your interactive shell is untouched.

**Q: Do I need to run it as root?**  
A: No, and the script will yell at you if you try.

**Q: Some packages failed to install. Is that a problem?**  
A: Not necessarily. Some BlackArch tools have unusual deps or are AUR-only. The script warns and continues — permanently failed packages are listed together at the end so you have a clean punch list.

**Q: Where are my Python CLI tools?**  
A: In `~/.local/bin`, available globally. No activation needed. Run `pipx list` to see them all.

**Q: Where are my Python libraries?**  
A: In `~/.venvs/sec`. Type `secenv` in fish to activate. Type `deactivate` when done.

**Q: Is this legal?**  
A: Installing security tools is legal everywhere I know of. *Using* them on systems you don't own is a different story. Don't be that person.

---

## Legal

MIT License — do whatever you want, don't blame me if something breaks.

**USE THESE TOOLS ONLY ON SYSTEMS YOU OWN OR HAVE EXPLICIT WRITTEN PERMISSION TO TEST.**  
Unauthorized access is a crime in basically every jurisdiction. This repo is for education, CTFs, and legal pentesting.

---

*Built for CachyOS × BlackArch — because Kali is for people who don't rice their terminal.*
