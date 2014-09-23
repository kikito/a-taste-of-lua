---
author: Enrique García Cota
title: A Taste of Lua

---

# A taste of Lua

### Enrique García Cota (@otikik)

### [APIStrat](http://apistrategyconference.com/), 2014-09

---
# 3 main parts:

## Intro
## Feel
## Applications

---

# Part 1: Intro

---

# It's Lua, not LUA

---

![fullscreen](images/brazil.svg)

---

# SOL &rArr;
## Simple Object Language

---

![fullscreen](images/sol.png)

---

# Lua &rArr;
## “Moon” in Portuguese
## (No Initials)

---
= data-transition='fade'

![fullscreen](images/lua-logo.png)

---
= data-transition='fade'

![fullscreen](images/earth-moon.png)

---

![float-left](images/roberto.png)

## Roberto Ierusalimschy
> Lua is portable, powerful, embeddable & fast.

---

![float-left](images/roberto.png)

## Roberto Ierusalimschy
> Lua is portable, powerful, __embeddable__ & fast.

---

## General purpose language

<center>~ vs ~</center>

## Embedable language

---

FIXME: Picture of General Language

---

FIXME: Picture of System created with General Language

---

FIXME: Picture of System

---

FIXME: Picture of System with Embedded Language

---

FIXME: Picture of Robotic Arm

---

![fullscreen](images/videogames.jpg)

---

## Portable

---

## Portable

### &rArr; C99

---

## Small

---

## Small

```bash
git clone https://github.com/LuaDist/lua.git
cloc lua/src
```

### &rArr; ~ 15k (C99)

---

## Small

```bash
git clone https://github.com/LuaDist/lua.git
cloc lua/src
```

### &rArr; ~ 200KB compiled

---

## Implementations

---

## Lua (5.1, 5.2, 5.3)
## LuaJIT
## eLua
## ...

---
= data-transition='fade'

![fullscreen](images/lua-venn-1.svg)

---
= data-transition='fade'

![fullscreen](images/lua-venn-2.svg)

---

# Part 2: Feel

---

## Learn Lua in 15 minutes

http://tylerneylon.com/a/learn-lua/

---

```lua
local name   = 'Peter'
local age    = 35
local genter = "male"

print(name .. " is a " .. age .. ' years old ' .. gender)
```

```bash
local multilineString = [[
  Lorem ipsum
  dolor sit amet
]]
```

```lua
-- a single-line Lua comment
--[[
  a multi-line comment in Lua
]]
```

---

### Functions

```lua
-- Function declaration
local function sum(a,b)
  return a + b
end

print(sum(3,2)) -- 5
```

---

### Functions

```lua
-- Almost the same as before
local sum = function(a,b)
  return a + b
end

print(sum(3,2)) -- 5
```

---
### Conditionals

```lua
local function isEven(n)
  if n % 2 == 0 then
    return true
  end
  return false
end

print(isEven(5)) -- false
```
---
### Conditionals

```lua
local function isEven(n)
  return n % 2 == 0
end

print(isEven(5)) -- false
```
---
### Arrays & Numeric Loop

```lua
local a = {'a', 'b', 'c', 'd'}
print(a[1]) -- a

for i = 1, #a do
  print(a[i])
end
```

---
### While loop

```lua
local a = {'a', 'b', 'c', 'd'}
print(a[1]) -- a

local i = 1
while i < #a do
  print(a[i])
  i = i + 1
end
```

---

### Repeat until loop

```lua
local a = {'a', 'b', 'c', 'd'}
print(a[1]) -- a

local i = 1
repeat
  print(a[i])
  i = i + 1
until i > #a
```

---

### Hashes / Objects

```lua
local person = {name = 'peter', age = 21}

print(person['name']) -- peter
print(person.name) -- also peter

for k,v in pairs(person) do
  print(k .. ' => ' .. v)
end
--[[
  name => peter
  age => 21
]]
```

---

### Hash vs Array

```lua
local a      = {'a', 'b', 'c', 'd'}
local person = {name = 'peter', age = 21}

print(a[1])
print(person['name'])

print(type(a)) -- table
print(type(person)) -- table
```

---

## Reuse

---

## Lua tables:

* Arrays
* Hashes
* Structs
* Objects
* References
* Environments

---

## Lua functions:

* Values
* Blocks
* Scopes
* Iterators
* Generators

---

### Types (~7)

```bash
string, number, table, boolean, function, thread, nil
```

### Libraries (~7)

```lua
string, math, table, os, io, coroutine, debug
```

### Top-level functions (~30)

```lua
assert          load          pcall       setmetatable
collectgarbage  loadfile      print       tonumber
dofile          loadstring    rawequal    tostring
error           module        rawget      type
rawset          xpcall        getfenv     next
unpack          getmetatable  require     select
ipairs          pairs         setfenv
```

---

![float-left](images/rocks.png)
## Libraries
### luarocks.org
### rocks.moonscript.org
### ~700 rocks

---

## Lua feels like
### A faster, smaller, better javascript

```javascript

// Very little of this stuff:
[9,10,1,2].sort()
> [1,10,2,9]

```

---

# Part 3: Applications

---

![fullscreen](images/redis.png)

---

> Key-value data store

---

```ruby
require "redis"
redis = Redis.new('localhost', 6379)

redis.set("name", "peter")
name = redis.get("name") # "peter"

redis.set("age", "25")
new_age = redis.incr("age") # 26
```
---

> Concurrent, but single threaded

---

![fullscreen](images/bartender.jpg)

---

![fullscreen](images/bartender2.jpg)

---

```ruby

counter = redis.get('counter')



redis.incr('counter') if counter.is_a? numeric

```

---
```ruby

counter = redis.get('counter')

########## CONTEXT SWITCH  ##########

redis.incr('counter') if counter.is_a? numeric

```


---

```ruby

lua_code = <<-EOS
  local counter = redis.call("GET", KEYS[1])
  if type(tonumber(counter)) == "number" then
    return redis.call("INCR", KEYS[1])
  end
EOS

redis.eval(lua_code, ["counter"])

```

---

![centered](images/vim.png)

---

```bash
brew install vim --with-lua
```

-or-

```bash
brew install macvim --with-lua
```

---

![fullscreen](images/neocomplete.gif)

---

![fullscreen](images/unite.gif)

---
```bash
                    Startup     Speed

      Vim script    0           1.498s
      Python        0.0166s     0.027s (2000%)
      Lua(jit)      0.0002s     0.001s (1152000%)
```
---

![centered](images/neovim.png)

---
= data-text='centered'

## Corona SDK

![centered](images/corona-sdk.png)

---
= data-text='centered'

coronalabs.com/i-want-to-build/games/

![fullscreen](images/corona-games.png)

---

![centered](images/corona-platforms.png)

---
= data-text='centered'

coronalabs.com/i-want-to-build/business-apps/

![centered](images/corona-apps.png)

---
= data-text='centered'

### www.love2d.org

![centered](images/love2d.png)


---

![fullscreen](images/nginx.png)

---

![fullscreen](images/openresty.png)

---

![fullscreen](images/taobao.jpg)

---

![fullscreen](images/raspberry.png)

---
= data-text='centered'

### www.techempower.com/benchmarks

![centered](images/techempower-1.png)

---
= data-text='centered'

### www.techempower.com/benchmarks

![centered](images/techempower-2.png)


---

FIXME: Add code example for Openresty

---

FIXME: Add APItools Logo

---

FIXME: APItools schema

---

FIXME: APItools Screenshot

---
```lua
return function(req, next_middleware)
  req.headers['Authorization'] = 'My Secret'

  return next_middleware()
end
```
---

```lua
return function(req, next_middleware)
  local res  = next_middleware()

  res.status = 200
  res.body   = 'Hodor'

  return res
end
```


---

# Conclusion

---

![fullscreen](images/destroyer.jpg)

---

![fullscreen](images/soldier.png)

---

![fullscreen](images/macgyver.jpg)

---

# Questions?
### Enrique García Cota (@otikik)

---
= data-text='centered'
![centered](images/macgyver2.jpg)

# Thank you! <span class="applause">&#9734;</span>


