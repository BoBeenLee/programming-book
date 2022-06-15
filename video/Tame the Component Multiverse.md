
Tame the Component Multiverse: Michael Chans
- https://www.youtube.com/watch?v=Hpx3kOtPovk


UI Testing Continnum

(TS)	 (Jest)	
Static - Unit - Integration - Visual - End to End

The UI Multi-verse

The 10-ish Dimensions of Web UI

1-Ideal

2,3-Async(variations)

4-Viewport

5-Browser engine

6-User abilities

7-Device capabilities

8-Authorization and logic

9-Localization(LTR/RTL)

10-Organization

Table stakes
- 1 view
- x6 viewports
- x3 browser engines (was 4)
- x3 device capabilities
- x4 user abilities

Scale

- 2 Authorization - user types
(one logical variation)
- 2 UI frameworks

Style
(My case)
- 2 theme
- 2 contrast modes
- 10 applications

We survive by juest not thinking about it

The problem is test creation

Suitability

- intefaces -> static
- implmentation -> unit
- coordination -> integration(non-visual), visual
- flows -> end to end

Suitability by Role

- engineers -> static, unit, integration
- QA -> end to end
- Visual -> engineers 2, QA 8?

UI Testing Continuum
- imperative -> static, unit, integration (Jest)
- declarative -> visual
- imperative -> end to end (Cypress)

How do we produce tests in this visual integration gap?

Declarative UI Testing
- Storybook
- Chromatic and CI

Sticker sheet for components

CSS debugging
- Features that make CSS debugging a snap.
	- Verify responsive behaviour
	- Debug layouts
	- Check alignment

Accessiblitiy tests
- During dev: use A11y panel to audit components as you build them.
- PR check: import stories into Jest and run Axe on CI

Verify event handlers
- Use ArgTypes to create callbacks that appear in the actions panel.
- Verify whether the handler received the correct arguments in a glance.

Overview story
- Use Docs Page to explain what the component does and when to use it.

Controls
- Graphical UI to interact with a component args dynamically

Chromatic

Visual tests
- Chromatic checks each commit for visual changes.
- They work by taking screenshots of every story and comparing them previous baseline.

Interaction tests
- Simulates user behavior in browser
- Powered by Testing Library & Play functions
- No waiting and no flake
- Low maintenance

Automated checks

Testing has hitorically been really rough for us because it's been like 'picture in your mind's eye, a modal, and imagine clicking on a button that opens that model...'

By writing the story, you get the documentation for the component, tests, and a playground... all for free.

We are similarly cursed

Because we love the web

10-ish dimensions of UI complexity

Tests are the wall at your back