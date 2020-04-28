# 2020121Full-Stack-Vuejs2-R03

## 记忆时间

## 0801. Managing Your Application State with Vuex

In the last chapter, you learned how Vue Router can be used to add virtual pages to a Vue.js single-page app. We will now add components to Vuebnb that share data across pages and therefore can't rely on transient local state. To do this, we will utilize Vuex, a Flux-inspired library for Vue.js that offers a robust means of managing global application state.

Topics covered in this chapter: 1) An introduction to the Flux application architecture and why it is useful for building user interfaces. 2) An overview of Vuex and its key features, including state and mutations. 3) How to install Vuex and set up a global store that can be accessed by Vue.js components. 4) How Vuex allows for superior debugging with Vue Devtools via mutation logging and time-travel debugging. 5) The creation of a save feature for Vuebnb listings and a saved listings page. 6) Moving page state into Vuex to minimize unnecessary data retrieval from the server.

## Summary

In this chapter, we learned about Vuex, Vue's official state management library, which is based on the Flux architecture. We installed Vuex in Vuebnb and set up a store where global state could be written and retrieved. We then learned the main features of Vuex including state, mutator methods and getters, and how we can debug Vuex using Vue Devtools. We used this knowledge to implement a listing save component, which we then added to our main pages. Lastly, we married Vuex and Vue Router to allow page state to be more efficiently stored and retrieved when the route changes.

In the next chapter, we'll cover one of the trickiest topics of full-stack apps - authentication. We'll add a user profile to Vuebnb so a user can persist their saved items to the database. We'll also continue to add to our knowledge of Vuex by utilizing some of its more advanced features.

