# 2020121Full-Stack-Vuejs2-R03

## 记忆时间

## 0801. Managing Your Application State with Vuex

In the last chapter, you learned how Vue Router can be used to add virtual pages to a Vue.js single-page app. We will now add components to Vuebnb that share data across pages and therefore can't rely on transient local state. To do this, we will utilize Vuex, a Flux-inspired library for Vue.js that offers a robust means of managing global application state.

Topics covered in this chapter: 1) An introduction to the Flux application architecture and why it is useful for building user interfaces. 2) An overview of Vuex and its key features, including state and mutations. 3) How to install Vuex and set up a global store that can be accessed by Vue.js components. 4) How Vuex allows for superior debugging with Vue Devtools via mutation logging and time-travel debugging. 5) The creation of a save feature for Vuebnb listings and a saved listings page. 6) Moving page state into Vuex to minimize unnecessary data retrieval from the server.

### Summary

In this chapter, we learned about Vuex, Vue's official state management library, which is based on the Flux architecture. We installed Vuex in Vuebnb and set up a store where global state could be written and retrieved. We then learned the main features of Vuex including state, mutator methods and getters, and how we can debug Vuex using Vue Devtools. We used this knowledge to implement a listing save component, which we then added to our main pages. Lastly, we married Vuex and Vue Router to allow page state to be more efficiently stored and retrieved when the route changes.

In the next chapter, we'll cover one of the trickiest topics of full-stack apps - authentication. We'll add a user profile to Vuebnb so a user can persist their saved items to the database. We'll also continue to add to our knowledge of Vuex by utilizing some of its more advanced features.

### 8.1 Flux application architecture

Imagine you've developed a multi-user chat app. The interface has a user list, private chat windows, an inbox with chat history and a notification bar to inform users of unread messages.

Millions of users are chatting through your app on a daily basis. However, there are complaints about an annoying problem: the notification bar of the app will occasionally give false notifications; that is, a user will be notified of a new unread message, but when they check to see what it is, it's just a message they've already seen.

What I've described is a real scenario that Facebook developers had with their chat system a few years ago. The process of solving this inspired their developers to create an application architecture they named Flux. Flux forms the basis of Vuex, Redux and other similar libraries.

Facebook developers struggled with this zombie notification bug for some time. They eventually realized that its persistent nature was more than a simple bug; it pointed to an underlying flaw in the architecture of the app.

The flaw is most easily understood in the abstract: when you have multiple components in an application that share data, the complexity of their interconnections will increase to a point where the state of the data is no longer predictable or understandable. When bugs like the one described inevitably arise, the complexity of the app data makes them near impossible to resolve:

Figure 8.1. The complexity of communication between components increases with every extra component

Flux is not a library. You can't go to GitHub and download it. Flux is a set of guiding principles that describe a scalable frontend architecture that sufficiently mitigates this flaw. It is not just for a chat app, but for any complex UI with components which share state, like Vuebnb. Let's now explore the guiding principles of Flux.

#### Principle #1 – Single source of truth

Components may have local data that only they need to know about. For example, the position of the scroll bar in the user list component is probably of no interest to other components:

```js
Vue.component('user-list', { 
    data() { 
        scrollPos: ... 
    } 
});
```

But any data that is to be shared between components, for example application data, needs to be kept in a single place, separate from the components that use it. This location is referred to as the store. Components must read application data from this location and not keep their own copy to prevent conflict or disagreement:

1『 Single source of truth 指的就是中心数据文件。』

Figure 8.2. Centralized data simplifies application state

#### Principle #2 – Data is read-only

Components can freely read data from the store. But they cannot change data in the store, at least not directly. Instead, they must inform the store of their intent to change the data and the store will be responsible for making those changes via a set of defined functions called mutator methods.

Why this approach? If we centralize the data-altering logic then we don't have to look far if there are inconsistencies in the state. We're minimizing the possibility that some random component (possibly in a third party module) has changed the data in an unexpected fashion:

Figure 8.3. State is read-only. Mutator methods are used to write to the store

#### Principle #3 – Mutations are synchronous

It's much easier to debug state inconsistencies in an app that implements the above two principles in its architecture. You could log commits and observe how the state changes in response (which automatically happens with Vue Devtools, as we'll see).

But this ability would be undermined if our mutations were applied asynchronously. We'd know the order our commits came in, but we would not know the order in which our components committed them. Synchronous mutations ensure state is not dependent on the sequence and timing of unpredictable events.

