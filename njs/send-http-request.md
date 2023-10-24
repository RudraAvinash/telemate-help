# Send HTTP request

Get page on [example.com](http://example.com)

```javascript
  HTTP.get( {
    url: "http://example.com",
    success: '/onLoading',
    error: '/onError'
    
    // if you need pass headers
    // headers: { "content-type": null }
  } )

/* also you can send POST request:
  HTTP.post( {
    url: "http://example.com",
    success: '/onLoading ',
    body: {},  // body params
    // headers: { "content-type": null }
  } )
*/
```

{% hint style="warning" %}
By default header "content-type" is 'application/json'. Some api may have a bug with this. Try set `headers: { "content-type": null }`
{% endhint %}

{% hint style="success" %}
You can use `GET`, `POST` methods.\
`HTTP.post` and `HTTP.get` only
{% endhint %}

\
\
Command `onLoading`

```javascript
// downloaded page stored on content field
Bot.sendMessage(options.response);
```

Command `onError`

```javascript
Bot.sendMessage("Error on downloading");
```

