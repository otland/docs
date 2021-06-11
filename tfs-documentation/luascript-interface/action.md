# Action

* [Action.onUse\(\)](game_interface.md#game-getspectators)

## Action.onUse\(player, item, fromPosition, itemEx, toPosition, isHotkey\)

{% hint style="info" %}
**onUse** is an event of the class **Action**
{% endhint %}

onUse is called whenever an item registered to the action is used. You can register actions in data/actions/actions.xml

After you have registered your action in actions.xml you can call the event in a script like so:

```lua
function onUse(player, item, fromPosition, target, toPosition, isHotkey) -- can name the arguments what you like.
    local SwordLevel = player:getSkillLevel(SKILL_SWORD) -- 1st arg is Player userdata
    if item:hasAttribute(ITEM_ATTRIBUTE_EXTRADEFENSE) then -- 2nd arg is Item userdata
        if fromPosition:isSightClear(toPosition) then -- both the 3rd and 5th arg's are Position userdata
            if target:isPlayer() then -- 4th arg is userdata for what the item was used on, can be player, item, npc, ect.
                if isHotkey then -- last arg is a boolean value, true/false
                    return player:sendTextMessage(MESSAGE_STATUS_SMALL,"You can't use this item with a hotkey!")
                end
                return target:sendTextMessag(MESSAGE_STATUS_WARNING,"Becareful someone with " ..Sword.. " is watching you")
            end
              return player:sendTextMessage(MESSAGE_STATUS_SMALL,"You must have a clear path to your target")
        end
        return player:sendTextMessage(MESSAGE_STATUS_SMALL,"Only extra strong items can weild such power")
    end
end
```

