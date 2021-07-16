
## Don't forget to Star it 
If you need help go my https://github.com/corropted/dj-games and scroll down there is discord link

```js

// Don't forget to star it 
// you can add this in command handler
// or you can use without command handler

const { MessageEmbed } = require('discord.js')
let embed = new MessageEmbed()
        .setTitle("RPS GAME")
        .setDescription("React to play!")
        .setColor('RANDOM')
        .setTimestamp()
        
        let msg = await message.channel.send(embed);
        await msg.react("✊")
        await msg.react("✂")
        await msg.react("📰")

        const filter = (reaction, user) => {
            return ['✊', '✂', '📰'].includes(reaction.emoji.name) && user.id === message.author.id;
        }

        const choices = ['✊', '✂', '📰']
        const me = choices[Math.floor(Math.random() * choices.length)]
        msg.awaitReactions(filter, {max:1, time: 60000, error: ["time"]}).then(
            async(collected) => {
                const reaction = collected.first()
                let result = new MessageEmbed()
                .setTitle("RESULT")
                .addField("Your choice", `${reaction.emoji.name}`)
                .addField("My choice", `${me}`)
                .setColor("RANDOM")
            await msg.edit(result)
                if ((me === "✊" && reaction.emoji.name === "✂") ||
                (me === "📰" && reaction.emoji.name === "✊") ||
                (me === "✂" && reaction.emoji.name === "📰")) {
                    message.channel.send(`${message.author}, you lost!`);
            } else if (me === reaction.emoji.name) {
                return message.channel.send(`${message.author}, it was a tie!`);
            } else {
                return message.channel.send(`${message.author}, you won!`);
            }
        })
        .catch(collected => {
                message.reply('Process has been cancelled since you did not respond in time!');
            })
}
}
```
