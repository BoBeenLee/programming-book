

[MobX State Tree - New generation of the state containers](https://www.youtube.com/watch?v=B0D6SW2W9n8&list=WL&index=48&t=0s)

- Tree-structure ( same as Redux )
- Initial state shape/type checking
- Immutable + Mutable
- Simple code structure
- A bit of magic

### Type Definition
Initial State ( Model Definition )
### Primitive Types 
- types.string
- types.number
- types.boolean
- types.Date

### Complex Types
- types.model
- types.array
- types.map

### Root of the Tree
```
.model({
  a :Astore,
  b :Bstore,
});
```

### Utility Types
- types.union
- types.enumeration
- types.optional
- types.maybe
- types.frozen
- etc...

### View (Computed Values)
```
.view(self => {
  get todos() { ... }, <--- Computed property
  findTodos(user) { ... }, <--- View function
});
```

### Data Mutation
```
.actions(self => ({
    setTitle(newTitle) {
      self.title = newTitle;
    }
}));
```

### Async Data Mutation
### Generators Support

### LifeCycle Hooks
- preProcessSnapshot
- afterCreate
- afterAttach
- beforeDetach
- beforeDestroy

#### afterAttach
```
.action(self => ({
  afterAttach() {
    self.fetchProjects();
  },
  fetchProjects() {
    self.githubProjects = [];
    self.state = "pending";
    fetchGithubProjectsSomehow().then(
      self.success,
      self.error
    )
  }
}));
```

### Utility Functions
- clone
- getParent
- getRoot
- getEnv
- getSnapshot
- applySnapshot

### getEnv
Dependency Injection
```
const store = Store.create({
  todos: [{title: "Grab Tea"}]
}, {
    logger: logger // inject logger to the tree
});

.actions(self => ({
  setTitle(newTitle) {
    // grab injected logger and log
    getEnv(self).logger.log('changed title to: ' + newTitle);
    self.title = newTitle;
  }
}));
```

### getSnapshot / applySnapshot

#### Data Serialization
- Store in local storage
- Send to the server
- Sync between clients

#### Data Deserialization
- Restore from local storage
- Instantiate state from server

### Connection with React
```
const mapping = ({ store }) => ({
  name: store.user.name,
  setName: store.user.setName
});

export default inject(mapping)(CenteredUserName);

```
### Compatible with Redux API

### A lot more:
- Action middlewares
- References and identifiers
- Patch Changes
- Time traveling
- etc...

But it's enough to start!
