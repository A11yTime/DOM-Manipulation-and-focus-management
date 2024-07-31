# Terminology: 
* ref to access underlying DOM nodes and directly access the internal structure of a child component. No ref is duplicate for elements rendered at the same time.
* $nextTick() life cycle method to let the DOM sync up (v-if/else condition)
* mounted() life cycle method let the DOM elements be mounted ->> Modal Dialog in most cases.
* direct use of ref with focus() elements available in DOM
* attribute-selection

## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```

### Lints and fixes files
```
npm run lint
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).
