# React Query: It’s Time to Break up with your "Global State”! –Tanner Linsley

- https://www.youtube.com/watch?v=seU46c6Jz7E

## Global State

- Avoid Props Drilling
- Accessed, Not Copied
- Shared Communication
- More Productivity
- Less Work

- useState/Reducer + Context
- Redux, Mobx, Unstated ...

## Global State Expectations

- App State
  - ex) toast, alert
- Server State
  - ex) workspaes, teams, users ...

## Async Data <> Client State

- Where they are stored
- Speed of access
- How they are accessed
- Who can make changes

## Client State, Server State

### Client State

- Non Persistent (비영구적인)
- Synchronous
- Client-Owned
- Reliably Up-To-Date

### Server State

- Remotely Persisted
- Asynchronous
- Shared Ownership
- Potentially Out-of-Date

## Server State Challenges

- Caching..
- Deduping Requests (중복 요청)
- Background Updates
- Outdated Requests
- Mutations
- Pagination / Incremental
- GC / Memory

##

- Complated
- Over Engineered
- Over Powered

## Practice

...
