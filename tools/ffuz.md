---
description: Fuzz Faster U Fool
icon: campfire
---

# ffuf

{% hint style="success" %}
## <mark style="color:purple;">Installation</mark>

{% code title="From Source" %}
```bash
go get github.com/ffuf/ffuf
```
{% endcode %}
{% endhint %}

***

{% hint style="info" %}
## <mark style="color:purple;">Operators</mark>

* <mark style="color:orange;">**`-u`**</mark> <mark style="color:purple;">-> Target URL.</mark>
* <mark style="color:orange;">**`-w`**</mark> <mark style="color:purple;">-> Path to wordlist.</mark>
* <mark style="color:orange;">**`-t`**</mark> <mark style="color:purple;">-> Number of threads to run ( Normal :</mark> <mark style="color:orange;">**`50`**</mark><mark style="color:purple;">; Fast:</mark> <mark style="color:orange;">**`200`**</mark><mark style="color:purple;">).</mark>
* <mark style="color:orange;">**`-v`**</mark> <mark style="color:purple;">-> Verbose Output.</mark>
* <mark style="color:orange;">**`-c`**</mark> <mark style="color:purple;">-> Colorful output.</mark>&#x20;
* <mark style="color:orange;">**`-e <extension>`**</mark> <mark style="color:purple;">-> Scan for extensions.</mark>&#x20;
* <mark style="color:orange;">**`-sf`**</mark> <mark style="color:purple;">-> Stop in first found result.</mark>
* <mark style="color:orange;">**`-p`**</mark> <mark style="color:purple;">-> Set a pause between request.</mark>
* <mark style="color:orange;">**`-rate <10>`**</mark> <mark style="color:purple;">-> Set rate-requests per second.</mark>
* <mark style="color:orange;">**`-retries`**</mark> <mark style="color:purple;">-> Number of retries for each request.</mark>
* <mark style="color:orange;">**`-timeout`**</mark> <mark style="color:purple;">-> Timeout before giving up on a request.</mark>
* <mark style="color:orange;">**`-of <format>`**</mark> <mark style="color:purple;">-> Output format (</mark><mark style="color:orange;">**`json`**</mark><mark style="color:purple;">,</mark> <mark style="color:orange;">**`csv`**</mark><mark style="color:purple;">,</mark> <mark style="color:orange;">**`html`**</mark><mark style="color:purple;">)</mark>
* <mark style="color:orange;">**`-x`**</mark> <mark style="color:purple;">-> Use a proxy for requests.</mark>
* <mark style="color:orange;">**`-replay-proxy`**</mark> <mark style="color:purple;">**->**</mark> <mark style="color:purple;"></mark><mark style="color:purple;">Routes</mark> <mark style="color:purple;"></mark><mark style="color:purple;">**only fuzzed**</mark> <mark style="color:purple;"></mark><mark style="color:purple;">requests through the proxy.</mark>
* <mark style="color:orange;">**`-H <"Header: Value">`**</mark> <mark style="color:purple;">-> Set a custom header.</mark>
* <mark style="color:orange;">**`-auth <username:password>`**</mark> <mark style="color:purple;">-> Basic HTTP authentication.</mark>
* &#x20;<mark style="color:orange;">**`-recursion -recursion-depth 1`**</mark> <mark style="color:purple;">-> Recursive fuzzing.</mark>
* <mark style="color:orange;">**`-request request.txt`**</mark> <mark style="color:purple;">-></mark> <mark style="color:purple;"></mark><mark style="color:purple;">**Specifies a custom HTTP request file that serves as a template (Add fuzzing points inside).**</mark>

### <mark style="color:purple;">Matchers/Filters</mark>

* <mark style="color:orange;">**`-mc`**</mark> <mark style="color:purple;">-> Match specific status code.</mark>
* <mark style="color:orange;">**`-ms`**</mark> <mark style="color:purple;">-> Match specific response size.</mark>
* <mark style="color:orange;">**`-mr <"regex">`**</mark> <mark style="color:purple;">-> Match by regex.</mark>
* <mark style="color:orange;">**`-ml`**</mark> <mark style="color:purple;">-> Match amount of lines in the response.</mark>
* <mark style="color:orange;">**`-mw`**</mark> <mark style="color:purple;">-> Match by words count in response.</mark>
* <mark style="color:orange;">**`-fw`**</mark> <mark style="color:purple;">-> Filter by content length.</mark>
* <mark style="color:orange;">**`-fc`**</mark> <mark style="color:purple;">-> Filter out specific status codes.</mark>
* <mark style="color:orange;">**`-ac`**</mark> <mark style="color:purple;">-> Set Auto-calibration filter.</mark>
* <mark style="color:orange;">**`-acc`**</mark> <mark style="color:purple;">-> Filter Custom-calibration.</mark>
* <mark style="color:orange;">**`-ic`**</mark> <mark style="color:purple;">-> Ignores comments and copyright.</mark>
{% endhint %}

***

{% hint style="warning" %}
## <mark style="color:purple;">Directory Fuzzing</mark>

{% code title="Basic Scan" %}
```bash
ffuf -c -w wordlist.txt:FUZZ -u http://SERVER_IP:PORT/FUZZ
```
{% endcode %}

{% code title="Recursive Scan" %}
```bash
ffuf -c -w /path/to/wordlist -u https://ffuf.io.fi/FUZZ -recursion -recursion-depth 2
```
{% endcode %}

{% code title="Scan for PHP pages" %}
```bash
ffuf -c -w wordlist.txt:FUZZ -u http://SERVER_IP:PORT/FUZZ.php
```
{% endcode %}

{% code title="Scan for HTML pages" %}
```bash
ffuf -c -w wordlist.txt:FUZZ -u http://SERVER_IP:PORT/FUZZ.html
```
{% endcode %}

{% code title="Fuzz Multiple locations" %}
```bash
ffuf -u https://W2/W1 -w ./wordlist.txt:W1,./domains.txt:W2
```
{% endcode %}
{% endhint %}

***

{% hint style="danger" %}
## <mark style="color:purple;">Extension fuzzing</mark>

{% code title="Standard use" %}
```bash
ffuf -c -w /path/to/wordlist -u https://ffuf.io.fi/FUZZ -e .bak, .zip
```
{% endcode %}

{% code title="Extension + Recursion" %}
```bash
ffuf -w wordlist.txt:FUZZ -u http://SERVER_IP:PORT/FUZZ -recursion -recursion-depth 1 -e .php -v -c
```
{% endcode %}
{% endhint %}

***

{% hint style="warning" %}
## <mark style="color:purple;">Subdomain fuzzing</mark>

{% code title="Subdomains" %}
```bash
ffuf -w wordlist.txt:FUZZ -u https://FUZZ.hackthebox.eu/
```
{% endcode %}

{% code title="VHOST Fuzzing" %}
```bash
ffuf -c -w /path/to/wordlist -u https://ffuf.io.fi -H "Host: FUZZ.ffuf.io.fi"
```
{% endcode %}
{% endhint %}

***

{% hint style="danger" %}
## <mark style="color:purple;">HTTP Fuzzing</mark>

{% code title="Cookie-based Authentication" %}
```bash
ffuf -c -w /path/to/wordlist -u https://ffuf.io.fi -b "sessionId=cookie_val"
```
{% endcode %}

{% code title="Fuzz from request template" %}
```bash
ffuf -request ~/Desktop/request.txt -w ./wordlist.txt -u http://site.com
```
{% endcode %}

{% code title="Request Template + Proxy" %}
```bash
ffuf -request ~/Desktop/request.txt -w ./wordlist.txt -x http://127.0.0.1:8080
```
{% endcode %}

{% code title="Request Template + Replay-proxy" %}
```bash
ffuf -request ~/Desktop/request.txt -w ./wordlist.txt -replay-proxy http://127.0.0.1:8080
```
{% endcode %}

### <mark style="color:purple;">Parameter Fuzzing</mark>

{% code title="GET Parameter Fuzzing" %}
```bash
ffuf -c -w /path/to/wordlist -u https://ffuf.io.fi?FUZZ=test_value
```
{% endcode %}

{% code title="POST Data Fuzzing" %}
```bash
ffuf -c -w /path/to/wordlist -X POST -d "username=admin&password=FUZZ" -u https://ffuf.io.fi/login.php
```
{% endcode %}

{% code title="JSON POST data fuzzing" %}
```bash
ffuf -c -w /path/to/wordlist -X POST -d "username=admin&password=FUZZ" -u https://ffuf.io.fi/login.php
```
{% endcode %}

### <mark style="color:purple;">Path Traversal fuzzing</mark>

{% code title="Fuzz LFI" %}
```bash
ffuf -w /opt/useful/SecLists/Fuzzing/LFI/LFI-Jhaddix.txt:FUZZ -u 'http://<SERVER_IP>:<PORT>/index.php?language=FUZZ' -fs 2287
```
{% endcode %}

{% code title="Fuzz webroot path" %}
```bash
ffuf -w /opt/useful/SecLists/Discovery/Web-Content/default-web-root-directory-linux.txt:FUZZ -u 'http://<SERVER_IP>:<PORT>/index.php?language=../../../../FUZZ/index.php' -fs 2287
```
{% endcode %}
{% endhint %}
