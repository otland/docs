### Game

#### Available methods:

\[createItem\(itemId, count\[, position\]\)\]\(\#Game.createItem{itemId, count\[, position\]}\)

\[createContainer\(itemId, size\[, position\]\)\]\(\#Game.createContainer{itemId, size\[, position\]}\)  

\[createMonster\(monsterName, position\[, extended = false\[, force = false\]\]\)\]\(\#Game.createMonster{monsterName, position\[, extended = false\[, force = false\]\]}\)  

\[createNpc\(npcName, position\[, extended = false\[, force = false\]\]\)\]\(\#Game.createNpc{npcName, position\[, extended = false\[, force = false\]\]}\)  

\[createTile\(x, y, z\[, isDynamic = false\]\)\]\(\#Game.createTile{x, y, z\[, isDynamic = false\]}\)  

\[createTile\(position\[, isDynamic = false\]\)\]\(\#Game.createTile{position\[, isDynamic = false\]}\)  

\[getExperienceStage\(level\)\]\(\#Game.getExperienceStage{level}\)  

\[getGameState\(\)\]\(\#Game.getGameState{}\)  

\[getHouses\(\)\]\(\#Game.getHouses{}\)  

\[getMonsterCount\(\)\]\(\#Game.getMonsterCount{}\)  

\[getNpcCount\(\)\]\(\#Game.getNpcCount{}\)  

\[getPlayerCount\(\)\]\(\#Game.getPlayerCount{}\)  

\[getPlayers\(\)\]\(\#Game.getPlayers{}\)  

\[getReturnMessage\(value\)\]\(\#Game.getReturnMessage{value}\)  

\[getSpectators\(position\[, multifloor = false\[, onlyPlayer = false\[, minRangeX = 0\[, maxRangeX = 0\[, minRangeY = 0\[, maxRangeY = 0\]\]\]\]\]\]\)\]\(\#Game.getSpectators{position\[, multifloor = false\[, onlyPlayer = false\[, minRangeX = 0\[, maxRangeX = 0\[, minRangeY = 0\[, maxRangeY = 0\]\]\]\]\]\]}\)  

\[getTowns\(\)\]\(\#Game.getTowns{}\)  

\[getWorldType\(\)\]\(\#Game.getWorldType{}\)  

\[loadMap\(path\)\]\(\#Game.loadMap{path}\)  

\[setGameState\(state\)\]\(\#Game.setGameState{state}\)  

\[setWorldType\(type\)\]\(\#Game.setWorldType{type}\)  

\[startRaid\(raidName\)\]\(\#Game.startRaid{raidName}\)  





\*\*\*



&lt;a name="Game.createItem{itemId, count\[, position\]}"/&gt;

\#\#\#\#\#\# Game.createItem\(itemId, count\[, position\]\)

&gt; \*\*Description:\*\* Creates an item.  

&gt; \*\*Parameters:\*\* &lt;ul&gt;&lt;li&gt;\_itemId\_ - \_Id of the item to be created\_&lt;/li&gt;&lt;li&gt;\_count\_ - \_How many are we creating?\_&lt;/li&gt;&lt;li&gt;\_position\_ - \_Where do we place it? \(optional\)\_&lt;/li&gt;&lt;/ul&gt;

&gt; \*\*Returns:\*\* The item created. \(userdata\)  

&gt; \*\*Example:\*\* 

\`\`\`Lua

-- Create an item somewhere on the map.

local item = Game.createItem\(2400, 1, Position\(100, 100, 7\)\)

--

-- Create a temporary item that is given to a player \(if it isn't moved from creation it will be deleted\)

local player = Player\(...\)

player:addItemEx\(Game.createItem\(2400, 1\)\)

\`\`\`

&gt; \*\*Added in version:\*\* 1.0



\*\*\*



&lt;a name="Game.createContainer{itemId, size\[, position\]}"/&gt;

\#\#\#\#\#\# Game.createContainer\(itemId, size\[, position\]\)

&gt; \*\*Description:\*\* Creates a container with given size.  

&gt; \*\*Parameters:\*\* &lt;ul&gt;&lt;li&gt;\_itemId\_ - \_Id of the item to be created\_&lt;/li&gt;&lt;li&gt;\_size\_ - \_Size of the container\_&lt;/li&gt;&lt;li&gt;\_position\_ - \_Where do we place it? \(optional\)\_&lt;/li&gt;&lt;/ul&gt;

&gt; \*\*Returns:\*\* The container created. \(userdata\)  

&gt; \*\*Example:\*\* 

\`\`\`Lua

-- Create an amulet of loss as a container with size 5 at position: x 100, y 100, z 7.

local item = Game.createContainer\(ITEM\_AMULETOFLOSS, 5, Position\(100, 100, 7\)\)

--

-- Create a temporary container that is given to a player \(if it isn't moved from creation it will be deleted\)

local player = Player\(...\)

player:addItemEx\(Game.createContainer\(ITEM\_AMULETOFLOSS, 5\)\)

\`\`\`

&gt; \*\*Added in version:\*\* 1.1



\*\*\*



&lt;a name="Game.createMonster{monsterName, position\[, extended = false\[, force = false\]\]}"/&gt;

\#\#\#\#\#\# Game.createMonster\(monsterName, position\[, extended = false\[, force = false\]\]\)

&gt; \*\*Description:\*\* Creates a monster.  

&gt; \*\*Parameters:\*\* &lt;ul&gt;&lt;li&gt;\_monsterName\_ - \_Name of the monster to be created\_&lt;/li&gt;&lt;li&gt;\_position\_ - \_Where do we place it?\_&lt;/li&gt;&lt;li&gt;\_extended\_ - \_Extend the range? \(optional, default: false\)\_&lt;/li&gt;&lt;li&gt;\_force\_ - \_Will it be created even if it cannot stand at the position? \(optional, default: false\)\_&lt;/li&gt;&lt;/ul&gt;

&gt; \*\*Returns:\*\* The monster created. \(userdata\)  

&gt; \*\*Example:\*\* 

\`\`\`Lua

-- This should always create this monster.

local monster = Game.createMonster\("demon", Position\(100, 100, 7\), false, true\)

if not monster then

	-- Something went wrong?

end

\`\`\`

&gt; \*\*Added in version:\*\* 1.0



\*\*\*



&lt;a name="Game.createNpc{npcName, position\[, extended = false\[, force = false\]\]}"/&gt;

\#\#\#\#\#\# Game.createNpc\(npcName, position\[, extended = false\[, force = false\]\]\)

&gt; \*\*Description:\*\* Creates a npc.  

&gt; \*\*Parameters:\*\* &lt;ul&gt;&lt;li&gt;\_npcName\_ - \_Name of the npc to be created\_&lt;/li&gt;&lt;li&gt;\_position\_ - \_Where do we place it?\_&lt;/li&gt;&lt;li&gt;\_extended\_ - \_Extend the range? \(optional, default: false\)\_&lt;/li&gt;&lt;li&gt;\_force\_ - \_Will it be created even if it cannot stand at the position? \(optional, default: false\)\_&lt;/li&gt;&lt;/ul&gt;

&gt; \*\*Returns:\*\* The npc created. \(userdata\)  

&gt; \*\*Example:\*\* 

\`\`\`Lua

-- This may possibly not create the npc.

local npc = Game.createMonster\("some npc", Position\(100, 100, 7\), false, false\)

if not npc then

	-- Something is probably blocking that position and around it aswell

end

\`\`\`

&gt; \*\*Added in version:\*\* 1.0



\*\*\*



&lt;a name="Game.createTile{x, y, z\[, isDynamic = false\]}"/&gt;

\#\#\#\#\#\# Game.createTile\(x, y, z\[, isDynamic = false\]\)

&gt; \*\*Description:\*\* Creates a tile if it can.  

&gt; \*\*Parameters:\*\* &lt;ul&gt;&lt;li&gt;\_x\_ - \_X coordinate\_&lt;/li&gt;&lt;li&gt;\_y\_ - \_Y coordinate\_&lt;/li&gt;&lt;li&gt;\_z\_ - \_Z coordinate\_&lt;/li&gt;&lt;li&gt;\_isDynamic\_ - \_Is this tile dynamic? \(optional, default: false\)\_&lt;/li&gt;&lt;/ul&gt;

&gt; \*\*Returns:\*\* The tile created or the previous existing one. \(userdata\)  

&gt; \*\*Example:\*\* 

\`\`\`Lua

local tile = Game.createTile\(100, 100, 7\)

local ground = tile:getGround\(\)

if ground then

	print\(ground:getName\(\)\)

end

\`\`\`

&gt; \*\*Added in version:\*\* 1.0



\*\*\*



&lt;a name="Game.createTile{position\[, isDynamic = false\]}"/&gt;

\#\#\#\#\#\# Game.createTile\(position\[, isDynamic = false\]\)

&gt; \*\*Description:\*\* Creates a tile if it can.  

&gt; \*\*Parameters:\*\* &lt;ul&gt;&lt;li&gt;\_position\_ - \_Location of the tile.\_&lt;/li&gt;&lt;li&gt;\_isDynamic\_ - \_Is this tile dynamic? \(optional, default: false\)\_&lt;/li&gt;&lt;/ul&gt;

&gt; \*\*Returns:\*\* The tile created or the previous existing one. \(userdata\)  

&gt; \*\*Example:\*\* 

\`\`\`Lua

local tile = Game.createTile\(Position\(100, 100, 7\)\)

local ground = tile:getGround\(\)

if ground then

	print\(ground:getName\(\)\)

end

\`\`\`

&gt; \*\*Added in version:\*\* 1.0



\*\*\*



&lt;a name="Game.getExperienceStage{level}"/&gt;

\#\#\#\#\#\# Game.getExperienceStage\(level\)

&gt; \*\*Description:\*\* Find the experience rate related to a certain level.  

&gt; \*\*Parameters:\*\* &lt;ul&gt;&lt;li&gt;\_level\_ - \_Level to get the stage with.\_&lt;/li&gt;&lt;/ul&gt;

&gt; \*\*Returns:\*\* The experience rate related to the specified level.  

&gt; \*\*Example:\*\* 

\`\`\`Lua

-- Print the experience rate for level 8 to the console

print\(Game.getExperienceStage\(8\)\)

\`\`\`

&gt; \*\*Added in version:\*\* 1.0



\*\*\*



&lt;a name="Game.getGameState{}"/&gt;

\#\#\#\#\#\# Game.getGameState\(\)

&gt; \*\*Description:\*\* Gets the current gamestate.  

&gt; \*\*Parameters:\*\* None  

&gt; \*\*Returns:\*\* Current gamestate on the server.  

&gt; \*\*Example:\*\* 

\`\`\`Lua

print\(Game.getGameState\(\)\)

\`\`\`

&gt; \*\*Added in version:\*\* 1.0



\*\*\*



&lt;a name="Game.getHouses{}"/&gt;

\#\#\#\#\#\# Game.getHouses\(\)

&gt; \*\*Description:\*\* Get all houses.  

&gt; \*\*Parameters:\*\* None  

&gt; \*\*Returns:\*\* A table containing all houses \(userdata\).  

&gt; \*\*Example:\*\* 

\`\`\`Lua

-- This prints the names of all houses that exist on the server

local houses = Game.getHouses\(\)

for i = 1, \#houses do

	print\(houses\[i\]:getName\(\)\)

end

\`\`\`

&gt; \*\*Added in version:\*\* 1.0



\*\*\*



&lt;a name="Game.getMonsterCount{}"/&gt;

\#\#\#\#\#\# Game.getMonsterCount\(\)

&gt; \*\*Description:\*\* Find the total amount of monsters on the server.  

&gt; \*\*Parameters:\*\* None  

&gt; \*\*Returns:\*\* Total amount of monsters on the server.  

&gt; \*\*Example:\*\* 

\`\`\`Lua

print\(Game.getMonsterCount\(\)\)

\`\`\`

&gt; \*\*Added in version:\*\* 1.0



\*\*\*



&lt;a name="Game.getNpcCount{}"/&gt;

\#\#\#\#\#\# Game.getNpcCount\(\)

&gt; \*\*Description:\*\* Find the total amount of npcs on the server.  

&gt; \*\*Parameters:\*\* None  

&gt; \*\*Returns:\*\* Total amount of npcs on the server.  

&gt; \*\*Example:\*\* 

\`\`\`Lua

print\(Game.getNpcCount\(\)\)

\`\`\`

&gt; \*\*Added in version:\*\* 1.0



\*\*\*



&lt;a name="Game.getPlayerCount{}"/&gt;

\#\#\#\#\#\# Game.getPlayerCount\(\)

&gt; \*\*Description:\*\* Find the total amount of players on the server.  

&gt; \*\*Parameters:\*\* None  

&gt; \*\*Returns:\*\* Total amount of players on the server.  

&gt; \*\*Example:\*\* 

\`\`\`Lua

print\(Game.getPlayerCount\(\)\)

\`\`\`

&gt; \*\*Added in version:\*\* 1.0



\*\*\*



&lt;a name="Game.getPlayers{}"/&gt;

\#\#\#\#\#\# Game.getPlayers\(\)

&gt; \*\*Description:\*\* Get all connected players.  

&gt; \*\*Parameters:\*\* None  

&gt; \*\*Returns:\*\* A table containing all connected players \(userdata\).  

&gt; \*\*Example:\*\* 

\`\`\`Lua

-- This prints the names of all players connected to the server

local players = Game.getPlayers\(\)

for i = 1, \#players do

	print\(players\[i\]:getName\(\)\)

end

\`\`\`

&gt; \*\*Added in version:\*\* 1.0



\*\*\*



&lt;a name="Game.getReturnMessage{value}"/&gt;

\#\#\#\#\#\# Game.getReturnMessage\(value\)

&gt; \*\*Description:\*\* Gets a message associated with the value.  

&gt; \*\*Parameters:\*\* &lt;ul&gt;&lt;li&gt;\_value\_ - \_Internal return value\_&lt;/li&gt;&lt;/ul&gt;

&gt; \*\*Returns:\*\* true  

&gt; \*\*Example:\*\* 

\`\`\`Lua

-- This makes no sense but its an example.

local player = Player\(...\)

player:say\(Game.getReturnMessage\(RETURNVALUE\_YOUARENOTTHEOWNER\), TALKTYPE\_SAY\)

\`\`\`

&gt; \*\*Added in version:\*\* 1.0



\*\*\*



&lt;a name="Game.getSpectators{position\[, multifloor = false\[, onlyPlayer = false\[, minRangeX = 0\[, maxRangeX = 0\[, minRangeY = 0\[, maxRangeY = 0\]\]\]\]\]\]}"/&gt;

\#\#\#\#\#\# Game.getSpectators\(position\[, multifloor = false\[, onlyPlayer = false\[, minRangeX = 0\[, maxRangeX = 0\[, minRangeY = 0\[, maxRangeY = 0\]\]\]\]\]\]\)

&gt; \*\*Description:\*\* Get all creatures in the area.  

&gt; \*\*Parameters:\*\* &lt;ul&gt;&lt;li&gt;\_position\_ - \_Center position\_&lt;/li&gt;&lt;li&gt;\_multifloor\_ - \_Search multiple floors? \(optional, default: false\)\_&lt;/li&gt;&lt;li&gt;\_onlyPlayer\_ - \_Find only players? \(optional, default: false\)\_&lt;/li&gt;&lt;li&gt;\_minRangeX\_ - \_Minimum range on the x axis \(optional, default: 0\)\_&lt;/li&gt;&lt;li&gt;\_maxRangeX\_ - \_Maximum range on the x axis \(optional, default: 0\)\_&lt;/li&gt;&lt;li&gt;\_minRangeY\_ - \_Minimum range on the y axis \(optional, default: 0\)\_&lt;/li&gt;&lt;li&gt;\_maxRangeY\_ - \_Maximum range on the y axis \(optional, default: 0\)\_&lt;/li&gt;&lt;/ul&gt;

&gt; \*\*Returns:\*\* A table containing creatures found \(userdata\).  

&gt; \*\*Example:\*\* 

\`\`\`Lua

-- This finds all players in a 5x5 area around \(100, 100, 7\)

local spectators = Game.getSpectators\(Position\(100, 100, 7\), false, true, 0, 2, 0, 2\)

for i = 1, \#spectators do

	local spectator = spectators\[i\]

	spectator:say\(spectator:getName\(\), TALKTYPE\_SAY\)

end

\`\`\`

&gt; \*\*Added in version:\*\* 1.0



\*\*\*



&lt;a name="Game.getTowns{}"/&gt;

\#\#\#\#\#\# Game.getTowns\(\)

&gt; \*\*Description:\*\* Get all towns.  

&gt; \*\*Parameters:\*\* None  

&gt; \*\*Returns:\*\* A table containing all towns \(userdata\).  

&gt; \*\*Example:\*\* 

\`\`\`Lua

-- This prints the names of all towns that exist on the server

local towns = Game.getTowns\(\)

for i = 1, \#towns do

	print\(towns\[i\]:getName\(\)\)

end

\`\`\`

&gt; \*\*Added in version:\*\* 1.0



\*\*\*



&lt;a name="Game.getWorldType{}"/&gt;

\#\#\#\#\#\# Game.getWorldType\(\)

&gt; \*\*Description:\*\* Gets the current world type.  

&gt; \*\*Parameters:\*\* None  

&gt; \*\*Returns:\*\* Current gamestate on the server.  

&gt; \*\*Example:\*\* 

\`\`\`Lua

print\(Game.getWorldType\(\)\)

\`\`\`

&gt; \*\*Added in version:\*\* 1.0



\*\*\*



&lt;a name="Game.loadMap{path}"/&gt;

\#\#\#\#\#\# Game.loadMap\(path\)

&gt; \*\*Description:\*\* This loads a new map chunk.  

&gt; \*\*Parameters:\*\* &lt;ul&gt;&lt;li&gt;\_path\_ - \_File path to the map.\_&lt;/li&gt;&lt;/ul&gt;

&gt; \*\*Returns:\*\* Nothing  

&gt; \*\*Example:\*\* 

\`\`\`Lua

Game.loadMap\("data/map/some\_other\_map.otbm"\)

\`\`\`

&gt; \*\*Added in version:\*\* 1.0



\*\*\*



&lt;a name="Game.setGameState{state}"/&gt;

\#\#\#\#\#\# Game.setGameState\(state\)

&gt; \*\*Description:\*\* Sets the current gamestate.  

&gt; \*\*Parameters:\*\* &lt;ul&gt;&lt;li&gt;\_state\_ - \_The new gamestate\_&lt;/li&gt;&lt;/ul&gt;

&gt; \*\*Returns:\*\* true  

&gt; \*\*Example:\*\* 

\`\`\`Lua

-- Shutdown the server

Game.setGameState\(GAME\_STATE\_SHUTDOWN\)

\`\`\`

&gt; \*\*Added in version:\*\* 1.0



\*\*\*



&lt;a name="Game.setWorldType{type}"/&gt;

\#\#\#\#\#\# Game.setWorldType\(type\)

&gt; \*\*Description:\*\* Sets the current world type.  

&gt; \*\*Parameters:\*\* &lt;ul&gt;&lt;li&gt;\_type\_ - \_The new world type\_&lt;/li&gt;&lt;/ul&gt;

&gt; \*\*Returns:\*\* true  

&gt; \*\*Example:\*\* 

\`\`\`Lua

-- Change to hardcore pvp

Game.setWorldType\(WORLD\_TYPE\_PVP\_ENFORCED\)

\`\`\`

&gt; \*\*Added in version:\*\* 1.0



\*\*\*



&lt;a name="Game.startRaid{raidName}"/&gt;

\#\#\#\#\#\# Game.startRaid\(raidName\)

&gt; \*\*Description:\*\* Starts a raid if one with said name exist.  

&gt; \*\*Parameters:\*\* &lt;ul&gt;&lt;li&gt;\_raidName\_ - \_Name of the raid.\_&lt;/li&gt;&lt;/ul&gt;

&gt; \*\*Returns:\*\* true if the raid started, nil otherwise.  

&gt; \*\*Example:\*\* 

\`\`\`Lua

if Game.startRaid\("test"\) then

	-- Raid was started.

end

\`\`\`

&gt; \*\*Added in version:\*\* 1.0



\#\#\#Global

\#\#\#\#Available methods:

\[addEvent\(callback, delay, ...\)\]\(\#addEvent{callback, delay, ...}\)  

\[stopEvent\(eventid\)\]\(\#stopEvent{eventid}\)  





\*\*\*



&lt;a name="addEvent{callback, delay, ...}"/&gt;

\#\#\#\#\#\# addEvent\(callback, delay, ...\)

&gt; \*\*Description:\*\* This function is used to run other functions at a later time.  

&gt; \*\*Parameters:\*\* &lt;ul&gt;&lt;li&gt;\_callback\_ - \_The function that should run at a later time.\_&lt;/li&gt;&lt;li&gt;\_delay\_ - \_Time before the callback runs in milliseconds.\_&lt;/li&gt;&lt;li&gt;\_...\_ - \_This can expand into any amount of variables, they are sent to the callback when it runs. \(optional\)\_&lt;/li&gt;&lt;/ul&gt;

&gt; \*\*Returns:\*\* The id associated with this event.  

&gt; \*\*Example:\*\* 

\`\`\`Lua

-- Creates an event that prints "Hello World!" to the console.

addEvent\(print, 1000, "Hello World!"\)

\`\`\`

&gt; \*\*Added in version:\*\* 1.0



\*\*\*



&lt;a name="stopEvent{eventid}"/&gt;

\#\#\#\#\#\# stopEvent\(eventid\)

&gt; \*\*Description:\*\* This function is used to stop functions that should run later.  

&gt; \*\*Parameters:\*\* &lt;ul&gt;&lt;li&gt;\_eventid\_ - \_The event id to stop.\_&lt;/li&gt;&lt;/ul&gt;

&gt; \*\*Returns:\*\* true if an event was stopped, false otherwise.  

&gt; \*\*Example:\*\* 

\`\`\`Lua

-- Creates an event that should print "Hello World!" but it's stopped before that can happen.

local event = addEvent\(print, 1000, "Hello World!"\)

stopEvent\(event\)

\`\`\`

&gt; \*\*Added in version:\*\* 1.0



\#\#\#os

\#\#\#\#Available methods:

\[mtime\(\)\]\(\#os.mtime{}\)  





\*\*\*



&lt;a name="os.mtime{}"/&gt;

\#\#\#\#\#\# os.mtime\(\)

&gt; \*\*Description:\*\* Returns the Unix time \(epoch\) in milliseconds  

&gt; \*\*Parameters:\*\* None  

&gt; \*\*Returns:\*\* The Unix time \(epoch\) in milliseconds  

&gt; \*\*Example:\*\* 

\`\`\`Lua

print\(os.mtime\(\) .. " milliseconds have passed since the Unix epoch"\)

\`\`\`

&gt; \*\*Added in version:\*\* 1.0



\#\#\#table

\#\#\#\#Available methods:

\[create\(arrayLength, keyLength\)\]\(\#table.create{arrayLength, keyLength}\)  





\*\*\*



&lt;a name="table.create{arrayLength, keyLength}"/&gt;

\#\#\#\#\#\# table.create\(arrayLength, keyLength\)

&gt; \*\*Description:\*\* Creates a new table with specified length.  

&gt; \*\*Parameters:\*\* &lt;ul&gt;&lt;li&gt;\_arrayLength\_ - \_Ordered indexes \(1, 2, ...arrayLength\)\_&lt;/li&gt;&lt;li&gt;\_keyLength\_ - \_Unordered indexes \(anything that does not follow the above\)\_&lt;/li&gt;&lt;/ul&gt;

&gt; \*\*Returns:\*\* The created table.  

&gt; \*\*Example:\*\* 

\`\`\`Lua

local t = table.create\(5, 0\)

for i = 1, \#t do

	t\[i\] = i + 1

end

\`\`\`

&gt; \*\*Added in version:\*\* 1.0

