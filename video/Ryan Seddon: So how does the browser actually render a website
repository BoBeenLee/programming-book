
[Ryan Seddon: So how does the browser actually render a website ](https://www.youtube.com/watch?v=SmE4OwHztCc&index=1&t=758s&list=WL)

What we'll cover
+ High level view
+ In-depth view
+ Performance insights

Bindings
Rendering: Parsing, layout, painting etc
Platform JavaScript VM

High level flow

Parse HTML
		   - Render Tree - Layout - Paint
Parse CSS

1. Parsing
+ HTML is forgiving by nature
+ Parsing isn't straigtforward
+ Can be halted
+ Will do speculative parsing
+ It's reentrant

Remeber xhtml strict

Javascript and HTML: Forgiveness by Default

Valid HTML5

Parsing flow

	<-(document.write())  Script Execution <-
Tokeniser									  	DOM
 	->        Tree Construction            -> 

Parse Tree
html
	-- head
	-- body
		-- p.wat
			-- #text
		-- div
			-- span
				-- #text

parse Tree to DOM Tree

<script>, <link> & <style>
Will halt the parser as a script can alter the document.
+ Network latency
+ link & style could halt JS execution

Speculative parsing
+ Will look ahead
+ External images, scripts, css

```
<script src='script.js'>
</script>

<img src="cat.gif" />
<link href="styles.css" />
```

Reentrant
+ Means the parsing process can be interrupted.

1. Performance insight
<script /> at the bottom
+ Parse uninterrupted
+ Faster to render
+ defer and async attributes
+ Trade off

Parsing a HTML document - Visualised

CSS Parsing
CSSOM
							Selectors ...
				CSSRule
CSSStyleSheet 				Declaration ..
				CSSRule
							Selectors ...


image source

2. Render / Frame tree

DOM + CSSOM
+ Combines thre two object models, style resolution
+ This is the actual representation of what will show on screen
+ Not a 1-to-1 mapping of your HTML


Parse HTML
	JS	   - Render Tree - Layout - Paint
Parse CSS

Multiple trees
+ RenderObjects
+ RenderStyles
+ RenderLayers
+ Line boxes

Not in the render tree
+ Non-visual elements head, script, title etc
+ Nodes hidden via display: none;

In the render tree, not in the DOM

<p>The quick brown<strong>fox</string>

RenderBlock(p)
	RenderText('The quick brown')
	RenderInline(strong)
		RenderText('fox')

RenderBlock(p)
	RootLineBox(line1)
		InlineBox(text)
		InlineBox(strong)
			InlineBox(text)

DOM Node to RenderObject
+ Visual output
+ Geometric info
+ can layout and paint
+ Holds style & computed metrics

Calculating visual properties
+ Combines all styles
+ defaults, external, style elements & inline
+ Complexity around matching rules for each element
+ Style computation

3. Layout
Recursive process
+ Traverse render tree
+ Nodes position and size
+ Layout its children

Will batch layouts
+ Incremental layouts
+ The browser will intelligently batch changes
+ Render tree items will flag themselves as dirty
+ The batch will traverse the tree and find all dirty trees
+ Asynchronous

Immediate layout
+ Doing a font-size change will relayout the entire document
+ Same with browser resize
+ Accessing certain properties via Javascript 
e.g. node.offsetHeight

Performance insight 2

Take note from the browser and batch
+ Act like browser and batch your DOM changes.
+ Do all your reads in one pass
+ Followed by writes

Bad example
Here we read then write, read then write.

var divHeight = div.clientWith / 1.7;
div.style.height = divHeight + 'px';

var div2Height = div2.clientWidth / 1.7;
div2.style.height = div2Height + 'px';

Good

var divHeight = div.clientWith / 1.7;
var div2Height = div2.clientWidth / 1.7;

div.style.height = divHeight + 'px';
div2.style.height = div2Height + 'px';

Real world
+ FastDom, Preventing layout thrashing
+ Most modern JS frameworks do this internally

4. paint
Paint setup
+ Will take the layed out render trees
+ Creates layers
+ Incremental process
+ Builds up over 12step phases.

RenderLayers
+ Creates layers from RenderObjects
+ Position nodes, transparency, overflow, canvas, video etc
+ Many-to-1 relationship a RenderLayer could contain multiple RenderObjects

Painting
+ Produces a bitmap from each layer
+ Bitmap is uploaded to the GPU as a texture
+ Composites the textures into a final image to render to the screen

Performance insight 3

inline critical CSS
+ The most important bits of your site/app
+ Speeds up first paint times
+ Externaljs and css can block
+ Delta last bitmap

All of these steps can apply after page load

Recap
+ parseing --> DOM Tree
+ DOM Tree --> Render Tree
+ Is actually 4trees
+ Layout computes where a Node will be on the screen
+ Painting computes bitmaps and composites to screen.
