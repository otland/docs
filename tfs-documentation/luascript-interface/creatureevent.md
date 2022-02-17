# CreatureEvent

There are many types of events for the CreatureEvent interface, here is a list.

* onLogin(player)
* onLogout(player)
* onThink(creature, interval)
* onPrepareDeath(creature, killer)
* onDeath(creature, corpse, killer, mostDamageKiller, lastHitUnjustified, mostDamageUnjustified)
* onKill(creature, target)
* onAdvance(player, skill, oldLevel, newLevel)
* onModalWindow(player, modalWindowId, buttonId, choiceId)
* onTextEdit(player, item, text)
* onHealthChange(creature, attacker, primaryDamage, primaryType, secondaryDamage, secondaryType, origin)
* onExtendedOpCode(player, opcode, buffer)

1. You can create a CreatureEvent script in data/creaturescripts/scripts folder, but
2. You must register CreatureEvents in data/creaturescripts/creaturescripts.xml, here is an example

```xml
<event type="logout" name="PlayerLogout" script="logout.lua" />
```

1. Alternatively you can use revscript method to register via lua, by saving a .lua file in data/scripts folder.
2. Any CreatureEvent that is **not onLogin**, **must** be registered to the creature using the creature:registerEvent(name) method, where name is the name of the event in the xml file (unless is revscript, then name is created when event is created), our above example would be done like this : creature:registerEvent("PlayerLogout") before it will be used by the creature. Remember player, monster, and npc inherit from creature so you can do player:registerEvent("PlayerLogout") as player inherits from creature.

## onLogin(player)

> * **player** -- 1st arg/parameter /_**userdata**_/ = The **player** who is trying to login

onLogin is called whenever any player tries to log in, its a great spot to register other CreatureEvents to players.

**You can register your event in creaturescripts.xml like so:**

```xml
<event type="login" name="PlayerLogin" script="login.lua" />
```

**You can then call the event in a script like so:**

login.lua

```lua
local firstItems = {2050, 2382} --- table with items for new player

function onLogin(player)
    if player:getLastLoginSaved() == 0 then --- player has never logged in before
        for i = 1, #firstItems do
            player:addItem(firstItems[i], 1) -- we give 1 of each item in table above to player
        end
        player:addItem(ITEM_BAG, 1) -- we give the player a bag too
    end
    return true --- we must return true to allow player to login, false or no return will keep player from logging in. 
end
```

**Always remember to return true if you wish to allow player login, returning false or not returning true will block player from logging in!**

## onLogout(player)

> * **player** -- 1st arg/parameter /_**userdata**_/ = The **player** who is trying to logout

onLogout is called whenever any player tries to logout, its a great spot to unregister other CreatureEvents to players.

**You can register your event in creaturescripts.xml like so:**

```xml
<event type="logout" name="PlayerLogout" script="logout.lua" />
```

**You can then call the event in a script like so:**

logout.lua

```lua
function onLogout(player)
    if player:isPzLocked() then
        player:sendTextMessage(MESSAGE_INFO_DESCR,"You must not be pz-locked, in order to logout")
        return false --- here we block player from logging out
    end
    --- if we made it to this point, player must not be pzlocked, so lets let him logout
    return true --- player logs out successfully
end
```

**Always remember to return true if you wish to allow player logout, returning false or not returning true will block player from logging out!**

## onThink(creature, interval)

> * **creature** -- 1st arg/parameter /_**userdata**_/ = The **creature** whom the event is triggering on
> * **interval** -- 2nd arg/parameter /_**integer**_/ = The **milliseconds** interval at which every iteration of the event will take place

onThink is similar to an infinite loop, as it does not stop unless the event is unregistered. It occurs every 1000 milliseconds, so once every second.

**You can register your event in creaturescripts.xml like so:**

```xml
<event type="think" name="thinkEvent" script="think.lua" />
```

**You can then call the event in a script like so:**

think.lua

```lua
function onThink(creature)
    if creature:isMonster() then
        creature:say("I'm hungry") --- if its a monster, says "I'm hungry"
        return true -- we return now as we have done as we intended
    end

    return true --- here we are returning incase creature wasn't a monster
end
```

**onThink doesn't require a return value of true to execute, returns are still valuable as a means of control over the script logic, and its good practice to use them, to make it a habit of knowing what your return should be**

## onPrepareDeath(creature, killer)

> * **creature** -- 1st arg/parameter /_**userdata**_/ = The **creature** that is preparing to die, can be a monster, player, or npc
> * **killer** -- 2nd arg/parameter /_**userdata**_/ = The **killer** is who killed the creature, can be a monster, player or npc

onPrepareDeath triggers **before creature death**, and so you can return false to prevent the death from happening. This is particularly useful for pvp arena and special event scenarios.

**You can register your event in creaturescripts.xml like so:**

```xml
<event type="preparedeath" name="deathPrep" script="preparedeath.lua" />
```

**You can then call the event in a script like so:**

preparedeath.lua

```lua
function onPrepareDeath(creature, killer)
    if creature:isMonster() and killer:isMonster() then
        return false -- returning false will prevent the monster from dieing to another monster, but not give it any hp back
    end

    return true --- it wasn't a monster killing a monster so we allow the death by returning true
end
```

**When returning false for onPrepareDeath , the creature will not die! Return true to continue with death of creature**
