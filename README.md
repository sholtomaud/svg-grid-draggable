# svg-grid-draggable

Make an svg element draggable inside the confines of a fixed grid.

## Usage

![screenshot](screenshot.png)

Using this library to move [svg-midi-notes](https://github.com/juliangruber/svg-midi-note) inside a [svg-midi-grid](https://github.com/juliangruber/svg-midi-grid):

```js
const html = require('bel')
const morph = require('nanomorph')
const Note = require('svg-midi-note')
const Grid = require('svg-midi-grid')
const Draggable = require('svg-grid-draggable')

const note = Note()
const draggable = Draggable()
const grid = new Grid()

const cellHeight = 10
const cellWidth = 20

const state = {
  x: 80,
  y: 100
}

const onstart = () => console.log('on start')
const onmove = () => console.log('on move')
const onend = ({ x, y }) => {
  state.x = x
  state.y = y
  console.log(`on end (${x}, ${y})`)
  update()
}

const render = () => html`
  <svg width=400 height=200>
    ${grid.render({ height: 201, width: 401, cellHeight, cellWidth })}
    ${draggable.render({
      x: state.x,
      y: state.y,
      cellHeight,
      cellWidth,
      onstart,
      onmove,
      onend,
      el: note.render({
        height: cellHeight,
        width: cellWidth,
        velocity: 1
      })
    })}
  </svg>
`

const update = () => {
  morph(el, render())
}

const el = render()
document.body.appendChild(el)
```

## Installation

```bash
$ npm install svg-grid-draggable
```

## API

### Draggable()
### draggable.render({ x, y, cellWidth, cellHeight, onstart, onmove, onend, el })

## License

MIT
