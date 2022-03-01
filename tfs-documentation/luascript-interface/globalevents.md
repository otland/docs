# GlobalEvents

* [onStartup()](globalevents.md#onstartup)
* [onShutdown()](globalevents.md#onshutdown)
* [onRecord()](globalevents.md#onrecord)
* [onTime()](globalevents.md#ontime)
* [onThink()](globalevents.md#onthink)

### onStartUp()

onStartup has no parameters, requires no return, and _**only runs once**_ during the start of the server.

**Example** _startup.lua_

```lua
function onStartup()
    print("There are " ..#Game.getHouses().. " houses registered to this map")
end
```

{% hint style="info" %}
The above will print the size of the table returned from Game.getHouses(), to the console on startup
{% endhint %}

You can register in **data/globalevents/globalevents.xml** by using **type**="_startup_" like so:

```xml
<globalevent type="startup" name="ServerStartup" script="startup.lua" />
```

### onShutdown()

onShutdown has no parameters, requires no return, and _**only runs once**_ during the shutdown of the server

**Example** _shutdown.lua_

```lua
function onShutdown()
    for index, player in pairs(Game.getPlayers()) do
        player:save()
    end
end
```

{% hint style="info" %}
The above will save any players still logged in before shutdown, please note players will already be kicked out, this is just an example.
{% endhint %}

You can register in **data/globalevents/globalevents.xml** by using **type**="_shutdown_" like so:

```xml
<globalevent type="shutdown" name="ServerShutdown" script="shutdown.lua" />
```

### onRecord()

onRecord has two parameters, requires return true, and runs each time a new record is made for most players online

> * current -- number value of new record, for most players online
> * old -- number value of old record, for most players online

**Example** _record.lua_

```lua
function onRecord(current, old)
    addEvent(Game.broadcastMessage, 150, "New record: " .. current .. " players are logged in.", MESSAGE_STATUS_DEFAULT)
    return true
end
```

{% hint style="info" %}
The above will broadcast a message informing the server of the new record and current players logged in
{% endhint %}

You can register in **data/globalevents/globalevents.xml** by using **type**="_record_" like so:

```xml
<globalevent type="record" name="PlayerRecord" script="record.lua" />
```

### onTime()

onTime has one parameter which represents the _**time**_ it executes, requires return true, and **runs each each day at same time**

**Example** _ontime.lua_

```lua
function onTime(interval)
    Game.startRaid("Dragons")
    return true
end
```

{% hint style="info" %}
The above will start a raid named "Dragons" at time specified in globalevents.xml
{% endhint %}

You can register in **data/globalevents/globalevents.xml** by giving it a unique name and setting the time using **time**="_time_" like so:

```xml
<globalevent name="StartDragonRaid" time="09:55:00" script="ontime.lua" />
```

### onThink()

onThink has one parameter which represents how often it executes in milliseconds, requires return true, and **runs as often as specified** in globalevents.xml

**Example** _onthink.lua_

```lua
function onThink(interval)
    for index, player in pairs(Game.getPlayers()) do
        player:save()
    end
    return true
end
```

{% hint style="info" %}
The above will save all players currently logged in. This is not very effecient, just an example
{% endhint %}

You can register in **data/globalevents/globalevents.xml** by giving it a unique name and setting how often it will execute using interval="1000" _**time is in milliseconds**_

```xml
<globalevent name="SaveOnThink" interval="10000" script="onthink.lua" />
```

{% hint style="info" %}
The above will execute every ten seconds 10 \* 1000 = 10000
{% endhint %}
