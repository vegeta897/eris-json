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

Usage
-----

Any time after initializing your bot, you can call `ErisJSON.botToJSON(bot)` to write the bot object to a tab-indented JSON file in the root folder named `bot.json`. You may specify a different name or path like this: `ErisJSON.botToJSON(bot, 'debug/client.json')`

You can write `message` objects the same way from a `messageCreate` event with `ErisJSON.messageToJSON(message)`.

Why?
----

Eris has a lot of state data in its [client](https://abal.moe/Eris/docs/Client) object, as well as its [message](https://abal.moe/Eris/docs/Message) objects. I have found it useful to see it all laid out in a JSON file. But simply running `JSON.stringify()` on the objects do not yield the complete structure, due to the use of getters and maps. There is also some redundant or useless data that this utility ignores. Eris comes with `.toJSON()` functions for the client and messages, but these give incomplete results.

Notes
-----

Some redundancy is eliminated in the bot and message objects. For example, the Channel objects listed in a guild's `channels` property do not contain `guild` properties of their own. Also, message objects contain a `user` property instead of `author` or `member` properties. It will contain all of the added properties of a Member when the message comes from a guild channel.

Collections (or maps) are converted to arrays. Maybe they should be converted to objects instead. Tell me what you think.

My sincere thanks and appreciation to [Abalabahaha](https://github.com/abalabahaha) for their awesome library.
