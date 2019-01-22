Eris JSON
=========

A helper utility for writing [Eris](https://abal.moe/Eris/) objects to JSON

```npm
npm install eris-json
```

Use Eris JSON to write your bot or message objects to JSON.

```js
const Eris = require('eris');
const ErisJSON = require('eris-json');

let bot = new Eris('BOT_TOKEN');

bot.on('ready', () => {
    ErisJSON.botToJSON(bot); // Write the bot's state to ./bot.json
});

bot.on('messageCreate', message => {
    ErisJSON.messageToJSON(message); // Write the message object to ./message.json
});

bot.connect();
```

Why?
----

Eris has a lot of state data in its [client](https://abal.moe/Eris/docs/Client) object, as well as its [message](https://abal.moe/Eris/docs/Message) objects. I have found it useful to see it all laid out in a JSON file. But simply running `JSON.stringify()` on the objects do not yield the complete structure, due to the use of getters and maps. There is also some redundant data that this utility filters out.
