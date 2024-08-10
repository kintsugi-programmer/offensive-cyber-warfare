# Gobuster Cheatsheet

## Table of Contents
- [Gobuster Cheatsheet](#gobuster-cheatsheet)
  - [Table of Contents](#table-of-contents)
  - [Introduction](#introduction)
  - [Installation](#installation)
  - [Basic Usage](#basic-usage)
    - [Wordlist](#wordlist)
    - [Modes](#modes)
    - [Common Options](#common-options)
  - [Advanced Usage](#advanced-usage)
    - [Recursive Search](#recursive-search)
    - [Custom User-Agent](#custom-user-agent)
    - [Verbose Output](#verbose-output)
    - [Using Multiple Wordlists](#using-multiple-wordlists)
  - [Example Commands](#example-commands)
  - [Uninstall](#uninstall)
    - [If Installed via Go](#if-installed-via-go)
    - [If Installed via Package Manager](#if-installed-via-package-manager)
    - [Verify Uninstallation](#verify-uninstallation)
  - [Conclusion](#conclusion)

## Introduction
**Gobuster** is a tool used to brute-force:

- URIs (directories and files) in web sites.
- DNS subdomains (with wildcard support).
- Virtual Host names on target web servers.
- Open Amazon S3 buckets
- Open Google Cloud buckets
- TFTP servers
Gobuster is useful for pentesters, ethical hackers and forensics experts. It also can be used for security tests.

```bash
root@kali:~# gobuster -h
Usage:
  gobuster [command]

Available Commands:
  completion  Generate the autocompletion script for the specified shell
  dir         Uses directory/file enumeration mode
  dns         Uses DNS subdomain enumeration mode
  fuzz        Uses fuzzing mode. Replaces the keyword FUZZ in the URL, Headers and the request body
  gcs         Uses gcs bucket enumeration mode
  help        Help about any command
  s3          Uses aws bucket enumeration mode
  tftp        Uses TFTP enumeration mode
  version     shows the current version
  vhost       Uses VHOST enumeration mode (you most probably want to use the IP address as the URL parameter)

Flags:
      --debug                 Enable debug output
      --delay duration        Time each thread waits between requests (e.g. 1500ms)
  -h, --help                  help for gobuster
      --no-color              Disable color output
      --no-error              Don't display errors
  -z, --no-progress           Don't display progress
  -o, --output string         Output file to write results to (defaults to stdout)
  -p, --pattern string        File containing replacement patterns
  -q, --quiet                 Don't print the banner and other noise
  -t, --threads int           Number of concurrent threads (default 10)
  -v, --verbose               Verbose output (errors)
  -w, --wordlist string       Path to the wordlist. Set to - to use STDIN.
      --wordlist-offset int   Resume from a given position in the wordlist (defaults to 0)

Use "gobuster [command] --help" for more information about a command.
```
## Installation
```bash
# Install Gobuster using Go
go install github.com/OJ/gobuster/v3@latest

# Or install using a package manager
apt install gobuster # for Debian-based systems
```

## Basic Usage
The general syntax for Gobuster is:
```bash
gobuster [mode] -u [URL] -w [wordlist] [options]
```
### Wordlist
```bash
wget https://raw.githubusercontent.com/danielmiessler/SecLists/master/Discovery/Web-Content/common.txt -O wordlist.txt
```
A **wordlist** is a file containing a list of words or phrases used in security testing, primarily for brute-forcing tasks. Common uses include:

- **Directory/File Brute-forcing**: Identifying hidden web directories or files (e.g., with tools like Gobuster).
- **Password Cracking**: Testing common passwords against hashed passwords (e.g., with tools like John the Ripper).
- **Fuzzing**: Inputting various strings to discover vulnerabilities in applications.

wordlist.txt :
```
.bash_history
.bashrc
.cache
.config
.cvs
.cvsignore
.env
.forward
.git
.git-rewrite
.git/HEAD
.git/config
.git/index
.git/logs/
.git_release
.gitattributes
.gitconfig
.gitignore
.gitk
.gitkeep

.
.
. etc
```

Wordlists can be default (provided with tools), community-contributed, or custom-made based on specific knowledge of a target. Examples include lists of common file names, directory structures, or passwords.

### Modes
1. **Directory/File Brute-forcing**:  
   Use `dir` mode to discover hidden directories and files.
```bash
gobuster -u https://example.com -w wordlist.txt dir
```

2. **DNS Subdomain Brute-forcing**:  
   Use `dns` mode to enumerate subdomains.
```bash
gobuster dns -d example.com -w /path/to/wordlist.txt
```
```bash
gobuster dns -d google.com -w ~/wordlists/subdomains.txt -i

===============================================================
Gobuster v3.2.0
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Mode         : dns
[+] Url/Domain   : google.com
[+] Threads      : 10
[+] Wordlist     : /home/oj/wordlists/subdomains.txt
===============================================================
2019/06/21 11:54:54 Starting gobuster
===============================================================
Found: www.google.com [172.217.25.36, 2404:6800:4006:802::2004]
Found: admin.google.com [172.217.25.46, 2404:6800:4006:806::200e]
Found: store.google.com [172.217.167.78, 2404:6800:4006:802::200e]
Found: mobile.google.com [172.217.25.43, 2404:6800:4006:802::200b]
Found: ns1.google.com [216.239.32.10, 2001:4860:4802:32::a]
Found: m.google.com [172.217.25.43, 2404:6800:4006:802::200b]
Found: cse.google.com [172.217.25.46, 2404:6800:4006:80a::200e]
Found: chrome.google.com [172.217.25.46, 2404:6800:4006:802::200e]
Found: search.google.com [172.217.25.46, 2404:6800:4006:802::200e]
Found: local.google.com [172.217.25.46, 2404:6800:4006:80a::200e]
Found: news.google.com [172.217.25.46, 2404:6800:4006:802::200e]
Found: blog.google.com [216.58.199.73, 2404:6800:4006:806::2009]
Found: support.google.com [172.217.25.46, 2404:6800:4006:802::200e]
Found: wap.google.com [172.217.25.46, 2404:6800:4006:802::200e]
Found: directory.google.com [172.217.25.46, 2404:6800:4006:802::200e]
Found: translate.google.com [172.217.25.46, 2404:6800:4006:802::200e]
Found: music.google.com [172.217.25.46, 2404:6800:4006:802::200e]
Found: mail.google.com [172.217.25.37, 2404:6800:4006:802::2005]
===============================================================
2019/06/21 11:54:55 Finished
===============================================================
```

### Common Options
- `-u`, `--url`: Target URL (for `dir` mode).
- `-w`, `--wordlist`: Path to the wordlist file.
- `-t`, `--threads`: Number of concurrent threads (default is 10).
  ```bash
    gobuster dir -u http://example.com -w /path/to/wordlist.txt -t 20
  ```
- `-r`, `--no-error`: Suppress errors (useful for cleaner output).
- `-s`, `--status-codes`: Comma-separated list of HTTP status codes to include in output (default is `200,204,301,302,307,403,401`).
  ```bash
    gobuster dir -u http://example.com -w /path/to/wordlist.txt -s '200,204,301,302,307,403'
  ```
- `-o`, `--output`: Output file to save results.
  ```bash
  gobuster dir -u http://example.com -w /path/to/wordlist.txt -o results.txt
  ```
- `-k`, `--insecure`: Skip SSL certificate verification (useful for self-signed certs).
  ```bash
  gobuster dir -u https://example.com -w /path/to/wordlist.txt -k
  ```
- `-x`, `--extensions`: Specify file extensions to search for (e.g., `php,html,txt`).
  ```bash
  gobuster dir -u http://example.com -w /path/to/wordlist.txt -x php,html
  ```

## Advanced Usage
### Recursive Search
To enable recursive searching, use the `--recursive` option along with the `-r` flag:
```bash
gobuster dir -u http://example.com -w /path/to/wordlist.txt -r
```

### Custom User-Agent
You can specify a custom User-Agent string:
```bash
gobuster dir -u http://example.com -w /path/to/wordlist.txt -A "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/58.0.3029.110 Safari/537.3"
```

### Verbose Output
For more detailed output, use the `-v` option:
```bash
gobuster dir -u http://example.com -w /path/to/wordlist.txt -v
```

### Using Multiple Wordlists
You can provide multiple wordlists by using `-w` multiple times:
```bash
gobuster dir -u http://example.com -w /path/to/wordlist1.txt -w /path/to/wordlist2.txt
```

## Example Commands
- **Basic Directory Scan**:
  ```bash
  gobuster dir -u http://example.com -w /usr/share/wordlists/dirb/common.txt
  ```
```bash
gobuster -u http://fakebank.com -w wordlist.txt dir
```
```bash
=====================================================
Gobuster v2.0.1
=====================================================
[+] Mode         : dir
[+] Url/Domain   : http://fakebank.com/
[+] Threads      : 10
[+] Wordlist     : wordlist.txt
[+] Status codes : 200,204,301,302,307,403
[+] Timeout      : 10s
=====================================================
2022/04/11 18:23:28 Starting gobuster
=====================================================
/images (Status: 301)
/DIRECTORY_NAME_OUTPUT (Status: 200)
=====================================================
2022/04/11 18:23:38 Finished
=====================================================
```

- **Brute-force Subdomains**:
```bash
gobuster dns -d example.com -w /usr/share/wordlists/seclists/Discovery/DNS/subdomains-top1million.txt
```

- **Brute-forcing with Custom Status Codes**:
```bash
gobuster dir -u http://example.com -w /path/to/wordlist.txt -s '200,403'
```

## Uninstall
To uninstall Gobuster, you can follow these steps based on how you installed it:

### If Installed via Go
1. **Remove the Gobuster binary**:
   Navigate to the directory where Go binaries are installed, typically `$GOPATH/bin`. You can find the path with:
   ```bash
   echo $GOPATH
   ```
   Then, delete the Gobuster binary:
   ```bash
   rm $GOPATH/bin/gobuster
   ```

2. **If you installed it using Go modules, you can run:**
   ```bash
   go clean -i github.com/OJ/gobuster/v3
   ```

### If Installed via Package Manager
If you installed Gobuster using a package manager like `apt`, use the following command to uninstall it:
```bash
sudo apt remove gobuster
```

### Verify Uninstallation
You can check if Gobuster is uninstalled by running:
```bash
gobuster
```
If it is uninstalled, you should see a message indicating that the command is not found.
## Conclusion
Gobuster is a powerful and versatile tool for discovering hidden files, directories, and subdomains. Use the options and commands outlined above to effectively scan web applications and enhance your security testing capabilities.

