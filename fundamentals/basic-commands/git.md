---
icon: git
---

# Git

<details>

<summary><mark style="color:purple;"><strong><code>Enumeration</code></strong></mark></summary>

{% hint style="info" %}
{% code title="Repository Status" %}
```sh
git status
```
{% endcode %}

{% code title="Repository Logs" %}
```sh
git log
```
{% endcode %}

{% code title="Check Commit" %}
```sh
git show b73481bb823d2dfb49c44f4c1e6a7e11912ed8ae
```
{% endcode %}
{% endhint %}

</details>

<details>

<summary><mark style="color:purple;"><strong><code>Remote Repository</code></strong></mark></summary>

{% code title="Check your remote URL" overflow="wrap" %}
```sh
git remote -v
```
{% endcode %}

{% code title=" Remote URL to SSH" overflow="wrap" %}
```sh
git remote set-url origin git@github.com:b0llull0s/AI-Maths.git
```
{% endcode %}

</details>

<details>

<summary><mark style="color:purple;"><strong><code>Branches</code></strong></mark></summary>

{% hint style="info" %}
* <mark style="color:purple;">Fetch the changes to local:</mark>

```sh
git fetch origin
```

* <mark style="color:purple;">Create and switch to a new branch:</mark>

```sh
git checkout <branch_name>
```

* <mark style="color:purple;">In case you can to create a feature branch:</mark>

```
git checkout -b feature-branch
```

* <mark style="color:purple;">Pull the latest changes:</mark>

```sh
git pull origin dev
```

* <mark style="color:purple;">Switch to another branch:</mark>

```sh
git switch <branch-name>
```

* <mark style="color:purple;">Push the changes:</mark>

```sh
git push origin <branch_name>
```

* <mark style="color:purple;">Fetch changes to local:</mark>

```sh
git fetch
```
{% endhint %}

</details>



