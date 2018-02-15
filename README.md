
# Getting Started with Dota 2 Custom Games
This is the ultimate starting guide to making Dota 2 custom games.

## Useful links
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



## Setup


### Install tools
todo



### Create a project
todo



### IDE
todo



### Wiki and references
todo



### Layout
addon_game_mode.lua

* activate
* precache



# Lua Basics
## Previous Experience (XP)
Anything with "XP:" is targeted at people who are familiar with other languages to highlight things which are different about Lua. To start there is no semi-colons to end a line, instead a new line is often used to signify a new line of code. Also Lua is a dynamically typed language which means that variables are not fixed to a specific type. One top of all of this Lua uses the "end" keyword to end a code block rather than the typical curly brackets "{ }". Lua also has garbage collection, so there is no need to worry about releasing variables form memory.



## Hello World
This will print a message into the console
```lua
print("Hello World")
```



## Variables
Variables are defined with the "local" keyword. They allow you to store a value such as a number, string, boolean, etc.

More: [Wiki](https://www.lua.org/pil/2.html), [TutorialsPoint](https://www.tutorialspoint.com/lua/lua_variables.htm)

```lua
local x = 10
local name = "john doe"
local isAlive = false
```

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



## Comments
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



## Conditional Statements
Conditional statements can decide which code you want to execute using the "if", "elseif", "else", "then" and "end" key words. The "then" keyword will signify the end of a comparison statement. "end" will be the end of the conditional block.

More: [Wiki](https://www.lua.org/pil/4.3.1.html), [TutorialsPoint](https://www.tutorialspoint.com/lua/lua_decision_making.htm)
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

Check if a value is defined:
```lua
local x
if x == nil then
  print("here")
end
--result: here
```

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


## Loops
A loop will repeats until a specified condition is reached. A basic for loop will increment the variable i on each iteration of the loop until it reaches the size of the colors table. Here is examples of each type of loop.

More: [Wiki](https://www.lua.org/pil/4.3.4.html), [TutorialsPoint](https://www.tutorialspoint.com/lua/lua_loops.htm)

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
* iterator loop
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
  ```lua
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

  

## Scope
A variable can only be seen in the block it is created in. Once the block ends the variable is not accessable anymore and will return nil
  ```
local a = 10
if a < 100 then
  local b = 10
  a = a + b
end
print(a)
print(b)

--[[
  result:
  20
  nil
]]
```


More: [Wiki](http://lua-users.org/wiki/ScopeTutorial)



## Table Manipulation
The variables section I touched on  tables earlier, but this section is about manipulating a table

More: [Wiki](http://lua-users.org/wiki/TablesTutorial), [TutorialsPoint](https://www.tutorialspoint.com/lua/lua_tables.htm)
* insert
  ```lua
  local colors = { "red", "green", "blue" }

  --insert at the end of a table
  table.insert(colors, "orange")
  -- colors = { "red", "green", "blue", "orange" }

  --insert at index
  table.insert(colors, 2, "pink")
  -- colors = { "red", "pink",  "green", "blue", "orange" }
  ```
* remove
  ```
    local colors = { "red", "green", "blue" }
    table.remove(colors, 1)
    -- colors = { "green", "blue" }

  ```
* nested tables
  ```
    local teamColors = {
      [teamA] = { "red", "white" },
      [teamB] = { "blue", "black" }
    }

    for teamName,colors in pairs(teamColors) do
      local colors = teamColors[teamName]
      local result = teamName .. ": "
      for i=1, table.getn(colors) do
        result = result .. colors[i] .. ","
      end
      print(result)
    end
    --[[
      result:
      teamA: red,white,
      teamB: blue,black,
    ]]
  ```



## Functions
Functions allow you to reuse code and optionally return a value. You can think of it like a box, you put something in and the box returns you back a result.

More: [Wiki](https://www.lua.org/pil/5.html), [TutorialsPoint](https://www.tutorialspoint.com/lua/lua_functions.htm)

```
function calculateTax(price)
  return price * 0.21
end

local chair = 50;
print("tax on a chair is: " .. calculateTax(chair))
--result: tax on a chair is: 10.5

local items = {
  [burger] = 5,
  [chips] = 2
}
for i=1, table.getn(items) do
  print(calculateTax(items[i]))
end
--result:
1.05
0.42
```



## Math
The math class has a number of functions for dealing with numbers. You may not need them but here is some of the more useful one functions:

More: [Wiki](http://lua-users.org/wiki/MathLibraryTutorial)

* abs (absolute value)
  ```
  local x = -10
  print(math.abs(x)) --result: 10
  local a = 10
  print(math.abs(a)) --result: 10
  ```
* ceil (round up decimal value)
  ```
  local x = 1.2
  print(math.ceil(x)) --result: 2
  ```
* deg (Convert value from radians to degrees)
  ```
  print(math.deg(math.pi)) -- result: 180
  ```
* floor (round down decimal value)
  ```
  local x = 1.2
  print(math.floor(x)) --result: 1
  ```
* pi (constant value of pi)
  ```
  print(math.pi) --3.1415926535898
  3.1415926535898
  ```
* rad (Convert value from degrees to radians)
  ```
  print(math.rad(180)) --result: 3.1415926535898
  ```
* random (random number generation)
  ```
  --random value between 0 tand 1
  print(math.random()) --result: 0.0012512588885159

  --random integer value from 1 to 100 (both inclusive)
  print(math.random(100)) --result: 20

  --random integer value from 20 to 100 (both inclusive)
  print(math.random(20, 100)) --result: 54
  ```
* sqrt (Square root of a number)
  ```
  print(math.sqrt(100)) --result: 10
  ```

  

# Dota 2 Custom Games
This part is more specific to writing Lua code for custom games in Dota 2.



## Classes
* require



## Thinker Functions
todo



## Game State
todo



## KV Files
todo



## Lua Abilities
todo



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



### Casting Behavior:
* GetBehavior()
  * Determines the type of targeting behavior used with the cursor, return expects value from DOTA_ABILITY_BEHAVIOR enum ( i.e. DOTA_ABILITY_BEHAVIOR_UNIT_TARGET, DOTA_ABILITY_BEHAVIOR_POINT )


* GetCooldown( nLevel )
  * Determines the cooldown started when the spell is cast. Return float value.


* GetCastRange( vLocation, hTarget )
  * Determines the cast range. Return integer value.


* GetChannelTime()
  * Determines the channel time. Return float value.



### Special Values
todo



### Properties
todo



### Thinker
todo



## Lua Modifiers
todo



### Linking
todo



### Event Listeners
* OnCreated( kv )
  * Called when the modifier is created, with a table of values in "kv". Client/Server. No return type.
* OnRefresh( kv )
  * Called when the modifier is refreshed (created when already existing ). Client/Server, No return type.



### States
* IsHidden()
  * Return true if this modifier should not appear on the buff bar. Client/Server, boolean return type.
* IsDebuff()
  * Return true if this modifier should appear as a debuff on the buff bar. Client/Server, boolean return type.
* IsPurgable()
  * Return true if this modifier can be purged. Client/Server, boolean return type.
* GetEffectName()
  * Return the name of the particle effect that is applied on the parent when this buff is active. Client/Server, string return type.

  

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
todo



### Modifier State
todo

More: [Wiki](https://developer.valvesoftware.com/wiki/Dota_2_Workshop_Tools/Lua_Abilities_and_Modifiers)



## Custom Nettables
todo



## Panorama
* layouts
* lists
* css