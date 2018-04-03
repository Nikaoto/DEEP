# deep
**deep** is a tiny library for queuing and executing actions in sequence. 

This functionality can be used in multiple ways, one of which is for [**LÖVE**](https://love2d.org),
where you can use the Z axis when drawing.

# Usage
Place `deep.lua` inside your project and require it:

```lua
deep = require "deep"
```

### Queue actions
```lua
deep.queue(3, print, "wound!")
deep.queue(1, print, "It's just")
deep.queue(2, print, "a flesh")
```

### Execute
```lua
deep.execute()
```
Prints:
```
It's just
a flesh
wound!
```

# Documentation

### `deep.queue(i, fun, ...)`
Queues a function for execution at index i.

```lua
deep.queue(100, print, "Hello")
-- can also be written as:
deep.queue(100, function() print("Hello") end)
```

Arguments:
* `i` `(number)` - The index of the action, must be positive.
* `fun` `(function)` - An anonymous or named function
* `...` `(*)` - The arguments of the passed named function


#### There are two ways to queue actions:
* Using anonymous functions
```lua
deep.queue(400, function() hit(iron, 100) end)
```

* Using named functions
```lua
deep.queue(400, hit, iron, 100)
```

Do **not** place a function call in the `fun` argument:
```lua
deep.queue(10, print("Hi")) -- Will call print("Hi") directly and pass the returned value (nil)
deep.execute() -- Does nothing, has nothing in queue
```

#### Queuing multiple actions
Simply use an anonymous function:
```lua
deep.queue(1, function()
	print("Hello")
	print("World!")
end)
```
---

### `deep:execute()`
Executes all of the queued actions.

```lua
-- Will execute the actions in random order
deep.queue(math.random(10), function() print("'Tis'") end)
deep.queue(math.random(10), function() print("but") end)
deep.queue(math.random(10), function() print("a") end)
deep.queue(math.random(10), function() print("scratch.") end)

deep.execute()
```

# Demos
The demo files have small examples of how deep's different functions should be used. I suggest 
you check out each one of them to learn about the various edge cases and details of deep.

Here's what demo1 does:
![demo](https://i.imgur.com/jRJXcZL.gif)