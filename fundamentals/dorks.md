---
icon: google
description: Advanced Google Search
---

# Dorks

{% tabs %}
{% tab title="Build-in Queries" %}
{% hint style="info" %}
{% code title="Specific site" %}
```
"<word>" site:<example.com>
```
{% endcode %}

{% code title="Key Words in the URL" %}
```
inurl:"</PATH/IN/THE/SITE.php>" site:<example.com>
```
{% endcode %}

{% code title="Key words in tittle" %}
```
intittle:"<word>" site:<example.com>
```
{% endcode %}

{% code title="Hyper-Links on the website" %}
```
link:"https://example.com
```
{% endcode %}

{% code title="Specific File Type" %}
```
filetype:<log> site:<example.com>
```
{% endcode %}
{% endhint %}
{% endtab %}

{% tab title="Operators" %}
{% hint style="info" %}
{% code title="Wildcard (*)" %}
```
"How to hack * using google"
```
{% endcode %}

{% code title="Quation marks (")" %}
```
Adding quotation marks around your search terms forces an exact match.
```
{% endcode %}

{% code title="OR (|)" %}
```
"how to hack" site:(reddit.com | stackoverflow.com)
```
{% endcode %}

{% code title="Minus (-)" %}
```
site:example.com password -ext:txt
```
{% endcode %}
{% endhint %}
{% endtab %}
{% endtabs %}

***

{% embed url="https://www.exploit-db.com/google-hacking-database" fullWidth="false" %}
Google Hacking Database
{% endembed %}

***

{% tabs %}
{% tab title="Subdomains" %}
{% hint style="warning" %}
```
site:<*.example.com>
```
{% endhint %}
{% endtab %}

{% tab title="APIs" %}
{% hint style="warning" %}
{% code title="Kibana" %}
```
site:example.com inurl:app/kibana
```
{% endcode %}
{% endhint %}
{% endtab %}

{% tab title="Files" %}
{% hint style="warning" %}
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
{% endhint %}
{% endtab %}

{% tab title="AWS" %}
{% hint style="warning" %}
{% code title="Buckets" %}
```
site:s3.amazonaws.com <Companay_name>
```
{% endcode %}
{% endhint %}
{% endtab %}

{% tab title="CISCO" %}
{% hint style="warning" %}
{% code title="Anyconnect" %}
```
intitle:index.of cisco anyconnect
```
{% endcode %}
{% endhint %}
{% endtab %}
{% endtabs %}
