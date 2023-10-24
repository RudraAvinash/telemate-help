# Variables

In BJS we have useful global variables.

| **Variable**               | **Description**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| -------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| request                    | <p>it is collection with a lot of data. You can see it by <code>Bot.sendMessage( inspect(request) )</code><br><br>All fields available <a href="https://core.telegram.org/bots/api#update">here</a>. All field will be in request.</p>                                                                                                                                                                                                                                                                                                                                                          |
| message                    | current message from user - string                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| user                       | <p>user who sent a command or text. </p><p></p><p>Its all that received us from [telegram as user](https://core.telegram.org/bots/api#user)</p>                                                                                                                              |
| chat                       | <p>data for current chat. </p><p></p><p>Its all that received us from [telegram as chat](https://core.telegram.org/bots/api#chat)</p> |
| bot                        | <p>data for bot. </p><p></p><p><strong>Fields:</strong> </p><p><code>id</code>, </p><p><code>name</code>, </p><p><code>token</code></p>                                                                                                                                                                                                                                                             |

### You can inspect any variable for debug

```javascript
Bot.inspect(user)
Bot.inspect(chat)
```
