
[Single Responsibility Components: Object-Oriented Design in React](https://www.youtube.com/watch?v=pSdp92Up8O8&index=1&list=WL&t=0s)

### React is functional
- UI is a function of application state.
- Idempotent render method.
- Optimisations like shouldComponentUpdate
- Uni-directional data flow (Flow/Redux)

### Components are Objects
- Encapsulate state
- Present a public API
- Represent objects in the "real world"
- Interact with/depend upon each other

The Single Responsibility Principle = Better Component Design
A Component should have one and only one reason to change.

### What will change?
- Cosmetic
Spacing, colours, animation, content, ...

SOLID CSS 아키텍쳐

- Functional
New features, reuse in a new place, ...

- Performance
UI stays the same but is served differently

- External
API endpoints, security updates, localisation, ...

### Refactor the code before making the change

### Isolate uncertainty

### SOLID
#### S Single Responsibility
One and only one reason to change

#### O Open-Closed
Open for extension, closed for modification

#### L LISKOV Substitution
Objects of the same type should ve interchangeable

#### I Interface Segregation
Fine-grained interfaces specific to a use-case

#### D Dependency inversion
Depend on abstractions, not concretions
