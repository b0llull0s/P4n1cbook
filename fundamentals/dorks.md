---
icon: google
description: Advanced Google Search
---

# Dorks

## <mark style="color:purple;">Build-in Queries:</mark>

{% hint style="info" %}
{% code title="Specific site" %}
```
"<word>" site:<example.com>
```
{% endcode %}
{% endhint %}

{% hint style="info" %}
{% code title="Key Words in the URL" %}
```
inurl:"</PATH/IN/THE/SITE.php>" site:<example.com>
```
{% endcode %}
{% endhint %}

{% hint style="info" %}
{% code title="Key words in tittle" %}
```
intittle:"<word>" site:<example.com>
```
{% endcode %}
{% endhint %}

{% hint style="info" %}
{% code title="Hyper-Links on the website" %}
```
link:"https://example.com
```
{% endcode %}
{% endhint %}

{% hint style="info" %}
{% code title="Specific File Type" %}
```
filetype:<log> site:<example.com>
```
{% endcode %}
{% endhint %}

## <mark style="color:purple;">Operators:</mark>

{% hint style="info" %}
{% code title="Wildcard (*)" %}
```
"How to hack * using google"
```
{% endcode %}
{% endhint %}

{% hint style="info" %}
<mark style="color:red;">**Adding quotation marks around your search terms forces an exact match.**</mark>
{% endhint %}

{% hint style="info" %}
{% code title="OR (|)" %}
```
"how to hack" site:(reddit.com | stackoverflow.com)
```
{% endcode %}
{% endhint %}

{% hint style="info" %}
{% code title="Minus (-)" %}
```
site:example.com password -ext:txt
```
{% endcode %}
{% endhint %}

## <mark style="color:purple;">Examples:</mark>

{% embed url="https://www.exploit-db.com/google-hacking-database" fullWidth="false" %}
Google Hacking Database
{% endembed %}

<details>

<summary><mark style="color:purple;"><strong>Recon</strong></mark></summary>

{% code title="Subdomains" %}
```
site:<*.example.com>
```
{% endcode %}

{% code title="APIs" %}
```
site:example.com inurl:app/kibana
```
{% endcode %}

</details>

<details>

<summary><mark style="color:purple;"><strong>Extensions</strong></mark></summary>

{% code title="PHP" %}
```
site:example.com ext:php
```
{% endcode %}

{% code title="Log" %}
```
site:example.com ext:log
```
{% endcode %}

{% code title="Passwords" %}
```
site:example.com ext:txt password
```
{% endcode %}

</details>

<details>

<summary><mark style="color:purple;"><strong>AWS</strong></mark></summary>

```
site:s3.amazonaws.com <Companay_name>
```

</details>

<details>

<summary><mark style="color:purple;"><strong>CISCO</strong></mark></summary>

{% code title="Anyconnect" %}
```
intitle:index.of cisco anyconnect
```
{% endcode %}

</details>
