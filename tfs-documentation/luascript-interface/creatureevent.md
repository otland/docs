---
description: CreatureEvent Interface
---

# CreatureEvent

There are many types of events for the CreatureEvent interface, here is a list.

* [onLogin\(player\)](creatureevent_interface.md#onLogin)
* [onLogout\(player\)](creatureevent_interface.md#onLogin)
* [onThink\(creature, interval\)](creatureevent_interface.md#onLogin)
* [onPrepareDeath\(creature, killer\)](creatureevent_interface.md#onLogin)
* [onDeath\(creature, corpse, killer, mostDamageKiller, lastHitUnjustified, mostDamageUnjustified\)](creatureevent_interface.md#onLogin)
* [onKill\(creature, target\)](creatureevent_interface.md#onLogin)
* [onAdvance\(player, skill, oldLevel, newLevel\)](creatureevent_interface.md#onLogin)
* [onModalWindow\(player, modalWindowId, buttonId, choiceId\)](creatureevent_interface.md#onLogin)
* [onTextEdit\(player, item, text\)](creatureevent_interface.md#onLogin)
* [onHealthChange\(creature, attacker, primaryDamage, primaryType, secondaryDamage, secondaryType, origin\)](creatureevent_interface.md#onLogin)
* [onExtendedOpCode\(player, opcode, buffer\)](creatureevent_interface.md#onLogin)

1. You can create a CreatureEvent script in data/creaturescripts/scripts folder, but
2. You must register CreatureEvents in data/creaturescripts/creaturescripts.xml, here is an example

   ```markup
   <event type="login" name="PlayerLogin" script="login.lua" />
   ```

3. Alternatively you can use revscript method to register via lua, by saving a .lua file in data/scripts folder.
4. Any CreatureEvent that is not onLogin, must be registered to the creature before it will be used by the creature.

## onLogin\(player\)

{% hint style="info" %}
**onLogin** is an event of the interface **CreatureEvent**
{% endhint %}

> * **player**  -- 1st arg/parameter /_**userdata**_/  =  The **player** who is trying to login

onLogin is called whenever any player tries to log in, its a great spot to register other CreatureEvents to players.

**After you have registered your event in creaturescripts.xml you can call the event in a script like so:**

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

## onLogout\(player\)

{% hint style="info" %}
**onLogout** is an event of the interface **CreatureEvent**
{% endhint %}

> * **player**  -- 1st arg/parameter /_**userdata**_/  =  The **player** who is trying to logout

onLogout is called whenever any player tries to logout, its a great spot to unregister other CreatureEvents to players.

**After you have registered your event in creaturescripts.xml you can call the event in a script like so:**

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

