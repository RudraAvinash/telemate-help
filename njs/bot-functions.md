# Bot functions

| Function                                   | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| ------------------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `Bot.runCommand(command, options)`         | <p>Run other command</p><p><code>Bot.runCommand("/contact")</code></p><p><br>and with options: </p><p><code>Bot.runCommand("/contact", {phone: "+15424", email: "example@example.com"})</code></p><p><br>in second command /contact:</p><p>Bot.sendMessage("Phone is:" + options.phone);</p>                                                                                                                                                                    |
| `Bot.run(options)`                         | <p>Run other command</p><p>Bot.run({ command: "/contact" })</p><p></p><p><a href="bot-functions.md#bot.run-params">see more</a></p>                                                                                                                                                                                                                                                                                                                             |
| `Bot.runAll(options)`                      | <p>Run other command for all chats</p><p><code>Bot.runAll({ command: "/broadcast" })</code></p><p></p><p><a href="bot-functions.md#bot.runall-options">see more</a></p>                                                                                                                                                                                                                                                                                         |
| `Bot.sendKeyboard(buttons, message)`       | <p>send keyboard and message. Message is required</p><p></p><p><code>Bot.sendKeyboard("about, help,\ncontacts", "send keyboard now")</code></p>                                                                                                                                                                                                                                                                                                                 |
| `Bot.sendInlineKeyboard(buttons, message)` | <p>Send inline keyboard and message. Message is required. Buttons is array. Button must have text fields: title(required), url or command.</p><p></p><p><code>Bot.sendInlineKeyboard([ {title: "google", url: "http://google.com" }, {title: "other command", command: "/othercommand"} ], "Please make a choice.")</code></p>                                                                                                                                  |
| `Bot.setProperty(name, value)`       | <p>Set property with name for bot. <a href="properties.md#set-property">Read more</a></p><p></p><p><code>Bot.setProperty("TotalScore", 100)</code> </p><p></p>                                                                                                                                                                                                       |
| `Bot.getProperty(name)`                    | <p>Read property with name. Name is case sensitive. Name is case sensitive. <a href="properties.md#get-property">Read more.</a></p><p></p><p><code>Bot.getProperty("TotalScore")</code></p><p></p><p>can get property with default value for non exist property:</p><p><code>Bot.getProperty("TotalScore", 100)</code> </p> |



## Bot.run(params)

Run other command

```javascript
Bot.run(params)
```

| Field            | Description                                                            |
| ---------------- | ---------------------------------------------------------------------- |
| `command`        | **Required**. Command for run. For example "/start". Can pass params   |
| `options`        | json for passing to command. Available through options in this command |
| `user_id`        | user telegramid for passing. **By default** this is current user.id           |
| `chat_id`        | chat\_id for passing. **By default** this is current chat.id           |

**Example 1**. Run a command `/balance` for another user

```javascript
Bot.run( {
    command: "/balance",
    user_id: 1234567890,
} )
```

## Bot.runAll(options)

Run other command for all chats

{% hint style="success" %}
Use this command for broadcasting any information: message, photo, video, keyboard and etc
{% endhint %}

{% hint style="warning" %}
**Bot.runAll** works for worked bots only.&#x20;
{% endhint %}

```javascript
Bot.runAll(params)
```

| Field       | Description                                                                                                                                                                                                   |
| ----------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `command`   | **Required**. Command for run. For example "/start". Can pass `params`                                                                                                                                        |
| `options`   | json for passing to command. Available through options in this command                                                                                                                                        |
| `on_create` | run this command on task creation with task information                                                                                                                                                       |
| `for_chats` | <p>Command will be runned for this chats type only. Can be:</p><p><code>"private-chats"</code></p><p><code>"group-chats"</code></p><p><code>"super-group-chats"</code></p><p><code>"all"</code> - default</p> |

**Example**:

Command: `/news`

```javascript
Bot.runAll( {
    // this command will be executed
    // for each private chat (user)
    command: "/broadcast",
    for_chats: "private-chats",
    on_create: "on_new_brodcast_task",
    // options: { any_data: "here" }
} )
```

Command: `/broadcast`

```javascript
// it have user and chat object!
// so we can send any information now: message, keyboard, photo and etc

Bot.sendKeyboard("New news", "hello!")

// we can get brodcast task info
/*
let task = options.task;
Bot.sendMessage(
   "Task progress: " + task.progress +
   "\n total: " + task.total +
   "\n cur index: " + task.cur_position +
   "\n status: " + task.status +
   "\n errors: " + task.errors_count
)
*/
```

Command: `on_new_brodcast_task`

```javascript
const task = options.run_all_task;
Bot.sendMessage(
  "Task for brodcasting created. Task id: " + task.id
);

// save task id:
Bot.setProperty("curBrodcastTaskID", task.id, "integer")

// Bot.inspect(options.run_all_task);
```

Command: `/progress`

```javascript
// show current runAll progress

const taskID = Bot.getProperty("curBrodcastTaskID");
let task = new RunAllTask({ id: taskID });
// Bot.inspect(task) // you can check all fields

if(!task.status){
  Bot.sendMessage("This task not found")
  return
}

Bot.sendMessage(
  "Current brodcast: " + 
  "/n Status: " + task.status + " " + task.progress + "%" +
  "/n Progress:" + task.cur_position + "/" + task.total
)

```
