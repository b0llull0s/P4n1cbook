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

{% code title="Fetch the changes to local" overflow="wrap" %}
```sh
git fetch origin
```
{% endcode %}

{% code title="Create and switch to a new branch" %}
```shell
git checkout <branch_name>
```
{% endcode %}

{% code title="In case you can to create a feature branch" overflow="wrap" %}
```sh
git checkout -b feature-branch
```
{% endcode %}

{% code title="Pull the latest changes" overflow="wrap" %}
```sh
git pull origin dev
```
{% endcode %}

{% code title="Switch to another branch" overflow="wrap" %}
```sh
git switch <branch-name>
```
{% endcode %}

{% code title="Push the changes" overflow="wrap" %}
```sh
git push origin <branch_name>
```
{% endcode %}

{% code title="Fetch changes to local" overflow="wrap" %}
```sh
git fetch
```
{% endcode %}

</details>



