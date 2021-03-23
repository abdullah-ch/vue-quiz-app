# quiz

1-> mounted : function() is called at the first render just like componentDidMount  
2-> data(){ return { stateObjects }  }  stores state of our component just like state in React's Class Based Component Components  
3-> watch : function() listens for the change in props of our components. (I really like this feature in Vue  
4-> watch: {object : {immediate : true}}, in this case watch will also listen when the props are first passed and will execute its business logic not only when the props change  
4(2)-> A Vue watcher allows you to listen to the component data and run whenever a particular property changes  
5-> computed: function() is the place where we do the computation on our state elements, props etc. A separate place computing is clean   


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
