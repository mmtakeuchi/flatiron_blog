---
layout: post
title:      "A Basic Component"
date:       2020-10-23 18:07:07 +0000
permalink:  a_basic_component
---


Components are the building blocks of a React app. They are like Javascript class or function, that are independent and reusable within the app. They created together to setup your desired UI. Here how a function and class component will look like.

```
function Hello = (props) => {
  return <h1>Hello {props.name}!</h1>;
}

class Hello extends React.Component {
  render() {
    return <h1>Hello {this.props.name}!</h1>;
  }
}
```

Both of these will return the same string. However there is a slight difference as you can tell from writing each component, based on if it a function, like the top example, or a class. The second part of these are the use a "props (properties), " which are arguments that hold data, and return a React element. These props are being passed from a parent component, so they can be used in these components.  So for this instance, the parent component is passing down a name argument. To be able to use these components are render the string, we need to connect wrap them in another function. 

```
const hello = <Hello  name="Jim" />;
ReactDOM.render(
  hello,
  document.getElementById('root')
);
```

Taking the two previouse examples down with us, we have a hello variable set to a Hello component with the prop, {name: "Steve"}. Now moving onto rendering the component, we call ReactDOM.render(). And within this function React will call Hello component, which will return `<h1>Hello Jim!</h1>`.  React will then update the DOM to render the new component, and shoe Hello Jim! on the page. 

An important note about components in React, is that they need to be written in uppercase, because React will treat components written in lowercase, as DOM tags. So how we have `<div />` or `<img />` tags for HTML, a component will be written like, `<Hello />` or `<World />`.




