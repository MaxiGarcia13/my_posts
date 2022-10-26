# The lifecycles of Vue JS.

## Introduction
My first mistake when I started programming with Vue JS, it was thinking that the life cycle was similar than React JS (I'd been programming with React JS for 4 years).

But no, each library or framework work a little bit different, but the result that they give us it is similar.

They give us special methods that allow us how things work behind-the-scenes. These methods allow us to know when a component is created, added to the DOM, updated, or destroyed.

In React JS in Function Components you have 3 phases:
- Initial Render or Mount
- Update (updating states or props)
- Unmount

### Code example: 

<iframe src="https://codesandbox.io/embed/optimistic-solomon-rr8ckk?fontsize=14&hidenavigation=1&theme=dark"
     style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;"
     title="optimistic-solomon-rr8ckk"
     allow="accelerometer; ambient-light-sensor; camera; encrypted-media; geolocation; gyroscope; hid; microphone; midi; payment; usb; vr; xr-spatial-tracking"
     sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts">
</iframe>

In each render and re-redender when the state change it, the function return the JSX and React (React js and ReactDom) calculate what thing changes and after that modify the places that it need a change in the dom. when the component is unmouted it clear the setInterval.

## How is it in Vue js?
![image](https://user-images.githubusercontent.com/38573357/198037458-8f5a26fe-ce1f-4822-a760-97c0e52958ed.png)

I get this image from [vuejs.org](https://vuejs.org/guide/essentials/lifecycle.html#lifecycle-diagram)

## Hooks

## Conclucion
