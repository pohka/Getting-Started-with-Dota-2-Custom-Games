
# Getting Started with Dota 2 Custom Games
This is the ultimate starting guide to making Dota 2 custom games.

## Refrences
* API:
[Lua](https://developer.valvesoftware.com/wiki/Dota_2_Workshop_Tools/Scripting/API),
[JavaScript](https://developer.valvesoftware.com/wiki/Dota_2_Workshop_Tools/Panorama/Javascript/API),
[CSS](https://developer.valvesoftware.com/wiki/Dota_2_Workshop_Tools/Panorama/CSS_Properties)
* Internal names:
[All](https://developer.valvesoftware.com/wiki/Dota_2_Workshop_Tools/Scripting/Built-In_Ability_Names),
[Abilities](https://developer.valvesoftware.com/wiki/Dota_2_Workshop_Tools/Scripting/Built-In_Ability_Names), [Heroes](https://developer.valvesoftware.com/wiki/Dota_2_Workshop_Tools/Scripting/Heroes_internal_names),
[Items](https://developer.valvesoftware.com/wiki/Dota_2_Workshop_Tools/Scripting/Built-In_Item_Names),
[Modifiers](https://developer.valvesoftware.com/wiki/Dota_2_Workshop_Tools/Scripting/Built-In_Modifier_Names)
* Working Engine Events:
* Tutorials: [ModDota](https://moddota.com/forums/tutorial-index)


<br><hr>
## Setup
### Install tools

<br>
### Create a project

<br>
### IDE

<br>
### Wiki and references

<br>
### Layout
addon_game_mode.lua
* activate
* precache

<br><hr>
<p align="center" style="font-size:30px;">Lua Basics</p>
### Previous Experience (XP)
Anything with "XP:" is targeted at people who are familiar with other languages to highlight things which are different about Lua. To start there is no semi-colons to end a line, instead a new line is often used to signify a new line of code. Also Lua is a dynamically typed language which means that variables are not fixed to a specific type. One top of all of this Lua uses the "end" keyword to end a code block rather than the typical curly brackets "{}". Lua also has garbage collection, so there is no need to worry about releasing variables form memory.

<br>
### Hello World
This will print a message into the console
```lua
print("Hello World")
```
<br>
### Variables
Variables are defined with the "local" keyword. They allow you to store a value such as a number, string, boolean, etc.
```lua
local x = 10
local name = "john doe"
local isAlive = false
```
<br>
Number operators:  
* \+ addition
* \- minus
* \* multiply
* / divide
* ^ power
* % modulus

XP: i++ and i-- operators don't exist for numbers in Lua
```lua
--adding 1 to x
local x = 10
print(x + 1) --result: 11
print(x * 2) --result: 20
print(x / 2) --result: 5
```
<br>
String concatenation uses the .. operator

XP: Lua doesn't use + to concatenate strings
```lua
local phrase = "My name is "
local name = "John Doe"
print(phase .. name) --result: My name is John Doe
```

One of the most useful variable type is the table. Multiple values together and access them with a key.
```lua
local info = {
  [name] = "John",
  [age] = 18
}
print(info.name .. ": " .. tostring(info.age)) --result: John: 18

--this syntax is also valid
print(info["name"] .. ": " .. tostring(info["age"])) --result: John: 18
```
<br>
XP: Arrays don't exist in Lua, instead you have indexed arrays. By default Lua starts counting from one and not zero.
```lua
local materials = {
  "concrete",
  "wood",
  "metal"
}
print(materials[1]) --result: concrete
```

Global variables can be access from everywhere
```lua
local _G.foo = 10
```
<br>
### Comments
Comments won't be executed and can explain what a block of code does in English. This will allow you and others to understand your better. Everything after "--" will be commented out, but only on that line. You can comment out a block of code using "--[[ ]]"
```lua
local x = 10 --this is a number
local y = "10" --this is a string
local isAlive = false --this is a boolean

--x=11 (this doesn't execute)

--[[
Everything in here is a commented out
x=11 (this doesn't execute)

I don't execute either
]]
```
<br>
### Conditional Statements
Conditional statements can decide which code you want to execute using the "if", "elseif", "else", "then" and "end" key words. The "then" keyword will signify the end of a comparison statement. "end" will be the end of the conditional block.
```lua
local c = 100
if c > 100 then
  print("greater than") --this is not executed
end

if c > 100 then
  print("over 100")
elseif c < 50 then
  print("less than 50")
else
  print("reached me")
end

--result: reached me
```
<br>
Check if a value is defined:
```lua
local x
if x == nil then
  print("here")
end
--result: here
```

<br>
Comparison symbols:
* == equality
* < less than
* \> greater than
* <= less than or equal to
* \>= greater than or equal to
* ~= inequality

You can also invert the value of a condition using the keyword "not"
```lua
let x = 10
if not x == 10 then
  print("here")
end
--result:
```

Combining statements using "or" and "and"
```lua
local x = 10
if x == 10 and x < 0 then
  print("both statements are true")
elseif x == 100 or x < 0 then
  print("at least one statement is true")
end
--result: at least one statement is true
```
<br>



### Loops
A loop will repeats until a specified condition is reached. A basic for loop will increment the variable i on each iteration of the loop until it reaches the size of the colors table. Here is examples of each type of loop

* for loop
  ```lua
  --prints all the colors
  local colors = { "red", "green", "blue" }
  local size = table.getn(colors)

  for i=1, size do
    print(colors[i])
  end
  ```
* while loop
  ```lua
  local i = 4
  local count = 0

  while i > 2 do
    count = count + i
  end

  print("count is " .. count)
  --result: count is 7
  ```
* foreach loop
  ```lua
    local colors = { "red", "green", "blue" }
    for key,value in pairs(colors) do
      print(key .. ":" .. value)
    end

    --[[
      result:
      1:red
      2:green
      3:blue
    ]]

    --another example
    local users = {
      [usa] = 10,
      [china] = 12,
      [russia] = 9
    }

    for country,count in pairs(user) do
      print(country .. ":" .. count)
    end
    --[[
      result:
      usa:10
      china:12
      russia:9
    ]]
  ```
* break
  ```
    --breaks allow you to end a loop early
    local colors = { "red", "green", "blue" }
    local size = table.getn(colors)

    for i=1, size do
      if color[i] == "green" then
        break --loop ends here
      end
      print(colors[i])
    end

    --result: red
  ```
  
<br>
### Scope


<br>
### Table Manipulation
* insert
* remove
* sort
* nested tables

<br>
### Functions



<br>
### Math
The math class has a number of functions for dealing with numbers. You may not need them but here is some of the more useful one functions:
* abs
* ceil
* deg
* exp
* floor
* pi
* rad
* random
* sqrt
* tointeger
* type

<br><hr>
<p align="center" style="font-size:30px;">Dota 2 Custom Games</p>
This part is more specific to writing Lua code for custom games in Dota 2.


<br>
### Classes
* require

<br>
### Thinker Functions

<br>
### Game State

<br>
### KV Files

<br>
## Lua Abilities

<br>
### Event Listeners:
* OnSpellStart()
  * When cast time ends, resources have been spent


* OnAbilityPhaseStart()
  * When cast time begins, resources have not been spent. Return true for successful cast, or false for unsuccessful.


* OnAbilityPhaseInterrupted()
  * When cast time is cancelled for any reason.


* OnProjectileThink( vLocation )
  * Thinker function for projectile(s) created by this ability
  * vLocation is the current projectile location.


* OnProjectileHit( hTarget, vLocation )
  * A projectile has travelled its max distance or collided with a unit
  * if hTarget is nil, it means the projectile has expired.
  * If the projectile has reached its end, it will expire even if false is passed
  * return true to destroy the particle, return false to continue the projectile ( this applies for linear projectiles that can hit multiple NPCs, like Dragon Slave.


* GetIntrinsicModifierName()
  * Return "modifier_name" of the modifier that is passively added by this ability.


* OnChannelFinish( bInterrupted )
  * When channel finishes
  * bInterrupted parameter notifies if the channel finished or not.


* OnUpgrade()
  * When the ability is leveled up.

<br>
### Casting Behavior:
* GetBehavior()
  * Determines the type of targeting behavior used with the cursor, return expects value from DOTA_ABILITY_BEHAVIOR enum ( i.e. DOTA_ABILITY_BEHAVIOR_UNIT_TARGET, DOTA_ABILITY_BEHAVIOR_POINT )


* GetCooldown( nLevel )
  * Determines the cooldown started when the spell is cast. Return float value.


* GetCastRange( vLocation, hTarget )
  * Determines the cast range. Return integer value.


* GetChannelTime()
  * Determines the channel time. Return float value.

<br>
### Special Values


<br>
### Properties

<br>
### Thinker

<br>
## Lua Modifiers

<br>
### Linking

<br>
### Event Listeners
* OnCreated( kv )
  * Called when the modifier is created, with a table of values in "kv". Client/Server. No return type.
* OnRefresh( kv )
  * Called when the modifier is refreshed (created when already existing ). Client/Server, No return type.

  <br>
### States
* IsHidden()
  * Return true if this modifier should not appear on the buff bar. Client/Server, boolean return type.
* IsDebuff()
  * Return true if this modifier should appear as a debuff on the buff bar. Client/Server, boolean return type.
* IsPurgable()
  * Return true if this modifier can be purged. Client/Server, boolean return type.
* GetEffectName()
  * Return the name of the particle effect that is applied on the parent when this buff is active. Client/Server, string return type.

  <br>
### Modifier Functions
```lua
function modifier_sven_warcry_lua:DeclareFunctions()
	local funcs = {
		MODIFIER_PROPERTY_MOVESPEED_BONUS_PERCENTAGE,
		MODIFIER_PROPERTY_PHYSICAL_ARMOR_BONUS,
		MODIFIER_PROPERTY_TRANSLATE_ACTIVITY_MODIFIERS,
	}

	return funcs
end
```
[Modifier functions API](https://developer.valvesoftware.com/wiki/Dota_2_Workshop_Tools/Scripting/API#modifierfunction)


### Thinkers

<br>
### Modifier State


[wiki reference](https://developer.valvesoftware.com/wiki/Dota_2_Workshop_Tools/Lua_Abilities_and_Modifiers)

<br>
## Custom Nettables

<br>
## Panorama
* layouts
* lists
* css
