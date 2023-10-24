# Properties

## Introducing

It is possible to save data in bot. Data can be numeric, text, datetime and etc.

For example:

* Bot can have DailyBonus saved in bot prop (it is global for all bot)
* User can have Balance saved in user prop (it is personall)

{% hint style="info" %}
Properties can be belong for user or for bot.
{% endhint %}

## Set property

```javascript
// set global prop
Bot.setProperty('myProp', 15);
 
// set JSON prop for user
User.setProperty('BIO', { email: "test@example.com", age: 10 });
```

{% hint style="success" %}
* so for global prop use `Bot.xxx` method
* for user's prop use `User.xxx` method
{% endhint %}

also you can use old style:

```javascript
 // set global prop
Bot.setProperty("myProp", 15);
```

## Get property

```javascript
// get global prop
var myProp = Bot.getProperty('myProp');
Bot.sendMessage("prop: " + myProp);
 
// get prop for user
var bio = User.getProperty('BIO');
Bot.sendMessage("Hello, " + bio);
```

or get prop with default value:

```javascript
// prop by default will be 15
var myProp = Bot.getProperty('myProp', 15);
```


## Delete property

Pass `null` to prop's value for property deleting:

```javascript
// prop "myProp" with null value will be removed
Bot.setProperty("myProp", null );
```



