---
description: Network File System
icon: network-wired
---

# NFS

{% embed url="https://github.com/NetDirect/nfsshell" %}

{% hint style="info" %}
* <mark style="color:purple;">Mount shares in to your local system:</mark>

```sh
sudo mount 10.10.10.34:/var/nfsshare /mnt
```
{% endhint %}

***

<details>

<summary><mark style="color:purple;"><strong><code>Enumeration</code></strong></mark></summary>

{% code title="Use nmap scripts" %}
```bash
nmap -sV --script=nfs-ls 10.10.10.34
```
{% endcode %}

{% hint style="info" %}
* <mark style="color:purple;">And the</mark> <mark style="color:orange;">**`showmount`**</mark> <mark style="color:purple;">command to list all the shares:</mark>

```sh
showmount -e 10.10.10.34
```

* <mark style="color:purple;">To look the configuration on the server side:</mark>

```sh
cat /etc/exports
```
{% endhint %}

</details>

<details>

<summary><mark style="color:purple;"><strong><code>Configuration</code></strong></mark></summary>

{% hint style="info" %}


#### <mark style="color:red;">**`Access Options`**</mark>&#x20;

* <mark style="color:orange;">**`rw`**</mark><mark style="color:purple;">**:**</mark> <mark style="color:purple;"></mark><mark style="color:purple;">Allows clients to read from and write to the shared directory.</mark>
* <mark style="color:orange;">**`ro`**</mark><mark style="color:purple;">**:**</mark> <mark style="color:purple;"></mark><mark style="color:purple;">Allows clients to only read from the shared directory.</mark>

***

#### <mark style="color:red;">**`Sync and Async Options`**</mark>

* <mark style="color:orange;">**`sync`**</mark>**:** <mark style="color:purple;">Ensures all changes are written to disk before the</mark> <mark style="color:orange;">**`NFS`**</mark> <mark style="color:purple;">server responds to the client. This is safer but slower.</mark>
* <mark style="color:orange;">**`async`**</mark><mark style="color:purple;">**:**</mark> <mark style="color:purple;"></mark><mark style="color:purple;">Allows the server to respond before data is written to disk. This improves performance but can lead to data loss if the server crashes.</mark>

***

#### <mark style="color:red;">**`User Mapping Options`**</mark>

* <mark style="color:orange;">**`root_squash`**</mark><mark style="color:purple;">**:**</mark> <mark style="color:purple;"></mark><mark style="color:purple;">Maps root user requests from clients to the</mark> <mark style="color:orange;">**`nfsnobody`**</mark> <mark style="color:purple;">user (or equivalent) on the server, restricting root access.</mark>
* <mark style="color:orange;">**`no_root_squash`**</mark><mark style="color:purple;">**:**</mark> <mark style="color:purple;"></mark><mark style="color:purple;">Grants root user on the client the same privileges as root on the server. Use with caution, as it can lead to security risks.</mark>
* <mark style="color:orange;">**`all_squash`**</mark><mark style="color:purple;">**:**</mark> <mark style="color:purple;"></mark><mark style="color:purple;">Maps all client users (including root) to the</mark> <mark style="color:orange;">**`nfsnobody`**</mark> <mark style="color:purple;">user (or equivalent) on the server.</mark>
* <mark style="color:orange;">**`no_all_squash`**</mark><mark style="color:purple;">**:**</mark> <mark style="color:purple;"></mark><mark style="color:purple;">Retains the original</mark> <mark style="color:orange;">**`UID`**</mark> <mark style="color:purple;">and</mark> <mark style="color:orange;">**`GID`**</mark> <mark style="color:purple;">of non-root users from the client on the server. This is the default.</mark>
* <mark style="color:orange;">**`anonuid=<UID>`**</mark><mark style="color:purple;">**:**</mark> <mark style="color:purple;"></mark><mark style="color:purple;">Sets the</mark> <mark style="color:orange;">**`UID`**</mark> <mark style="color:purple;">of the anonymous user for</mark> <mark style="color:orange;">**`all_squash`**</mark> <mark style="color:purple;">or</mark> <mark style="color:orange;">**`root_squash`**</mark><mark style="color:purple;">. Default is</mark> <mark style="color:orange;">**`65534`**</mark> <mark style="color:purple;">(</mark><mark style="color:orange;">**`nfsnobody`**</mark><mark style="color:purple;">).</mark>
* <mark style="color:orange;">**`anongid=<GID>`**</mark><mark style="color:purple;">**:**</mark> <mark style="color:purple;"></mark><mark style="color:purple;">Sets the</mark> <mark style="color:orange;">**`GID`**</mark> <mark style="color:purple;">of the anonymous user. Default is</mark> <mark style="color:orange;">**`65534`**</mark><mark style="color:purple;">.</mark>

***

#### <mark style="color:red;">**`Security and Access Control`**</mark>

* <mark style="color:orange;">**`secure`**</mark>**:** <mark style="color:purple;">Requires clients to use a privileged port (below</mark> <mark style="color:orange;">**`1024`**</mark><mark style="color:purple;">) for communication. This is the default.</mark>
* <mark style="color:orange;">**`insecure`**</mark><mark style="color:purple;">**:**</mark> <mark style="color:purple;"></mark><mark style="color:purple;">Allows clients to connect from any port, including unprivileged ports (above</mark> <mark style="color:orange;">**`1024`**</mark><mark style="color:purple;">). Necessary for some client configurations.</mark>
* <mark style="color:orange;">**`no_subtree_check`**</mark><mark style="color:purple;">**:**</mark> <mark style="color:purple;"></mark><mark style="color:purple;">Disables</mark> <mark style="color:orange;">**`subtree`**</mark> <mark style="color:purple;">checking. Recommended for shared directories where the export does not match the actual filesystem hierarchy, as it improves performance.</mark>
* <mark style="color:orange;">**`subtree_check`**</mark><mark style="color:purple;">**:**</mark> <mark style="color:purple;"></mark><mark style="color:purple;">Enables</mark> <mark style="color:orange;">**`subtree`**</mark> <mark style="color:purple;">checking. Verifies that the requested file is within the exported tree. This is the default.</mark>

***

#### <mark style="color:red;">**`Performance Options`**</mark>

* <mark style="color:orange;">**`no_wdelay`**</mark><mark style="color:purple;">**:**</mark> <mark style="color:purple;"></mark><mark style="color:purple;">Prevents the</mark> <mark style="color:orange;">**`NFS`**</mark> <mark style="color:purple;">server from delaying writes. Useful when multiple clients write to the same file simultaneously.</mark>
* <mark style="color:orange;">**`wdelay`**</mark><mark style="color:purple;">**:**</mark> <mark style="color:purple;"></mark><mark style="color:purple;">Causes the server to delay writes slightly to optimize performance when multiple write requests arrive. This is the default.</mark>

***

#### <mark style="color:red;">**`Client Specification`**</mark>

* <mark style="color:orange;">**`<IP>`**</mark><mark style="color:purple;">**:**</mark> <mark style="color:purple;"></mark><mark style="color:purple;">Specifies a single client IP (e.g.,</mark> <mark style="color:orange;">**`10.10.10.1`**</mark><mark style="color:purple;">).</mark>
* <mark style="color:orange;">**`<subnet>`**</mark><mark style="color:purple;">**:**</mark> <mark style="color:purple;"></mark><mark style="color:purple;">Specifies a subnet (e.g.,</mark> <mark style="color:orange;">**`10.10.10.0/24`**</mark><mark style="color:purple;">).</mark>
* <mark style="color:orange;">**`*`**</mark><mark style="color:purple;">**:**</mark> <mark style="color:purple;"></mark><mark style="color:purple;">Allows all clients to connect. Use cautiously as this is less secure.</mark>
* <mark style="color:orange;">**`<hostname>`**</mark><mark style="color:purple;">**:**</mark> <mark style="color:purple;"></mark><mark style="color:purple;">Specifies a hostname for allowed clients.</mark>
{% endhint %}

</details>
