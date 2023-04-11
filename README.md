import discord

client = discord.Client()

spam_count = {}

@client.event
async def on_ready():
    print('Bot is ready')

@client.event
async def on_message(message):
    if message.author == client.user:
        return
    
    if message.content in spam_count and spam_count[message.content] >= 3:
        await message.delete()
        await message.channel.send(f'{message.author.mention}, please do not spam.')
    elif message.content in spam_count:
        spam_count[message.content] += 1
    else:
        spam_count[message.content] = 1

    await client.process_commands(message)

client.run('qUGWRPaYhATgjGw-nGHoKW_Sxo4ZRd-V')
