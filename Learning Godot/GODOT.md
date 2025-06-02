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
should avoid using comments to explain 

## Match 
depending on the value it executes the code
match x:
	1:
		print(hello)
		\_:
		print (\_ is a wildcard)

## Arrays 
arrays can store multiple items together
arrays can also contain elements of different data types
![[Pasted image 20250405232455.png]]
**Retrieving data from array**
	filledArray # get the entire array
	filledArray[0] get value at specific index 

**Push and Pop array method**
	Push adds element to either to the beginning or the end of an array
	Pop removes and returns an element from the beginning or the end of an array
	
	var arrays   = [1,2,3,4,5]
	
	arrays.pop_back() [1,2,3,4]
	arrays.pop_front() [2,3,4]
	arrays.push_back(5) [2,3,4,5]
	arrays.push_front(1) [1,2,3,4,5]

**Clearing an array**
	
	var arrays = [1,2,3,4,5]
	
	arrays = [] 
	arrays.resize(0)
	arrays.clear()

**Duplicating an array (deep copy)**
	
	var arrays = [1,2,3,4,5]
	var duplicatedArray = arrays.duplicate(true)
	to do a shallow copy set the true to false

**Deep copy vs shallow copy**
	Deep copy: all nested arrays and dictionaries are duplicated and will not be shared with the original array
			shallow copy: refences to the original nested arrays and dictionaries are kept, so that modifying a subarray or dictionary in the copy will also impact those refences in the source array

## Enums
enums are data types that contain a fix set of constants
good at assigning consecutive integers

**How to declare an enum**
	
	enum {left, right, front, back} # Globally named
	
	same as writing the following
	const left = 0
	const right = 1
	const front = 2
	const back = 3

**Declaring enums**
	
	enum {left, right, front = 10, back} # Globally named
	
	same as writing the following
	const left = 0
	const right = 1
	const front = 10
	const back = 11

	#not globally set
	enum MoveSet {letf, right, front, back}
	MoveSet.left #0

## Dictionaries
Dictionaries are associative container that contains values referenced by unique keys
also called a key-value store

**Dictionary format**
			key           value
var name = { literal value : value }

**Declaring Dictionaries**
	
	var emptyDictionary = {} # empty dic
	var dictionaryContainer = {"name" : "John"}
	var anotherContainer = {1 : "John"}
	var complexContainer = {1:[1,2,3]}
	#you can even add dictionaries into dictionaries

**Accessing Dictionary**
	
	dictionaryContainer["name"] #returns "John"
	anotherContainer[1] #returns "John"

**Add key/value to existing Dictionary**
	
	dictionaryContainer.newKey = 100
	dictionaryContainer["newKey"] = 100
	
	#you can add ints as a key
	dictionaryContainer[1] = 100

**Dictionary comparisons**
	
	dictionary1 == dictionary2
	#returns false, even if the keys/value pair are the same in both dictionaries
	
	#Use the Hash method
	dictionary1.hash() == dictionary2.hash()
	#this will return true if the hashes are the same, and false if they are different

**Clear dictionary**
	
	dictionary1.clear()

**Erase a specific key in dictionary**
	
	#removes specific key/value pair
	dictionary1.erase("key")

## Functions
are always part of a class
can return data

**Functions Format**
	
	func <name>(<parameter>):
		pass
	# pass keyword does nothing except prevents the compiler error from empty functions. Pass can also be used in loops to aboid the compiler errors as well

**Pass Keyword**
	
	func <name>(<param>)
		pass #does nothing
		var x = 100 #executes

**Creating a function with a specified return**
	
	func nameOfFunction() -> int:
		return 100
	#anything after the return keyword (return statement), will stop the function and retrun back that value when the function is called


## Classes
describes the contents of the objects that belong to it. 
classes describe an aggregate of data fields such as variables and defines the operations such as methods
think of a class as a blueprint for creating objects, with initial value states and implementation behavior

By default, all script files are unnamed classes
this means you can only reference them by using the file's path name: using absolute or relative path

**absolute path** : "C:\Data\FilePath"
**GDScripts:** "res://rootOfGDScriptProject.gd"
**Relative Path** (starts on folder of file): "./FilePath.gd"


**Register Scripts as Class**
if you want to give a name to a class use the class_name keyword followed by a unique name
this will register your class name as a new type in Godot's editor. You can also add an icon image by using a comma followed by the image location

You can use the new registered name in other scripts

	
	extends Player # you can inherit the class
	var a = Player.new() create an instanced object


use the class function to instance a class 
its built in to classes
	
	var a = ClassName.new()

**Extends keyword**
	
	# Inherists Node
	extends Node
	extends keyword is the life blood of a gdscript class. lets you use Godots global classes and use their methods

**Inheritance in Godot**
A class can inherit from the following:
Global Class
Another Class File
An inner class inside another class file
Multiple inheritance is not allowed

**Inned Classes**
a clas file can contain inner classes. Inner classes are defined using the class keyword. They can be instanced using the ClassName.new() function. 

class innerClass:
	keep it indented, acts like a class, can have member variables, functions

**Virtual Method**
Summary: A virtual method is a method that can be redifined in derived classes.

A virtual method has an implementation in a base class as well as the derived class. it is used when a method's basic functionality is the same but sometimes more functionality is needed in the derived class