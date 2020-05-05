---
layout: post
title:      "Diffrenece between render and component on React Router"
date:       2020-05-05 15:44:19 -0400
permalink:  diffrenece_between_render_and_component_prop_on_react_router
---


the doc say for component prop:
> When you use component (instead of render or children, below) the router uses React.createElement to create a new React element from the given component. That means if you provide an inline function to the componentprop, you would create a new component every render. This results in the existing component unmounting and the new component mounting instead of just updating the existing component. When using an inline function for inline rendering, use the render or the children prop (below).
> 

```
<Route path="/dashboard" component="{Dashboard}" />

```
What if you want to pass props to Dashboard?
Do not simply add a props to the route. ReactRouter does not pass these props to the component.

Alternatively, consider creating an inline function that returns a dashboard to the component as shown below.

```
<Route path="/dashboard" component={() => <Dashboard isAuthed="{true}" />} />
```

Although the above method works, it is not a good solution for performance. According to the doc:
> When you use the component props, the router uses React.createElement to create a new React element from the given component. That means if you provide an inline function to the component attribute,_ you would create a new component every render._ This results in the existing component unmounting and the new component mounting instead of just updating the existing component.
> 

It is not recommended to pass a function to a component because it does not recycle an existing component, but mounts a new component after unmounting each time the component is rendered.

The Reactor team provided a simple solution.
Instead of using components as props, use renders.
render allows functional components. And using render does not unnecessarily remount the component.

```
<Route path="/dashboard" render={props => <Dashboard {...props} isAuthed="{true}" />} />
```

In summary, if you want to pass props to a component that is rendered through a Reactor, instead of using Route's component props, you should use render props. When using render, the component is not unnecessarily remounted, but props passed to the component returned by the inline function are passed properly.
