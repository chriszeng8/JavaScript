1. understanding the how JS memory works
JS (four types of var)
*bool
*number
*string (16 string)
*objects  (key value map)

1. object graph

Root 
root reference to object var, then to scalar var

			root
			/  \
	  obj_var
		/
	scal_var


Object has two sizes.
* Shallow size (object itself)
* Retained size (object itself + object's descendents)

What is garbage?
* garbage: all variables which cannot be reached from the root node.

How does GC (garbage collection) occur?
* finding phase: find all garbage (nodes that cannot be reached from the root node)
* collection phase: memory is returned to the system

Every time create "new" object (every call to *new*)
* reserves memory for object from young memory pool

Object can be split into young objects and old objects.
The V8 (google's JS engine) internally decide on when to promote a object
from young to old pool.

Allocation are cheap/fast until the "young" memory pool runs out of memory, at which point,
the garbage collection is forced, rather than being done at a particular point.


Chrome DevTool Memory Profiling 101
* Use Memory timeline: to validate a suspicious action (e.g., App slows down over time)
 see if memory is growing over time

 * To dip a bit deeper, and figure out what happened to the heap.
