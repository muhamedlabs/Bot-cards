# Bot-cards

import discord
from discord.ext import commands

bot = commands.Bot(command_prefix='!')

# Dictionary to store user profiles
user_profiles = {}

@bot.command(name='create_profile')
async def create_profile(ctx, name, age, interests):
    """Create a user profile and store it in the dictionary."""
    user_id = ctx.author.id
    user_profiles[user_id] = {
        'name': name,
        'age': age,
        'interests': interests
    }
    await ctx.send(f"Profile created for {name}")

@bot.command(name='show_profile')
async def show_profile(ctx, member: discord.Member = None):
    """Show the profile of a user."""
    if member is None:
        member = ctx.author

    user_id = member.id
    if user_id in user_profiles:
        profile = user_profiles[user_id]
        profile_info = f"Name: {profile['name']}\nAge: {profile['age']}\nInterests: {profile['interests']}"
        await ctx.send(f"Profile for {member.display_name}:\n{profile_info}")
    else:
        await ctx.send("Profile not found.")

bot.run('YOUR_BOT_TOKEN')
