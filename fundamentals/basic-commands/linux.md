---
description: Basic commands
icon: linux
---

# Linux

<details>

<summary><mark style="color:purple;"><strong><code>System Commands</code></strong></mark></summary>

{% hint style="info" %}
#### <mark style="color:red;">`File & Directory Management`</mark>

{% code title="List all files + details" %}
```bash
ls -al
```
{% endcode %}

{% code title="List all files recursively" %}
```bash
ls -lAR
```
{% endcode %}

{% code title="Read raw binary data" overflow="wrap" %}
```bash
cat example | hexdump -C
```
{% endcode %}

{% code title="Count number of lines in a file" overflow="wrap" %}
```bash
wc -l myfile.txt
```
{% endcode %}

{% code title="Print full path " overflow="wrap" %}
```bash
realpath file.txt
```
{% endcode %}

{% code title="Copy recursively " %}
```bash
cp -r dir/ /home/user/
```
{% endcode %}

{% code title="Find all .txt files" overflow="wrap" %}
```bash
find /home/user -name "*.txt"
```
{% endcode %}

{% code title="Find files larger than 10MB" %}
```bash
find / -type f -size +10M
```
{% endcode %}

{% code title="Search with regex" overflow="wrap" %}
```bash
sudo find / -regex ".*alacritty.*" 2>/dev/null
```
{% endcode %}

{% code title="Update locate db" %}
```bash
sudo updatedb
```
{% endcode %}

{% code title="Look file from the database" overflow="wrap" %}
```bash
locate file.txt
```
{% endcode %}

{% code title="Full path of a binary" overflow="wrap" %}
```bash
which binary
```
{% endcode %}

{% code title="Delete recursively" %}
```bash
rm -rf <dir>
```
{% endcode %}
{% endhint %}

***

{% hint style="info" %}
#### <mark style="color:red;">`Process Management`</mark>

```
// Some code
```
{% endhint %}

***



</details>

<details>

<summary><mark style="color:purple;"><strong><code>User/Group Management</code></strong></mark></summary>



</details>

<details>

<summary><mark style="color:purple;"><strong><code>Permission &#x26; Security</code></strong></mark></summary>



</details>

<details>

<summary><mark style="color:purple;"><strong><code>Networking Commands</code></strong></mark></summary>

{% hint style="info" %}
<mark style="color:red;">**`Ping and TCPdump Network Analysis for RCE Detection`**</mark>

* <mark style="color:purple;">Simply</mark> <mark style="color:orange;">**`ping`**</mark> <mark style="color:purple;">your own host, you can use the command directly or as a payload for a script:</mark>

```bash
ping -c 1 10.10.14.6
```

* <mark style="color:purple;">And catch it with</mark> <mark style="color:orange;">**`tcpdump`**</mark><mark style="color:purple;">**:**</mark>

```bash
sudo tcpdump -ni <interface> icmp
```
{% endhint %}



</details>

<details>

<summary><mark style="color:purple;"><strong><code>Chroot</code></strong></mark></summary>



</details>

<details>

<summary><mark style="color:purple;"><strong><code>base64</code></strong></mark></summary>



</details>



{% hint style="info" %}
## <mark style="color:purple;">`System Commands`</mark>

#### <mark style="color:red;">`Process Management`</mark>

{% code title="List details for process" %}
```bash
ps -ef | grep process
```
{% endcode %}

{% code title="Show a detailed process tree with wide output" %}
```bash
ps -auxwf
```
{% endcode %}

{% code title=" Show process tree for a specific user" %}
```bash
pstree user
```
{% endcode %}

{% code title="Show process IDs (PIDs) with the tree view" %}
```bash
pstree -p
```
{% endcode %}

{% code title="Show real-time process stats" %}
```bash
htop
```
{% endcode %}

{% code title="Get the current process ID" %}
```sh
echo $$
```
{% endcode %}

{% code title="Kill a process" %}
```bash
sudo kill -9 <PID>
```
{% endcode %}

#### <mark style="color:red;">`System Management`</mark>

{% code title="Print Info about the system" %}
```bash
uname -a 
```
{% endcode %}

{% code title="Print Environment" %}
```bash
env
```
{% endcode %}

{% code title="Shows details about all block devices" %}
```bash
lsblk -f
```
{% endcode %}

{% code title="List PCI devices" %}
```bash
lspci
```
{% endcode %}

{% code title="Display Disk Usage" %}
```bash
df -h
```
{% endcode %}

{% code title="Show the size of files and directories in the current directory" %}
```bash
du -sh *
```
{% endcode %}

{% code title="Shows the 10 largest directories on the system" %}
```bash
sudo du -hsx /* | sort -rh | head -n 10
```
{% endcode %}

{% code title="Display RAM info" %}
```bash
free -h
```
{% endcode %}

{% code title="Displays the maximum allowed size of a process's lockable memory" %}
```bash
ulimit -l
```
{% endcode %}

{% code title="Put a process in the background" %}
```bash
bg
```
{% endcode %}

{% code title="List all process in the background" %}
```bash
jobs
```
{% endcode %}

{% code title="Puts a process into the foreground" %}
```bash
fg
```
{% endcode %}

{% code title="Display overall system performance stats" %}
```bash
vmstat
```
{% endcode %}

{% code title="Print stats every 5 seconds" %}
```bash
vmstat 5
```
{% endcode %}

{% code title="Print stats every 5 seconds for 10 iterations" %}
```bash
vmstat 5 10
```
{% endcode %}

{% code title="Show the system uptime" %}
```bash
uptime
```
{% endcode %}

{% code title="Show info about current login user" %}
```bash
w
```
{% endcode %}

#### <mark style="color:red;">`Logs`</mark>

{% code title="Display login records" %}
```bash
last
```
{% endcode %}

{% code title="Display bad login attempts" %}
```bash
lastb
```
{% endcode %}

{% code title="Shows log as they are written" %}
```bash
journalctl -f 
```
{% endcode %}

{% code title="Shows logs from the current boot" %}
```bash
journalctl -b
```
{% endcode %}

{% code title="Shows logs from the previous boot" %}
```bash
journalctl -b -1
```
{% endcode %}

{% code title="Shows logs from a specific service" %}
```bash
journalctl -u <service>
```
{% endcode %}

{% code title="Shows logs from a time range" %}
```bash
journalctl --since "2024-11-01" --until "2024-11-10"
```
{% endcode %}

{% code title="Show logs by priority level" %}
```bash
journalctl -p <level>
```
{% endcode %}

#### <mark style="color:red;">`Priority Levels:`</mark>

* <mark style="color:orange;">`0`</mark> <mark style="color:purple;">--></mark> <mark style="color:purple;">**`emergency`**</mark>
* <mark style="color:orange;">`1`</mark> <mark style="color:purple;">--></mark> <mark style="color:purple;">**`alert`**</mark>
* <mark style="color:orange;">`2`</mark> <mark style="color:purple;">--></mark> <mark style="color:purple;">**`critical`**</mark>
* <mark style="color:orange;">`3`</mark> <mark style="color:purple;">--></mark> <mark style="color:purple;">**`error`**</mark>
* <mark style="color:orange;">`4`</mark> <mark style="color:purple;">--></mark> <mark style="color:purple;"></mark><mark style="color:purple;">**`warning`**</mark>
* <mark style="color:orange;">`5`</mark> <mark style="color:purple;">--></mark> <mark style="color:purple;"></mark><mark style="color:purple;">**`notice`**</mark>
* <mark style="color:orange;">`6`</mark> <mark style="color:purple;">--></mark> <mark style="color:purple;"></mark><mark style="color:purple;">**`informational`**</mark>
* <mark style="color:orange;">`7`</mark> <mark style="color:purple;">--></mark> <mark style="color:purple;"></mark><mark style="color:purple;">**`debug`**</mark>

{% code title="Shows logs for a specific process" %}
```bash
journalctl _PID=<pid>
```
{% endcode %}

{% code title="Shows logs from the kernel" %}
```bash
journalctl -k
```
{% endcode %}

{% code title="Show kernel and boot messages" %}
```bash
dmesg
```
{% endcode %}
{% endhint %}

***

{% hint style="info" %}
## <mark style="color:purple;">`User/Group Management`</mark>

#### <mark style="color:red;">`Users`</mark>

{% code title="Display user and group ID of the current user" %}
```bash
id 
```
{% endcode %}

{% code title="id from a specific user" %}
```bash
id username
```
{% endcode %}

{% code title="Edit sudoers file" %}
```bash
sudo visudo
```
{% endcode %}

{% code title="Switch to the root user" %}
```bash
su
```
{% endcode %}

{% code title="Switch to another user" %}
```bash
su - username
```
{% endcode %}

#### <mark style="color:red;">`User Management`</mark>

{% code title="Creates a new user" %}
```bash
sudo useradd newuser
```
{% endcode %}

{% code title="Creates a new user with home directory and bash shell " %}
```bash
sudo useradd -m -s /bin/bash newuser
```
{% endcode %}

{% code title="Add user to the sudo group" %}
```bash
sudo usermod -aG sudo newuser
```
{% endcode %}

{% code title="Set or change password" %}
```bash
sudo passwd newuser
```
{% endcode %}

{% code title="Set zsh as default shell" %}
```bash
sudo usermod --shell /usr/bin/zsh alice
```
{% endcode %}

#### <mark style="color:red;">`Groups`</mark>

{% code title="Create group" %}
```bash
sudo groupadd newgroup
```
{% endcode %}

{% code title="Delete Group" %}
```bash
sudo groupdel group
```
{% endcode %}

{% code title="Add user to group" %}
```bash
sudo gpasswd -a newuser newgroup
```
{% endcode %}
{% endhint %}

***

{% hint style="info" %}
## <mark style="color:purple;">`Permission & Security`</mark>

#### <mark style="color:red;">`File Ownership`</mark>

{% code title="Set file permissions to rwxr-xr-x" %}
```bash
sudo chmod 755 file.txt
```
{% endcode %}

{% code title="Adds read permissions for all users" %}
```bash
sudo chmod a+r shell.sh
```
{% endcode %}

{% code title="Add execution permission" %}
```bash
sudo chmod +x script.sh
```
{% endcode %}

{% code title="Change file owner and group" %}
```bash
sudo chown user:group file.txt
```
{% endcode %}

{% code title="Change group ownership" %}
```bash
sudo chgrp group file.txt
```
{% endcode %}

{% code title="Prevent world-writable files" %}
```bash
umask 022 
```
{% endcode %}

#### <mark style="color:red;">`Access Control Lists`</mark>

{% code title="Show the ACL" %}
```bash
getfacl file.txt
```
{% endcode %}

{% code title="Grant read/write permissions to 'user' on file.txt" %}
```bash
setfacl -m u:user:rw file.txt
```
{% endcode %}

#### <mark style="color:red;">`Security Policies`</mark>

{% code title="Display the current SELinux mode" %}
```bash
getenforce
```
{% endcode %}

{% code title="Disable SELinux " %}
```bash
sudo setenforce 0
```
{% endcode %}

#### <mark style="color:red;">`File Integrity`</mark>

{% code title="Generates a SHA256 file" %}
```bash
sha256sum file.txt
```
{% endcode %}

{% code title="Generates a MD5 hash" %}
```bash
md5sum file.txt
```
{% endcode %}

{% code title="Initialize the Tripwire database" %}
```bash
sudo tripwire --init
```
{% endcode %}

{% code title="Check the integrity of the system" %}
```bash
sudo tripwire --check
```
{% endcode %}

{% code title="Generate a report" %}
```bash
sudo tripwire --update
```
{% endcode %}
{% endhint %}

***

{% hint style="info" %}
## <mark style="color:purple;">`Networking Command`</mark>

{% code title="Display network interfaces and their IP addresses" %}
```bash
ifconfig
```
{% endcode %}

{% code title="Display IP addresses of all network interfaces" %}
```bash
ip a 
```
{% endcode %}

{% code title="Bring interface up" %}
```bash
sudo ip link set eth0 up
```
{% endcode %}

{% code title="Show networks accessible via the VPN" %}
```bash
netstat -rn
```
{% endcode %}

{% code title="Show listening TCP/UDP ports" %}
```bash
netstat -tuln
```
{% endcode %}

{% code title="Show listening ports and services" %}
```bash
ss -tuln
```
{% endcode %}

{% code title="Show listening ports for a process" %}
```bash
ss -tulnp | grep PID
```
{% endcode %}

{% code title="Display the Routing Table" %}
```bash
ip route show
```
{% endcode %}

{% code title="Add a route" %}
```bash
sudo ip route add 192.168.2.0/24 via 192.168.1.254
```
{% endcode %}

{% code title="Delete a Route" %}
```bash
sudo ip route del 192.168.2.0/24
```
{% endcode %}

{% code title="Add a Default Gateway" %}
```bash
sudo ip route add default via 192.168.1.1
```
{% endcode %}

{% code title="Change a route's metric" %}
```bash
sudo route change -net 192.168.2.0 netmask 255.255.255.0 gw 192.168.1.254 metric 200
```
{% endcode %}

{% code title="Trace the network path to example.com" %}
```bash
traceroute example.com
```
{% endcode %}
{% endhint %}

***

{% hint style="info" %}
## <mark style="color:purple;">`Chroot`</mark>

#### <mark style="color:red;">`Decrypt the system`</mark>

{% code title="Decrypt partition" %}
```bash
sudo cryptsetup luksOpen /dev/sda3 cryptdisk
```
{% endcode %}

{% code title="Mounts the decrypted device" %}
```bash
sudo mount /dev/mapper/cryptdisk /mnt
```
{% endcode %}

{% code title="Mounts the boot partion" %}
```bash
sudo mount /dev/sda1 /mnt/boot
```
{% endcode %}

{% code title="chroot into a mounted partition" %}
```bash
sudo arch-chroot /mnt
```
{% endcode %}

#### <mark style="color:red;">`Connect using`</mark><mark style="color:orange;">`WPA`</mark>

{% code title="Shows the current connection status for the wpa" %}
```bash
wpa_cli status
```
{% endcode %}

{% code title="Creates the passphrase" %}
```bash
sudo wpa_passphrase "MyWiFi" "mypassword123" | sudo tee /etc/wpa_supplicant/wpa_supplicant.conf
```
{% endcode %}

{% code title="Connect using passphrase" %}
```bash
sudo wpa_supplicant -B -i wlan0 -c /etc/wpa_supplicant/wpa_supplicant.conf
```
{% endcode %}

### <mark style="color:red;">`Boot/UEFI Management`</mark>

{% code title=" Displays the current boot entries in the UEFI firmware" %}
```bash
efibootmgr
```
{% endcode %}

{% code title="deletes the boot entry "0"" %}
```bash
sudo efibootmgr --delete-bootnum --bootnum 0
```
{% endcode %}
{% endhint %}

***

{% hint style="info" %}
### <mark style="color:purple;">`base64`</mark>

* <mark style="color:purple;">Using</mark> <mark style="color:orange;">**`base64`**</mark> <mark style="color:purple;">help to keep file integrity</mark>
* <mark style="color:purple;">Check hashes to avoid file corruption</mark>

{% code title="Generate hash" %}
```sh
md5sum <file>
```
{% endcode %}

***

#### <mark style="color:red;">`Encoding`</mark>

{% code title="Encode File + Redirect Output" %}
```bash
base64 file.txt > hash.txt
```
{% endcode %}

{% code title="Encode String + Redirect Output" %}
```bash
echo "your_string_here" | base64 > encoded_file.txt
```
{% endcode %}

* <mark style="color:purple;">In</mark> <mark style="color:orange;">**`Base64`**</mark> <mark style="color:purple;">encoding, by default, some implementations add line breaks every</mark> <mark style="color:purple;"></mark>_<mark style="color:purple;">76 characters</mark>_ <mark style="color:purple;"></mark><mark style="color:purple;">(following the</mark> <mark style="color:orange;">`RFC 2045 standard`</mark><mark style="color:purple;">).</mark>

{% code title="Encode File Without line break" %}
```bash
base64 -w 0 <file>
```
{% endcode %}

{% code title="Encode String without line breaks" %}
```bash
echo -n "your_string_here" | base64 -w 0
```
{% endcode %}

***

{% code title="Safe URL encoding" %}
```bash
base64 -w 0 <file> | tr '+/' '-_' > url_safe_encoded.txt
```
{% endcode %}

#### <mark style="color:red;">`Decoding`</mark>

{% code title="Decode String + Output to a file" %}
```bash
echo <string> | base64 -d > <file>
```
{% endcode %}

{% code title="Decode File + Output to a file" %}
```bash
base64 -d -i <file> > <decoded_file>
```
{% endcode %}

{% code title="Decode File without line breaks" %}
```bash
base64 -d -w 0 file.txt > decoded_output.bin
```
{% endcode %}
{% endhint %}

