---
description: Data query and manipulation language for APIs
icon: chart-bullet
---

# GraphSQL

{% hint style="info" %}
* <mark style="color:purple;">Uses</mark> <mark style="color:orange;">**`HTTP/HTTPS`**</mark><mark style="color:purple;">, typically over</mark> <mark style="color:orange;">**`POST`**</mark> <mark style="color:purple;">requests.</mark>
* <mark style="color:orange;">**`JSON`**</mark><mark style="color:purple;">-based queries and responses.</mark>
* <mark style="color:purple;">Typically uses a single endpoint for all operations.</mark>
* <mark style="color:orange;">**`Apollo Server`**</mark> <mark style="color:purple;">commonly uses</mark> <mark style="color:orange;">**`port 4000`**</mark> <mark style="color:purple;">as its default when started without configuration.</mark>
* <mark style="color:orange;">**`Express-based GraphQL servers`**</mark> <mark style="color:purple;">frequently use</mark> <mark style="color:orange;">**`port 3000`**</mark><mark style="color:purple;">, simply because that's the default for many Express setups.</mark>
* <mark style="color:orange;">**`Introspection`**</mark> <mark style="color:purple;">allows clients to query the API schema for available operations and data types</mark>.
{% endhint %}

***

{% hint style="info" %}
### <mark style="color:purple;">Fuzzing Tips</mark>

1. <mark style="color:orange;">**`Test Query Depth and Complexity`**</mark><mark style="color:purple;">: Check server limits on nested or complex queries to prevent performance issues.</mark>
2. <mark style="color:orange;">**`Validate Input Types and Arguments`**</mark><mark style="color:purple;">: Test inputs with invalid data to identify validation weaknesses.</mark>
3. <mark style="color:orange;">**`Examine Query Aliasing and Batching`**</mark><mark style="color:purple;">: Test for data leaks via aliased queries and batched requests.</mark>
4. <mark style="color:orange;">**`Check for Introspection Misuse`**</mark><mark style="color:purple;">: Ensure introspection doesn't expose sensitive or unnecessary schema details.</mark>
5. <mark style="color:orange;">**`Assess Authorization Controls`**</mark><mark style="color:purple;">: Confirm proper enforcement of access controls for queries and operations.</mark>
6. <mark style="color:orange;">**`Evaluate Rate Limiting`**</mark><mark style="color:purple;">: Ensure the API handles excessive or malicious requests effectively.</mark>
7. <mark style="color:orange;">**`Fuzz Mutations`**</mark><mark style="color:purple;">: Test for security and validation flaws in mutation operations.</mark>
{% endhint %}

***

{% hint style="info" %}
### <mark style="color:orange;">`Introspection`</mark> <mark style="color:purple;">Queries</mark>

{% code title="Query All types in the Schema" %}
```graphql
?query={__schema{types{name}}}
```
{% endcode %}

* <mark style="color:purple;">Queries all fields defined under the</mark> <mark style="color:orange;">**`Query`**</mark>  <mark style="color:purple;">type</mark><mark style="color:purple;">:</mark>

{% code overflow="wrap" %}
```graphql
?query={__type(name:"Query"){fields{name,description}}}
```
{% endcode %}

* <mark style="color:purple;">Fetches the fields of the</mark> <mark style="color:orange;">**`User`**</mark> <mark style="color:purple;">type:</mark>

{% code overflow="wrap" %}
```graphql
?query={__type(name:"User"){fields{name,type{name,kind},description}}}
```
{% endcode %}

* <mark style="color:purple;">Fetches details about</mark> <mark style="color:orange;">**`args`**</mark> <mark style="color:purple;">for each field of the</mark> <mark style="color:orange;">**`User`**</mark> <mark style="color:purple;">type:</mark>

{% code overflow="wrap" %}
```graphql
?query={__type(name:"User"){fields{name,type{name,kind},description,args{name,type{name,kind}}}}}
```
{% endcode %}
{% endhint %}

***

{% hint style="info" %}
### <mark style="color:purple;">Data Queries</mark>

* <mark style="color:purple;">Queries the actual</mark> <mark style="color:orange;">**`user`**</mark> <mark style="color:purple;">object for its</mark> <mark style="color:orange;">**`username`**</mark> <mark style="color:purple;">and</mark> <mark style="color:orange;">**`password`**</mark> <mark style="color:purple;">fields.</mark>

```graphql
?query=query{user{username,password}}
```
{% endhint %}

***

{% hint style="info" %}
### <mark style="color:purple;">Use</mark> <mark style="color:orange;">`curl`</mark>

{% code overflow="wrap" %}
```bash
curl -X POST -H "Content-Type: application/json" -d '{"query":"YOUR_QUERY_HERE"}' http:///graphql
```
{% endcode %}
{% endhint %}
