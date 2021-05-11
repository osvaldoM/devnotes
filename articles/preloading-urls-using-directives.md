---
title: "Preloading urls on hover using vue custom directives"
published: 2021-05-11
updated: 2021-05-11
summary: "I recently added a functionality in which when a user hovered over a certain link on my page,
I would preload the url to where that link pointed. The reasons and limi....."
tags: [ 'vue']
---

I recently added a functionality in which when a user hovered over a certain link on my page,
I would preload the url to where that link pointed.
The benefits and limitations around this are clearly explained in this [post](http://instantclick.io/) from [instantclick.io](http://instantclick.io/), 
but in summary:

> Before visitors click on a link, they hover over that link. Between these two events, 200 ms to 300 ms usually pass by (test yourself here). InstantClick makes use of that time to preload the page, so that the page is already there when you click.

Here is what happens with this approach:
- User hovers over a link on the page;
- We send a GET request to the value of the link's href property;
- By the time the user clicks on the link, the page will already be in the cache(or at least, connection latency will have decreased).

I firstly implemented this as follows:

```html
<template>
  <div>
    <a href="/page-to-be-preloaded" v-on:mouseover.once="preload"> Hover over me to preload</a>
  </div>
</template>

<script>
export default {
  methods: {
    preload({target}) {
        console.log('fetching', target.href);
        fetch(target.href);
    }
  }
};
</script>
```

I noticed that this preload technique could be reused in other parts of my application, but adding
a component for a pre-load link seemed cumbersome, since this doesn't declare any reusable HTML
or require any state management, so I decided to use custom directives, which are another form of code reusability in vue that
allows us to work directly with DOM elements.

To achieve that, first lets create a directive :
```javascript
export const preloadOnHover = ({
    inserted(el) {
        if(el.tagName.toLowerCase() !== 'a') {
            console.error('preload directive added to non-link element');
            return;
        }
        if(el.href === window.location.href) //We could even validate the url here.
            return;
        el.addEventListener('mouseover', ({target}) => {
            console.log('preloading', target.href)
            fetch(target.href)
        }, {
            once: true
        });
    }
});
```

A few things to note in this implementation are:
-  We validate to see if the element we want to is a link and that it has the `href` attribute
-  Since we passed a value of true to the `once` parameter, the event handler will only be executed once.


In order to make use of our newly created directive, we just need to declare it as a directive in our component
and then add it to our template as`v-preload-on-hover`
```html
<template>
    <div>
        <a href="/page-to-be-preloaded" v-preload-on-hover> Hover to preload</a>
        <!-- If using vue-router, we can add <router-link v-preload-on-hover></router-link> > -->
    </div>
</template>

<script>
    import {preloadOnHover} from '../directives';

    export default {
        directives: {
            preloadOnHover
        },
    };
</script>
```


# A few things we should take into consideration

- Whenever possible, consider using HTML resource hints(prefetch, preconnect, preload, etc) instead, to improve 
   the loading speed of pages/assets that are likely to be needed for the current/next navigation.

- Since we're using `mouseover` events, this only works on devices with a pointer/mouse, for devices with touch input,
we'd have to adapt this solution to use other events(eg: `touchstart`)

- This should be used carefuly, since we don't want to waste bandwidth by prefetching assets that might not be needed.
    

The final code for this component can be seen in this [code sandbox project](https://codesandbox.io/s/wizardly-aryabhata-160c5?file=/src/components/HelloWorld.vue:0-220), and I hope you learned something interesting from this article.

Happy coding!!🚀🚀🚀🚀🚀
