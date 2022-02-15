---
description: Action's Event Interface
---

# Action

* [Action.onUse()](https://app.gitbook.com/s/-LVBMVPm-MlN4K7ZoPJo/tfs-documentation/luascript-interface/game\_interface.md#game-getspectators)

### Action.onUse(player, item, fromPosition, itemEx, toPosition, isHotkey)

{% hint style="info" %}
**onUse** is an event of the class **Action**
{% endhint %}

> * **player**  -- 1st arg/parameter /_**userdata**_/  =  The **player** who uses the item.
> * **item** -- 2nd arg/parameter/ _**userdata**_/ = The first **item** player uses/use with.
> * **fromPosition** - 3rd arg/parameter/_**userdata**_/ = The **position** the first item is at.
> * **itemEx** -- 4th arg/parameter/_**userdata**_/ = The target of item's _Use With_, can be **item** or **creature**
> * **toPosition** - 5th arg/parameter/ _**userdata**_/ = The **position** the first item is used on, with crosshairs.
> * **isHotkey** - 6th arg/parameter/ _**boolean**_/ = Did the player use item via hot key? **True/False**.

1. onUse is called whenever an item registered to the action is used.&#x20;
2.  You can register actions in data/actions/actions.xml

    ```markup
    <action itemid="4856" script="test.lua" />
    ```

    ```markup
    <action fromid="2146" toid="2147" script="other/enchanting.lua" />
    ```
3. Alternatively you can use [revscript](https://app.gitbook.com/@otland/s/ots-guide/tfs-documentation/luascript-interface/action#revscript-action) method to register via lua, by saving a .lua file in data/scripts folder.

**After you have registered your action in actions.xml you can call the event in a script like so:**

```lua
function onUse(player, item, fromPosition, target, toPosition, isHotkey)  -- can name the arguments what you like.
    local SwordLevel = player:getSkillLevel(SKILL_SWORD)
    if SwordLevel < 70 then
        player:sendCancelMessage("This technique requires a sword fighting skill of 70 or higher.")
        return false
    end

    if not item:hasAttribute(ITEM_ATTRIBUTE_EXTRADEFENSE) then
        player:sendCancelMessage("Only swords known for their well balance and extra defense are suitable for this task.")
        return false
    end

    if fromPosition:isSightClear(toPosition) then 
        player:sendCancelMessage("You must have a clear path to your target")
        return false
    end

    if target:isPlayer() then 
        player:sendCancelMessage("To execute this technique properly, the target needs to be a player.")
        return false
    end

    if isHotkey then 
        player:sendCancelMessage("You can't use this item with a hotkey!")
        return false
    end
     -- Executing the technique

    -- Teleport to the position
    player:teleportTo(toPosition)

    -- Configure bleeding damage
    local bleed = {
        damage=50,
        rounds=10,
        interval=1
    }
    -- Apply deadly bleeding attack on target
    player:addDamageCondition(target, CONDITION_BLEEDING, DAMAGELIST_CONSTANT_PERIOD, bleed.damage, bleed.interval, bleed.rounds)

    -- Warn target that they just got slashed hard from player:getName and their blood is puring out!
    target:sendTextMessage(MESSAGE_STATUS_WARNING, "You just recieved a blood gushing wound from "..player:getName().."'s deadly sword technique!")
   return true
end
```

## Revscript Action

Revscript Actions share the same event **onUse()** with the same arguments listed above.

To access any events through revscripts, you must create a variable first to access the interface

{% hint style="warning" %}
> you **must** have **one** variable **per event** callback no matter which type of interface you wish to access!
{% endhint %}

Here is an example.

```lua
local swordTechnique = Action() -- we created a variable to access Action interface
```

Revscript Action has the available _methods_ and _event_ to use with its interface

> **Event**
>
> * **onUse**(player, item, fromPosition, itemEx, toPosition, isHotkey)
>
> **Methods**
>
> * action:**register**() -- Registers the action **event**.&#x20;
> * action:**id**(_**x**_)    -- Registers items with **id** _**x**_ for event
> * action:**aid**(_**x**_) -- Registers items with **action id** _**x**_ for event
> * action:**uid**(_**x**_) -- Registers items with **unique id** _**x**_ for event
> * action:**allowFarUse**(t/f) -- Allow far use? _**True/False**_
> * action:**blockWalls**(t/f) -- Do walls block item usage? _**True/False**_
> * action:**checkFloor**(t/f) -- Are we on same floor as target? _**True/False**_

## Action:id()

```lua
local swordTechnique = Action() -- we created a variable to access Action interface

swordTechnique:id(2376) -- sword's itemId to register for event
```

## Action:aid()

```lua
local swordTechnique = Action() -- we created a variable to access Action interface

swordTechnique:aid(15428) -- an actionId to register for event
```

## Action:uid()

```lua
local swordTechnique = Action() -- we created a variable to access Action interface

swordTechnique:uid(1337) -- a uniqueId to register for event
```

## Action:allowFarUse()

```lua
local swordTechnique = Action() -- we created a variable to access Action interface

swordTechnique:allowFarUse(true) -- True/False. True we can be more than one square away to use
```

## Action:blockWalls()

```lua
local swordTechnique = Action() -- we created a variable to access Action interface

swordTechnique:blockWalls(true) -- True/false. True and walls will block usage of item.
```

## Action:checkFloor()

```lua
local swordTechnique = Action() -- we created a variable to access Action interface

swordTechnique:checkFloor(true) -- True/false. True and we can only use item on same floor as us.
```

**To register an Action script using the Revscript Method, please first ensure it is saved at proper directory location, inside you data/scripts folder, then you can see the same action as above demonstrated as a revscript like so:**

```lua
local swordTechnique = Action() -- we created a variable to access Action interface

-- Here we register items to use for action, using swordTechnique variable.
swordTechnique:id(2376) -- sword's itemId to register for event
swordTechnique:aid(15428) -- an actionId to register for event
swordTechnique:uid(1337) -- a uniqueId to register for event

-- Here we configure our other action methods, still using swordTechniqu variable.
swordTechnique:allowFarUse(true)
swordTechnique:checkFloors(true)
swordTechnique:blockWalls(true)

 --- Here we call the event using the same swordTechnique variable.
function swordTechnique.onUse(player, item, fromPosition, target, toPosition, isHotkey) -- can name the arguments what you like.

    local SwordLevel = player:getSkillLevel(SKILL_SWORD)
    if SwordLevel < 70 then
        player:sendCancelMessage("This technique requires a sword fighting skill of 70 or higher.")
        return false
    end


    if not item:hasAttribute(ITEM_ATTRIBUTE_EXTRADEFENSE) then
        player:sendCancelMessage("Only swords known for their well balance and extra defense are suitable for this task.")
        return false
    end


    if fromPosition:isSightClear(toPosition) then 
        player:sendCancelMessage("You must have a clear path to your target")
        return false
    end


    if target:isPlayer() then 
        player:sendCancelMessage("To execute this technique properly, the target needs to be a player.")
        return false
    end


    if isHotkey then 
        player:sendCancelMessage("You can't use this item with a hotkey!")
        return false
    end

    -- Executing the technique

    -- Teleport to the position
    player:teleportTo(toPosition)

    -- Configure bleeding damage
    local bleed = {
        damage=50,
        rounds=10,
        interval=1
    }
    -- Apply deadly bleeding attack on target
    player:addDamageCondition(target, CONDITION_BLEEDING, DAMAGELIST_CONSTANT_PERIOD, bleed.damage, bleed.interval, bleed.rounds)

    -- Warn target that they just got slashed hard from player:getName and their blood is puring out!
    target:sendTextMessage(MESSAGE_STATUS_WARNING, "You just recieved a blood gushing wound from "..player:getName().."'s deadly sword technique!")

    return true
end

-- Finally after all logic is completed, we register the event, still using swordTechnique
swordTechnique:register()
```
