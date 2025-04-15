---
icon: laptop-binary
---

# Binaries

{% code title="Show the real path" %}
```sh
which binary
```
{% endcode %}

{% code title="Display Binary data" %}
```bash
cat example | hexdump -C
```
{% endcode %}

<details>

<summary><mark style="color:purple;"><strong>Understanding</strong></mark><strong> </strong><mark style="color:orange;"><strong><code>ltrace</code></strong></mark><strong> </strong><mark style="color:purple;"><strong>Outputs</strong></mark></summary>

<mark style="color:purple;">The quickest way to get a feel for what a binary is doing is to run it with</mark> <mark style="color:orange;">**`ltrace`**</mark><mark style="color:purple;">, which will print all the library calls it’s making:</mark>

```sh
ltrace <BINARY> id
```

{% hint style="info" %}


#### <mark style="color:red;">**`UID Checks and Privilege Escalation`**</mark>

* <mark style="color:purple;">The</mark> <mark style="color:orange;">**`setuid(0)`**</mark> <mark style="color:purple;">function call attempts to set the</mark> <mark style="color:orange;">**`UID`**</mark> <mark style="color:purple;">to</mark> <mark style="color:orange;">**`root`**</mark><mark style="color:purple;">. If it succeeds returns</mark> <mark style="color:orange;">**`0`**</mark><mark style="color:purple;">.</mark>&#x20;
* <mark style="color:purple;">A failure (</mark><mark style="color:orange;">**`-1`**</mark><mark style="color:purple;">) may indicate the program requires elevated permissions to execute certain operations.</mark>
{% endhint %}

***

{% hint style="info" %}


#### <mark style="color:red;">**`Whitelists/Blacklists`**</mark>

* <mark style="color:orange;">**`strncmp`**</mark> <mark style="color:purple;">or</mark> <mark style="color:orange;">**`strcmp`**</mark> <mark style="color:purple;">calls are used to compare input against predefined strings. A return value of</mark> <mark style="color:orange;">**`-1`**</mark> <mark style="color:purple;">indicates a mismatch.</mark>
* <mark style="color:orange;">**`strcspn`**</mark> <mark style="color:purple;">calls are used to check for forbidden characters (e.g.,</mark> <mark style="color:orange;">**`|`**</mark><mark style="color:purple;">,</mark> <mark style="color:orange;">**`&`**</mark><mark style="color:purple;">,</mark> <mark style="color:orange;">**`>`**</mark><mark style="color:purple;">, which could be part of command injection attempts).</mark>
{% endhint %}

***

{% hint style="info" %}


#### <mark style="color:red;">**`File Operations and File Descriptors`**</mark>

* <mark style="color:purple;">Look for files related to user credentials, configuration, or logs.</mark>
{% endhint %}

***

{% hint style="info" %}


#### <mark style="color:red;">**`External Command Execution`**</mark>

* <mark style="color:purple;">Calls to</mark> <mark style="color:orange;">**`system()`**</mark><mark style="color:purple;">,</mark> <mark style="color:orange;">**`execvp()`**</mark><mark style="color:purple;">, or similar functions: These often indicate the program is executing shell commands.</mark>
* <mark style="color:purple;">Input passed to these commands: If user input directly influences these calls, it might indicate an injection vulnerability.</mark>
{% endhint %}

***

{% hint style="info" %}


#### <mark style="color:red;">**`Signals and Inter-Process Communication`**</mark>

* <mark style="color:purple;">Signals like</mark> <mark style="color:orange;">**`SIGCHLD`**</mark><mark style="color:purple;">,</mark> <mark style="color:orange;">**`SIGSEGV`**</mark><mark style="color:purple;">, or</mark> <mark style="color:orange;">**`SIGKILL`**</mark> <mark style="color:purple;">in the output.</mark>
* <mark style="color:purple;">Use of</mark> <mark style="color:orange;">**`kill()`**</mark> <mark style="color:purple;">to manage or terminate processes, which can indicate how the program interacts with other processes.</mark>
{% endhint %}

</details>

