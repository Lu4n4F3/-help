from settings import settings
import discord
# import * - es una forma rápida de importar todos los archivos de la biblioteca
from bot_logic import *

# La variable intents almacena los privilegios del bot
intents = discord.Intents.default()
# Activar el privilegio de lectura de mensajes
intents.message_content = True
# Crear un bot en la variable cliente y transferirle los privilegios
client = discord.Client(intents=intents)


# Una vez que el bot esté listo, ¡imprimirá su nombre!
@client.event
async def on_ready():
    print(f'We have logged in as {client.user}')


# Cuando el bot reciba un mensaje, ¡enviará mensajes en el mismo canal!
@client.event
async def on_message(message):
    if message.author == client.user:
        return
    if message.content.startswith('$hello'):
        await message.channel.send('¡Hola! Soy un bot')
    elif message.content.startswith('$smile'):
        await message.channel.send(gen_emodji())
    elif message.content.startswith('$coin'):
        await message.channel.send(flip_coin())
    elif message.content.startswith('$pass'):
        await message.channel.send(gen_pass(10))
    elif message.content.startswith('$help'):
        help_message = (
            "           comando de Biyoo(★‿★)\n"
            "$hello  -> Biyoo te saludara: '¡Hola! Soy un bot\n"
            "$smile -> Biyoo te enviara un emoji al azar feliz 😀😄😊\n"
            "$coin -> Se elegira al azar 'cara' o 'cruz\n"
            "$pass -> Generara un password al azar"
        )
        await message.channel.send(help_message)
    else:
        await message.channel.send("No puedo procesar este comando, ¡lo siento!")


client.run("MTI0ODA4MDI1OTQzODQ3NzQyMw.GZxU4z.nJ1MHzFanlPA5b7DOp4ay-v2L5ObRl7ll_39xo")
