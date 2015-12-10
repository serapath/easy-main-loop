# easy-main-loop
re-render virtual dom every time update(state) is called

# usage
```js
var start = require('easy-main-loop')
var style = require('easy-jss')
var h     = require('virtual-dom/h')

function app (state, update) {
  var s = style('#style_css', state.theme)
  return h('div', { className: s('.test') }, [
    h('h1', 'clicked ' + state.n + ' times'),
    h('button', { className: s('.test2'), onclick: onclick }, 'click me!'),
    h('button', { className: s('.test2'), onclick: adaptTheme }, 'fontcolor')
  ])
  function adaptTheme () {
    console.log(s.css('.test2', 'background-color', '#ff0'))
  }
  function onclick () {
    state.n +=1
    state.theme.color1 = state.n%3 ? '#00f' : '#f00'
    update(state)
  }
}


var initialState = {
  n: 0,
  theme: {
    color1: '#f00',
    color2: '#0f0'
  }
}
var container = '#content'
start(app, initialState, container)
```
