# Junior vs Senior React Folder Structure - How To Organize React Projects

- https://www.youtube.com/watch?v=UUga4-z7b6s

## Source

- https://github.com/WebDevSimplified/react-folder-structure

## 📂 Advanced React Folder Structure

    root
    ├── advanced
    ├──── public
    ├──── src
    ├────── assets         # images, css...
    ├────── components     # components with next
    ├────── context
    ├────── data           # constant data?
    ├────── features       # all of the code for a feature and putting it in one single place (ex) authentication - login, signup, user data...)
    ├──────── authentication
    ├────────── components
    ├────────── hooks
    ├────────── services
    ├────────── index.js   # only import index.js
    ├──────── projects
    ├────────── components
    ├────────── hooks
    ├────────── services
    ├────────── index.js   # only import index.js
    ├──────── settings
    ├────────── components
    ├────────── hooks
    ├────────── services
    ├────────── index.js   # only import index.js
    ├──────── todos
    ├────────── components
    ├────────── hooks
    ├────────── services
    ├────────── index.js   # only import index.js
    ├────── hooks          # shared hooks
    ├────── layouts        # shared layouts
    ├────── libs           # third-party libraries (ex) fetch, axios, sentry...) - facade pattern을 통한 구현
    ├────── pages
    ├────── services        # integrating with an api (ex) logging, analytics... )
    ├────── utils # very small and simple functions, generally pure function (ex) uri, browser)
    └── README.md
