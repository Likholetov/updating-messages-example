# updating-messages-example
Example of updating messages of telegram bot

Platform: Node.js 

Thanks to: [node-telegram-bot-api](https://github.com/yagop/node-telegram-bot-api) 

## Usage

```js
const TelegramBot = require('node-telegram-bot-api')

// replace the value below with the Telegram token you receive from @BotFather
const token = 'YOUR_TELEGRAM_BOT_TOKEN'

// Create a bot that uses 'polling' to fetch new updates
const bot = new TelegramBot(token, {polling: true})

// Send a response for "/start"
bot.onText(/\/start/, msg => {

    const text = "Old message text"

    bot.sendMessage(msg.chat.id, text, {
        reply_markup: {
            inline_keyboard: [
                [
                    {
                        text: 'click to update',
                        callback_data: 'update'
                    }
                ]
            ]
        }
    })    
})

// Response for 'callback_query'
bot.on('callback_query', query => {

    const chatId = query.from.id
    const messageId = query.message.message_id

    // edit message
    bot.editMessageText('New message text', {chat_id:chatId, message_id:messageId, reply_markup:{
        inline_keyboard: [
            [
                {
                    text: 'new button text',
                    callback_data: 'new callback data'
                }
            ]
        ]
    }})
})
```
