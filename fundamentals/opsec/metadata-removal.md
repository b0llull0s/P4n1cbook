---
icon: broom-wide
---

# Metadata Removal

<details>

<summary><mark style="color:orange;"><strong><code>DOCX</code></strong></mark> </summary>

<mark style="color:orange;">**`DOCX`**</mark> <mark style="color:purple;">**files are essentially a ZIP archive containing XML files**</mark>

1. <mark style="color:purple;">Make a backup of your file first.</mark>
2. <mark style="color:purple;">Rename the file extension from</mark> <mark style="color:orange;">**`.docx`**</mark> <mark style="color:purple;">to</mark> <mark style="color:orange;">**`.zip`**</mark>
3. <mark style="color:purple;">Unzip it.</mark>

{% hint style="info" %}
<mark style="color:red;">**`Files containing metadata`**</mark>

* <mark style="color:orange;">**`core.xml`**</mark> <mark style="color:purple;">--> contains author, creation date, etc.</mark>
* <mark style="color:orange;">**`app.xml`**</mark> <mark style="color:purple;">--> contains application-specific metadata</mark>
* <mark style="color:orange;">**`custom.xml`**</mark> <mark style="color:purple;">--> may contain custom properties</mark>
{% endhint %}

4. <mark style="color:purple;">Delete the sensitive content from these files.</mark>

* <mark style="color:purple;">Re-zip the contents:</mark> <mark style="color:orange;">**`zip -r ../clean_document.docx *`**</mark> <mark style="color:purple;">from inside the folder.</mark>
* <mark style="color:purple;">Rename back to</mark> <mark style="color:orange;">**`.docx`**</mark>

</details>
