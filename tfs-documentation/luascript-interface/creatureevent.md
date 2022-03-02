# CreatureEvent

There are many types of events for the CreatureEvent interface, here is a list.

* ****[**onLogin**](creatureevent.md#onlogin-player)**(player)**
* ****[**onLogout**](creatureevent.md#onlogout-player)**(player)**
* ****[**onThink**](creatureevent.md#onthink-creature-interval)**(creature, interval)**
* ****[**onPrepareDeath**](creatureevent.md#onpreparedeath-creature-killer)**(creature, killer)**
* ****[**onDeath**](creatureevent.md#ondeath-creature-corpse-killer-mostdamagekiller-lasthitunjustified-mostdamageunjustified)**(creature, corpse, killer, mostDamageKiller, lastHitUnjustified, mostDamageUnjustified)**
* ****[**onKill**](creatureevent.md#onkill-killer-victim)**(creature, target)**
* ****[**onAdvance**](creatureevent.md#onadvance-player-skill-oldlevel-newlevel)**(player, skill, oldLevel, newLevel)**
* ****[**onModalWindow**](creatureevent.md#onmodalwindow-player-modalwindowid-buttonid-choiceid)**(player, modalWindowId, buttonId, choiceId)**
* ****[**onTextEdit**](creatureevent.md#ontextedit-player-item-text)**(player, item, text)**
* ****[**onHealthChange**](creatureevent.md#onhealthchange-creature-attacker-primarydamage-primarytype-secondarydamage-secondarytype-origin)**(creature, attacker, primaryDamage, primaryType, secondaryDamage, secondaryType, origin)**
* ****[**onManaChange**](creatureevent.md#onmanachange-creature-attacker-primarydamage-primarytype-secondarydamage-secondarytype-origin)**(creature, attacker, primaryDamage, primaryType, secondaryDamage, secondaryType, origin)**
* ****[**onExtendedOpCode**](creatureevent.md#onextendedopcode-player-opcode-buffer)**(player, opcode, buffer)**

<!---->

* [x] You can create a CreatureEvent script in data/creaturescripts/scripts folder, but
* [x] You must register CreatureEvents in data/creaturescripts/**creaturescripts.xml**, here is an example

```xml
<event type="logout" name="PlayerLogout" script="logout.lua" />
```

* **Alternatively you can use **_**revscript**_** method to register via **_**lua**_**, by saving a .lua file in data/scripts folder.**
* **Any CreatureEvent that is not onLogin, must be registered to the creature using the creature:registerEvent(name) method, where name is the name of the event in the xml file (unless is revscript, then name is created when event is created), our above example would be done like this : creature:registerEvent("PlayerLogout") before it will be used by the creature.**

**Please keep in mind you can name your script whatever you want as long as it ends in .lua, and its full name is in the xml, with script=""**

## onLogin(player)

> * **player** -- 1st arg/parameter /_**userdata**_/ = The **player** who is trying to login

**onLogin is called whenever any player tries to log in, its a great spot to **_**register**_** other CreatureEvents to players.**

**You can register your event in creaturescripts.xml like so:**

```xml
<event type="login" name="PlayerLogin" script="login.lua" />
```

**You can then call the event in a script like so:**

**Example:** login.lua

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

**onLogout is called whenever any player tries to logout, its a great spot to **_**unregister**_** other CreatureEvents to players.**

**You can register your event in creaturescripts.xml like so:**

```xml
<event type="logout" name="PlayerLogout" script="logout.lua" />
```

**You can then call the event in a script like so:**

**Example:** logout.lua

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

**onThink is similar to an infinite loop, as it **_**does not stop unless the event is unregistered**_**. It occurs every 1000 milliseconds, so once every second.**

**You can register your event in creaturescripts.xml like so:**

```xml
<event type="think" name="thinkEvent" script="think.lua" />
```

**You can then call the event in a script like so:**

**Example:** think.lua

```lua
function onThink(creature)
    if creature:isMonster() then
        creature:say("I'm hungry") --- if its a monster, says "I'm hungry"
        return -- we return now as we have done as we intended
    end

    return --- here we are returning incase creature wasn't a monster
end
```

**Returns strictly serve as a control mechanism when using this hook**

## onPrepareDeath(creature, killer)

> * **creature** -- 1st arg/parameter /_**userdata**_/ = The **creature** that is preparing to die
> * **killer** -- 2nd arg/parameter /_**userdata**_/ = The **killer** is who killed the creature

**onPrepareDeath triggers before creature death, and so you can return false to prevent the death from happening. This is particularly useful for pvp arena and special event scenarios.**

**You can register your event in creaturescripts.xml like so:**

```xml
<event type="preparedeath" name="deathPrep" script="preparedeath.lua" />
```

**You can then call the event in a script like so:**

**Example:** preparedeath.lua

```lua
function onPrepareDeath(creature, killer)
    if creature:isMonster() and killer:isMonster() then
        return false -- returning false will prevent the monster from dieing to another monster, but not give it any hp back
    end

    return true --- it wasn't a monster, killing a monster, so we allow the death by returning true
end
```

**When returning false for onPrepareDeath , the creature will not die! Return true to continue with death of creature**

## onDeath(creature, corpse, killer, mostDamageKiller, lastHitUnjustified, mostDamageUnjustified)

> * **creature** -- 1st arg/parameter /_**userdata**_/ = The **creature** that **has been killed**
> * **corpse** -- 2nd arg/parameter /_**userdata**_/ = The **corpse** is a **container** object, inherits from **item**, contains items dropped by the creature
> * **killer** -- 3rd arg/parameter /_**userdata**_/ = The **killer** is who killed the creature
> * **mostDamageKiller** -- 4th arg/parameter /_**userdata**_/ = The **mostDamageKiller** dealt most damage to the **creature**
> * **lastHitUnjustified** -- 5th arg/parameter /_**boolean**_/ = is **true** if killer's last hit was unjustified, _**false if not**_.
> * **mostDamageUnjustified** -- 6th arg/parameter /_**boolean**_/ = is **true** if killer recieved _**unjustified**_ from most damage to creature, **false if not** [//](broken-reference): #

**onDeath triggers after creature death and is uniquely **_**suited for handling multiple killers**_**, as well as determining if the death was **_**unjustified**_** or not.**

**You can register your event in creaturescripts.xml like so:**

```xml
<event type="death" name="PkRevenge" script="pkdeath.lua" />
```

**You can then call the event in a script like so:**

**Example:** pkdeath.lua

```lua
function onDeath(creature, corpse, killer, mostDamageKiller, lastHitUnjustified, mostDamageUnjustified)
    if creature:isMonster() and killer:isMonster() then
        return -- returning false would serve as same result as return here, just exits the script. So if monster killed monster, do nothing.
    end

    if not lastHitUnjustified and not mostDamageUnjustified then
        return -- exits script if this wasn't an unjust kill
    end

    if killer and mostDamageKiller then -- makes sure neither are nil
        if killer:isPlayer() and mostDamageKiller:isPlayer() then -- checks if both are player class
            if killer:getGuid() == mostDamageKiller:getGuid() then -- if both are one in the same
                return -- exits script, because we are looking for multiple players in an unjust kill
            end
            --- here we now know it has to be at least two players who took part in the kill
            corpse:remove() -- we destroyed the corpse so those pker's don't get it!
            return -- scripts purpose is served, we exit
        end
    end
end
```

**Returns strictly serve as a control mechanism when using this hook**

## onKill(killer, victim)

> * **killer** -- 1st arg/parameter /_**userdata**_/ = The **creature** that **has killed**
> * **victim** -- 2nd arg/parameter /_**userdata**_/ = The **victim** is a **creature** that died

**onKill triggers after creature death and is great for handling specific kills, ie, killed a boss, a player of a certain guild, stuff like that, without having to register to each of the victims.**

**You can register your event in creaturescripts.xml like so:**

```xml
<event type="kill" name="bossKill" script="bosskill.lua" />
```

**You can then call the event in a script like so:**

**Example:** bosskill.lua

```lua
function onKill(killer, victim)
    if not killer:isPlayer() then
        return -- killer is not a player, no need to execute any further.
    end
    if not victim:isMonster() and victim:getType():isBoss() then
        return -- victim is not a boss, no need to execute any further.
    end
    -- anything here, happens because the killer is a player, and the victim is a monsterType, that returns true with :isBoss()
    killer:sendTextMessage(MESSAGE_INFO_DESCR, "Congratulations you killed a Boss!")
end
```

**Returns strictly serve as a control mechanism when using this hook**

## onAdvance(player, skill, oldlevel, newlevel)

> * **player** -- 1st arg/parameter /_**userdata**_/ = The **player** that gained a level!
> * **skill** -- 2nd arg/parameter /_**integer**_/ = The **skill** is an integer representing a **constant value** found here. -- insert link
> * **oldlevel** -- 3rd arg/parameter /_**integer**_/ = The **oldlevel** is an **integer** value of the level _before_ the advancement.
> * **newlevel** -- 4th arg/parameter /_**integer**_/ = The **newlevel** is an **integer** value of the level _after_ the advancement.

**onAdvance triggers when a player gains a level, magic level, or skill level.**

**You can register your event in creaturescripts.xml like so:**

```xml
<event type="advance" name="fishingLevels" script="fishinglevels.lua" />
```

**You can then call the event in a script like so:**

**Example:** fishinglevels.lua

```lua
function onAdvance(player, skill, oldlevel, newlevel)
    if not skill == SKILL_FISHING then -- we only run this if the skill gained was fishing skill
        return true
    end
    if newlevel >= 100 then
        player:getPosition():sendMagicEffect(CONST_ME_PLUNGING_FISH)
        player:sendTextMessage(MESSAGE_EVENT_ADVANCE, "Congratulations you are officially a BIG FISHER!")
    end
    return true
end
```

**:TODO: Unsure atm if return true is necessary to advance or not.**

## onModalWindow(player, modalWindowId, buttonId, choiceId)

> * **player** -- 1st arg/parameter /_**userdata**_/ = The **player** the modal window is being called for, the player whom its registered to.
> * **modalWindowId** -- 2nd arg/parameter /_**integer**_/ = The **modalWindowId** is an integer representing the modalwindow's id.
> * **buttonId** -- 3rd arg/parameter /_**integer**_/ = The **buttonId** is an **integer** representing
> * **choiceId** -- 4th arg/parameter /_**integer**_/ = The **newlevel** is an **integer** value of the level _after_ the advancement.

**onModalWindow is called whenever any modalwindow is sent to the player**

**You can register your event in creaturescripts.xml like so:**

```xml
<event type="modalwindow" name="coolMenu" script="modalwindow.lua" />
```

**You can then call the event in a script like so:**

**Example:** modalwindow.lua

```lua
function onModalWindow(player, modalWindowId, buttonId, choiceId)
    -- TODO
end
```

**:TODO:**

## onTextEdit(player, item, text)

> * **player** -- 1st arg/parameter /_**userdata**_/ = The **player** the modal window is being called for, the player whom its registered to.
> * **item** -- 2nd arg/parameter /_**userdata**_/ = The **item** that is being edited
> * **text** -- 3rd arg/parameter /_**string**_/ = The **text** is the **string** that the player writes.

**onTextEdit is called whenever any writes text to any item**

**You can register your event in creaturescripts.xml like so:**

```xml
<event type="textedit" name="bookPassword" script="bookPassword.lua" />
```

**You can then call the event in a script like so:**

**Example:** bookPassword.lua

```lua
function onTextEdit(player, modalWindowId, buttonId, choiceId)
    -- TODO
end
```

**:TODO:**

## onHealthChange(creature, attacker, primaryDamage, primaryType, secondaryDamage, secondaryType, origin)

> * **creature** -- 1st arg/parameter /_**userdata**_/ = The **creature** whom's health is changing, either up or down.
> * **attacker** -- 2nd arg/parameter /_**userdata**_/ = The **attacker** is the **creature** causing the healthchange.
> * **primaryDamage** -- 3rd arg/parameter /_**integer**_/ = The **primaryDamage** is the amount of health change for a primary damage type.
> * **primaryType** -- 4th arg/parameter /_**integer**_/ = The **primaryType** is a **constant value** found here. -- insert link
> * **secondaryDamage** -- 5th arg/parameter /_**integer**_/ = The **secondaryDamage** is the amount of health change for a secondary damage type.
> * **secondaryType** -- 6th arg/parameter /_**integer**_/ = The **secondaryType** is a **constant value** found here. -- insert link
> * **origin** -- 7th arg/parameter /_**integer**_/ = The **origin** is a **constant value** found here. -- insert link

**onHealthChange is called when a creatures healh changes, up or down.**

**You can register your event in creaturescripts.xml like so:**

```xml
<event type="healthchange" name="cursedhealth" script="cursedhealth.lua" />
```

**You can then call the event in a script like so:**

**Example:** cursedhealth.lua

```lua
function onHealthChange(creature, attacker, primaryDamage, primaryType, secondaryDamage, secondaryType, origin)
    -- TODO
end
```

**:TODO:**

## onManaChange(creature, attacker, primaryDamage, primaryType, secondaryDamage, secondaryType, origin)

> * **creature** -- 1st arg/parameter /_**userdata**_/ = The **creature** whom's health is changing, either up or down.
> * **attacker** -- 2nd arg/parameter /_**userdata**_/ = The **attacker** is the **creature** causing the healthchange.
> * **primaryDamage** -- 3rd arg/parameter /_**integer**_/ = The **primaryDamage** is the amount of health change for a primary damage type.
> * **primaryType** -- 4th arg/parameter /_**integer**_/ = The **primaryType** is a **constant value** found here. -- insert link
> * **secondaryDamage** -- 5th arg/parameter /_**integer**_/ = The **secondaryDamage** is the amount of health change for a secondary damage type.
> * **secondaryType** -- 6th arg/parameter /_**integer**_/ = The **secondaryType** is a **constant value** found here. -- insert link
> * **origin** -- 7th arg/parameter /_**integer**_/ = The **origin** is a **constant value** found here. -- insert link

**onManaChange is called when a players mana changes, up or down.**

**You can register your event in creaturescripts.xml like so:**

```xml
<event type="manachange" name="buffedMana" script="buffedMana.lua" />
```

**You can then call the event in a script like so:**

**Example:** buffedMana.lua

```lua
function onManaChange(creature, attacker, primaryDamage, primaryType, secondaryDamage, secondaryType, origin)
    -- TODO
end
```

**:TODO:**

## onExtendedOpCode(player, opcode, buffer)

> * **player** -- 1st arg/parameter /_**userdata**_/ = The **player**
> * **opcode** -- 2nd arg/parameter /_**userdata**_/ = The **opcode**
> * **buffer** -- 3rd arg/parameter /_**integer**_/ = The **buffer**

**onExtendedOpCode is called when**

**You can register your event in creaturescripts.xml like so:**

```xml
<event type="extendedopcode" name="opCode" script="opCode.lua" />
```

**You can then call the event in a script like so:**

**Example:** opCode.lua

```lua
function onExtendedOpCode(player, opcode, buffer)
    -- TODO
end
```

**:TODO:**
