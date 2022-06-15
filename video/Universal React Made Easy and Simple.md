[Universal React Made Easy and Simple](https://www.youtube.com/watch?v=evaMpdSiZKk)

Emergent Convention
- pages/ top level components (entry points)
- lib/ data fetching and trasnformation helpers
- components/ standalone and "pure" components

Top level components define their data needs via an extra lifecycle hook 'getInitialProps'

<Link> allows for page transitions with out losing client state.

Example: authentication. Load user once, maintain global state, don't refetch, sync upon change

With prefetching + SSR, we get the UX of a SPA with the initial perf of a 1990s website

By default each entry point maps to a route. e.g.: '/a' renders './pages/a'

However, the server can match any incoming URL to any entrypoint.

Design Constraint: the client shouldn't need to load the entire route map ahead of time

<Link href="" as=""> Router.push(href, as)
<Link href="" as="" replace> Router.replace(href, as)
<Link href="" prefetch> Router.prefetch(href)

e.g.: Instagram '/explore' page

5. HMR Subscriptions

Next.js now automatically subscribes to hot-reloading only the entry points open during dev

This improved iteration performance by 10x-15x for our codebase.

6. Immutable build artifacts

if the script fails to load due to a build mismatch, a full page transition is performed


it's possible to maintain a global client store.
The server can 'await' its population

Meet <style jsx>

Ahead-of-time Style Isolation via a babel transformation

Offered as a default, but not prescriptive.
Attempts to solve the "global CSS injection" problem

Out of the box, <style jsx> dedupes (only one underlying element), detaches & server-renders

You can arbitrary and seamlessly extend babel settings


9. Server extension
like express

This API allows you to cache easily at the top level

Ongoing Work and Future Directions

import() support

Almost done, but we have to iron out some failure scenarios

If we import('./dynamic-component') but we deployed a new version of the codebase..

Solution: always server builds with a caching CDN that caches the immutable artifacts permanently

2. Light weight development

3. <link rel="preload"> generation

Off-thread Javascript prefetching and parsing
