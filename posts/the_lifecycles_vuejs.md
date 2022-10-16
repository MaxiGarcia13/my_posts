# The lifecycles of Vue JS.

## Introduction
My first mistake when I started programming with Vue JS, it was thinking that the life cycle was similar than React JS (I'd been programming with React JS for 4 years).

But no, each library or framework work a little bit different, but the result that they give us it is similar.

They give us special methods that allow us how things work behind-the-scenes. These methods allow us to know when a component is created, added to the DOM, updated, or destroyed in the Vue instance.

### How does it work in React JS?
In React you have two ways to create a component, and the lifecycle work different.

**Class Component:**
You have 4 phases:
- Initialization: This is the stage where the component is constructed with the given Props and default state. This is done in the constructor of a Component Class.
- Mounting: is the stage of rendering the JSX returned by the render method itself.
- Updating: is the stage when the state of a component is updated and the application is repainted.
- Unmounting: is the final step of the component lifecycle where the component is removed from the page.

[Imagen]

**Function Component:**
You have 3 phases:
- Initial Render or Mount
- Update (updating states or props)
- Unmount

[Imagen]

In both cases they return a JSX and React and React DOM calculate what thing changes and they do the changes only in the places that need it.



### How does it work in Vue JS?


## Conclucion
