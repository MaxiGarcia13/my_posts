# The lifecycles of Vue JS.

## Introduction
When I started to develop with Vue js My first mistake was thinking that the life cycle was similar than React JS (I'd been programming with React JS for 4 years).

But no, each library or framework work a little bit different, but the result that they give us it is similar.

Each Vue component or React Function component goes through a series of steps. for example when it's created, it needs to set up data, mount the component into the DOM, and update the DOM when data changes.

it also runs functions called lifecycle hooks, giving users the opportunity to add their own code at specific steps.

_If you work with React Class component it is similar, but if you only work with React function component it is a little bit different how you can access to the diferent phases of the life-cicly. In this article i will talk about React function component._

In React JS in FC you have 3 Phases:
- Initial Render or Mount
- Update (updating states or props)
- Unmount

***Code example:***

```js
import React, { useEffect, useState } from "react";

export const Counter = (props) => {
  const [count, setCount] = useState(0);

  const countHandler = () => {
    setCount((preValue) => ++preValue);
  };

  useEffect(() => {
    setInterval(countHandler, props.delay ?? 1000);
    return clearInterval(countHandler);
  }, []);

  return <div className="counter">{count}</div>;
};
```

Go to [demo](https://codesandbox.io/embed/optimistic-solomon-rr8ckk?fontsize=14&hidenavigation=1&theme=dark) 🚀

In Vue js we have more phases (In this graphic we can see it better):

![image](https://user-images.githubusercontent.com/38573357/198037458-8f5a26fe-ce1f-4822-a760-97c0e52958ed.png)

I get this image from [vuejs.org](https://vuejs.org/guide/essentials/lifecycle.html#lifecycle-diagram)

***Code example:***
```js
<template>
  <div class="counter">{{ count }}</div>
</template>

<script>
import { ref, onBeforeUnmount } from "vue";

export default {
  name: "counter",
  props: {
    delay: Number,
  },
  setup(props) {
    const count = ref(0);

    const countHandler = () => {
      count.value += 1;
    };

    setInterval(countHandler, props.delay ?? 1000);
    onBeforeUnmount(countHandler);

    return { count };
  },
};
</script>
```
Go to [demo](https://codesandbox.io/s/eager-cache-7w7si9?file=/src/components/counter.vue:0-426) 🚀

## How they work it:

### React JS:
In React in each render and re-redender of the component react will call the function component and each variable or each hooks that you use it for example useEffect, it try to calculte again the function (first check what hooks need to update in your component and then).

```js
const IamABadComponent = ()=> {
// In each render or re-render this const it'll create and assign the value.
 const defaultDelay = 1000 * 2;

 const fn = () => {};

 const unMount = () => {
  console.log("Bye")
 };

 //             👇🏻 it is the array dependencies, in this case the function exect when the component mount.
 useEffect((fn, []);

 // this other case the function exect when the component mount and when the 'props.delay' change the value.
 useEffect((fn, [props.delay]);

// When you want to execute some logic before the component is unmount you can use a retun of the callback.
 useEffect((()=> { return unMount }, []);

return <div>Test</div>
}
```

### Vue js
Vue JS bring us some hooks for access in some phases of the life-cycle

#### onMounted
Registers a callback to be called after the component has been mounted.

A component is considered **mounted** after all of its synchronous child components have been mounted (does not include async components or components inside <Suspense> trees).

See the [demo](https://codesandbox.io/s/eager-cache-7w7si9?file=/src/components/counter.vue)

#### onBeforeMount
Registers a hook to be called right before the component is to be mounted.

When this hook is called, the component has finished setting up its reactive state, but no DOM nodes have been created yet. It is about to execute its DOM render effect for the first time.

#### onUnmounted
Registers a callback to be called after the component has been unmounted.

A component is considered **unmounted** after:
- All of its child components have been unmounted.
- All of its associated reactive effects (render effect and computed / watchers created during setup()) have been stopped.

See the [demo](https://codesandbox.io/s/eager-cache-7w7si9?file=/src/components/counter.vue)

#### onBeforeUnmount
Registers a hook to be called right before a component instance is to be unmounted.

When this hook is called, the component instance is still fully functional.

#### onUpdated
Registers a callback to be called after the component has updated its DOM tree due to a reactive state change.

This hook is called after any DOM update of the component, which can be caused by different state changes.

_⚠️ Do not mutate component state in the updated hook - this will likely lead to an infinite update loop!_

#### onBeforeUpdate
Registers a hook to be called right before the component is about to update its DOM tree due to a reactive state change.

This hook can be used to access the DOM state before Vue updates the DOM. It is also safe to modify component state inside this hook.

#### onErrorCaptured
Registers a hook to be called when an error propagating from a descendant component has been captured.

Errors can be captured from the following sources:
- Component renders
- Event handlers
- Lifecycle hooks
- setup() function
- Watchers
- Custom directive hooks
- Transition hooks

The hook can return false to stop the error from propagating further. See error propagation details below.

See the [Demo](https://codesandbox.io/s/eager-cache-7w7si9?file=/src/components/error-boundary.vue)


## Good practice

## Conclucion
