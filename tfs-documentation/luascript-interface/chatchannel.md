# ChatChannel

There are many types of events for the ChatChannel interface, here is a list.

* \[canJoin(player)]
* \[onJoin(player)]
* \[onLeave(player)]
* \[onSpeak(player, type, message)]

1. You can create a ChatChannel script in data/chatchannels/scripts folder, but
2. You must register ChatChannel in data/chatchannels/chatchannels.xml, here is an example

```xml
<channel id="8" name="GodChannel" script="godchat.lua" />
```

1. Alternatively you can use revscript method to register via lua, by saving a .lua file in data/scripts folder.

**Please keep in mind you can name your script whatever you want as long as it ends in .lua, and its full name is in the xml, with script=""**

## canJoin(player)

> * **player** -- 1st arg/parameter /_**userdata**_/ = The **player** who is trying to join the channel

canJoin is called whenever any player attempts to open the registered channel.

**You can register your event in movement.xml like so:**

```xml
<channel id="8" name="GodChannel" script="godchat.lua" />
```

**You can then call the event in a script like so:**

godchat.lua

```lua
function canJoin(player)
    return player:getAccountType() > ACCOUNT_TYPE_GAMEMASTER -- if account type is higher access than a gamemaster returns true to allow joining, otherwise returns false and doesn't allow access
end
```

**Always remember to return true if you wish to allow player to join the channel, false if not!**

## onJoin(player)

> * **player** -- 1st arg/parameter /_**userdata**_/ = The **player** whom has just joined the channel

onJoin is called whenever any player joins the registered chatchannel

**You can register your event in creaturescripts.xml like so:**

```xml
<channel id="8" name="GodChannel" script="godchat.lua" />
```

**You can then call the event in a script like so:**

godchat.lua

```lua
function onJoin(player)
    player:sendChannelMessage("System:", "Welcome to GodChat!", MESSAGE_STATUS_CONSOLE_RED, 8)
end
```

**onJoin will execute its logic everytime a player joins the channel, returns don't matter for this event!**

## onLeave(player)

> * **player** -- 1st arg/parameter /_**userdata**_/ = The **player** who has left the registered chatchannel

onLeave is called whenever a player leaves the registered chatchannel

**You can register your event in creaturescripts.xml like so:**

```xml
<channel id="8" name="GodChannel" script="godchat.lua" />
```

**You can then call the event in a script like so:**

godchat.lua

```lua
function onLeave(player)
    player:sendTextMessage(MESSAGE_STATUS_CONSOLE_RED, "You have left GodChat")
end
```

**onLeave will execute its logic everytime a player leaves the channel, returns don't matter for this event!**

## onSpeak(player, type, message)

> * **player** -- 1st arg/parameter /_**userdata**_/ = The **player** that is removing the item
> * **type** -- 2nd arg/parameter /_**integer**_/ = a constant value representing the TALK\_TYPE
> * **message** -- 3rd arg/parameter /_**string**_/ = the text that player has sent

onSpeak runs everytime a player in the chatchannel sends a message.

**You can register your event in creaturescripts.xml like so:**

```xml
<channel id="8" name="GodChannel" script="godchat.lua" />
```

**You can then call the event in a script like so:**

godchat.lua

```lua
function onSpeak(player, type, message)
    if player:getAccountType() == 10 then
        if message == "hidehealth" then
            player:setHiddenHealth(true)
        end
        if message == "showhealth" then
            player:setHiddenHealth(false)
        end
    else
        player:sendTextMessage(MESSAGE_INFO_DESCR, "You do not have appropriate account type to execute this channel command!")
    end
end
```

**onSpeak executes everytime a player speaks in registered channel, returns don't matter here**

Here is a complete example including all the events in one file

```xml
<channel id="8" name="GodChannel" script="godchat.lua" />
```

godchat.lua

```lua
function canJoin(player)
    return player:getAccountType() > ACCOUNT_TYPE_GAMEMASTER -- if account type is higher access than a gamemaster returns true to allow joining, otherwise returns false and doesn't allow access
end

function onJoin(player)
    player:sendChannelMessage("System:", "Welcome to GodChat!", MESSAGE_STATUS_CONSOLE_RED, 8)
end

function onLeave(player)
    player:sendTextMessage(MESSAGE_STATUS_CONSOLE_RED, "You have left GodChat")
end

function onSpeak(player, type, message)
    if player:getAccountType() == 10 then
        if message == "hidehealth" then
            player:setHiddenHealth(true)
        end
        if message == "showhealth" then
            player:setHiddenHealth(false)
        end
    else
        player:sendTextMessage(MESSAGE_INFO_DESCR, "You do not have appropriate account type to execute this channel command!")
    end
end
```
