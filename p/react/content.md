# React

*August 10, 2022*

Kappa Theta Pi Technical Development

with Neha Desaraju

---

## What is React?

* JS library for front-end web development
* Allows you to build apps with more complex data workflows and UX
* Introduces reusability which decreases development time and improves standardization

---

## How does it work?

* Components are capsules that contain some JS, HTML, and CSS and can be reused
* Able to generate "custom" HTML components <!-- .element: class="fragment" -->
* For example, instead of adding a nav bar div for each page, you create one and call it from each page <!-- .element: class="fragment" -->

--

![Components](https://replit.com/cdn-cgi/image/quality=80,metadata=copyright,format=auto/https://storage.googleapis.com/replit/images/1561252846504_5e3cc11a92f83c5fe98fe1b11797d4e1.png)

---

## Components

* Write in JSX, a flavor of JS that includes HTML
```jsx [|2]
let HelloComponent = (
    <div className="hello">
        <h1>Hello world!</h1>
        <AnotherComponent />
	</div>
);
```
* Since it's still JS, we can't use `class` (it's reserved) and have to use `className` instead

---

## Create a React app

* Use an online IDE to avoid setup, like Replit or Glitch, and use the provided template
* Or use `create-react-app` in your terminal (with npm and node installed)

--

### Main page

* *index.html* does not have much content, just a div
* *index.js* is where the app starts

```jsx [1-2|4,6]
import React from 'react';
import ReactDOM from `react-dom`;
import './index.css'; // global styles
import App from './App'; // where all other components start

ReactDOM.render(<App />, document.getElementById('root'));
```

--

### Inside App.js

```jsx [|1|5-6,14-15|8-12]
import React, { Component } from 'react';
import logo from './logo.svg'
import './App.css'

class App extends Component {
    render() {
        return (
            <div className='App'>
                <header className='App-header'>
                    ...
                </header>
            </div>
        )
    }
}
```

---

## Creating custom components

Inside the *components* folder, create **Heading.js**

```jsx [|13]
import React, { Component } from 'react';

class Heading extends Component {
    render() {
        return (
            <div className="my-heading">
                <h1>My heading</h1>
            </div>
        )
    }
}

export default Heading;
```

--

Then, inside **App.js** add

```jsx
...
import Heading from 'components/Heading'

class App extends Component {
    render() {
        return (
            <div className='App'>
                <Heading />
                <header className='App-header'>
                    ...
                </header>
            </div>
        )
    }
}
```

---

## Props

* Allow you to pass data from a parent to a child element ("properties")
* Useful for when you want to change data inside an element but keep overall element the same

```jsx [8]
...
import Heading from 'components/Heading'

class App extends Component {
    render() {
        return (
            <div className='App'>
                <Heading myPropName='someContent'}/>
                <header className='App-header'>
                    ...
                </header>
            </div>
        )
    }
}
```

--

Inside **Heading.js**, you can access the prop data like

```jsx [7]
import React, { Component } from 'react';

class Heading extends Component {
    render() {
        return (
            <div className="my-heading">
                <h1>{ this.props.myPropName }</h1>
            </div>
        )
    }
}

export default Heading;
```

---

This presentation was made with ❤️ and `revealjs` by Neha Desaraju.