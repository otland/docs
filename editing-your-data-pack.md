# Editing your server

#### What languages are used

There is only two programming languages that are used when creating scripts for TFS, which are Lua and XML.

XML is used for storing data, such as items.xml, which holds all the attributes for items \(name, attack, defense, etc\), and lets you edit them.

Lua is used for dynamic scripting, which lets you do tons of things with your character, your server, the game world, items, creatures, and so on. You can start learning Lua from [here](https://www.lua.org/pil/contents.html).

#### TFS Scripting Interface

There are a few main functions that are needed when creating scripts.

The current scripting interfaces are: Actions, Chatchannels, Creaturescripts, Events, Globalevents, Movements, Npc, Spells, Talkactions, and Weapons.

For scripting purposes, you should use a reference or memorize the main functions used in these interfaces, these functions are:

###### Actions:

```lua
function onUse(player, item, fromPosition, target, toPosition, isHotkey)
```

###### Chatchannels:

```lua
function canJoin(player)
function onSpeak(player, type, message)
```

###### Creaturescripts:

```lua
function onLogin(player)
function onLogout(player)
function onThink(creature, interval)
function onPrepareDeath(creature, killer)
function onDeath(creature, corpse, killer, mostDamageKiller, lastHitUnjustified)
function onKill(creature, target)
function onAdvance(player, skill, oldLevel, newLevel)
function onModalWindow(player, modalWindowId, buttonId, choiceId)
function onTextEdit(player, item, text)
function onHealthChange(creature, attacker, primaryDamage, primaryType, secondaryDamage, secondaryType, origin)
function onManaChange(creature, attacker, manaChange, origin)
function onExtendedOpcode(player, opcode, buffer)
```

###### Globalevents:

```lua
function onThink(interval, lastExecution)
function onStartup()
function onShutdown()
function onRecord(current, old)
function onTime()
```

###### Movements:

```lua
function onStepIn(creature, item, toPosition, fromPosition)
function onStepOut(creature, item, toPosition, fromPosition)
function onEquip(player, item, slot)
function onDeEquip(player, item, slot)
function onAddItem(moveitem, tileitem, pos)
function onRemoveItem(moveitem, tileitem, pos)
```

###### Npc:

```
??????????????????????????????????????????
```

###### Spells:

```lua
function onCastSpell(creature, variant)
```

###### Talkactions:

```lua
function onSay(player, words, param)
```

###### Weapons:

```lua
function onUseWeapon(player, variant)
```

#### Code styling

#### 



