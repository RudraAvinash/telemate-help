# Api functions

Api functions it all functions from [https://core.telegram.org/bots/api](https://core.telegram.org/bots/api)

You can use it with BJS.&#x20;

### **Example 1.** Send message to current chat

```javascript
Api.sendMessage({
text: "Hello!"
})
```

### Send audio to other chat:

```javascript
Api.sendMessage({
  chat_id: 1234567890,
  text: "Hello!"
});
```



You can pass allowed parameters. For example for [sendMessage](https://core.telegram.org/bots/api#sendaudio) it can be parse\_mode.

```javascript
Api.sendMessage({
text: "Hi",
parse_mode: "markdown"
});
```

### **Example 2.** Send photo with inline keyboard

```javascript
// see all parameters in https://core.telegram.org/bots/api#sendphoto
Api.sendPhoto({
  photo: "URL of Image", // it is picture!
  caption: "Test photo",

  reply_markup: { inline_keyboard: [
    // line 1
    [
      // open the link on button pressing
      { text: "button1", url: "http://example.com" },
      // run command /onButton2 on button pressing
      { text: "button2", callback_data: "/onButton2" }
    ],
    // line 2
    [
       // see all params in
       // https://core.telegram.org/bots/api#inlinekeyboardbutton
       { text: "button3", callback_data: "/onButton3" }
    ]
  ]}
});
```

## Get methods

You can call Api get methods (and others methods too). Need pass `on_result` key.&#x20;

For example get all user's profile photos:

#### Command `/get`

```javascript
Api.getUserProfilePhotos({
    user_id: user.id,
    // this command will be executed after getting photos
    on_result: "onGetProfilePhotos"
});
```

####

#### Command `onGetProfilePhotos`

```javascript
if(!options.ok){
   return Bot.sendMessage("Error!");
}

if(options.result.total_count==0){
   return Bot.sendMessage("You have no photos in profile")
}

let photos = options.result.photos;
for(let i in photos){
   Api.sendPhoto( { photo: photos[i][0].file_id } );
}

// and passed bb_options:
// Bot.inspect(options.bb_options)
```

## Error handling

It is possible to capture error with `on_error` param

```javascript
Api.sendMessage({
  text: "Hello!",
  on_error: "/on_error"
});
```

In command `on_error`:

```javascript
Bot.sendMessage("We have error with sending audio");
Bot.inspect(options)
```
