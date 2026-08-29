# MoveEvent

There are many types of events for the MoveEvent interface, here is a list.

* \[onStepIn(creature, item, pos, fromPosition)]
* \[onStepOut(creature, item, pos, fromPosition)]
* \[onEquip(player, item, slot, isCheck)]
* \[onDeEquip(player, item, slot, isCheck)]
* \[onAddItem(moveitem, tileitem, pos)]
* \[onRemoveItem(moveitem, tileitem, pos)]

1. You can create a MoveEvent script in data/movements/scripts folder, but
2. You must register MoveEvents in data/movements/movements.xml, here is an example

```xml
<movevent event="StepIn" itemid="293" script="decay.lua" />
```

1. Alternatively you can use revscript method to register via lua, by saving a .lua file in data/scripts folder.

**Please keep in mind you can name your script whatever you want as long as it ends in .lua, and its full name is in the xml, with script=""**

## onStepIn(creature, item, pos, fromPosition)

> * **creature** -- 1st arg/parameter /_**userdata**_/ = The **creature** who is doing the stepin movement
> * **item** -- 2nd arg/parameter /_**userdata**_/ = The **item** that is being stepped on.
> * **pos** -- 3rd arg/parameter /_**userdata**_/ = The **position** for the location being stepped on
> * **fromPosition** -- 4th arg/parameter /_**userdata**_/ = The **position** which the creature moved from

onStepin is called whenever any creature steps on the registered item id(s)

**You can register your event in movement.xml like so:**

```xml
<movevent event="StepIn" fromid="11165" toid="11188" script="mud.lua" />
```

**You can then call the event in a script like so:**

mud.lua

```lua
local combat = Combat()
combat:setParameter(COMBAT_PARAM_EFFECT, CONST_ME_MAGIC_RED)

local condition = Condition(CONDITION_PARALYZE)
condition:setParameter(CONDITION_PARAM_TICKS, 20000)
condition:setFormula(-1, 80, -1, 80)
combat:addCondition(condition)

function onStepIn(creature, item, pos, fromPosition)
    if not creature:hasCondition(CONDITION_PARALYZE) then
        combat:execute(creature, Variant(creature))
    end
    return true
end
```

**Always remember to return true if you wish to allow creature to step there, returning false or not returning true will block creature from stepping there!**

## onStepOut(creature, item, pos, fromPosition)

> * **creature** -- 1st arg/parameter /_**userdata**_/ = The **creature** who is doing the stepin movement
> * **item** -- 2nd arg/parameter /_**userdata**_/ = The **item** that is being stepped on.
> * **pos** -- 3rd arg/parameter /_**userdata**_/ = The **position** for the location being stepped on
> * **fromPosition** -- 4th arg/parameter /_**userdata**_/ = The **position** which the creature moved from

onStepOut is called whenever any player tries to step off registered item id(s)

**You can register your event in creaturescripts.xml like so:**

```xml
<movevent event="StepOut" fromid="11165" toid="11188" script="mud.lua" />
```

**You can then call the event in a script like so:**

mud.lua

```lua
local mudIds = {11165, 11166, 11167, 11168, 11169, 11170, 11171, 11172, 11173, 11174, 11175, 11176, 11178, 11179, 11180, 11181, 11182, 11183, 11184, 11185, 11186, 11187, 11188}

function onStepOut(creature, item, pos, fromPosition)
    for i = 1, #mudIds do
        if Tile(fromPosition):getItemById(mudIds[i]) then
            pos:sendDistanceEffect(fromPosition, CONST_ANI_SMALLEARTH, creature)
        end
    end
    return true
end
```

**Always remember to return true if you wish to allow creature to step off the tile they are on, returning false or not returning true will block the creature from being able to step off!**

## onEquip(player, item, slot, isCheck)

> * **player** -- 1st arg/parameter /_**userdata**_/ = The **player** who is equipping the item
> * **item** -- 2nd arg/parameter /_**userdata**_/ = The **item** that is being equipped
> * **slot** -- 3rd arg/parameter /_**integer**_/ = The **slot** item is being equipped to, represents a const value.
> * **isCheck** -- 4th arg/parameter /_**boolean**_/ = is this before item is equipped, true or false

onEquip runs twice everytime a player equips an item. It runs once before it is equipped, and runs again after. The parameter "isCheck" is true value the first time, before the item is equipped, and false the second time, after it is equipped. This is kind of unique to consider as it is one item with one registered event that runs two times.

**You can register your event in creaturescripts.xml like so:**

```xml
   <movevent event="Equip" itemid="8891" slot="armor" script="pallyarmor.lua">
       <vocation name="Paladin" />
       <vocation name="Royal Paladin" showInDescription="0" />
```

**You can then call the event in a script like so:**

pallyarmor.lua

```lua
function onEquip(player, item, slot, isCheck)
    if isCheck then
        return true -- we return true here because we don't want to apply anything until after armor is equipped.
    end

    player:setCapacity(player:getCapacity() + 20)

    return true
end
```

**Must return true to equip without error!**

## onDeEquip(player, item, slot, isCheck)

> * **player** -- 1st arg/parameter /_**userdata**_/ = The **player** that is removing the item
> * **item** -- 2nd arg/parameter /_**userdata**_/ = The **item** that is being removed
> * **slot** -- 3rd arg/parameter /_**userdata**_/ = The **slot** that the item is being removed from.
> * **isCheck** -- 4th arg/parameter /_**userdata**_/ = is this before item is removed, true or false

onDeEquip runs twice everytime a player de-equips an item. It runs once before it is de-equipped, and runs again after. The parameter "isCheck" is true value the first time, before the item is de-equipped, and false the second time, after it is de-equipped. This is kind of unique to consider as it is one item with one registered event that runs two times.

**You can register your event in creaturescripts.xml like so:**

```xml
<movevent event="DeEquip" itemid="8891" slot="armor" script="pallyarmor.lua" />
```

**You can then call the event in a script like so:**

pallyarmor.lua

```lua
function onDeEquip(player, item, slot, isCheck)
    if isCheck then
        return true -- we return true here because we don't want to apply anything until after armor is removed
    end

    player:setCapacity(player:getCapacity() - 20)

    return true
end
```

**Must return true to remove item without error!**
