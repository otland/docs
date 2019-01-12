# Editing your data pack

### What languages are used

There are only two languages used when working with TFS are XML and Lua. XML being the markup language that lets you register Lua scripts and can store information, while Lua is for scripting and interacting with the game world. You can start learning Lua from [here](https://www.lua.org/pil/contents.html).

### TFS Scripting Interface

There are a few main functions that are needed when creating scripts.

The current scripting interfaces are: Actions, Chatchannels, Creaturescripts, Events, Globalevents, Movements, Npc, Spells, Talkactions, and Weapons.

For scripting purposes, you should use a reference or memorize the main functions used in these interfaces, these functions are:

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
function onThink(interval, lastExecution)
function onStartup()
function onShutdown()
function onRecord(current, old)
function onTime()
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

