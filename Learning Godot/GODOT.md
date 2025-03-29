how to change your game resolution?
in Project -> Display -> window -> Viewport

## Signleton
Only one instance of the class
globally accessible

## PackedScene
is the file when we save a scene. The .tscn 

## Instantiate
we just clone the scene into the memory not into the scene it self
we have to either use add_child() which adds it as a child of the node which it calls
or we can use add_sibling which is get_parent().add_child()

## Remote
when testing our game "remote" and "local" will spawn
![[Pasted image 20250326171856.png]]
local is the game
remote is the live game

## Signals
we can create a signal using:
	signal name_of_our_signal
or if we need arguments
	signal name_of_our_signal(argument)
we can emit signals only in the script where we create them
	 name_of_our_signal.emit()
we can think of emit as a activate, it activates the signal
We need a reference where the signal is
Then we can connect a function to it
	 reference.name_of_our_signal.connect(name_of_our_function)

## Memory managment 
variables in godot have reference count
so if x=200 godot stores this value in memory (lets say 0x144, with 1 ref count)
then we create var y = x.  var y will point to the same memory block in our case 0x144 and the ref count will be 2
then if we say y = 1 it will allocate a new memory block lets say 0x145 with 1 ref count and x will still be at 0x144 with 1 ref count
when we do x = 0 godot will allocate a new memory block for it lets say 0x146 with 1 ref count 
and the memory block 0x144 will have 0 ref count and will be freed up.

NODES do not free up memory when deleted. 
you have to use queue_free() method to delete them and free up the memory.(queues our node for deletion at the end of our current frame)

## Naming conventions
Can use longer names
should avoid using comments to explain dfhdfg