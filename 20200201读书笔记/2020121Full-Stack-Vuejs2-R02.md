## 记忆时间

## 0601. Composing Widgets with Vue.js Components

Components are becoming an essential aspect of frontend development, and are a feature in most modern frontend frameworks, including Vue, React, Angular, Polymer, and so on. Components are even becoming native to the web through a new standard called Web Components.

In this chapter, we will use components to create an image carousel for Vuebnb, which allows users to peruse the different photos of a room listing. We'll also refactor Vuebnb to conform to a component-based architecture. Topics covered in this chapter: 1) What components are and how to create them with Vue.js. 2) Component communication through props and events. 3) Single-file components-one of Vue's most useful features. 4) Adding custom content to a component with slots. 5) The benefit of architecting apps entirely from components. 6) How render functions can be used to skip the template compiler. 7) Using the runtime-only build of Vue to lighten the bundle size.

### Summary

In this chapter, we saw how components are used to create reusable custom elements. We then registered our first Vue.js components, defining them with template strings. Next, we looked at component communication with props and custom events. We used this knowledge to build an image carousel within the listing page modal window.

In the second half of the chapter, we got an introduction to single-file components, which we used to refactor Vuebnb into a component-based architecture. We then learned how slots can help us make more versatile components by combining parent and child content. Finally, we saw how the runtime-only build can be used to give a Vue app a smaller size. In the next chapter, we will make Vuebnb a multi-page app by building a home page, and using Vue Router to allow navigation between pages without reloading.

### 01. Components

When we're constructing a template for a web app, we can use HTML elements such as div, table, and span. This variety of elements makes it easy to create whatever structures we need for organizing content on the page. What if we could create our own custom elements, through, for example, my-element? This would allow us to create reusable structures specifically designed for our app.

Components are a tool for creating custom elements in Vue.js. When we register a component, we define a template which renders as one or more standard HTML elements:

![](./res/2020007.png)

Figure 6.1. Components facilitate reusable markup and render as standard HTML

#### 1.1 Registration

There are many ways to register a component, but the easiest is to use the component API method. The first argument is the name you want to give the component, the second is the configuration object. The configuration object will often include a template property to declare the component's markup using a string:

```js
Vue.component('my-component', { 
    template: '<div>My component!</div>' 
}); 

new Vue({ 
    el: '#app' 
});
```

Once we've registered a component like this, we can use it within our project:

```html
<div id="app"> 
    <my-component></my-component> 
    <!-- Renders as <div>My component!</div> --> 
</div>
```

#### 1.2 Data

In addition to reusable markup, components allow us to reuse JavaScript functionality. The configuration object can not only include a template but can also include its own state, just like the Vue instance. In fact, each component can be thought of as a mini-instance of Vue with its own data, methods, lifecycle hooks, and so on. We treat component data slightly differently to the Vue instance though, as components are meant to be reusable. For example, we might create a bank of check-box components like this:

```js
<div id="app"> 
    <check-box></check-box> 
    <check-box></check-box> 
    <check-box></check-box> 
</div> 

<script> 
    Vue.component('check-box', { 
        template: '<div v-on:click="checked = !checked"></div>' 
        data: { 
            checked: false 
        } 
    }); 
</script>
```

As it is, if a user clicks a checkbox div, the checked state toggles from true to false for every checkbox simultaneously! This is not what we want, but it is what will happen, as all instances of the component refer to the same data object and therefore have the same state.

To give each instance its own unique state, the data property shouldn't be an object, but a factory function that returns an object. That way, every time the component is instantiated, it links to a fresh data object. Implementing this is as simple as:

```js
data() { 
    return { checked: false } 
}
```


