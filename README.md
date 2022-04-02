# What is StatsManager?
StatsManager, put simply, is a system for storing a player's stats.
For basic usage, it doesn't need a longer explanation than that.

**StatsManager doubles as a data-saving solution method as well as maintaining stats for a player**

You can think of it a bit like LeaderStats, except made more user-friendly.
Take the module from [Roblox](https://www.roblox.com/library/8829267262/StatsManager)
Grab the module from [Github](https://github.com/GammaShock/StatsManager)

**But why use this module?**
Includes the functionality to:
- Decide which stats you want  to be saved
- Set whether one or multiple clients can see stats
- Set a template easily using `StatsManager:SetTemplate(table)`
- Simple to get player stats, just use `StatsManager:GetData(player)`
- Works with **ProfileService** and **DataStore2**
- Fire an event when stats are changed
- Easily modify data

As a bonus, other members of the API are optional and provide additional functionality, they don't need to be used!

My favourite part about the module is that how easy it is to read and modify stats. These examples are both valid code. Changing a value always will fire the update signal, and will save upon exiting.
```lua
print(stats.Cash)
```
```lua
stats.Cash = stats.Cash + 10
```
___


## - Server usage
#### StatsManager:SetWrapper(wrapper:String)
Wrapper is a string. Can either be set to "ProfileService" or "DataStore2". Defaults to ProfileService if it hasn't been set
```lua
StatsManager:SetWrapper(wrapper:string)
```
#### StatsManager:SetTemplate(Table)
Set default values, and save functionality for each individual stat
```lua
StatsManager:SetTemplate(template) --Template is a table
```
___
##  - Server & Client
#### StatsManager:GetData()
Get data for a specific player
```lua
local stats = StatsManager:GetData() --Leave nil for localplayer
local stats = StatsManager:GetData(player:Player, maximumWaitTime:number) 
```

### stats:GetUpdateSignal(statName:string)
Returns a RbxScriptSignal, fired when stat is changed
```lua
stats:GetUpdateSignal(statName:string):Connect(function(newValue)
	--Additional functionality here
end)
```
___

# What's actually happening
Under the hood, StatsManager currently uses **DataStore2** and **ProfileService**, however you can choose which wrapper you would like to use. Each wrapper has unique functionality that you can read up on. One main benefit of using ProfileService is that you will have session locking, which is why it is currently a more popular option.

___

# Template Settings
- **Visibility** - `"Public" / "Private" / "Server"`
-- Public - Every user can see your stats, as well as the server
-- Private - Only the LocalPlayer and the server can see the stats
-- Server - Only the server can see the stats 

- **DefaultValue** - `any`
	This can be any value, and it will be the default value of the stat
- **Save** - `true / false`
	Set's whether the stat will be saved, for next time the user log's in. This value *defaults to true*, so set it to false if you don't want to save a particular stat.

-  **ClientEditBehaviour** - `"Modify" / "None"`
	*Default's to none*, however if modify is set to "Modify", a list of allowed value must also be set for the ClientAllowedValues setting.

- **ClientPrivilegeCheck** - `function`
	If a function is defined, and the value returned from it is true, the client will be given permission to edit the specified stat.

- **ClientAllowedValues** - `Array`
	A list of values that the client is allowed to change the value of the stat to.
  
___
