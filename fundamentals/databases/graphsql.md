---
icon: chart-bullet
description: Data query and manipulation language for APIs
---

# GraphSQL

{% hint style="info" %}
* <mark style="color:orange;">**`Apollo Server`**</mark> <mark style="color:purple;">commonly uses</mark> <mark style="color:orange;">**`port 4000`**</mark> <mark style="color:purple;">as its default when started without configuration.</mark>
* <mark style="color:orange;">**`Express-based GraphQL servers`**</mark> <mark style="color:purple;">frequently use</mark> <mark style="color:orange;">**`port 3000`**</mark><mark style="color:purple;">, simply because that's the default for many Express setups.</mark>
{% endhint %}

***

{% hint style="info" %}
### <mark style="color:purple;">Introspection Queries</mark>

{% code title="Query Information Schema" %}
```graphql
?query={__schema{types{name}}}
```
{% endcode %}

* <mark style="color:purple;">Queries all fields defined under the query</mark> <mark style="color:orange;">**`type`**</mark><mark style="color:purple;">:</mark>

{% code overflow="wrap" %}
```graphql
?query={__type(name:"Query"){fields{name,description}}}
```
{% endcode %}

* <mark style="color:purple;">Fetches the fields of the</mark> <mark style="color:orange;">**`User`**</mark> <mark style="color:purple;">type.</mark>

```graphql
?query={__type(name:"User"){fields{name}}}
```
{% endhint %}

***

{% hint style="info" %}
### <mark style="color:purple;">Data Queries</mark>

* <mark style="color:purple;">Queries the actual</mark> <mark style="color:orange;">**`user`**</mark> <mark style="color:purple;">object for its</mark> <mark style="color:orange;">**`username`**</mark> <mark style="color:purple;">and</mark> <mark style="color:orange;">**`password`**</mark> <mark style="color:purple;">fields.</mark>

```graphql
?query=query{user{username,password}}
```
{% endhint %}







curl -X POST -H "Content-Type: application/json" -d '{"query":"YOUR\_QUERY\_HERE"}' http:///graphql



?query={\_\_type(name:"User"){fields{name,type{name,kind},description\}}}

?query={\_\_type(name:"User"){fields{name,type{name,kind},description,args{name,type{name,kind\}}\}}}
