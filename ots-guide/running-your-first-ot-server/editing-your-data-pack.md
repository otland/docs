# Editing your datapack

### What are the languages used

There are two main languages used when working with TFS: XML and Lua. Depending on your knowledge, you may also want to edit the sources, which would mean you would have to work with C++ as well. XML is a markup language that lets you register Lua scripts and store information, while Lua is used for scripting and interacting with the game world. You can start learning Lua with [Programming in Lua](https://www.lua.org/pil/contents.html) or [Stigma's Lua guide](https://stigmax.gitbook.io/lua-guide/).

### TFS scripting interface

There are a few main functions that are needed when creating scripts.

The current scripting interfaces are: Actions, Chatchannels, Creaturescripts, Events, Globalevents, Monsters, Movements, Npc, Spells, Talkactions and Weapons.

For scripting purposes, you should use some reference or memorize the main functions used in these interfaces:

**Actions:**

```lua
function onUse(player, item, fromPosition, target, toPosition, isHotkey)
```

**Chatchannels:**

```lua
function canJoin(player)
function onSpeak(player, type, message)
```

**Creaturescripts:**

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

**Globalevents:**

```lua
function onThink(interval)
function onStartup()
function onShutdown()
function onRecord(current, old)
function onTime()
```

**Monsters:**

```lua
function onThink(interval)
function onCreatureMove(creature, newTile, newPos, oldTile, oldPos, teleport)
function onCreatureDisappear(creature, isLogout)
function onCreatureAppear(creature, isLogin)
function onCreatureSay(creature, type, text)
```

**Movements:**

```lua
function onStepIn(creature, item, toPosition, fromPosition)
function onStepOut(creature, item, toPosition, fromPosition)
function onEquip(player, item, slot)
function onDeEquip(player, item, slot)
function onAddItem(moveitem, tileitem, pos)
function onRemoveItem(moveitem, tileitem, pos)
```

**Npc:**

```lua
function onCreatureAppear(cid)
function onCreatureDisappear(cid)
function onCreatureSay(cid, type, msg)
function onThink()
```

**Spells:**

```lua
function onCastSpell(creature, variant)
```

**Talkactions:**

```lua
function onSay(player, words, param)
```

**Weapons:**

```lua
function onUseWeapon(player, variant)
```

