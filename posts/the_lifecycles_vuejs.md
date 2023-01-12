# Vue JS Lifecycles (for React JS developer)

When I started to develop with Vue js My first mistake was thinking that the life cycle was similar to React JS.

But no, each library or framework works a little bit different, but the result that they give us is similar.

Each Vue component or React Function component goes through a series of steps. For example when a component is instantiated, both libraries needs to set up data, mount the component into the DOM, and update the DOM when data changes.

Vue exposes different functions for each step, and in React you can access them through `useEffect` , giving users the opportunity to add their own code at specific phases.

_If you work with React Class component it is a little bit similar, but if you only work with React function component it is different how you can access to the multiple phases of the lifecicle. In this article I will talk about React function component._

In **React JS FC** you have 3 Phases:

- Initial Render or Mount
- Update (updating states or props)
- Unmount

```js
import React, { useEffect, useState } from 'react';

export const Counter = (props) => {
  const [count, setCount] = useState(0);

  const countHandler = () => {
    setCount((preValue) => preValue + 1);
  };

  useEffect(() => {
    const intervalId = setInterval(countHandler, props.delay ?? 1000);
    return () => clearInterval(intervalId);
  }, []);

  return <div className='counter'>{count}</div>;
};
```

Go to [demo](https://codesandbox.io/embed/optimistic-solomon-rr8ckk?fontsize=14&hidenavigation=1&theme=dark) 🚀

**Vue JS** exposes more phases. For each phase there is a different function that will trigger the given callback when needed. In this image you can see the full lifecycle:

![image](https://user-images.githubusercontent.com/38573357/198037458-8f5a26fe-ce1f-4822-a760-97c0e52958ed.png)

I got this image from [vuejs.org](https://vuejs.org/guide/essentials/lifecycle.html#lifecycle-diagram)

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

    const intervalId = setInterval(countHandler, props.delay ?? 1000);
    onBeforeUnmount(() => clearInterval(intervalId));

    return { count };
  },
};
</script>
```

Go to [demo](https://codesandbox.io/s/eager-cache-7w7si9?file=/src/components/counter.vue:0-426) 🚀

## How does it work?

### React JS:

In React each render and re-render of the component will call the function component, and each variable or hook that you have used inside of it. For example, `useEffect`. The clever part about React is that in some of the hooks you can pass an array of dependencies, and if these dependencies have not changed, it won't actually execute the callback.

```js
const IamABadComponent = ()=> {
// In each render or re-render these constabnts will be created and assigned the value.
 const defaultDelay = 1000 * 2;
 const fn = () => {};

 const unMount = () => {
  console.log("Bye")
 };

 //             👇🏻 The array of dependencies. An empty array means that the function will only be executed when the component is mounted.
 useEffect(fn, []);

 // In this case the function will be called when the component is mounted and when the `delay` prop has been changed.
 useEffect((fn, [props.delay]);

 // If you want to execute some cleanup logic before the component is unmounted you can return a callback from `useEffect`.
 useEffect((()=> { return unMount }, []);

return <div>Test</div>
}
```

<!--
PENDING TO REVIEW:
After here I would try to rethink it with some storytelling. Maybe expose a medium-complex problem and solve it both with React & Vue comparing its solutions?
-->

### Vue js

Vue JS exposes different hooks to access the multiple phases of each component lifecycle.

#### onMounted

Registers a callback to be called after the component has been mounted.

A component is considered **mounted** after all of its synchronous child components have been mounted (does not include async components or components inside <Suspense> trees).

```js
<template>
  <div class="counter">{{ count }}</div>
</template>

<script>
import { ref, onMounted } from "vue";

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

    onMounted(() => {
      setInterval(countHandler, props.delay ?? 1000);
    });

    return { count };
  },
};
</script>
```

Go to [demo](https://codesandbox.io/s/eager-cache-7w7si9?file=/src/components/counter.vue)

#### onBeforeMount

Registers a hook to be called right before the component is to be mounted.

When this hook is called, the component has finished setting up its reactive state, but no DOM nodes have been created yet.

#### onUnmounted

Registers a callback to be called after the component has been unmounted.

A component is considered **unmounted** after:

- All of its child components have been unmounted.
- All of its associated reactive effects (render effect and computed / watchers created during setup()) have been stopped.

```js
<template>
  <div class="counter">{{ count }}</div>
</template>

<script>
import { ref, onMounted, onUnmounted } from "vue";

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

    onUnmounted(()=> {
      clearInterval(countHandler)
    });

    return { count };
  },
};
</script>
```

Go to [demo](https://codesandbox.io/s/eager-cache-7w7si9?file=/src/components/counter.vue)

#### onBeforeUnmount

Registers a hook to be called right before a component instance is to be unmounted.

When this hook is called, the component instance is still fully functional.

#### onUpdated

This hook is called after any DOM update of the component, which can be caused by different state changes.

_⚠️ Do not mutate component state in the updated hook - you can create an infinite update loop!_

#### onBeforeUpdate

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

The hook can return false to stop the error from propagating further.

```js
<template>
  <slot v-if="!hasError" />
  <div v-else>
    <h2>🚨 something was wrong</h2>
    <p>{{ errorMessage }}</p>
  </div>
</template>
<script>
import { reactive, onErrorCaptured } from "vue";

export default {
  name: "error-boundary",
  setup: function () {
    const state = reactive({
      hasError: false,
      errorMessage: "",
    });

    onErrorCaptured((err) => {
      state.hasError = true;
      state.errorMessage = err;
      return false;
    });

    return state;
  },
};
</script>
```

Go to [demo](https://codesandbox.io/s/eager-cache-7w7si9?file=/src/components/error-boundary.vue)

## Conclusion

It's important to understand how the life cycle and the component works and how you can use it. You can improve the performance of your component by avoiding unnecessary renders and create more robust components.

If you want to know more about life-cycle you can go to the official documentation of:

- [Vue JS](https://vuejs.org/api/composition-api-lifecycle.html)
- [React JS](https://reactjs.org/docs/state-and-lifecycle.html)
