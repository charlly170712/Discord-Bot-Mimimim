# Discord-Bot-Mimimim
It is a basic project done by a beginner
import discord
import random
import os
import requests
from discord.ext import commands
from main import get_pas

permisos = discord.Intents.default()
permisos.message_content=True

Mimimim = commands.Bot(command_prefix="/", intents=permisos)
@Mimimim.event
async def on_ready(): 
    print("el bot esta en linea")
@Mimimim.command()
async def hola(ctx):
    await ctx.send("Hosla, como estas? Soy Mimimim, en que necesitas mi ayuda?")

@Mimimim.command()
async def pas(ctx, logi:int):
    resultado = get_pas(logi)
    await ctx.send(f"Tu contraseña es: {resultado}")

@Mimimim.command()
async def meme(ctx):
    magis = os.listdir('img')
    imad = random.choice(magis)
    with open(f"img/{imad}", "rb") as f:
        imagen = discord.File(f)
        await ctx.send(file=imagen)

def get_onepiece_image_url():
    url = 'https://kitsu.io/api/edge/anime?filter[text]=tokyo'
    res = requests.get(url)
    data = res.json()
    return data['data'][0]['attributes']['posterImage']['small']

@Mimimim.command('tokyo')
async def onepiece(ctx):
    image_onepiece = get_onepiece_image_url()
    await ctx.send(image_onepiece)

Mimimim.run("MTQ2OTY3NzUzNDc2MDQwNzA2MA.GtFHW4.Mg-S3WtN0P9vyOan6rpjR5d3cqXZY-dN5BTuNU")
