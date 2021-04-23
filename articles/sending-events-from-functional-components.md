---
title: "Sending events from vue functional components"
published: 2021-04-19
updated: 2021-04-19
summary: "Functional components have a scary name for something that is supposed to be so simple. In this article I will briefly explain what are functional components and how we can use them to send events to a parent component"
tags: [ 'vue' ]
---

## What are functional components

A functional component in vue is a special type of component that is stateless, that is, it manages no internal state.

The main advantage of not managing any internal state is that vue doesn't have to create a vue instance or observable properties for that component, and instead,
the component becomes a simple function which makes rendering much faster because the vue compiler has less work to do.

Since a functional component is not attached to a vue instance and therefore, cannot emit events to its parent component, I wanted to share a simple pattern/workaround for overcoming this limitation.

First, Let's create a normal(non-functional) vue component to display a list of notes called `NoteList.vue` . This component will delegate displaying list-items to a more specific component called `NoteListItem.vue`. 

NoteList.vue
```html
<template>
    <div>
        <h1>Notes</h1>
        <ul>
            <li v-for="note in notes" :key="note.id">
                <note-list-item :note="note" @remove-note="removeNote"></note-list-item>
            </li>
        </ul>
    </div>
</template>

<script>
    import NoteListItem from "./NoteListItem";
    export default {
        components: { NoteListItem },
        data() {
            return {
                notes: [
                    {
                        id: 1,
                        description: "this is the first note",
                    },
                    {
                        id: 2,
                        description: "this is the second note",
                    },
                    {
                        id: 3,
                        description: "this is the third note",
                    },
                    {
                        id: 4,
                        description: "this is the fourth note",
                    },
                ],
            };
        },
        methods: {
            removeNote(id) {
                const noteIndex = this.notes.findIndex((note) => note.id === id);

                if (noteIndex > -1) {
                    return this.notes.splice(noteIndex, 1);
                }
            },
        },
    };
</script>
```

NoteListItem.vue

```html
<template>
  <div>
    <div>{{note.description}}</div>
    <button @click="$emit('remove-note',note.id)">Remove</button>
  </div>
</template>

<script>
export default {
  props: {
    note: Object
  }
}
</script>

```

Looking at the `NoteListItem.vue` component,  we can notice two things:

- It doesn't have any internal observable properties 
  
- The data it uses to render is received through props

- It has no lifecycle methods 

`NoteListItem.vue` has a very simple job, render a list item that it receives from it's parent, so we can tell Vue to optimize its rendering performance.

Components within a `v-for` loop are usually great candidates for becoming functional.

## Making a component functional.

In order to make a component functional, a few changes have to be made to the `NoteListItem.vue` component. The `NoteList` component remains unchanged.

 - First, if we are using Single File Components we add the `functional` keyword in the template declaration 
 - Afterwords, props are accessed through a `props` object that contains the provided props. 

NoteListItem.vue

```html
<template functional>
  <div>
    <div>{{props.note.description}}</div>
    <button @click="$emit('remove-note',note.id)">Remove</button>
  </div>
</template>

<script>
export default {
  props: {
    note: Object
  }
}
</script>
```

Currently, if we run the app and click on the remove button, the following error will be thrown:

![vue error](https://i.postimg.cc/kXrd6Rw4/Selection-512.jpg)

Since there is no vue, instance, the $emit function is not available, so we have to find another way for sending the `remove-note` event to the parent.

## Sending events from functional components.

A pattern for sending events to a parent that is not described in the official docs is to directly call the event handler from the `listeners` property 
and pass in any required arguments

NoteListItem.vue
```html
<template functional>
  <div>
    <div>{{props.note.description}}</div>
    <button @click="listeners['remove-note'](props.note.id)">Remove</button>
  </div>
</template>

<script>
export default {
  props: {
    note: Object
  }
}
</script>
```

### Interesting caveats
  
- Like in normal components, we can pass in $event as an argument to the handler.
- We can get rid of the <script> section, since the props property is optional and is used only for validation.


The final code for this component can be seen in this [code sandbox project](https://codesandbox.io/s/lucid-brown-rf6t9)

Happy coding!!🚀🚀🚀🚀🚀

