---
icon: golang
---

# GO

{% code title="Install Individual packages" overflow="wrap" %}
```sh
go get github.com/ffuf/ffuf
```
{% endcode %}

{% code title="Update Dependencies" overflow="wrap" %}
```sh
got get -u github/fatih/color@latest
```
{% endcode %}

{% code title="Create mod folder" overflow="wrap" %}
```sh
go mod init <projectfolder>
```
{% endcode %}

{% code title="Add Dependencies" overflow="wrap" %}
```sh
go mod ini
```
{% endcode %}

{% code title="Compile Code" overflow="wrap" %}
```sh
go build
```
{% endcode %}

{% code title="Run code" %}
```sh
go run <code>
```
{% endcode %}

{% code title="Clean Unused dependencies" overflow="wrap" %}
```
go mod tidy
```
{% endcode %}

{% code title="List all dependencies" overflow="wrap" %}
```sh
go list -m all
```
{% endcode %}
