---
description: Secure Shell Protocol - Port 22
icon: key
---

# SSH

<details>

<summary><mark style="color:purple;"><strong><code>Key Generation</code></strong></mark></summary>

{% code title="RSA" overflow="wrap" %}
```sh
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```
{% endcode %}

{% code title="Ed25519" %}
```sh
ssh-keygen -t ed25519
```
{% endcode %}

{% code title="ECDSA" overflow="wrap" %}
```sh
ssh-keygen -t ecdsa-sk
```
{% endcode %}

{% hint style="info" %}
<mark style="color:purple;">**`FIDO/U2F NO-TOUCH MODE`**</mark>

{% code title="Without Touch-Mode" overflow="wrap" %}
```sh
ssh-keygen -O no-touch-required -t ed25519-sk
```
{% endcode %}

{% code title="Allow mode on sshd" overflow="wrap" %}
```bash
no-touch-required sk-ssh-ed25519@openssh.com AAAAInN... user@example.com
```
{% endcode %}
{% endhint %}

</details>

<details>

<summary><mark style="color:purple;"><strong><code>Enumeration</code></strong></mark></summary>

{% code title="Show Details" %}
```bash
ssh-keygen -C "$(whoami)@$(uname -n)-$(date -I)"
```
{% endcode %}

{% code title="Key lenght" %}
```bash
ssh-keygen -l -f public_key
```
{% endcode %}

{% code title="Check SSH access" %}
```sh
netexec ssh <IP> -u <USER> -p 'password'
```
{% endcode %}

{% code title="SSH Brute Force" overflow="wrap" %}
```sh
nmap -n -p22 --script ssh-brute --script-args userdb=usernames.txt,passdb=passwords.txt <IP>
```
{% endcode %}

</details>

<details>

<summary><mark style="color:purple;"><strong><code>Trouble-shooting</code></strong></mark></summary>

{% hint style="info" %}
<mark style="color:red;">**`SSH2_MSG_KEX_ECDH_REPLY`**</mark> <mark style="color:purple;">error:</mark>

```sh
ssh -o MACs=hmac-sha2-256 <HOST>
```
{% endhint %}

{% hint style="info" %}
* <mark style="color:purple;">Sometimes the</mark> <mark style="color:orange;">**`/etc/hosts.allow`**</mark> <mark style="color:purple;">or</mark> <mark style="color:orange;">**`/etc/hosts.deny`**</mark> <mark style="color:purple;">may be configured to blacklist or whitelist</mark> <mark style="color:orange;">**`IPs`**</mark> <mark style="color:purple;">trying to connect to the server:</mark>

{% code title="Whitelist" %}
```
ALL : 10.10.16.8

```
{% endcode %}

* <mark style="color:purple;">Add that in the</mark> <mark style="color:orange;">**`/hosts.allow`**</mark> <mark style="color:purple;">file; make sure to let a blank line at the end.</mark>
* <mark style="color:orange;">**`sshd_wl`**</mark> <mark style="color:purple;">is the syslink to</mark> <mark style="color:orange;">**`host.allow`**</mark> <mark style="color:purple;">and is normally in</mark> <mark style="color:orange;">**`.ssh`**</mark>
{% endhint %}

{% hint style="info" %}
* <mark style="color:purple;">In recent versions of</mark> <mark style="color:orange;">**`OpenSSH`**</mark><mark style="color:purple;">, certain older key types like</mark> <mark style="color:orange;">**`ssh-rsa`**</mark> <mark style="color:purple;">have been deprecated because of security concerns with the</mark> <mark style="color:orange;">**`SHA-1`**</mark> <mark style="color:purple;">hash algorithm they use:</mark>

{% code overflow="wrap" %}
```sh
ssh root@10.10.10.34 -i id_rsa -o PubkeyAcceptedKeyTypes=ssh-rsa
```
{% endcode %}
{% endhint %}

</details>

<details>

<summary><mark style="color:red;"><strong><code>OpenSSH Vulnerabilities</code></strong></mark></summary>

#### [<kbd><mark style="color:orange;">**`Repology`**<mark style="color:orange;"></kbd>](https://repology.org/project/openssh/cves?version=8.9.p1)

{% hint style="info" %}
<mark style="color:orange;">`RsaCtfTool`</mark>

* &#x20;[<mark style="color:orange;">**`RSA attack tool`**</mark>](https://github.com/RsaCtfTool/RsaCtfTool/tree/master) <mark style="color:purple;">(mainly for ctf) - retrieve private key from weak public key and/or uncipher data.</mark>
* <mark style="color:purple;">Install</mark> <mark style="color:orange;">**`libmpc-dev`**</mark><mark style="color:purple;">,</mark> <mark style="color:orange;">**`libgmp3-dev`**</mark> <mark style="color:purple;">and</mark> <mark style="color:orange;">**`sagemath`**</mark>
* <mark style="color:purple;">Also recommend to use a virtual environment</mark>

{% code overflow="wrap" %}
```sh
RsaCtfTool/RsaCtfTool.py --publickey decoder.pub --decryptfile pass.crypt
```
{% endcode %}
{% endhint %}

{% hint style="danger" %}
<mark style="color:red;">**`CVE-2008-0166`**</mark>

* <mark style="color:orange;">**`Debian OpenSSL Predictable PRNG`**</mark> <mark style="color:purple;">-> Check the</mark> [<mark style="color:purple;">**repo**</mark>](https://github.com/g0tmi1k/debian-ssh/tree/master)
* <mark style="color:purple;">Look for matches for a given</mark> <mark style="color:orange;">**`public_key`**</mark><mark style="color:purple;">:</mark>

```sh
grep -R -n `cat public_key` rsa/
```
{% endhint %}

</details>

<details>

<summary><mark style="color:orange;"><strong><code>sshd</code></strong></mark> <mark style="color:purple;"><strong>-</strong></mark> <mark style="color:orange;"><strong><code>SSH</code></strong></mark> <mark style="color:purple;"><strong>Server</strong></mark></summary>

{% code title="Configuration File" overflow="wrap" %}
```systemd
/etc/ssh/sshd_config
```
{% endcode %}

{% code title="Sampler config" overflow="wrap" %}
```editorconfig
# Disable root login
PermitRootLogin no

# Use SSH Protocol 2 only
Protocol 2

# Use only strong authentication methods
PasswordAuthentication no
PubkeyAuthentication yes
ChallengeResponseAuthentication no
KbdInteractiveAuthentication no

# Limit user access (replace 'youruser' with your username)
AllowUsers youruser

# Use non-standard port (optional, requires adjustment to QEMU port forwarding)
Port 2233

# Restrict key exchange, ciphers, and MACs to strong algorithms
KexAlgorithms curve25519-sha256@libssh.org,diffie-hellman-group-exchange-sha256
Ciphers chacha20-poly1305@openssh.com,aes256-gcm@openssh.com,aes128-gcm@openssh.com
MACs hmac-sha2-512-etm@openssh.com,hmac-sha2-256-etm@openssh.com

# Strict mode
StrictModes yes

# Disable X11 forwarding
X11Forwarding no

# Set low login grace time
LoginGraceTime 30s

# Limit maximum authentication attempts
MaxAuthTries 3

# Enable logging
LogLevel VERBOSE

# Disable GSSAPI authentication
GSSAPIAuthentication no

# Disable host-based authentication
HostbasedAuthentication no

# Disable empty passwords
PermitEmptyPasswords no

# Disable TCP forwarding for stealthiness
AllowTcpForwarding no
GatewayPorts no

# Set idle timeout (15 minutes)
ClientAliveInterval 300
ClientAliveCountMax 3
```
{% endcode %}

{% hint style="info" %}
<mark style="color:purple;">**Enable**</mark>**&#x20;**<mark style="color:orange;">**`fail2ban`**</mark>**&#x20;**<mark style="color:purple;">**to prevent brute force attempts**</mark>

{% code overflow="wrap" lineNumbers="true" %}
```sh
sudo pacman -S fail2ban
sudo cp /etc/fail2ban/jail.conf /etc/fail2ban/jail.local
```
{% endcode %}

{% code title="Edit the SSH jail configuration" overflow="wrap" %}
```sh
sudo nano /etc/fail2ban/jail.local
```
{% endcode %}

{% code title="Add this to the SSH section" %}
```editorconfig
[sshd]
enabled = true
port = ssh
filter = sshd
logpath = /var/log/auth.log
maxretry = 3
findtime = 600
bantime = 3600
```
{% endcode %}

{% code title="Enable/Start the service" overflow="wrap" lineNumbers="true" %}
```sh
sudo systemctl enable fail2ban
sudo systemctl start fail2ban
```
{% endcode %}
{% endhint %}

{% hint style="info" %}
<mark style="color:purple;">**`Configure system auditing`**</mark>

{% code title="Set up audit" overflow="wrap" lineNumbers="true" %}
```sh
sudo pacman -S audit
sudo systemctl enable auditd
sudo systemctl start auditd
```
{% endcode %}

{% code title="Configure it" overflow="wrap" lineNumbers="true" %}
```sh
sudo auditctl -w /etc/ssh/sshd_config -p wa -k sshd_config
sudo auditctl -w /etc/passwd -p wa -k user_modification
sudo auditctl -w /etc/shadow -p wa -k user_modification
```
{% endcode %}
{% endhint %}

</details>
