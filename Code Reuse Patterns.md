
https://www.youtube.com/watch?v=0BNgi9vofaw&index=7&list=WL

Code Reuse Patterns 
* Simple composition
* High Order Composition
* Render callback

Rules of Thumb
* Render prop
	* Default
	  1. Dynamic
	  2. Easy to write and read
	  3. Isolation
	* Unless..
	  1. Need to communicate with the Inner Component

* HOC
	* Default
	  1. Static
	  2. Great for packaging
	  3. Access to props and lifecycle

* Render callback
	* Default
	  1. Dynamic
	  2. Can add info to it's children
	  3. No collisions
	* Unless..
	  1. Need to access inner props
	  2. Packaging in a new class

