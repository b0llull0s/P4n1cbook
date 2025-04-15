---
description: Basic commands
icon: linux
---

# Linux

<details>

<summary><mark style="color:purple;"><strong><code>Specifications &#x26; Performance</code></strong></mark></summary>

```sh
uptime
```

{% code title="Shows details about all block devices" %}
```bash
lsblk -f
```
{% endcode %}

{% code title="Display RAM info" %}
```bash
free -h
```
{% endcode %}

{% code title="Stats 5s for 10 itinerations" %}
```bash
vmstat 5 10
```
{% endcode %}

{% hint style="info" %}
<mark style="color:red;">**`Check RAM remaining to Memory Locking`**</mark>

{% code title="Check" %}
```sh
ulimit -l
```
{% endcode %}

{% code title="Set a new limit" %}
```sh
ulimit -l 10240
```
{% endcode %}
{% endhint %}

{% code title="List USB" %}
```sh
lsusb
```
{% endcode %}

{% code title="List Peripherals" %}
```bash
lspci
```
{% endcode %}

</details>

<details>

<summary><mark style="color:purple;"><strong><code>Store Management</code></strong></mark></summary>

{% code title="List all files recursively" %}
```sh
ls -lAR
```
{% endcode %}

{% code title="Show Sizes Current Directory" %}
```bash
du -sh *
```
{% endcode %}

{% code title="Largest 10 directories" overflow="wrap" %}
```sh
sudo du -hsx /* | sort -rh | head -n 10
```
{% endcode %}

</details>

<details>

<summary><mark style="color:purple;"><strong><code>File Enumeration</code></strong></mark></summary>

{% code title="Print full path " %}
```bash
realpath file.txt
```
{% endcode %}

{% code title="Count Lines" %}
```bash
wc -l myfile.txt
```
{% endcode %}

{% hint style="info" %}
<mark style="color:orange;">**`locate`**</mark>

{% code title="Look for a file" %}
```bash
locate file.txt
```
{% endcode %}

{% code title="Update the db" %}
```bash
sudo updatedb
```
{% endcode %}
{% endhint %}

{% hint style="info" %}
<mark style="color:orange;">**`find`**</mark>

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
{% endhint %}

</details>

<details>

<summary><mark style="color:purple;"><strong><code>Process Management</code></strong></mark></summary>

{% hint style="info" %}
{% code title="List process" %}
```bash
ps -ef | grep process
```
{% endcode %}

{% code title="Processes by Trees" %}
```bash
ps -auxwf
```
{% endcode %}

{% code title="User process tree + PID" %}
```bash
pstree -p user
```
{% endcode %}

{% code title="Current process ID" %}
```bash
echo $$
```
{% endcode %}

{% code title="Background process" %}
```bash
bg
```
{% endcode %}

{% code title="List background process" overflow="wrap" %}
```bash
jobs
```
{% endcode %}

{% code title="Foreground process" %}
```bash
fg
```
{% endcode %}
{% endhint %}

</details>

<details>

<summary><mark style="color:purple;"><strong><code>Users/Groups</code></strong></mark></summary>

{% hint style="info" %}
{% code title="Edit sudoers file" %}
```bash
sudo visudo
```
{% endcode %}

#### <mark style="color:orange;">**`Users`**</mark>

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

#### <mark style="color:orange;">**`Groups`**</mark>

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

</details>

<details>

<summary><mark style="color:purple;"><strong><code>File Ownership</code></strong></mark></summary>

{% code title="Set file permissions to rwxr-xr-x" %}
```bash
sudo chmod 755 file.txt
```
{% endcode %}

{% code title="Read permissions for all users" %}
```bash
sudo chmod a+r shell.sh
```
{% endcode %}

{% code title="Change file owner and group" %}
```bash
sudo chown user:group file.txt
```
{% endcode %}

{% code title="Add execution permission" %}
```bash
sudo chmod +x script.sh
```
{% endcode %}

{% code title="Change group ownership" %}
```bash
sudo chgrp group file.txt
```
{% endcode %}

</details>

<details>

<summary><mark style="color:purple;"><strong><code>Logs</code></strong></mark></summary>

{% code title="Current login user" %}
```bash
w
```
{% endcode %}

{% code title="Display login records" %}
```bash
last
```
{% endcode %}

{% code title="Display bad login attempts" %}
```sh
lastb
```
{% endcode %}

{% code title="Kernel and boot messages" %}
```bash
dmesg
```
{% endcode %}

{% hint style="info" %}
#### <mark style="color:orange;">**`journalctl`**</mark>

{% code title="Shows logs live" %}
```sh
journalctl -f 
```
{% endcode %}

{% code title="Logs from the current boot" %}
```sh
journalctl -b
```
{% endcode %}

{% code title="Logs from the previous boot" %}
```bash
journalctl -b -1
```
{% endcode %}

{% code title="Logs from a specific service" %}
```bash
journalctl -u <service>
```
{% endcode %}

{% code title="Logs for a specific process" %}
```bash
journalctl _PID=<pid>
```
{% endcode %}

{% code title="Shows logs from the kernel" %}
```sh
journalctl -k
```
{% endcode %}

{% code title="Logs by time-frame" %}
```bash
journalctl --since "2024-11-01" --until "2024-11-10"
```
{% endcode %}

#### <mark style="color:red;">**`Priority Levels`**</mark>

```bash
journalctl -p <level>
```

* <mark style="color:orange;">**`0`**</mark> <mark style="color:purple;">**-->**</mark> <mark style="color:purple;">**`emergency`**</mark>
* <mark style="color:orange;">**`1`**</mark> <mark style="color:purple;">**-->**</mark> <mark style="color:purple;">**`alert`**</mark>
* <mark style="color:orange;">**`2`**</mark> <mark style="color:purple;">**-->**</mark> <mark style="color:purple;">**`critical`**</mark>
* <mark style="color:orange;">**`3`**</mark> <mark style="color:purple;">**-->**</mark> <mark style="color:purple;">**`error`**</mark>
* <mark style="color:orange;">**`4`**</mark> <mark style="color:purple;">**-->**</mark> <mark style="color:purple;">**`warning`**</mark>
* <mark style="color:orange;">**`5`**</mark><mark style="color:purple;">**-->**</mark> <mark style="color:purple;">**`notice`**</mark>
* <mark style="color:orange;">**`6`**</mark> <mark style="color:purple;">**-->**</mark> <mark style="color:purple;">**`informational`**</mark>
* <mark style="color:orange;">**`7`**</mark> <mark style="color:purple;">**-->**</mark> <mark style="color:purple;">**`debug`**</mark>
{% endhint %}



</details>

{% hint style="info" %}
<mark style="color:red;">**`Prevent world-writable files`**</mark>

```bash
umask 022
```
{% endhint %}

<details>

<summary><mark style="color:purple;"><strong><code>Access Control Lists</code></strong></mark></summary>

{% code title="Grant read/write permissions to 'user' on file.txt" %}
```bash
setfacl -m u:user:rw file.txt
```
{% endcode %}

{% code title="Show the ACL" %}
```bash
getfacl file.txt
```
{% endcode %}

</details>

{% hint style="info" %}
<mark style="color:red;">**`Change a route's metric`**</mark>

{% code overflow="wrap" %}
```sh
sudo route change -net 192.168.2.0 netmask 255.255.255.0 gw 192.168.1.254 metric 200
```
{% endcode %}
{% endhint %}

<details>

<summary><mark style="color:orange;"><strong><code>tripwire</code></strong></mark></summary>

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

</details>

<details>

<summary><mark style="color:orange;"><strong><code>SELinux</code></strong></mark></summary>

{% code title="Display  mode" %}
```bash
getenforce
```
{% endcode %}

{% code title="Disable SELinux " %}
```bash
sudo setenforce 0
```
{% endcode %}

</details>

<details>

<summary><mark style="color:orange;"><strong><code>Chroot</code></strong></mark></summary>

{% hint style="info" %}


#### <mark style="color:red;">**`Decrypt the system`**</mark>

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

#### <mark style="color:red;">**`Connect using WPA`**</mark>

{% code title="Shows connection status" %}
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

#### <mark style="color:red;">**`Boot/UEFI Management`**</mark>

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



</details>

<details>

<summary><mark style="color:orange;"><strong><code>base64</code></strong></mark></summary>

{% hint style="info" %}
{% code title="Generate MD5 hash" %}
```sh
md5sum <file>
```
{% endcode %}

{% code title="Generates a SHA256 hash" %}
```bash
sha256sum file.txt
```
{% endcode %}

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

</details>

<details>

<summary><mark style="color:orange;"><strong><code>ip</code></strong></mark></summary>

{% code title="Bring interface up" overflow="wrap" %}
```bash
sudo ip link set eth0 up
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

</details>

<details>

<summary><mark style="color:orange;"><strong><code>ping</code></strong></mark></summary>

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

{% hint style="info" %}
<mark style="color:orange;">**`TTL`**</mark>**&#x20;**<mark style="color:purple;">**Values and**</mark>**&#x20;**<mark style="color:orange;">**`OS`**</mark>**&#x20;**<mark style="color:purple;">**Fingerprinting**</mark>

* <mark style="color:purple;">The</mark> <mark style="color:orange;">**`TTL`**</mark> <mark style="color:purple;">value in the ping response is a starting value decremented by one for each hop the packet takes; Values differ between operating systems:</mark>
* <mark style="color:orange;">**`Linux/Unix`**</mark> <mark style="color:purple;">-></mark> <mark style="color:orange;">**`64`**</mark>
* <mark style="color:orange;">**`Windows`**</mark> <mark style="color:purple;">-></mark> <mark style="color:orange;">**`128`**</mark>
* <mark style="color:orange;">**`Cisco`**</mark> <mark style="color:purple;">-></mark> <mark style="color:orange;">**`255`**</mark>
{% endhint %}

{% code title="Send 4 packages" overflow="wrap" %}
```bash
ping -c 4 example.com
```
{% endcode %}

{% hint style="info" %}
* <mark style="color:purple;">It sends</mark> <mark style="color:orange;">**`ICMP Echo Request`**</mark> <mark style="color:purple;">packets to a target and waits for</mark> <mark style="color:orange;">**`ICMP Echo Reply`**</mark> <mark style="color:purple;">packets in return.</mark>

{% code title="Output Example" overflow="wrap" %}
```bash
PING 192.168.1.1 (192.168.1.1) 56(84) bytes of data.
64 bytes from 192.168.1.1: icmp_seq=1 ttl=64 time=0.123 ms
64 bytes from 192.168.1.1: icmp_seq=2 ttl=64 time=0.120 ms
64 bytes from 192.168.1.1: icmp_seq=3 ttl=64 time=0.122 ms
```
{% endcode %}

* <mark style="color:orange;">**`TTL`**</mark>**&#x20;**<mark style="color:purple;">**(Time to Live)**</mark><mark style="color:purple;">: The maximum number of hops a packet can traverse before being discarded.</mark>
* <mark style="color:orange;">**`Time`**</mark><mark style="color:purple;">: The round-trip time (</mark><mark style="color:orange;">**`RTT`**</mark><mark style="color:purple;">) for the packet to reach the destination and return.</mark>
{% endhint %}

</details>

<details>

<summary><mark style="color:orange;"><strong><code>ss</code></strong></mark></summary>

{% code title="Listening ports & services" %}
```bash
ss -tuln
```
{% endcode %}

{% code title="Listening ports + PID" %}
```bash
ss -tulnp | grep PID
```
{% endcode %}

{% code title="Trace the network path" %}
```bash
traceroute example.com
```
{% endcode %}

</details>

<details>

<summary><mark style="color:orange;"><strong><code>Qemu</code></strong></mark></summary>

{% code title="Installation" overflow="wrap" lineNumbers="true" %}
```sh
sudo pacman -S qemu libvirt dnsmasq virt-manager bridge-utils ebtables
sudo systemctl enable --now libvirtd
```
{% endcode %}

{% code title="Check/Backup the XML" overflow="wrap" %}
```sh
sudo virsh net-dumpxml c2-lab
```
{% endcode %}

{% hint style="info" %}
<mark style="color:red;">**`Manual XML Virtual Network Configuration`**</mark>

{% code title="Locked-down Version" overflow="wrap" %}
```xml
<network>
  <name>c2-lab</name>
  <bridge name="virbr2" stp="off" delay="0"/>  <!-- Disable STP (not needed) -->
  <forward mode="none"/>                       <!-- NO NAT, NO ROUTING -->
  <interface type="network">
  <mac address="52:54:00:XX:XX:XX"/>  <!-- Set a static MAC -->
  <source network="c2-lab"/>
  <model type="virtio"/>
</interface>
  <ip address="192.168.100.1" netmask="255.255.255.0">
  <ip family="ipv6" address="fe80::1" prefix="64"/>
    <!-- No DHCP (assign IPs manually) -->
  </ip>
</network>
```
{% endcode %}
{% endhint %}

{% code title="Disable ICMP" overflow="wrap" %}
```sh
sudo iptables -I FORWARD -i virbr2 -p icmp -j DROP
```
{% endcode %}

{% hint style="info" %}
<mark style="color:purple;">**`Start the Virtual-Network`**</mark>

{% code overflow="wrap" lineNumbers="true" %}
```sh
sudo virsh net-define c2-lab.xml
sudo virsh net-start c2-lab
```
{% endcode %}

{% code title="Start on boot" overflow="wrap" %}
```sh
sudo virsh net-autostart c2-lab
```
{% endcode %}

{% code title="Check Network Info" overflow="wrap" %}
```sh
sudo virsh net-info c2-lab
```
{% endcode %}

{% code title="Check for leaks" %}
```sh
sudo iptables -L -v -n | grep virbr2
```
{% endcode %}
{% endhint %}

</details>
