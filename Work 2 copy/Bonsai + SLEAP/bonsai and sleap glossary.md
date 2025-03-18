- indirect sort 
	- sorting the objects without moving them in the memory
		- 1) create an array of pointers to objects 
		- 2) sort the pointers based on the object keys 
		- 3) rearrange the objects in place based on the pointers
*^^ i dont know what this means*

- concatenate
	- link things together in a chain or series
	- *likely has a specific meaning in code - look that up specifically if the term comes up again*

- c type index order
	- the most rapidly changing index is the last value
	- for optimum cache performance
- fortran index order
	- indexed with the most rapidly changing value first 
	- memory skips around the array, lowering cache performance
*^^ i dont know what this means*

- array
	- a data structure containing values or variables that are identified by an array index or key
	- *ie its a list or table or data with all values tagged with a coordinate to identify where in the array the value is located*
	- arrays can have multiple axes, and each axis is a dimension
- index (plural: indices)
	- used to label, identify and reference values in an array
	- the count for an index starts at 0, the first position is the 0 position
- boolean
	- a type of data or operation that can have only one of two values, true or false
- tuple
	- a finite ordered list of elements
	- *usually the contents are unable to be changed - check and see if this is truw in bonsai*

- compiled programming language 
	- the target machine translates the program directly
	- tend to be faster and more efficient than interpreted languages
	- if any changes are made the code needs to be 'rebuilt' and then sent to the machine again
- interpreted programming language
	- the machine does not translate the program directly, instead relying on a interpreting program to read and execute the code
	- slower than compiled languages, but tend to be more flexible
	- interpreting programs run the code line by line and execute each command in order
	- if any changes are made, the code adapts in real time (does not need to be rebuilt)

- arduino
	- a microcontroller implemented in the metheus rigs

- observable sequence
	- the modules of a bonsai code - the ability to see what is triggered when by following the line

- recursive
	- a program that calls itself 
		- a base case is provided and then in the program the function itself is called WITH a modified argument
		- the function should get closer and closer to the base case as it runs, or else it might go into infinite recursion (never finish)
	- function that solves problems by solving smaller instances of the same problem 
		- ie it breaks something down and digests it that way


transpose - vector - scalar - tuple
- find where these were used and in what context to pull the correct definition

### Bonsai Specific Terms

under 'Source' in bonsai toolbox
- DSP
	- *digital signal processing*
- OSC
	- TCP
	- UDP
- IO

no method overload