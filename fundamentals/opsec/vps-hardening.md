---
icon: shield-quartered
---

# VPS Hardening

<details>

<summary><mark style="color:orange;"><strong><code>Fail2Ban</code></strong></mark><strong> </strong><mark style="color:purple;"><strong>Configuration</strong></mark></summary>

{% code title="Make a backup" overflow="wrap" %}
```sh
sudo cp /etc/fail2ban/jail.conf /etc/fail2ban/jail.local
```
{% endcode %}

{% code title="Edit the file" %}
```sh
sudo nano /etc/fail2ban/jail.local
```
{% endcode %}

{% code title="Enable it" overflow="wrap" %}
```sh
sudo systemctl enable --now fail2ban
```
{% endcode %}

{% code title="Test it" overflow="wrap" %}
```sh
sudo fail2ban-client status sshd
```
{% endcode %}

{% hint style="info" %}
<mark style="color:red;">**`Configuration Template`**</mark>

{% code overflow="wrap" %}
```ini
# [sshd]
enabled   = true
port      = 2222                # Match your custom SSH port
filter    = sshd                # Use default SSH filter
logpath   = /var/log/auth.log   # Debian/Ubuntu (use /var/log/secure for RHEL)
maxretry  = 3                   # Ban after 3 failed attempts
findtime  = 10m                 # Track failures within 10 minutes
bantime   = 4w                  # Ban for 4 weeks (adjust as needed)
ignoreip  = 127.0.0.1/8         # Whitelist localhost
banaction = ufw                 # Use UFW if installed (better than iptables)

# [mysqld-auth]
enabled  = true
port     = 3306,33060
filter   = mysqld-auth
logpath  = /var/log/mysql/error.log
maxretry = 3
bantime  = 1d
```
{% endcode %}
{% endhint %}

</details>

<details>

<summary><mark style="color:purple;"><strong>Edit</strong></mark><strong> </strong><mark style="color:orange;"><strong><code>OpenSSH</code></strong></mark><strong> </strong><mark style="color:purple;"><strong>config file</strong></mark></summary>

{% code title="Make a backup" overflow="wrap" %}
```sh
sudo cp /etc/ssh/sshd_config /etc/ssh/sshd_config.bak
```
{% endcode %}

{% code title="Edit the file" overflow="wrap" %}
```sh
sudo nano /etc/ssh/sshd_config
```
{% endcode %}

{% code title="Test config syntax" %}
```sh
sudo sshd -t  
```
{% endcode %}

{% code title="Apply changes" %}
```sh
sudo systemctl restart sshd 
```
{% endcode %}

{% hint style="info" %}
<mark style="color:red;">**`Configuration Template`**</mark>

{% code overflow="wrap" %}
```ini
# ====== SSH Protocol & Encryption ======
Protocol 2                  # Only use SSHv2 (v1 is insecure)
Port 2222                   # Custom port to reduce bot scans
HostKey /etc/ssh/ssh_host_ed25519_key  # Prefer Ed25519 keys
KexAlgorithms curve25519-sha256@libssh.org  # Strong key exchange
Ciphers chacha20-poly1305@openssh.com,aes256-gcm@openssh.com  # Modern encryption
MACs hmac-sha2-512-etm@openssh.com  # Secure message integrity

# ====== Authentication Hardening ======
PermitRootLogin no          # Disable direct root login
PasswordAuthentication no   # Disable password logins (keys only)
PermitEmptyPasswords no     # Explicitly block empty passwords
HostbasedAuthentication no  # Disable trust-based auth
MaxAuthTries 3              # Allow 3 auth attempts per session
AuthenticationMethods publickey,keyboard-interactive  # Enforce SSH + 2FA
ChallengeResponseAuthentication yes  # Required for 2FA (e.g., TOTP)
UsePAM yes

# ====== Session & Connection Limits ======
ClientAliveInterval 300     # Check alive every 5 mins
ClientAliveCountMax 0       # Terminate idle sessions immediately (no grace)
MaxSessions 2               # Allow max 2 concurrent sessions per connection
LoginGraceTime 30           # Disconnect if auth takes >30s

# ====== Forwarding & Sandboxing ======
X11Forwarding no            # Disable GUI forwarding
AllowAgentForwarding no     # Block SSH agent forwarding
AllowTcpForwarding no       # Disable port forwarding (unless needed)

# ====== Logging & Information Hiding ======
DebianBanner no             # Hide OS/version in pre-auth banner
PrintMotd no                # Disable post-login MOTD (potential info leak)
LogLevel VERBOSE            # Detailed logs for auditing
Banner /etc/issue.net       # Static pre-login banner (optional)

# ====== User Access Control ======
AllowUsers user1 user2      # Whitelist allowed users
DenyUsers *                 # Explicitly block others (redundant but clear)
```
{% endcode %}

* <mark style="color:purple;">For</mark> <mark style="color:orange;">**`keyboard-interactive`**</mark> <mark style="color:purple;">to work, configure PAM.</mark>
* <mark style="color:purple;">Update firewall rules.</mark>
* <mark style="color:purple;">Pair with</mark> <mark style="color:orange;">**`Fail2ban`**</mark> <mark style="color:purple;">to ban IPs after</mark> <mark style="color:orange;">**`MaxAuthTries`**</mark> <mark style="color:purple;">violations.</mark>
{% endhint %}

</details>

<details>

<summary><mark style="color:purple;"><strong>Automate</strong></mark><strong> </strong><mark style="color:orange;"><strong><code>UFW</code></strong></mark><strong> </strong><mark style="color:purple;"><strong>hardening</strong></mark></summary>

{% code overflow="wrap" %}
```sh
#!/bin/bash

# =============================================
# UFW HARDENING SCRIPT FOR VPS 
# =============================================

# Colors for output
RED='\033[0;31m'
GREEN='\033[0;32m'
YELLOW='\033[1;33m'
NC='\033[0m' # No Color

# Check if running as root
if [ "$(id -u)" -ne 0 ]; then
  echo -e "${RED}Error: This script must be run as root. Use sudo.${NC}" >&2
  exit 1
fi

# ---- Step 1: Verify SSH Port ---- 
CURRENT_SSH_PORT=$(grep -oP '^Port \K\d+' /etc/ssh/sshd_config 2>/dev/null || echo "22")
echo -e "${YELLOW}[?] Detected SSH port: ${CURRENT_SSH_PORT} (from sshd_config)${NC}"

read -rp "Confirm SSH port to allow in UFW [Press Enter for ${CURRENT_SSH_PORT}]: " SSH_PORT
SSH_PORT=${SSH_PORT:-$CURRENT_SSH_PORT}

# ---- Step 2: Whitelist Current IP ----
CURRENT_IP=$(curl -4 -s ifconfig.co)
if [ -z "$CURRENT_IP" ]; then
  echo -e "${RED}Error: Could not detect your public IP. Manually add it later.${NC}"
else
  echo -e "${YELLOW}[+] Your current public IP: ${CURRENT_IP}${NC}"
  read -rp "Whitelist this IP for SSH? [y/N]: " WHITELIST_IP
  if [[ $WHITELIST_IP =~ ^[Yy]$ ]]; then
    IP_WHITELIST="from $CURRENT_IP"
  fi
fi

# ---- Step 3: Apply UFW Rules ----
echo -e "\n${GREEN}[+] Applying UFW Rules...${NC}"

# Reset UFW (uncomment if needed)
# echo -e "${YELLOW}Resetting UFW...${NC}"
# ufw --force reset

# Default policies
ufw default deny incoming
ufw default allow outgoing

# SSH rules
ufw allow "$SSH_PORT/tcp" comment 'SSH port'
ufw limit "$SSH_PORT/tcp" comment 'Rate-limit SSH'  # 6 connections/minute/IP
[ -n "$IP_WHITELIST" ] && ufw allow "$IP_WHITELIST to any port $SSH_PORT" comment 'Trusted IP SSH'

# MySQL rules
read -rp "Is MySQL/MariaDB installed and needed? [y/N]: " NEED_MYSQL
if [[ $NEED_MYSQL =~ ^[Yy]$ ]]; then
  read -rp "Allow MySQL remotely? (Only if apps need it from another server) [y/N]: " MYSQL_REMOTE
  if [[ $MYSQL_REMOTE =~ ^[Yy]$ ]]; then
    read -rp "Enter trusted IP for MySQL access: " MYSQL_IP
    ufw allow from "$MYSQL_IP" to any port 3306 comment 'Allow remote MySQL'
  else
    ufw allow from 127.0.0.1 to any port 3306 comment 'Allow local MySQL'
  fi
else
  ufw deny 3306/tcp comment 'Block MySQL'
fi

# Common service blocks
ufw deny 3389/tcp comment 'Block RDP'
ufw deny 23/tcp   comment 'Block Telnet'

# Optional: Block ICMP (ping)
read -rp "Block ICMP (ping) requests? [y/N]: " BLOCK_ICMP
[[ $BLOCK_ICMP =~ ^[Yy]$ ]] && ufw deny icmp comment 'Block Ping'

# Enable logging
ufw logging on
ufw logging medium

# Enable UFW
echo -e "\n${YELLOW}[!] Enabling UFW in 10 seconds...${NC}"
echo -e "${RED}>>> OPEN A SECOND SSH CONNECTION NOW TO TEST <<<${NC}"
echo -e "${YELLOW}>>> If you get locked out, reboot the VPS to disable UFW <<<${NC}"
sleep 10
ufw enable

# Final status
echo -e "\n${GREEN}[+] UFW Rules Applied:${NC}"
ufw status numbered

# ---- Step 4: Verify SSH Access ----
echo -e "\n${YELLOW}[!] Test SSH access from another terminal before closing this session!${NC}"
echo -e "Command to test: ${GREEN}ssh -p $SSH_PORT $(whoami)@$(hostname -I | awk '{print $1}')${NC}"
```
{% endcode %}

{% hint style="info" %}
<mark style="color:red;">**`Add more rules if hosting services`**</mark>

```sh
sudo ufw allow 80/tcp
```

```sh
sudo ufw allow 443/tcp
```
{% endhint %}

</details>

<details>

<summary><mark style="color:orange;"><strong><code>MySQL</code></strong></mark><strong> </strong><mark style="color:purple;"><strong>hardening</strong></mark></summary>

{% code title="Change MySQL’s port in /etc/mysql/my.cnf" overflow="wrap" %}
```ini
[mysqld]
port = 33060
```
{% endcode %}

{% code title="Forbid root login from remote" %}
```sql
UPDATE mysql.user SET Host='localhost' WHERE User='root';
FLUSH PRIVILEGES;
```
{% endcode %}

{% code title="Use strong passwords and restrict users" overflow="wrap" %}
```sql
CREATE USER 'user'@'192.168.1.100' IDENTIFIED BY 'YourComplexPassword!123';
GRANT ALL PRIVILEGES ON odoo_db.* TO 'user'@'192.168.1.100';
```
{% endcode %}

</details>

<details>

<summary><mark style="color:orange;"><strong><code>CrowdSec</code></strong></mark><strong> </strong><mark style="color:purple;"><strong>Configuration</strong></mark></summary>

<pre class="language-sh" data-title="Add SSH Parsing/Detection" data-overflow="wrap" data-line-numbers><code class="lang-sh"><strong>sudo cscli parsers install crowdsecurity/sshd-logs
</strong><strong>sudo cscli scenarios install crowdsecurity/ssh-bf
</strong>sudo cscli collections install crowdsecurity/sshd
</code></pre>

{% code title="Verify Setup" overflow="wrap" %}
```sh
sudo cscli hub list
```
{% endcode %}

{% hint style="info" %}
<mark style="color:red;">**`Tailor to Your SSH Port`**</mark>

* <mark style="color:purple;">Edit the SSH log path in</mark> <mark style="color:orange;">**`/etc/crowdsec/acquis.yaml`**</mark><mark style="color:purple;">:</mark>

{% code overflow="wrap" %}
```yaml
filenames:
  - /var/log/auth.log    # Debian/Ubuntu
  # - /var/log/secure   # RHEL/CentOS
labels:
  type: syslog
filter: "programname=='sshd'"
```
{% endcode %}

{% code title="If using a custom SSH port, modify the SSH detection rule:" overflow="wrap" %}
```sh
sudo sed -i 's/port: 22/port: 2222/' /etc/crowdsec/scenarios/ssh-bf.yaml
```
{% endcode %}
{% endhint %}

{% code title="Start CrowdSec" overflow="wrap" %}
```sh
sudo systemctl enable --now crowdsec
```
{% endcode %}

{% code title="Check Bans" overflow="wrap" %}
```sh
sudo cscli decisions list
```
{% endcode %}

{% hint style="info" %}
<mark style="color:red;">**`Integrate with UFW`**</mark>

{% code title="Install UFW Bouncer" overflow="wrap" %}
```sh
sudo pacman -S crowdsec-firewall-bouncer-ufw  # Debian/Ubuntu
```
{% endcode %}

{% code title="Edit /etc/crowdsec/bouncers/crowdsec-firewall-bouncer.yaml" overflow="wrap" %}
```yaml
mode: ufw
deny_action: deny
deny_log: true
```
{% endcode %}

{% code title="Restart Services" overflow="wrap" %}
```sh
sudo systemctl restart crowdsec
sudo systemctl restart crowdsec-firewall-bouncer
```
{% endcode %}
{% endhint %}

{% hint style="info" %}
<mark style="color:red;">**`Ban Duration & Sensitivity`**</mark>

{% code title="Edit /etc/crowdsec/profiles.yaml" overflow="wrap" %}
```yaml
name: default
decisions:
  - type: ban
    duration: 24h    # Increase from default 4h
scenarios:
  - ssh-bf
  # Add other scenarios (e.g., http-bf)
```
{% endcode %}

{% code title="Community Blocklists" overflow="wrap" %}
```sh
sudo cscli collections install crowdsecurity/linux
sudo cscli collections install crowdsecurity/http-cve
```
{% endcode %}
{% endhint %}

{% code title="Show attack statistics" overflow="wrap" %}
```sh
sudo cscli metrics
```
{% endcode %}

{% code title="List active bans" overflow="wrap" %}
```sh
sudo cscli decisions list
```
{% endcode %}

{% code title="View all detected threats" overflow="wrap" %}
```sh
sudo cscli alerts list
```
{% endcode %}

{% code title="Update threat intelligence" overflow="wrap" %}
```sh
sudo cscli hub upgrade
```
{% endcode %}

{% code title="Live debug logs" overflow="wrap" %}
```sh
sudo tail -f /var/log/crowdsec.log
```
{% endcode %}

</details>
