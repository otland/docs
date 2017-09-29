# Talkactions

```lua
function onSay(player, words, param)
    if player:getAccountType() <= ACCOUNT_TYPE_GOD then
        return true
    end

    player:sendTextMessage(MESSAGE_EVENT_ADVANCE, "Hello World")

    return false
end
```



