# How to make lua scripts for Stand Mod Menu

If you want to make lua scripts for stand you will need some things to know. The first one is that you should read [lua documentation](https://www.lua.org/manual/5.4/), in case you know something about coding you can skip that part for now, but in the future you will need it.

## Seting up the coding enviroment
1. First thing you are going to do is install [Visual Studio Code](https://code.visualstudio.com/Download).
2. When you open it you are going to go to extensions tab and search for **Lua**. And install the ones made by *sumneko*.
3. When it is install you are going to create a folder in your desktop and then in VSCode go to `File > Open Folder` and open it.
4. Now press `Ctrl + Shift + P` and search `settings.json`, here are 3 types of settings.json but you will open the **WORKSPACE** one.
5. Here you will paste this (**inside the keys**):

```
"Lua.diagnostics.globals": [
    "menu",
    "players",
    "entities",
    "chat",
    "directx",
    "util",
    "v3",
    "lang",
    "filesystem",
    "https",
    "memory",
    "profiling",
    "SYSTEM",
    "APP",
    "AUDIO",
    "BRAIN",
    "CAM",
    "CLOCK",
    "CUTSCENE",
    "DATAFILE",
    "DECORATOR",
    "DLC",
    "ENTITY",
    "EVENT",
    "FILES",
    "FIRE",
    "GRAPHICS",
    "HUD",
    "INTERIOR",
    "ITEMSET",
    "LOADINGSCREEN",
    "LOCALIZATION",
    "MISC",
    "MOBILE",
    "MONEY",
    "NETSHOPPING",
    "NETWORK",
    "OBJECT",
    "PAD",
    "PATHFIND",
    "PED",
    "PHYSICS",
    "PLAYER",
    "RECORDING",
    "REPLAY",
    "SAVEMIGRATION",
    "SCRIPT",
    "SECURITY",
    "SHAPETEST",
    "SOCIALCLUB",
    "STATS",
    "STREAMING",
    "TASK",
    "VEHICLE",
    "WATER",
    "WEAPON",
    "ZONE"
],
"Lua.runtime.nonstandardSymbol": [
    "+=",
    "-=",
    "!=",
    "*=",
    "/="
],
```

6. Now take my [extension](), extract it and copy that folder in `C:\Users\[user]\.vscode\extensions`.
7. Reload VSCode.

## Resources

Now you will make your first lua script for Stand, and you will need resources to look at:

* [Stand API](https://stand.gg/help/lua-api-documentation)
* [GTA5 Natives Reference](https://nativedb.dotindustries.dev/natives)

You need to know that at first in the script you will write this almost always:
```
util.keep_running() --keeps script running
util.require_natives(1651208000) --tells stand to get that natives from the stand repository

--Your code here
```

Look at this script:
```

```
This script makes a button in stand and when you press it you are teleported to the following coordinates. But first we need to tell stand what we are moving. Because of that, we created a local variable called `_player`, that gets our player ped. But why we write `PLAYER.GET_PLAYER_PED(players.user())`, we write that because we can't write `GET_PLAYER_PED()`, we have to call it from the `PLAYER` namespace.

Now lets talk about the button. We create a button with `menu.action(int parent, string menu_name, table<any, string> command_names, string help_text, function on_click, ?function on_command = nil, ?string syntax = nil)`.

This is more simple than we think:
- `int` parent
    - This is the variable that you put in for where this function (in this case, button), should appear. This either could be the `root`, which is where everything in your script starts from, or a `menu.list`, which is a list of functions. What this means is that you can either:
        1. Put `menu.my_root()` (or a variable of it, doesn't matter, since variables store values) in the parent
        2. Put a variable that has your `menu.list` value in it.
- `string` menu_name
    - This is just the name that will appear as your button.
- `table`<any, string> command_names
    - This is a `table` of valid commands that you can type into the Stand Command Box that will activate this function. Since it is a `table`, you can make multiple commands for one function.
- `string` help_text
    - This is the small print that appears at the bottom of the menu explaining what the hell this function actually does.
- `funciton` on_click
    - This is the function (code) that will be executed if you click this action button.
- `?function` on_command `= nil`
    - Basically, if you set this, this will run different code if you used the function from the command box or not. Notice how it says `=nil` at the end, and a `?` at the beginning? This is because this ***isn't required; if you have nothing there, it will do the same code if you click it, or use it from the command box***.
- `?string` syntax `= nil`
    - This changes what shows up in help text of the menu, like `Command: <string>`. If you put `"aaa"` in here, it will display `Command: aaa` instead of `Command: <commandname>`.

