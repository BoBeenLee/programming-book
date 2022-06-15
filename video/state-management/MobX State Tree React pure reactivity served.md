## MobX
A reactive state management system.<br/><br/>
Anything that can be derived from the application state, should be derived.
Automatically.

### MobX in a nutshell
+ Observables used for defining the application state and Observers react to any change.
+ Reactions are used for handling side effects inside a Mobx application.
+ Computed Values are pure functions used for deriving complex values from the application state.
+ Actions are methods used for changing the application state called by views

### MobX in action
```
   -> Action -> App State -> 
UI 							Computed Value and Reactions
   <------------------------
```

### MobX State Tree
Opinionated transactional MobX powered state container <br/>
An opinionated state management system <br/>

+ Write imperative code hiding a reactive implementation
+ Immutable/Mutable tree with snapshots
+ Type system checked at runtime
+ Any Store lifecycle hooks

### Tree in depth
+ A node can exist only once in a Tree
+ Any node in a Tree is a Tree itself
+ All leaves in the Tree must be serializable
+ Every change to a model correspond to a snapshot and a patch

<img src="https://f001.backblazeb2.com/file/develop-pics/mobx-structure.png" />
