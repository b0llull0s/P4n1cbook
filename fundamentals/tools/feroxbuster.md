---
icon: rust
description: Recursive Web Enumeration Tool - Rust
---

# feroxbuster

## <mark style="color:purple;">Installation</mark>

{% tabs %}
{% tab title="Arch" %}
{% hint style="success" %}
<pre class="language-sh" data-title="AUR repo" data-full-width="false"><code class="lang-sh"><strong>yay -S feroxbuster
</strong></code></pre>
{% endhint %}
{% endtab %}

{% tab title="Kali" %}
{% hint style="success" %}
```sh
sudo apt get feroxbuster
```
{% endhint %}
{% endtab %}
{% endtabs %}

***

{% hint style="info" %}
## <mark style="color:purple;">Common Uses</mark>

{% code title="Basic Usage" %}
```sh
feroxbuster -u <url> -w <wordlist>
```
{% endcode %}

{% code title="Verbose Output" %}
```sh
feroxbuster -u <url> -w <wordlist> -v
```
{% endcode %}

{% code title="Save output to a file" %}
```sh
feroxbuster -u <url> -w <wordlist> --output <file.txt>
```
{% endcode %}

{% code title="Look for extensions" %}
```bash
feroxbuster -u <url> -w <wordlist> --extensions .txt, .js
```
{% endcode %}
{% endhint %}

***

{% hint style="warning" %}
## <mark style="color:purple;">Scanner Parameters</mark>

{% code title="Number of threads" %}
```sh
feroxbuster -u <url> -w <wordlist> -t <number_of_threads>
```
{% endcode %}

{% code title="Maximum amount of active connections per thread" %}
```sh
feroxbuster -u <url> -w <wordlist> --scan-limit <number>
```
{% endcode %}

{% code title="Set a timeout" %}
```sh
feroxbuster -u <url> -w <wordlist> --rate-limit <number>
```
{% endcode %}

* <mark style="color:purple;">For example, in this case there will be</mark> <mark style="color:orange;">**8**</mark> <mark style="color:purple;">active connections and each connection will have a timeout of</mark> <mark style="color:orange;">**500ms**</mark> <mark style="color:purple;">for</mark> <mark style="color:orange;">**1**</mark> <mark style="color:purple;">URL at the time</mark>

```sh
feroxbuster --threads 4 --scan-limit 2 --rate-limit 2
```

* <mark style="color:purple;">On the other the hand, here there will be</mark> <mark style="color:orange;">**8**</mark> <mark style="color:purple;">active connection with a timeout of</mark> <mark style="color:orange;">**500ms**</mark> <mark style="color:purple;">for</mark> <mark style="color:orange;">**4**</mark> <mark style="color:purple;">URLs at the time</mark>

```sh
feroxbuster --threads 2--scan-limit 4 --rate-limit 2
```
{% endhint %}

***

{% hint style="warning" %}
## <mark style="color:purple;">Filters</mark>

{% code title="Exclude by status code" %}
```sh
feroxbuster -u <url> -w <wordlist> -x 404
```
{% endcode %}

{% code title="Include by status code" %}
```bash
feroxbuster -u <url> -w <wordlist> -c 200
```
{% endcode %}

{% code title="Exclude by size request" %}
```sh
feroxbuster -u <url> -w <wordlist> -S <size>
```
{% endcode %}

{% code title="Exclude by regex" %}
```bash
feroxbuster -u <url> -w <wordlist> -X "Access Denied"
```
{% endcode %}

{% code title="Exclude by words" %}
```bash
feroxbuster -u <url> -w <wordlist> -W 0-10
```
{% endcode %}

{% code title="Exclude by lines" %}
```bash
feroxbuster -u <url> -w <wordlist> -N 50-
```
{% endcode %}

{% code title="Exclude a directory" %}
```bash
feroxbuster -u <url> -w <wordlist> --dont-scan /uploads
```
{% endcode %}

{% code title="Exclude similar pages" %}
```bash
feroxbuster -u <url> -w <wordlist> --filter-similar-to error.html
```
{% endcode %}
{% endhint %}

***

{% hint style="warning" %}
## <mark style="color:purple;">Special Options</mark>

{% code title="Recursive Scan" %}
```bash
feroxbuster -u http://example.com -w wordlist.txt --depth 3
```
{% endcode %}

{% code title="Disable Recursion" %}
```bash
feroxbuster -u http://example.com -w wordlist.txt --no-recursion
```
{% endcode %}

{% code title="Follow redirects automatically" %}
```bash
feroxbuster -u http://example.com -w wordlist.txt --url-redirect
```
{% endcode %}

{% code title="Specify the user agent" %}
```sh
feroxbuster -u <url> -w <wordlist> -H "User-Agent: <user_agent>"
```
{% endcode %}

{% code title="Provide a User Cookie" %}
```bash
feroxbuster -u http://example.com -w /path/to/wordlist.txt -H "Cookie: sessionid=your_session_id"
```
{% endcode %}

{% code title="Follow redirects from 302 responses" %}
```sh
feroxbuster -u <url> -w <wordlist> -r
```
{% endcode %}

{% code title="Use SSL verification/Disable TLS validation" %}
```sh
feroxbuster -u <url> -w <wordlist> --insecure
```
{% endcode %}

{% code title="Collect Words" %}
```sh
feroxbuster -u <url> -w <wordlist> --collect-words
```
{% endcode %}

{% code title="Extract links" %}
```bash
feroxbuster -u <url> -w <wordlist> --extract-links
```
{% endcode %}

{% code title="Collect Backups" %}
```sh
feroxbuster -u <url> -w <wordlist> --collect-backups
```
{% endcode %}
{% endhint %}
