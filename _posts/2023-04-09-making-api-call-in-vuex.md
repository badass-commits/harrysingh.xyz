---
layout: post
title: "How to make API Calls with Vuex"
date: 2023-04-09 14:00:00 -0600
---

Today I'll explain how to make API calls with Vuex. While Vuex does a great job of keeping your data synchronized across the frontend of your application, you'll need to talk with a database at some point to make sure that any changes will be persisted permanently. Fortunately, Vue makes it very easy for us to work with an API, especially when we use Vue-resource. While Vue-resource is [no longer part of the official Vue ecosystem](https://medium.com/the-vue-point/retiring-vue-resource-871a82880af4#.xs5m1t7e6), I think it is still an easy way to get up and going with APIs. But regardless of the API wrapper you choose to use, the concepts I describe here will still be applicable to your app.

## The Big Picture
As we know from the [Vuex docs](https://vuex.vuejs.org/en), Vuex works like this:

![api-call-vuex-1](/assets/images/posts/api-call-vuex-1.png)

Right away, we can see that the Vuex team has already told us to interact with a backend API via Actions. This is because Actions can be asynchronous, while Mutations must be synchronous. In this structure, it makes sense that Actions should be the place for API calls because they can wait for the data before committing to a Mutation. While this may seem a tad confusing conceptually, the big takeaway is to remember to only handle API calls in your Actions.

## API Setup
Before we begin, I'd like to say thank you to [jonagoldman](https://github.com/vuejs/vuex/issues/85) on GitHub for outlining this setup. Now, let's jump into the code and see how to set up API calls in our Actions. As usual, I'll be working with a Laravel Spark project, but feel free to set up your directories as you see fit.

![api-call-vuex-2](/assets/images/posts/api-call-vuex-2.png)

As you can see above, I have a `vuex` directory with two sub-directories for `modules` and `utils` as well as my top-level `store.js`. Inside of the `utils` directory, there is a file called `api.js`. This is a little helper file where I've wrapped some `vue-resource` calls within HTTP actions.

```
//resources/assets/js/vuex/utils/api.js

import Vue from 'vue'

export default {
    get(url, request) {
        return Vue.http.get(url, request)
            .then((response) => Promise.resolve(response.body.data))
            .catch((error) => Promise.reject(error));
    },
    post(url, request) {
        return Vue.http.post(url, request)
            .then((response) => Promise.resolve(response))
            .catch((error) => Promise.reject(error));
    },
    patch(url, request) {
        return Vue.http.patch(url, request)
            .then((response) => Promise.resolve(response))
            .catch((error) => Promise.reject(error));
    },
    delete(url, request) {
        return Vue.http.delete(url, request)
            .then((response) => Promise.resolve(response))
            .catch((error) => Promise.reject(error));
    }
}
```

Now, within an `actions.js` file, you can import `api.js` and use `api.get(url, request)` to make a request. This isn't a required step, but I find that it keeps my Actions more concise and readable. Plus, if I ever wanted to stop using `vue-resource`, I'd just need to edit this file and my Actions would be fine.

With that out of the way, let's hop into an `actions.js` file and see what your API calls can look like. Side note: your `actions.js` file can be for your Modules or for your top-level store, just remember to do your imports correctly.

## API in Actions
Here's what a fully fleshed out `actions.js` might look like:
```
import api from '../../utils/api.js'

const actions = {
    getIncrementers (context) => {
        return api.get('/incrementers')
            .then((response) => context.commit('GET_INCREMENTERS', response))
            .catch((error) => context.commit('API_FAILURE', error));
    },
    createIncrementer (context, data) => {
        return api.post(data.url, data.request)
            .then((response) => context.commit('CREATE_INCREMENTER', response))
            .catch((error) => context.commit('API_FAILURE', error));
    },
    updateIncrementer (context, data) => {
        return api.patch(data.url, data.request)
            .then((response) => context.commit('UPDATE_INCREMENTER', response))
            .catch((error) => context.commit('API_FAILURE', error));
    },
    deleteIncrementer (context, url) => {
        return api.delete(url)
            .then((response) => context.commit('DELETE_INCREMENTER', response))
            .catch((error) => context.commit('API_FAILURE', error));
    }
};

export default actions
```
As you can see, we've used each of our HTTP actions from `api.js` - with some slight variations - to give you a complete picture of what you can do. Each of the variations are pretty self-explanatory, but let's run through them. In the `getIncrementers` function, you can see that we've hard-coded in the url. Typically, I prefer to pass in my url when I map the Action to my component, so I can handle any dynamic urls. But if the url is as simple as `/incrementers`, then you can probably get away with leaving it hard-coded. Now if you look at the rest of the function, you can see that since `api.get()` returns a Promise we can then chain on our Mutation commits. So if the API call succeeds, I'm committing to the `GET_INCREMENTS` Mutation and passing along the API response as well. And if the API call fails, I'm performing a different commit to `API_FAILURE` with the error so I can let the user know that something went wrong.

In the createIncrementer and updateIncrementer functions, we're handling things slightly differently. Since we need to pass some data to the API, we've included a data Object in the Action. From the data Object I can then get the url and the request and pass it to the API. Lastly, in the deleteIncrementer function, you can see that we're just passing in a url for the API to reference. This is how I typically handle the dynamic urls I was talking about earlier.

## The Wrap Up
And there you have it! A quick look at how to get up and running with APIs and Vuex. With this in hand, and our articles on [Modules](https://metricloop.com/blog/how-to-set-up-modules-in-vuex) and setting up [Vuex](https://metricloop.com/blog/how-to-use-vuex-in-a-laravel-spark-project), you should be well on your way to building some awesome apps with Vuex.
