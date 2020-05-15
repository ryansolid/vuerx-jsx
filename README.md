# Vuerx JSX

This library is a demonstration of how Vue's Reactivity system can be leveraged directly in JSX for considerably better performance than pairing it with a Virtual DOM library. Even the fastest Virtual DOM library will have overhead when reconciling many small discreet changes into a scheduled render and patch.

It accomplishes this with using [Babel Plugin JSX DOM Expressions](https://github.com/ryansolid/babel-plugin-jsx-dom-expressions). It compiles JSX to DOM statements and wraps expressions in functions that can be called by the library of choice. In this case `effect` wraps these expressions ensuring the view stays up to date. Unlike Virtual DOM only the changed nodes are affected and the whole tree is not re-rendered over and over.

To use call render:

```js
import { render } from 'vuerx-jsx';

render(App, document.getElementById('main'));
```

And include 'babel-plugin-jsx-dom-expressions' in your babelrc, webpack babel loader, or rollup babel plugin.

```js
"plugins": [["jsx-dom-expressions", {moduleName: 'vuerx-jsx'}]]
```

## Installation

```sh
> npm install vuerx-jsx babel-plugin-jsx-dom-expressions
```

## Example

[Vue Counter(Functions)]() Coming Soon

## API

VueRX JSX works both with function and class components(extend Component from this library). It also ships a specialize map function for optimal list rendering that takes an array as it's first argument.

```jsx
const list = ref(["Alpha", "Beta", "Gamma"]);

<ul>{
  map(() => ref.value, item => <li>{item}</li>)
}</ul>
```

VueRX JSX also supports a Context API.


Alternatively this library supports Tagged Template Literals or HyperScript for non-precompiled environments by installing the companion library and including variants:
```js
import { html } from 'vuerx-jsx/html'; // or
import { h } from 'vuerx-jsx/h';
```
There is a small performance overhead of using these runtimes but the performance is still very impressive. Tagged Template solution is much more performant that the HyperScript version, but HyperScript opens up compatibility with some companion tooling like:

* [HyperScript Helpers](https://github.com/ohanhi/hyperscript-helpers) Use an element as functions DSL
* [Babel Plugin HTM](https://github.com/developit/htm/tree/master/packages/babel-plugin-htm) Transpile Tagged Template Literals to HyperScript for IE11 compatibility

Further documentation available at: [Lit DOM Expressions](https://github.com/ryansolid/lit-dom-expressions) and [Hyper DOM Expressions](https://github.com/ryansolid/hyper-dom-expressions).
