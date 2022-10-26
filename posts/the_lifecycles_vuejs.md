# The lifecycles of Vue JS.

## Introduction
My first mistake when I started programming with Vue JS, it was thinking that the life cycle was similar than React JS (I'd been programming with React JS for 4 years).

But no, each library or framework work a little bit different, but the result that they give us it is similar.

Each Vue component or React Function component goes through a series of initialization steps. for example when it's created, it needs to set up data, mount the component into the DOM, and update the DOM when data changes. it also runs functions called lifecycle hooks, giving users the opportunity to add their own code at specific stages.

In React JS in Function Components you have 3 phases:
- Initial Render or Mount
- Update (updating states or props)
- Unmount

***Code example:***

```
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
```
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
In React in each render and re-redender of the component react'll call the function component and each variable or each hooks that you use it for example useEffect, they calculte again.

```
const IamABadComponent = ()=> {
// In each render or re-render this const it'll create and assign the value. 
 const defaultDelay = 1000; 
 
 const fn = () => {};
 
 //             👇🏻 array is the array dependencies, in this case the function exect when the component mount.
 useEffect((fn, []);
 
 // this other case the function exect when the component mount and when the 'props.delay' change the value.
 useEffect((fn, props.delay ?? defaultDelay); 
 
return <div>Test</div>
}
```

### Vue js
The setup function it'll calculate one time, and then each hooks 


## Vue Lifecycle Hooks

## Good practice

## Conclucion
