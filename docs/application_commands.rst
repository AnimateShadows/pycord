:orphan:

.. currentmodule:: discord
.. versionadded:: 2.0
.. _application_commands:

Application Commands
====================

Application commands are commands that an application can register to Discord. They provide users a way of interacting
directly with your application that feels deeply integrated into Discord.

Application commands can be used with either :class:`.Bot` or :class:`.ext.commands.Bot`.

.. code-block:: python3

    import discord
    bot = discord.Bot()

    @bot.command() # creates slash command by default
    async def foo(ctx, arg):
        await ctx.respond(arg)

    # or

    from discord.ext import commands
    bot = commands.Bot()

    @bot.slash_command()
    async def foo(ctx, arg):
        await ctx.respond(arg)

How to use Application Commands in a Cog
----------------------------------------

This is gonna be a short 

Application Command Types
-------------------------

There are currently three types of application commands: slash, user and message commands.

These have their corresponding decorators.

.. code-block:: python3

    @bot.slash_command()
    async def foo(ctx):
        await ctx.respond("Hello world!")

    @bot.user_command()
    async def bar(ctx, user):
        await ctx.respond(user.id)

    @bot.message_command()
    async def foobar(ctx, message):
        await ctx.respond(message.id)

You can also use the :attr:`.Bot.command` decorator by supplying an application command class.

.. code-block:: python3

    from discord import UserCommand

    @bot.command(..., cls=UserCommand)
    # is the same as
    @bot.user_command(...)

Options
-------

Options are arguments passed into slash commands.

These can be defined as normal function arguments:

.. code-block:: python3

    @bot.slash_command()
    async def say_hello(ctx, name):
        await ctx.respond(f"Hello {name}!")

Typehints can be used to set option types. All option types are listed under :class:`.SlashCommandOptionType`.

.. code-block:: python3

    @bot.slash_command()
    async def foo(ctx, number: int, member: discord.Member):
        # command code

All option fields can be set using :class:`.Option` as the type of the argument.

.. code-block:: python3

    from discord import Option

    @bot.slash_command()
    async def show_color(
        ctx,
        color: Option(str, "Your color choice", choices=["red", "green"], required=False)
    ):
        # command code

Slash Command Groups
--------------------

To get started with using slash command groups you should firstly define your command group.

.. code-block:: python3
    
    py_list = bot.command_group()

We are defining the ``py_list`` phrase to bot.command_group, Once you have done this make sure to then make the group
inside your defined phrase:

.. code-block:: python3
        
        "python_versions_list", "A List of commands showing python versions"

Now that you have defined your command group you can actually make the commands, This isn't too hard in anyway shape or form.

.. code-block:: python3
    
    @py_list.command(guild_ids=[])

The example shown above is what every command should look like ``my_list_name.command()``

and everything from here should be self explanitory and the same as normal application commands.