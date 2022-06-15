[Creating Interactive Frontend Apps With GopherJS And React](https://www.youtube.com/watch?v=IucPdpcyubg&feature=youtu.be)

Today we will
* Write a browser-based. interactive frontent app in Go
* Using myitcv.io/react. a wrapper around Facebook's React
* Learn to love go generate
* Enjoy the benefits of writing frontend apps in Go, thereby solving many the problems associated with using Javascript
* End up with teams of happy frontend Gophers

What do we mean by 'frontend'?
For the purposes of this talk:
* A browser/equivalent (e.g. Electron) on a client device
* Rendering of HTML and CSS
* Backend could be local/remote/non-existent

What do we mean by 'interactive'?
For the purposes of this talk:
* Intra-page-load responsiveness
* Visual changes, i.e. re-rendering in response to user interactions
* May or may not involve backend calls: could be entirely frontend logic

What do we mean by 'app'?
For the purposes of this talk:
* HTML page/pages that are interative
* Page -> a single page application - everything retrieved in a single page load
* Pages -> logic split across multiple pages (and hence page loads)

Why is any of this important?
* Browser is an extremely good cross platform way of building frontend apps
* Billions of devices
* Zero cost to adoption
* Low cost from a development perspective (or should be at least!)

How do we make HTML and CSS dynamic in this way?
DOM model represents a document with a logical tree.
Using Javascript we can then manipulate the DOM:
* add, change, and remove HTML elements and attributes
* change CSS styles
* react to existing events (e.g. mouse clicks, key press)
* create new events (e.g. timer events)

Javascript? Really?
"Javascript is ubiquitous on the web, and that's not going to change anytime soon, so there's no point in carrying the baggage necessary for multiple scripting engines that never materialized"
A Mozilla maintainer, 2012

Javascript: the reality
* Javascript 'won' the browser battle
* Easily picked up and learnt
* Standardized via ECMAScript
* asm.js WebAssembly (possibly) represent tomorrow's world

What's the option space for writing interactive frontend apps?
A very incomplete list:
* Javascript
* CoffeeScript (compiles to Javascript)
* Typescript (compiles to Javascript)
* ClojureScript (compiles to Javascript)
* Other languages that compile to Javascript/asm.js/WebAssembly
* ...

A brief (incomplete) analysis of Typescript
* Typed superset of Javascript that compiles to Javascript
* Large language; extensive specification, more edge cases, harder to write tools that work with language.
* Painful hangovers from Javascript
* Myriad compiler options to satisfy myriad backgrounds of newcomers
* Low development velocity
* No single-source-of-truth gofmt equivalent

Is there another way?
* We want to write interative frontend apps
* We ultimately have to use Javascript to do so.

What is GopherJS?
* A compiler from Go to Javascript
* Developed by Richard Musiol et al
* Principlally targets the browser

What does GopherJS support?
* Full language coverage, including goroutines
* Almost the entire standard library
* Performance is good in most cases
* Source map support (debugging)
* DOM package
* Javascript interoperability package

Where do we stand?
* Written an interactive frontend app in Go.
* Used myitcv.io/react and reactGen to declare components, props and state
* A new found love for go generate
* But no 'data' in our application...





