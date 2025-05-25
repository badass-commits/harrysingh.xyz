---
layout: post
title: "Setting up Tailwind in a Laravel project"
date: 2023-11-10 14:00:00 -0600
---

[Tailwind](https://tailwindcss.com/) is the new CSS utility framework on the block, and it's quickly become my favorite way to build an interface. Oftentimes, the hardest part of trying out a new framework, package, or language is getting set up.

The folks building Tailwind have done an incredible job documenting the process, and it's super easy to do. But, sometimes it's still nice to see how someone else did it. So, let's jump in and see how it's done.

### Getting Started
To start, let's assume we're working with a brand new Laravel project. I won't jump into how to set that up, but if you need a refresher you can reference the docs [here](https://tailwindcss.com/docs/installation). With Laravel all set up, let's take a look at the Tailwind installation docs [here](https://tailwindcss.com/docs/installation).

Looking at their docs, we can see that the easiest way to get the ball rolling is to just drop their CDN into your project and start coding. This is great for trying it out, but let's up the ante and work it into our build processes.

### Installation
We can pull Tailwind into our project by using the following `NPM` or `Yarn` commands.
```
# Using npm
npm install tailwindcss --save-dev
# Using Yarn
yarn add tailwindcss --dev
```
With the package pulled into our project, we can generate the Tailwind config file. We can call our config file anything we like, but let's call it `tailwind.js`. Now, we can run the following command from the root of our project.
```
./node_modules/.bin/tailwind init tailwind.js
```
### Configuration
Bada bing bada boom, we've got ourselves a config file in the root of our project. Open it up and take a look around. As you can see, the Tailwind team has done an excellent job of documenting and explaining everything that the config file does. You can add colors, adjust your breakpoints, refine your spacing, and so much more. Just think of how much easier it's going to be to keep all of your styles consistent!

Let's hop on over now to our Sass directory found at `resources/assets/sass`. Here we can see that Laravel has included some default files out of the box. You can go ahead and delete them if you'd like.

### SaaS Setup
In that directory, we can now create our `index.sass` file (you can call your file anything you like - just don't call it late for dinner!). Here, we're going to copy in the following code from the Tailwind docs.
```
/**
 * This injects Tailwind's base styles, which is a combination of
 * Normalize.css and some additional base styles.
 *
 * You can see the styles here:
 * https://github.com/tailwindcss/tailwindcss/blob/master/css/preflight.css
 */
@tailwind preflight;

/**
 * Here you would add any of your custom component classes; stuff that you'd
 * want loaded *before* the utilities so that the utilities could still
 * override them.
 *
 * Example:
 *
 * .btn { ... }
 * .form-input { ... }
 *
 * Or if using a preprocessor:
 *
 * @import "components/buttons";
 * @import "components/forms";
 */

/**
 * This injects all of Tailwind's utility classes, generated based on your
 * config file.
 */
@tailwind utilities;

/**
 * Here you would add any custom utilities you need that don't come out of the
 * box with Tailwind.
 *
 * Example :
 *
 * .bg-pattern-graph-paper { ... }
 * .skew-45 { ... }
 *
 * Or if using a preprocessor..
 *
 * @import "utilities/background-patterns";
 * @import "utilities/skew-transforms";
 */
 ```
 Notice that they have semicolons at the end of their `@tailwind` imports. Go ahead and remove them. At this point, if you're using PHPStorm, you might notice that your file structure has a bunch of red lines all over it. Don't worry about them, you can ignore them or find a way to turn them off. If you figure out how to turn them off, write a tutorial for me to follow ;).

This is now our master Sass file where we can import our custom Sass, and export to our `public/css` directory in our build process. When you import your custom Sass, it's important to follow the order of imports that they specify in order to avoid any issues with your CSS getting overwritten.

### Build Process
Finally, we're ready to add Tailwind to our build process. Let's open up our `webpack.mix.js` file. At the top, right below `let mix = require('laravel-mix');` let's add `let tailwindcss = require('tailwindcss');`.

Now, in our `mix` we can update the default `.sass` options like so (note: if you didn't name your master Sass file `index.sass` make sure you update it here):
```
mix.js('resources/assets/js/app.js', 'public/js')
    .sass('resources/assets/sass/index.sass', 'public/css/app.css')
    .options({
      processCssUrls: false,
      postCss: [ tailwindcss('./tailwind.js') ],
    });
```
Currently, there's an unresolved issue with one of Mix's dependencies. So, to use Sass with Tailwind we're disabling processCssUrls. For more info on what that means, check out the Mix docs [here](https://github.com/JeffreyWay/laravel-mix/blob/master/docs/css-preprocessors.md#css-url-rewriting).

Finally, we can now run `npm run prod` to compile Tailwind into our CSS.

### Using Tailwind
In your blade files, you can now add `<link href="{{ asset('css/app.css') }}" rel="stylesheet">` in your `head` tag and start using Tailwind to rapidly build responsive UIs.

### That's a Wrap
I hope this little walkthrough went smoothly for you, and that you really enjoy using Tailwind like I have. If you do end up loving it, make sure you share it with your friends and throw a thank you over to the awesome Tailwind team on [Twitter](https://twitter.com/tailwindcss). And until next time, happy coding!
