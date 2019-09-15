# TFS 1.4 official release

In this section, we will cover the new official release of The Forgotten Server, TFS 1.4 !

One of the major features from this release is [Revscriptsys](https://github.com/otland/forgottenserver/wiki/Revscriptsys), which allows us to register scripts using Lua instead of XML. Another important feature is a custom RSA key loader, which will allow you to use the RSA private key from a PEM file you may generate, thereby granting more security to your server. Some of the other features are: a Docker image to easily set up TFS, storing town lists in database, POSIX signal handling...

Following these lines, you can find a changelog made of newly added features, issues that have been fixed, enhancements, and so on.

## Changelog TFS 1.4

### Features

* Revscriptsys
* Custom RSA key loader
* Docker image
* Storage of town lists in database
* Improved POSIX signal handling \(SIGINT, SIGTERM, SIGHUP and SIGUSR1 signals added\)
* Improved rule violation and bugs reporting system

### Functionalities changed from sources to Lua

* Commands
* Loot drop mechanism
* Actions.xml itemid increase/decrease function removed
* Party experience share
* House management
* Levitate

### Added

* Creature:
  * Creature:setHealth\(health\)
  * Creature:setSkillLoss\(skillLoss\)
  * Creature:addSummon\(monster\) and Creature:removeSummon\(monster\)
  * Added Creature:getZone\(\)
    * ZONE\_PROTECTION
    * ZONE\_NOPVP
    * ZONE\_PVP
    * ZONE\_NOLOGOUT
    * ZONE\_NORMAL
  * Secondary functionality for Creature:move method:
    * Creature:move\(tile\[, flags = 0\]\)
* Enums:
  * CONST\_ME\_EARLY\_THUNDER
  * CONST\_ME\_RAGIAZ\_BONECAPSULE
  * CONST\_ME\_CRITICAL\_DAMAGE
  * CONST\_ME\_PLUNGING\_FISH
  * MESSAGE\_GUILD
  * MESSAGE\_PARTY\_MANAGEMENT
  * MESSAGE\_PARTY
* Events:
  * Player:onReportRuleViolation\(targetName, reportType, reportReason, comment, translation\)
  * Player:onItemMoved\(item, count, fromPosition, toPosition\) or Player.onItemMoved\(self, item, count, fromPosition, toPosition, fromCylinder, toCylinder\)
  * Party:onShareExperience\(exp\) or Party.onShareExperience\(self, exp\)
  * Monster:onDropLoot\(corpse\)
* Game:
  * Game.getClientVersion\(\)
* Group:
  * Group:hasFlag\(flag\)
* House
  * House:getItems\(\)
  * House:getDoorIdByPosition\(position\)
  * House:canEditAccessList\(listId, player\)
  * House:kickPlayer\(player, targetPlayer\)
* Item
  * Item:getCustomAttribute\(key\)
  * Item:setCustomAttribute\(key, value\)
  * Item:removeCustomAttribute\(key\)
  * Item:isLoadedFromMap\(\)
* ItemType:
  * ItemType:isBlocking\(\)
  * ItemType:isGroundTile\(\)
  * ItemType:isMagicField\(\)
  * ItemType:isUseable\(\)
  * ItemType:isPickupable\(\)
  * ItemType:getAmmoType\(\)
  * ItemType:getCorpseType\(\)
* Party:
  * Party\(player\)
* Player
  * Player:getSpecialSkill\(specialSkillType\)
  * Player:addSpecialSkill\(specialSkillType, value\)
    * SPECIALSKILL\_CRITICALHITCHANCE
    * SPECIALSKILL\_CRITICALHITAMOUNT
    * SPECIALSKILL\_LIFELEECHCHANCE SPECIALSKILL\_LIFELEECHAMOUNT
    * SPECIALSKILL\_MANALEECHCHANCE
    * SPECIALSKILL\_MANALEECHAMOUNT
  * Added special skill support for conditions:
    * CONDITION\_PARAM\_SPECIALSKILL\_CRITICALHITCHANCE
    * CONDITION\_PARAM\_SPECIALSKILL\_CRITICALHITAMOUNT
    * CONDITION\_PARAM\_SPECIALSKILL\_LIFELEECHCHANCE
    * CONDITION\_PARAM\_SPECIALSKILL\_LIFELEECHAMOUNT
    * CONDITION\_PARAM\_SPECIALSKILL\_MANALEECHCHANCE
    * CONDITION\_PARAM\_SPECIALSKILL\_MANALEECHAMOUNT
  * Player:hasChaseMode\(\)
  * Player:hasSecureMode\(\)
  * Player:getFightMode\(\)
    * FIGHTMODE\_ATTACK
    * FIGHTMODE\_BALANCED
    * FIGHTMODE\_DEFENSE
  * Player:sendHouseWindow\(house, listId\)
  * Player:setEditHouse\(house, listId\)
  * Additional optional parameter for Player:setGhostMode method:
    * Player:setGhostMode\(enabled\[, showEffect=true\]\)
  * Secondary functionality for Player:sendTextMessage method:
    * Player:sendTextMessage\(type, text, channelId\)
* Tile:
  * Tile:addItem\(itemId\[, count/subType = 1\[, flags = 0\]\]\)
  * Tile:addItemEx\(item\[, flags = 0\]\)

**Fixed**

* MonsterType:getLoot\(\) crash
* MonsterType:isSummonable\(\) returned wrong flag
* Combat:execute\(\) crash
* Limited container:addItem subtype to 100

### Changed

* onManaChange's parameters match onHealthChange
* Player constructor accepts GUID parameter
* Player:getDepotChest sets last depotId for saving purposes
* Player:showTextDialog\(item, text\) accepts item userdata
* Changed Player:addMount to accept mount name along with id
* Renamed Combat:setCondition to Combat:addCondition



