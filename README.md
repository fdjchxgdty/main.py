import discord
from discord.ext import commands

bot = commands.Bot(command_prefix="!", intents=discord.Intents.all())

# قائمة بالكلمات الممنوعة (سبام)
BLOCKED_WORDS = ["http://", "https://", "discord.gg/", "spam", "bot", "أي كلمة أخرى تريد منعها"]

@bot.event
async def on_message(message):
    # تجاهل الرسائل من البوت نفسه
    if message.author.bot:
        return

    # التحقق من وجود كلمات ممنوعة
    if any(word in message.content.lower() for word in BLOCKED_WORDS):
        await message.delete()
        await message.channel.send(f"{message.author.mention} يُمنع نشر الروابط أو السبام هنا!", delete_after=5)
        return

    # السماح بتنفيذ الأوامر الأخرى (مثل !ping)
    await bot.process_commands(message)

@bot.command()
async def ping(ctx):
    await ctx.send("Pong!")

bot.run("MTM1NDkyMDcwODA3Njk5ODc4Nw.GpbIIk.JnAKe7KHEnzVkZlwRQVHfeaOMaGPZL1SdoXpd4")  # استبدل TOKEN_HERE بتوكن البوت الخاص بك
