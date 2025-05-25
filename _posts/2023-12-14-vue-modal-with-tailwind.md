---
layout: post
title: "Build a customizable Vue.js modal with Tailwind CSS"
date: 2023-12-14 14:00:00 -0600
---

As I was hanging out with the Tailwind CSS [Slack community](https://tailwindcss.slack.com/join/shared_invite/enQtMjc2NTA1NTg0NTEyLTY4ZTg1YWFjM2NjMTRkMmNkMTA4MGNiZTFmNDYyYTJhNjNkY2QxODQwODE4MWRiZDFlNzdmOGI0MmQ1M2EzZmQ) the other day, I had a request to write a tutorial on how to make a Vue.js modal styled with Tailwind. That sounds like an excellent component to build, so let's get to it.

### Set Up
Per usual, we'll be starting with a regular Laravel project. I've covered this process in a previous post, but for a quick recap here are the steps.

1. Create a new Laravel project by following the [docs](https://laravel.com/docs/5.5/installation)
2. [Configure](https://nick-basile.com/blog/post/how-to-build-a-vuejs-component-with-tailwind-in-a-laravel-project) our `welcome.blade.php` so we can use Vue.js
3. Add Tailwind CSS to the project through [Yarn or NPM](https://tailwindcss.com/docs/installation/#npm)
4. [Profit](https://www.youtube.com/watch?v=tO5sxLapAts)?

### Hop on the Event Bus
With our usual configuration out of the way, we can layer on the custom details we need for this project. Since we'll want to trigger our modal from anywhere in our code, we need to set up a Vue event bus.

This is super simple. We just hop into our `app.js` file and right after we require Vue, we can and add the following:
```
//Event Bus
window.bus = new Vue();
```
Now, we can use our event bus to communicate between components. If you're looking for some more information about what a event bus does, you can always check out the [Vue docs](https://vuejs.org/v2/guide/components.html#Non-Parent-Child-Communication). But, I think it'll start to make more sense when we use it.

With that set up, we can get rid of the example component (if you haven't already) and add in our modal component.

In `resources/assets/js/components`, we can delete the `ExampleComponent.vue` and add our own file called `modal.vue`. Now, inside of `resources/assets/js/app.js` we can update the component import to reference our `modal` component instead of the example so it looks like this:

```
Vue.component('modal-component', require('./components/modal.vue'));
```
Now, we can go ahead and add our component to our `welcome.blade.php`.

Lastly, we're going to use some "advanced" JavaScript in this tutorial. But, no need to worry, we'll walk through it step-by-step. So, in the same directory as `modal.vue` we can add `modal.js`.

To see this all running in the browser, we'll need to run our Laravel Mix. If you're following along, I recommend using `npm run watch` so your code changes automatically get compiled.

With our Vue component ready, let's add a custom color that we'll end up needing for our modal background overlay to our Tailwind config.

### The Time Has Come to Configure Tailwind
Can you believe that we've already made it through 3 other Tailwind tutorials on this blog before we had to edit the default settings? While the default settings have gotten us this far, we need to add a color to make sure our modal background has an opacity.

To add this color, we can hop into our `tailwind.js` file that should be in the root directory of our project. Here we can see all sorts of options, but we just need to focus on the color variable. Inside this object, we can add this: `'transparent-black': 'rgba(0,0,0,.2)'`.

Now, we need to make sure we run our Laravel Mix so this new color gets added to our Tailwind code. After you run that, you'll be able to reference this color like you have any other Tailwind color. How cool is that?

### Super Spooky Advanced JS
With all of our set up out of the way, we're finally ready to start building this modal. Let's get the "hard" stuff out of the way first by opening up our `modal.js` and creating a [JavaScript Class](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes) that we can use to create dynamic modals on the fly.

To start, let's think about what we'll want our modal to do. We'll obviously need to be able to show and dismiss it when needed. The header and body text should probably be customizable as well. Plus, it would be great if we could tell it what type of modal to be, like a succesful modal or an error one.

With that in mind, we can come up with a JavaScript class that'll be a representation of what our modal should be. Now, you might be asking yourself, "why don't we just do all of this in our Vue component and be done?" And, you're totally right! You could skip all of this entirely and just worry about passing events to your Vue component.

However, I really like using classes for use-cases like this because it allows us to define an API that you, and your teammates, can use to interact with a component. So, instead of worrying about how to package up the correct data to send to your component, you can do something like this instead:
```
vueModal().title('Hello World').success().show();
```
Pretty cool, right? With that little detour out of the way, let's return to creating our class by just defining and exporting it, like so:
```
let VueModal = class VueModal {
  constructor() {

  }

};

export default VueModal;
```
As you can see, we have a nice, simple JavaScript class. Thinking back to what we talked about earlier, we want our modal to have a header, a body, a "type", and to be toggable. So, let's define this in our class.
```
let VueModal = class VueModal {
  constructor(header = null, body = null, type = null, visible = true) {
    this.header = header || 'title';
    this.body = body || 'text';
    this.type = type || 'default';
    this.visible = visible;
  }

};

export default VueModal;
```
All we've done here is define the properties that we want to store on the class. We've also provided some handy default values in case we forget to pass in the data.

Now, we're going to add some "setters" so we can use that chainable API I previewed earlier. We want to create methods that'll allow us to set all of the properties as we need to. So, those methods will look something like this:
```
let VueModal = class VueModal {
  constructor(header = null, body = null, type = null, visible = true) {
    this.header = header || 'Title';
    this.body = body || 'text';
    this.type = type || 'default';
    this.visible = visible;
  }

  title(header) {
    this.header = header;

    return this;
  }

  text(body) {
    this.body = body;

    return this;
  }

  appearance(type) {
    this.type = type;

    return this;
  }

  success() {
    this.type = 'success';

    return this;
  }

  error() {
    this.type = 'error';

    return this;
  }

  info() {
    this.type = 'info';

    return this;
  }

  warning() {
    this.type = 'warning';

    return this;
  }

  show() {
    window.bus.$emit('show-modal', this);

    return this;
  }

  dismiss() {
    window.bus.$emit('dismiss-modal');

    return this;
  }
};

export default VueModal;
```
We've added a lot here, but really all that we've done is provided some handy methods that let us set our class' values and define our modal on the fly. Take a look at the methods and see what we're doing. In most cases, we're either taking in a passed value and setting a property, or we're setting it based on a hard-coded value.

The only exceptions are `show()` and `dismiss()`. Here, we're leveraging that event bus we created earlier to talk to our Vue component. When we create our Vue component, we'll register some listeners that can respond to these messages.

While this wraps up our modal class, you may still be a bit confused about how it'll work. Don't worry, as we build our Vue component, it'll start making a lot more sense.

### It's Vue Time
Our Vue component is going to be pretty simple because we've already done most of the work defining our data in our class. Let's jump into our template and get this party started.

Like any good modal we'll need: a background overlay, the modal itself, a header, some body text, and a button. So, our template will look like this:
```
<template>
    <div v-if="modal.visible" @click.self="dismissModal">
        <div>
            <div>
                <h1>{{ modal.header }}</h1>
            </div>
            <div>
                <p>{{ modal.body }}</p>
            </div>
            <div>
                <button :class="typeColor" @click="dismissModal">Ok</button>
            </div>
        </div>
    </div>
</template>
```
Pretty simple, right? We've got our background wrapper, which we're toggling based on whether `modal.visible` is true. Then, we've also bound a method on click that'll dismiss the modal when only the background is clicked. We achieve that with the fancy click modifier `.self`. This lets our user interact with the modal without accidently dismissing it.

In the modal itself, we're really just displaying our modal attributes. Lastly, our button has the same `dimissModal` method binding as our wrapper plus some dynamic classes that change based on the type of modal we're showing. All in all, not the most complicated component ever.

Now that we're all warmed up, let's check out our component's script section.
```
<script>
    import VueModal from './modal.js';

    export default {
        data() {
          return {
              modal: {
                  header: 'Header',
                  body: 'Body',
                  type: 'default',
                  visible: false,
              }
          }
        },
        computed: {
          typeColor() {
              let color;

              switch(this.modal.type) {
                  case 'success':
                      color = 'bg-green hover:bg-green-dark'
                      break;
                  case 'error':
                      color = 'bg-red hover:bg-red-dark'
                      break;
                  case 'info':
                      color = 'bg-blue hover:bg-blue-dark'
                      break;
                  case 'warning':
                      color = 'bg-yellow hover:bg-yellow-dark'
                      break;
                  default:
                      color = 'bg-teal hover:bg-teal-dark'
              }

              return color;
          }
        },
        created() {
            this.initModal();
        },
        methods: {
          initModal() {
              window.vueModal = (header = null, body = null, type = null, visible = true) => {
                  return new VueModal(header, body, type, visible)
              };

              this.initListeners();
          },
          initListeners() {
              window.bus.$on('show-modal', (modal) => {
                  this.modal = modal;
                  document.body.classList.add("overflow-hidden");
              });

              window.bus.$on('dismiss-modal', () => {
                  this.modal.visible = false;
                  document.body.classList.remove("overflow-hidden");
              });
          },
          dismissModal() {
              return vueModal().dismiss();
          }
        }
    }
</script>
```
Let's break all of this down from the top. At the beginning of this section, we're importing our VueModal class so we can use is throughout our component. Next, we have our data. Here, we have a modal object where we've defined some default values for our modal. Using an object like this also makes it easier for us to overwrite these values with the values we instantiate in our VueModal class.

Below our data, we have a computed property called typeColor. In here, we have a switch statement that matches our Tailwind styles to the type we define in our data. You earned some bonus points if you noticed that these type values correspond with what we defined in our class earlier.

Next, we have our created lifecycle hook. In here, we're calling the `initModal()` method. Moving right along to our methods object, we can see that the first method is in fact `initModal()`. Here's the bread and butter of what we've been working towards.

First, we're binding a method to the window called `vueModal()`. This method accepts the values we need to pass to our VueModal class. Then, it instantiates a new instance of our VueModal class and passes in any of the values defined. Lastly, we then call our next method: `initListeners()`.

Inside of `initListeners()`, we've created two listeners to respond to the events that we set up in our class earlier. In the show-modal listener, we're setting our modal data to the passed in value, which was an instance of our class. Then, we're using some vanilla JavaScript to add `.overflow-hidden` to the document's body element. This prevents the page from scrolling when our modal is open. In our second listener, we're simply hiding our modal and removing `.overflow-hidden` from the body.

Finally, we have our last method `dismissModal()`. Here, we're simply calling the `.dismiss()` method on the `vueModal()` we defined earlier when we initialized the modal.

Whew, that was a good bit of code! But, now we have a nice modal component that we can trigger with a chainable API. Let's run our Laravel Mix; grab that preview snippet from earlier, and run that through our console.
![vue-tailwind-modal-1](/assets/images/posts/vue-tailwind-modal-1.png)
If everything went as planned, you should have started with an empty page, and then the modal should have appeared when you ran our snippet. Finally you can see how valuable using a class can be. We can trigger easy-to-understand, customizable modals from anywhere in our code!

Feel free to take a break now and play around with our modal. When you're ready to continue, we'll finish our modal with some Tailwind classes.

### Sailing off with Tailwind
Let's wrap this modal up with some nice Tailwind classes. To start, we'll need our wrapper `div` to take up the whole page; center our modal in the middle, and have our custom background. We can do that by adding the following classes: `.pin` `.absolute` `.flex` `.items-center` `.justify-center` `.bg-transparent-black`. Most of this is pretty self-explanatory, but `.pin` is a little special. It applies the following css to an element:
```
top: 0;
right: 0;
bottom: 0;
left: 0;
width: 100%;
height: 100%;
```
For an absolutely positioned element, like our background, this is perfect for ensuring it fills the entire page in any situation.

Onto the modal itself! We can give it some rounded corners, dynamic sizing, white background, and more with the following: `.bg-white`, `.rounded`, `.shadow`, `.p-8`, `.m-4`, `.max-w-lg`, `.max-h-full`, `.text-center`, `.overflow-y-scroll`.

Our interior divs don't need too much work. The first one can have a `.mb-4` for some spacing from the body, while the second one can have some extra spacing from the button with an `.mb-8`.

Finally, our button just needs some spacing to round out the dynamic classes it's receiving from our computed property. We'll just add `.text-white`, `.py-2`, `.px-4`, and `.rounded`.

Bada bing bada boom, we've got ourselves a fully styled modal component! Running our snippet from earlier, let's see how it looks.
![vue-tailwind-modal-2](/assets/images/posts/vue-tailwind-modal-2.png)

### That's a Wrap
Well isn't that a thing of beauty. Good work coming along for this tutorial. I hope that I've been able to expose you to some patterns that'll prove useful in your future projects!