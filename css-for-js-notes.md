
# CSS for JS Notes

## Absolute Positioning

- Trick for centering an element using absolute

```CSS

  .some-box {
    position: absolute;
    background-color: blue;
    top: 10px;
    left: 10px;
    right: 0px;
    bottom: 0px;
    width: 80px;
    height: 80px;
    margin: auto;
  }
```

- Algorithm for absolute positioning inside and element
- When deciding where to place an absolutely-positioned element, it crawls up through the tree, looking for a non-static ancestor (any element that has a position other than the default value of static).
  - If it finds one, that element becomes the containing block, and the absolute child will be anchored to that element.
  - If it doesn't find one, it'll be anchored based on the "initial containing block", a box the size of the viewport at the very top of the document.

- screenshot sizing: Command + Shift + 4 and hit escape
- Cmd + Shift + 4, and hitting "Escape" to dismiss without taking a screenshot

- React component library Reach, accessibility <https://reach.tech/>

## Component

- combination of a class in css, function in JS, and a partial in HTML, all rolled into one and ability to pass over rides
- packaged deal, for markup and functionality

## Create a perspective effect

- create a div in the DOM
- add a class to that div with property of `position: fixed` to take it out of normal flow
- add properties to it for the size and position you want

```css
.perspectiveEffect {
  position: fixed;
  top: 60%;
  left: 0;
  height: 40%;
  width: 100%;
  background-color: hsl(195deg, 20%, 86%);
}
```

- add a `position: relative` to elements to make them non-static, that makes the z-index just render the order that it is in the DOM, one on top of another

## CSS in modern JS ecosystem

- React, create a new way, a component, bundle the styling, markup, JS and behavior into a component. This is your lego block to use in differ situations.
- Component, straight line between the markup. Put walls up for that component.
- This component owns this markup, and nothign else in the app can touch this component

## Styled Components

- Styled Components, runs at runtime, in the browser on the users device
- Differ from Sass, which runs on server compile time before the user has requested it
- In React, anything that starts with a capital letter, is a component. `<FormWrapper>`
- Lets you write styles that are associated with a component, does this by generating a class name under the hood that is dynamic and globally unique. So you don't have to worry about naming conventions or scoping issues. All of this is taken care of by the tool
- Biggest issues dev has with CSS, naming things, specificity and collisions.
- The goal is to avoid naming collisions
- You should be able to clearly answer which styles affect this element.

## CSS Ecosystem

### Vanilla CSS

*Pros:*

- No tooling means less complexity, no runtime performance costs
- Modern CSS features like CSS Custom Properties? make certain tooling features (eg. Sass variables) redundant

*Cons:*

- Global and unscoped. The CSS you write in one place will be applied everywhere. Using a naming convention like BEM can help, but it's high-friction and prone to failure at scale: naming collisions are still possible, and it requires enormous dedication and willpower to stay 100% consistent with it.
- Requires that you remember to add vendor prefixes for many CSS properties, to ensure optimal browser support.
- Can't easily share data between CSS and JS.
- When it comes to modern JS application development, it feels a bit like a square peg being squeezed into a round hole. CSS is built for documents, not apps.

### Sass / Less

*Pros:*

- Includes powerful tools like for-loops, mixins, and nesting
- Has really high developer satisfaction compared with vanilla CSS.

*Cons:*

- Requires a build step (and it's pretty slow in development compared with hot-reloading)
- Because it compiles to CSS, it remains global by nature, and isn't scoped to specific components. - It inherits a lot of "cons" from vanilla CSS, such as not automatically vendor-prefixing.
- Everything happens at build time, so it can't react to things in real-time. As we'll learn later on, Sass variables are nowhere near as powerful as CSS variables for this reason.
- Requires native dependencies that can fail or get out-of-date. I can't access my old Sass projects without spending hours dealing with native dependency issues. I can't just npm install — it's a real pain.
- CSS has added a bunch of new features over the years, and there have been naming clashes. CSS has a native min function now, and it's way better than Sass' min function, but the keyword is already reserved. There are workarounds, but it's added friction.
It's becoming less and less popular in the JS scene. While popularity isn't everything, a fading solution will have less community resources, less support, and more potential for trouble.

### Aphrodite

*Pros:*

- Scoping and specification issues entirely disappear. This is the real game-changer, and the reason so many React applications use one CSS-in-JS solution or another.
- Allowed you to use JS within your CSS! This makes it easy to share state (eg. design tokens). It also allows for complex iteration and generation without the need to learn a new DSL (as you would with Sass/Less).
- Encourages good habits — no support for nesting, or other things that can land you in hot water.
- Automatically adds vendor prefixes, so you don't have to worry about it.
- Similar API to React Native makes it easy to move between projects, or possibly port components between them (though the CSS alternative on React Native is a bit different, so this isn't trivial).
- Having styles and JSX in the same file is awesome. No need to keep tabbing between files.

*Cons:*

- Requires a build step
- High-friction. It's a lot of messing around, and it's so easy to forget the css() function call.
- Has a cost in terms of bundle size and runtime execution time, though it's relatively small.
- Styles must be written in JS. Property names are camelCased, values must be quoted. This can lead to surprising and frustrating differences, like needing to write content: '""' for pseudoelements (discussed later in this course).
- Writing global styles is a bit funky (requires using an extension with some unintuitive syntax).
- It's not a very active project — no new releases in 2020. Possibly as a result, the project has been losing the mindshare game.

### CSS Modules

*Pros:*

- Solves scoping and specificity! The .wrapper class you write will be globally-unique, even if a different CSS file has a .wrapper as well. If you were to console.log in the JS file, you'd see something like .wrapper-abc123.
- Feels like writing straight-up CSS, which can be nice and familiar
- Offers a composes feature, to extend existing CSS classes

*Cons:*

- Doesn't really offer any modern convenience features, like autoprefixing
- Hard to share data between CSS and JS

### Styled-components

*Pros:*

- Solves scoping and specificity in a magnificent way. This solution is tailor-made for component-driven architectures, and it fits like a glove.
- Feels like writing CSS (since you are just writing css!), with some of the quality-of-life improvements from Sass/Less rolled in.
- Offers good solutions for animations and global styles — you can write 100% of your CSS with this tool
- Extremely high developer satisfaction.
- Best-in-class performance: styled-components version 5 has gotten extremely performant, as we'll see in a future lesson. Plus it supports SSR, which allows us to improve performance even more.
- The most popular CSS-in-JS solution out there, according to the # of Github projects that depend on it. Lots of active development, an engaged community, and plenty of resources.

*Cons:*

- Requires a build system
- It's primarily a React tool (you can use styled-components with Vue and possibly other frameworks, but those communities will be much smaller).
- Obfuscates the underlying markup tags, which can make it harder to get a sense of the HTML semantics at a glance.

### Emotion

*Pros:*

- Can be used without React (albeit with a different syntax)
- Slightly smaller bundle size compared with styled-components

*Cons:*

- Not as popular or battle-tested as styled-components — according to Github in early 2021, ~100k projects depend on Emotion, while ~500k projects use styled-components.
emotion/styled takes a different approach towards dynamic props which can be slightly less flexible.

### Tailwind

*Pros:*

- Solves scoping and specificity
- Encourages good habits when it comes to following a design system — instead of specifying sizes in pixels, for example, they're specified in terms of size (lg, xl)
- Includes built-in design tokens (colors, sizes…), which can make it easier to come up with a nice design.
- Can be faster to write, once you get the hang of it
Not React-specific
- Tailwind has exploded in popularity in 2020, and has an extremely passionate user base, and a ton of community resources.

*Cons:*

- Relatively steep learning curve, compared to other tools
- Because not all CSS can be turned into utilities, you'll likely need a secondary system for writing more-traditional CSS
- Tailwind is the fastest-growing CSS solution right now, but its ecosystem is still quite a bit smaller than styled-components (according to Github dependent-project stats, at least)
- Adds a lot of "bulk" to your markup. In real-world scenarios, many many classes are required, and this can make it harder to read. For example:

### CSS-in-JS

Some of the tools in this list are part of a category of tools known as “CSS-in JS”—styled-components, CSS modules, and Aphrodite are all examples of “CSS-in-JS” tools.

A tool is considered “CSS in JS” if the CSS is processed in some way by JavaScript at runtime before being applied.

The name “CSS-in-JS” has always bothered me—it's a misnomer! It makes it sound like we've come up with some pure-JavaScript way of doing styling. Nothing could be further from the truth: we're still writing 100% full-fat real-world CSS. JS is the delivery mechanism for our CSS, that's all.

Don't let anyone make you feel bad for choosing a CSS-in-JS tool. Most of the critics are curmudgeons who have never actually used these tools themselves.

if we want to be the worlds leading learning company externally, it needs to start internally.

### Styled Components

```CSS
const Button = styled.button `
font-size: 32px;
`;

```

- Figure out what your sematic HTML should be, then figure out where your styles should go, then style an element and name it

## Global Styles

- Use a reset, [Eric Myers for example](https://meyerweb.com/eric/tools/css/reset/)
- How can I import a design token in here
- React app that consumes our style package which includes design tokens from Figma. Design tokens is used in our global reset all using styled components.

## Dynamic Styles

## Component Library

- Reach UI, not as opinionated as other frameworks
- A blank canvas for us to add our own styles
- Discourage students from using library frameworks, at some point you are going to need a component that isn't in the library. Then you have to recreate a component that doesn't already exist, it's not trivial.
- You have to start over writing styles, it's not trivial.
- Harder then it would have been to just build the component yourself
- Long term, it doesn't help
- Pro, MVP's or prototypes,
- Long term, enterprise, build yourself
- But you don't have to start from scratch
- Other options, un-opinionated when it comes to style
- Reach UI, you have a lot of little accessibility challenges, hard to do in React Context building it from scratch
- Use a component library without the styles

- Maybe two parts, our style package that has our design tokens
- And the React boiler plate app, that includes dependencies
  - styled components
  - starter atomic components Reach UI
  - global reset
  - pvs style package with design tokens

## Taking measurements

- Cmd + Shift + 4
- to get the curser
- <https://cleanshot.com/> screenshot tool

## Inversion of control nesting

```CSS
const TextLink = styled.a`
  /* Standard styles: */
  color: blue;
  text-decoration: none;
  /* Styles when rendered inside a quote: */
  ${QuoteContent} & {
    color: black;
    text-decoration: revert;
  }
`;
```

## Implicit spacing

Choose a number for your spacing, and everything is a multiple of that number. For example 4. Implicit grid, all spacing should be multiples of 4px, some cases you need to optical align something.

If you use these multiples of 4, then you ensure consistency because you don't have random spacing all over the place.

## Flexbox

```CSS
.wrapper {
  display: flex;
  flex-direction: row; /* row, column */
  justify-content: flex-start; /* flex-end, space-between… */
  align-items: stretch; /* flex-end, baseline… */
}
```

### CENTERING VERTICAL HEIGHT

```CSS
/* set the parent container to 100%, has to be both html and body, html has no parent, so it falls back on view port height */
html, body {
  height: 100%;
}

.wrapper {
  display: flex;
  flex-direction: row;
  /* primary axis, x axis */
  justify-content: center;
  /* cross axis, y axis */
  align-items: center;
  /* height based on the html, body  */
  min-height: 100%;
}

```

- note about vh units, problem on mobile, because it represents the maximum size of viewport. Address bar and footer bar.

Long shot but anyone know where to find historical weather data for a lighting strike that happened in the neighborhood on Saturday August 14th? or if anything like that even exist.

### RESPONSIVE NAV

```HTML
<style>
  /* mobile styles */
  ul {
    display: flex;
    flex-direction: column;
    align-items: center;
  }
  a {
    display: block;
    padding: 8px;
  }
  /* desktop styles */
  @media (min-width: 300px) {
    ul {
      flex-direction: row;
      justify-content: space-evenly;
    }
  }
</style>

<nav>
  <ul class="nav">
    <li>
      <a href="">Home</a>
    </li>
    <li>
      <a href="">Browse</a>
    </li>
    <li>
      <a href="">Contact</a>
    </li>
  </ul>
</nav>
```

### Chat app bubbles using Flex

```HTML
<style>
  /* Default / cosmetic styles */
html, body {
  height: 100%;
}
ol {
  min-height: 100%;
  list-style-type: none;
  margin: 0;
  padding: 0;
}
.message {
  display: block;
  padding: 16px;
  margin: 8px;
  border-radius: 6px;
  width: -moz-fit-content;
  width: fit-content;
  max-width: 70%;
}
.message.sent {
  background: hsl(240deg 100% 47%);
  color: white;
}
.message.received {
  background: hsl(0deg 0% 90%);
  color: black;
}

  /* TODO */
  ol {
    height: 100%;
    display: flex;
    flex-direction: column;
    justify-content: flex-end;
    align-items: start;
  }
  
  .sent {
    align-self: flex-end;
  }
</style>

<ol>
  <li class="message sent">
    Can you get me a big salad?
  </li>
  <li class="message received">
    What big salad? I'm going to the coffee shop.
  </li>
  <li class="message sent">
    They have big salads.
  </li>
  <li class="message received">
    I've never seen a big salad.
  </li>
  <li class="message sent">
    They have a big salad.
  </li>
  <li class="message received">
    Is that what I ask for?
  </li>
  <li class="message received">
    The <em>BIG</em> salad?
  </li>
</ol>
```

## Flexbox, Growing and Shrinking

- `flex-basis: 200px`
- Sets the hypethetical width or height (depending on the flex-direction) of an flex item
- Really confusing, the difference between `width` and `flex-basis`, when you use both of them, `flex-basis` always wins.

- **Takeaways**
- Two important sizes when dealing with Flexbox: `minimum content size`, and `hypothetical size`
- The `minimum content size` is the smallest an item can get without it's contents overflowing
- SETTING THE `width` in a flex row (or height) set the hypothetical size. It is not gauranteed.

- flex-basis has the same effect as width in a flex row (height in a column). You can use them interchangeably, but flex-basis will win if there's a conflict.
- flex-grow will allow a child to consume any excess space in the container. It has no effect if there isn't any excess space.
- flex-shrink will pick which item to consume space from, if the container is too small. It has no effect if there is any excess space.
- flex-shrink can't shrink an item below its minimum content size. If all the items are below their minimum content size, this property has no effect.

## Flex Shorthand

- width applies to the hypethetical spcace
- `flex: 1`, what you are actually saying is `flex-grow: 1` and set the `flex-basis: 0px` to distribute the space evenly.
- Al spcae Distributed evenly: `flex-basis: 0`
- Extra space distributed: `flex-basis: auto`
- [Flex basis graphic](https://www.w3.org/TR/css-flexbox-1/#valdef-flex-flex-basis)

### Sample Flex card layout

```HTML
<style>
  article {
  margin: 8px;
  border-radius: 16px;
  box-shadow: 0px 2px 24px hsl(0deg 0% 0% / 0.2);
  }
  article img {
    border-radius: 12px 12px 0px 0px;
  }
  article section {
    padding: 8px 16px 16px;
  }
  article h2 {
    margin-bottom: 8px;
  }
  article p {
    font-weight: 300;
  }

  /* TODO, create a card layout */

  article img {
    width: 100%;
  }
  
  main {
    display: flex;
    flex-direction: row;
  }
  
  article {
    flex: 1;
    flex-basis: 0;
  }
</style>

<main>
  <article>
    <img src="/course-materials/cat-300px.jpg" />
    <section>
      <h2>Study: Catnip is GOOD</h2>
      <p>The number-crunching mousers have good news for us all: catnip is as good for us as it feels!</p>
    </section>
  </article>
  <article>
    <img src="/course-materials/cat-two-300px.jpg"
    />
    <section>
      <h2>My journey from the city to the exurbs</h2>
      <p>When the human said we'd be moving to rural Wisconsin, I was indifferent; who cares where we live, as long as they keep the wet food coming, right? But I soon discovered: Wisconsin has an incredible bounty of mice and cheese.</p>
    </section>
  </article>
  <article>
    <img src="/course-materials/cat-three-300px.jpg" />
    <section>
      <h2>Their trinkets deserve to fall.</h2>
      <p>Fellow felines, I trust that you know my frustration well. Humans are constantly running around doing unimportant things. Going out without bringing us anything back. It boggles the mind! But I found One Neat Trick to get them to pay us more attention…</p>
    </section>
  </article>
</main>

```

### Sidebar Layout

```HTML
<style>
  nav, main {
  height: 200px;
  border: 3px solid;
  }

  nav {
    border-color: hsl(330deg 100% 50%);
    background: hsl(330deg 100% 50% / 0.2);
  }

  main {
    border-color: hsl(45deg 100% 50%);
    background: hsl(45deg 100% 50% / 0.2);
  }

  .wrapper {
    display: flex;
    justify-content: center;
  }

  nav {
    /* TODO */
    flex: 1;
    max-width: 150px;
  }

  main {
    /* TODO */
    flex: 2;
    max-width: 500px;
  }
</style>

<div class="wrapper">
  <nav></nav>
  <main></main>
</div>

```

## Flex shorthand

- Flex shorthand set all three properties. Flex grow, Flex shrink, Flex basis

```HTML
<style>
  main {
    /* Flex shorthand */
    flex: 1; /* flex-grow: 1, flex-shrink: 1, flex-basis: 0px */
    width: 200px; /* width will loose out to flex-basis */
  }
</style>

```

- Flex basis will always win in a battle against width

 ```HTML
<style>
  main {
    /* Flex write it out */
    flex: 1 1 200px; /* flex-grow: 1, flex-shrink: 1, flex-basis: 200px */
  }
</style>

```

## Flex Wrapping

- Flex wrap, set a default hypethetical size, and when an item falls below that size, it will force it to line wrap, if you have `flex-wrap: wrap;` set.
- Also set a `max-width`, so when an item wraps, it will not grow to fill an entire column

- Dog demo with cards wrapping

 ```HTML
<style>
  main {
    display: flex;
    /* Flex Wrap */
    flex-wrap: wrap;
  }
  article {
    flex: 1 1 150px;
    max-width: 250px;
  }
  article img {
    width: 100%;
  }
  /* Demo */
  article {
  margin: 8px;
  border-radius: 16px;
  box-shadow: 0px 2px 24px hsl(0deg 0% 0% / 0.2);
  }
  article img {
    border-radius: 12px 12px 0px 0px;
  }
  article section {
    padding: 8px 16px 16px;
  }
  article h2 {
    margin-bottom: 8px;
  }
  article p {
    font-weight: 300;
  }
</style>

<main>
  <article>
    <img src="/course-materials/dog-one-300px.jpg" />
    <section>
      <h2>The One Weird Trick to get tasty dinner scraps</h2>
      <p>Step one: Find the friendliest human at the dinner table. Step two: Give them sad pupper eyes. Step 3: Get slid human food on the sly.</p>
    </section>
  </article>
  <article>
    <img src="/course-materials/dog-two-300px.jpg"
    />
    <section>
      <h2>How to show them you mean business</h2>
      <p>Every dog park has their own scene. Different cliques. If you want to make a name for yourself, you'll need to make a good first impression…</p>
    </section>
  </article>
  <article>
    <img src="/course-materials/dog-three-300px.jpg" />
    <section>
      <h2>Life in the outdoors</h2>
      <p>We purchased and tested the 10 best outdoors accessories so you don't have to. Here's what we found…</p>
    </section>
  </article>
</main>

```

## Items vs. Content

- Content, you are moving a group of items, you are positioning things as a cohesive group, not individual items
- Items, the cross axis, managed individually

- Card style wrapping, center

```HTML
<style>
  main {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
  }
  article {
    flex: 0 1 150px;
    max-width: 150px;
  }

  /*Demo*/
  article {
  margin: 8px;
  border-radius: 16px;
  background-color: hsl(240deg 90% 90%);
  border: 2px solid hsl(240deg 80% 60%);
  height: 200px;
  }
  article:first-child {
    background-color: hsl(335deg 90% 90%);
    border-color: hsl(335deg 80% 60%);
  }
  article:last-child {
    background-color: hsl(45deg 90% 90%);
    border-color: hsl(45deg 80% 60%);
  }
</style>

<main>
  <article></article>
  <article></article>
  <article></article>
</main>
```

## Modern Layouts

- [ten modern layouts css](https://web.dev/one-line-layouts/#02.-the-deconstructed-pancake:-flex:-lessgrowgreater-lessshrinkgreater-lessbasewidthgreater)

## Gaps spacing

- `margin-right: auto` consumes all the extra space in the flex container. Within the flexbox specs.
- `gap: 8px;` adds a gutter between each flex child, not in all major browsers, Safafi or IE.
- Alternative to gap, create a spacer component

**Sample Header**

```Java
function Header() {
  return (
    <Wrapper>
      <Logo>My Thing</Logo>
      <AuthButton>Log in</AuthButton>
      <AuthButton>Sign up</AuthButton>
    </Wrapper>
  )
}

const Wrapper = styled.header`
  display: flex;
  gap: 8px;
`;

const Logo = styled.a`
  font-size: 1.5rem;
  margin-right: auto;
`;

const AuthButton = styled.button``

render(<Header />);

```

## Ordering

- You can flip the order, going from last to first
- `flex-direction: row-reverse`
- `flex-direction: column-reverse`

### Blog table of contents example

- For keyboard accessibility, you can flip the order, so keyboard users can tab through the table of contents. But it's displayed on the right side.

```HTML
<style>
  .wrapper {
    display: flex;
    flex-direction: row-reverse;
  }
  main {
    flex: 1;
  }
  aside {
    min-width: 200px;
  }

  /*
  These styles are purely cosmetic,
  and shouldn't need to be tweaked.
*/

aside {
  margin-left: 16px;
}

nav h2 {
  font-size: 1rem;
  text-transform: uppercase;
  color: #555;
  letter-spacing: 2px;
  font-weight: 400;
}

nav {
  background: #eee;
  padding: 16px;
}

p {
  margin-bottom: 64px;
}

ul {
  list-style-type: none;
  padding-left: 16px;
}

li {
  padding: 8px 0;
}

nav a {
  color: black;
  text-decoration: none;
}

form {
  padding: 32px;
  border: 1px dotted;
}

form h2 {
  margin-bottom: 16px;
}

input {
  width: 75px;
}
</style>

<div class="wrapper">
  <aside>
    <nav>
    <h2>Table of Contents</h2>
      <ul>
        <li>
          <a href="#heading-one">Heading One</a>
        </li>
        <li>
          <a href="#heading-two">Heading Two</a>
        </li>
        <li>
          <a href="#heading-three">Heading Three</a>
        </li>
      </ul>
    </nav>
  </aside>
  <main>
    <h2 id="heading-one">Heading One</h2>
    <p>Imagine if this was a <a href="">real blog post</a>, and this was <a href="">real content</a>!</p>
    <h2 id="heading-two">Heading Two</h2>
    <p>In order to keep this playground manageable, the content is going to be much shorter than it would be in a real-world scenario.</p>
    <h2 id="heading-three">Heading Three</h2>
    <p>I hope that makes sense!</p>
    <form>
      <h2>Join the newsletter!</h2>
      <label>
        Email:
        <input />
      </label>
      <button>Subscribe</button>
    </form>
  </main>

</div>


```

## Flexbox interacts with other properties, i.e. position fixed

- What happens when you put `position: fixed` on a `flex` item? **postition fixed will always win**
- General rule, items cannot participate in multiple layout modes at once.
- Although, `relative` position is a special case. The layout mode is inherited.
- Margin collapse, only happens in Flow layout, not when elements are laid out with flex
- `z-index` typically only works on items using `postitioned` layout (relative, absolute, fixed, sticky). Exception, **children of `display: flex` parent can also use `z-index`.**

## Multiple Layout Modes

- You can mix multiple layout modes in some cases to create certain situations. For example; scroll and fixed.

```HTML
<style>
  section {
    display: flex;
    gap: 32px;
    border: 3px solid hotpink;
    overflow: auto;
  }
  
  .col {
    flex: 1;
    padding: 16px;
  }
  
  .col:first-of-type {
    position: sticky;
    top: 0;
  }
  
  .col:last-of-type {
    height: 0px;
  }

  /* Cosmetic styles */
  h1, p, li {
    margin-bottom: 16px;
  }
</style>

<section>
  <div class="col">
    <h1>Growing Column</h1>
    <p>This column will grow very tall indeed, whilst the adjacent one will be clamped to whatever height this one rests at!</p>
    <p>Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since the 1500s, when an unknown printer took a galley of type and scrambled it to make a type specimen book.</p>
  </div>
  
  <div class="col">
    <p>Here is a list of all the letters in the English language:</p>
    <ol>
      <li>Item A</li>
      <li>Item B</li>
      <li>Item C</li>
      <li>Item D</li>
      <li>Item E</li>
      <li>Item F</li>
      <li>Item G</li>
      <li>Item H</li>
      <li>Item I</li>
      <li>Item J</li>
      <li>Item K</li>
      <li>Item L</li>
      <li>Item M</li>
      <li>Item N</li>
      <li>Item O</li>
      <li>Item P</li>
      <li>Item Q</li>
      <li>Item R</li>
      <li>Item S</li>
      <li>Item T</li>
      <li>Item U</li>
      <li>Item V</li>
      <li>Item W</li>
      <li>Item X</li>
      <li>Item Y</li>
      <li>Item Z</li>
    </ol>
  </div>
</section>

```

## Flexbox Recipes

- Practical everyday layouts in flexbox
- [MDN Layout Cookbook Recipes](https://developer.mozilla.org/en-US/docs/Web/CSS/Layout_cookbook)

### Holy Grail Layout

```HTML
<style>
  .wrapper {
    display: flex;
    flex-direction: column;
    height: 100vh;
  }
  
  .middle {
    border: 3px dotted;
    flex: 1;
    display: flex;
  }
  
  nav, aside {
    flex: 1;
  }
  
  main {
    flex: 3;
  }

  /* demo styles */
  .box {
  border: 3px solid;
  padding: 16px;
}

  header.box {
    border-color: hsl(45deg 100% 50%);
    background-color: hsl(45deg 100% 50% / 0.2);
  }
  nav.box {
    border-color: hsl(170deg 100% 35%);
    background-color: hsl(170deg 100% 35% / 0.2);
  }
  main.box {
    border-color: hsl(220deg 100% 50%);
    background-color: hsl(220deg 100% 50% / 0.2);
  }
  aside.box {
    border-color: hsl(300deg 100% 45%);
    background-color: hsl(300deg 100% 45% / 0.2);
  }
  footer.box {
    border-color: hsl(350deg 100% 60%);
    background-color: hsl(350deg 100% 60% / 0.2);
  }

  body {
    padding: 0;
  }

  * {
    box-sizing: border-box;
  }
  
</style>

<div class="wrapper">
  <header class="box">Header</header>
  <section class="middle">
    <nav class="box">Nav</nav>
    <main class="box">Main Content</main>
    <aside class="box">Ad unit</aside>
  </section>
  <footer class="box">Footer</footer>
</div>

```

### Sticky Sidebar

```HTML
<style>
  .wrapper {
    display: flex;
  }

  nav {
    position: sticky;
    top: 0;
    border: solid deeppink;
    align-self: flex-start;
  }

  main {
    flex: 1;
  }

  /* demo styles */
  body {
  padding: 0;
}

  * {
    box-sizing: border-box;
  }

  nav, main {
    padding: 16px;
  }

  img {
    display: block;
    width: 300px;
    margin: 16px 0 64px;
  }
</style>

<section class="wrapper">
  <nav class="box">
    <h2>Navigation</h2>
    <ul>
      <li>Section One</li>
      <li>Section Two</li>
    </ul>
  </nav>
  <main class="box">
    <p>This container contains random stuff to increase its height.</p>
    <img src="/course-materials/cat-300px.jpg" />
    <p>Normally, a blog post would exist in this container.</p>
    <img src="/course-materials/dog-one-300px.jpg" />
    <p>This container contains random stuff to increase its height.</p>
    <img src="/course-materials/cat-two-300px.jpg" />
    <p>Normally, a blog post would exist in this container.</p>
    <img src="/course-materials/dog-two-300px.jpg" />
  </main>
</section>
```

### Center picture

```HTML
<style>
  .wrapper {
    width: 50vw;
    display: flex;
    flex-direction: column;
  }
  img {
    display: block;
    width: 300px;
    margin-top: 30px;
    align-self: center;
  }

  /*demo*/

  body {
  padding: 32px;
}

  * {
    box-sizing: border-box;
  }

  .wrapper {
    border: 2px solid;
    margin: 16px auto;
  }
  
</style>

<section class="wrapper">
  <p>This is a cat:</p>
  <img src="/course-materials/cat-300px.jpg" />
</section>

```

## Shoe store exercise

- Confusing ass `Flex: 1` concepts to center the header. I need to spend more time with that property. I still don't get it.
- Check out the sole-and-ankle repo for the break down.
- Very powerful flex options
- `align-items: baseline` is really cool
- And you can do so much wiht Flexbox, grid card style layout

## Module 5 - Responsive Design and Behavioral Design

- Great way to test on mobile, your device
- ngrok, software that will allow you to make a local host publicly available url.
- Just run your local site, via live-server or whatever the app is.
- Then in the terminal, run `ngrok http 3000`, the port number should match the port number of whatever app you are running.
- Then just text yourself the url, to check it out on your phone

### Media queries

- Media queries are like if statements in JS
- This one is saying, anything below 400, update the font-size

```CSS
  @media (max-width: 400px) {
    .signup-button {
      font-size: 2rem;
    }
  }
```

### With styled components

- This is how you render media queries with styled components

```CSS
const SignupButton = styled.button`
  color: deeppink;
  font-size: 1rem;

  @media (max-width: 400px) {
    font-size: 2rem;
  }
`;
```

- We can nest media queries within our component definitions.
- vs. regular media queries, grouped by viewport size.

### Mobile first vs. desktop first

- It depends, on the device you are designing for.
- `max-width` for desktop default
- `min-width` for mobile first
- pick one direction and try not to mix and match
- [Mobile Friendly Modal](https://codesandbox.io/s/exercise-mobile-friendly-modal-d2klo?file=/src/Modal.js)

### Mobile Modal

- [Reach UI](https://reach.tech/dialog)
- [Code Sandbox](https://codesandbox.io/s/exercise-mobile-friendly-modal-forked-sf7ir?file=/src/Modal.js)
- [Vanilla A11y Dialog](https://github.com/KittyGiraudel/a11y-dialog)

## Other Media Queries

- [- Interaction Media Queries](https://drafts.csswg.org/mediaqueries-4/#mf-interaction)
- [Hover on mobile demo](https://loud-magnetic-afrovenator.glitch.me/)
- What's the difference between "hover" and "pointer"? They actually refer to two distinct capabilities. hover is the ability for a device to move the cursor without also triggering a click/tap on the element underneath; a mouse can do this, but your finger or a stylus can't. pointer refers to the level of control the user has over the position of the cursor.
- [Can I use Support](https://caniuse.com/css-media-interaction)

### Hover Pointer

Mouse / Trackpad                  hover fine
Touchscreen (smartphone, tablet)  none coarse
Keyboard (focus navigation)       none none
Eye-tracking                      none fine
Basic stylus digitizers           none fine
Sip-and-puff switches             none none
Microsoft Kinect / Wii remote     hover coarse

```CSS
@media (hover: hover) and (pointer: fine) {
  button:hover {
    text-decoration: underline;
  }
}
```

### Boolean logic in media queries `and`

- `and` is essentially the same as `&&` in JS. In order for the styles to be applied, all of the queries must be satisfied.

```CSS
@media (hover: hover) and (pointer: fine) {
  /* Your Styles */
}
```

### Preference-based media queries

- can hook into and access user preferences. Tailer to user's personal preference. For example. light and dark mode.

```CSS
@media (prefers-color-scheme: dark) {
  /* Dark-mode styles here */
}
```

### Picking Breakpoint values

- Pick break points that are in device dead zones. Not the exact resolution of a device. That way you can group them into chunks.
- [Screen resolution stats](https://gs.statcounter.com/screen-resolution-stats)
- [The right way to do breakpoints](https://www.freecodecamp.org/news/the-100-correct-way-to-do-css-breakpoints-88d6a5ba1862/)
- The breakdown
0-550px — Mobile
550-1100px — Tablet
1100-1500px — Laptop
1500+px — Desktop

- Don't bother distinguishing between differ phone sizes, just group all into phone/mobile

### Implementing Breakpoints

- Decide if you are going desktop first, or mobile first.
- Desktop First

```CSS
/* Default: Desktop monitors, 1501px and up */
@media (max-width: 1500px) {
  /* Laptop */
}
@media (max-width: 1100px) {
  /* Tablets */
}
@media (max-width: 550px) {
  /* Phones */
}
```

- Mobile First

```CSS
/* Default: Phones from 0px to 549px */
@media (min-width: 550px) {
  /* Tablets */
}
@media (min-width: 1100px) {
  /* Laptop */
}
@media (min-width: 1500px) {
  /* Desktop */
}
```

- Target exclusive ranges

```CSS
@media (min-width: 550px) and (max-width: 1099.99px) {
  /* Tablet-only styles */
}
```

- Managing Breakpoints, styled components

```Java
// constants.js
// For this example, I'm going mobile-first.
const BREAKPOINTS = {
  tabletMin: 550,
  laptopMin: 1100,
  desktopMin: 1500,
}
const QUERIES = {
  'tabletAndUp': `(min-width: ${BREAKPOINTS.tabletMin}px)`,
  'laptopAndUp': `(min-width: ${BREAKPOINTS.laptopMin}px)`,
  'desktopAndUp': `(min-width: ${BREAKPOINTS.desktopMin}px)`,
}
```

- To use the breakpoint, import and interpolate the values

```JAVA
import { QUERIES } from '../../constants';
const Wrapper = styled.div`
  padding: 16px;
  @media ${QUERIES.tabletAndUp} {
    padding: 32px;
  }
`;
```

### Picking the right unit

- px's or rem's?
- rems, refresher, unit is based on the base font size. Base value of 16px, but user can adjust via browser settings
- px, when you used px base units, those setting won't change based on user browser settings
- screen size / base font size. 1100/16 = 68.75

```CSS
@media (min-width: 68.75rem) {
  /* Desktop styles */
}
```

- rem base dviewports scale with teh user's chosen default font size. As the font gets bigger, the breakpoints slide up the scale.
- this gets confusing, use [styled components](https://styled-components.com/docs) to do the math for us

```Java
// constants.js
const BREAKPOINTS = {
  tabletMin: 550,
  laptopMin: 1100,
  desktopMin: 1500,
}
const QUERIES = {
  'tabletAndUp': `(min-width: ${BREAKPOINTS.tabletMin / 16}rem)`,
  'laptopAndUp': `(min-width: ${BREAKPOINTS.laptopMin / 16}rem)`,
  'desktopAndUp': `(min-width: ${BREAKPOINTS.desktopMin / 16}rem)`,
}
```

### One off media query

- Totally fine to have a one off occasional custom value
- A well matched set of breakpoints values should be used most of the time.

## CSS Variables

- CSS variables function exactly like CSS properties (display, color, etc). You are not setting a variable, you are creating a brand new property.

```CSS
strong {
  display: block;
  color: red;
  --favorite-food: tomato;
  --temperature: 18deg;
}
```

- Custom properties always start with two dashes (`--`), to differentiate them from built-in properties.
- No particular reason, [space jam website from 1996](https://www.spacejam.com/1996/)

### Not Global

- A common misconception is that CSS variables are global. When you attach a variable to an element. It is only available on that element and it's children.

- they are often hung on `:root`

```CSS
:root {
  --color-primary: red;
  --color-secondary: green;
  --color-tertiary: blue;
}
```

- `:root` is an alias for `html`, so by hanging them on the top level element, they become globally available.
- But you can attach CSS variables to any element, not just the root one.

### Default Values, Fallback Value

- `var` function takes two arguments, the second argument is a default value

```CSS
.btn {
  padding: var(--inner-spacing, 16px);
}
```

- If `inner-spacing` is assigned it will use that property, otherwise it will use the fallback of 16px.

### Reactive properties

- So what? We have had variables in Sass or Less for years.
- The biggest difference, these are available at runtime. Sass/Less variables are compiled away when you build the site.
- CSS variables are reactive, when their value changes, any properties that reference taht value also change.
- For example, you can click on a button to increase font size, or change a color etc.

```HTML
<style>
  button {
    font-size: var(--inflated-size);
  }
</style>

<button>Click me</button>

<script>
  let fontSize = 1;
  const button = document.querySelector('button');

  button.addEventListener('click', () => {
    fontSize += 0.25;
    button.style.setProperty(
      '--inflated-size',
      fontSize + 'rem'
    );
  });
</script>
```

### Responsive value

- You can use CSS variables for responsive design
- For example, change the size of a button on mobile for recommended min tap size, 44.44px

```JAVA
const FancyButton = styled.button`
  /* Other styles omitted for brevity */
  @media (pointer: coarse) {
    min-height: 44px;
  }
`;
```

- make a CSS variable for other elements, like input etc.
- define a global style CSS variable, `--min-tap-height`

```JAVA
const GlobalStyles = createGlobalStyle`
  @media (pointer: coarse) {
    html {
      --min-tap-height: 44px;
    }
  }
`;
```

- Then you can use this property inside a styled component

```JAVA
const FancyButton = styled.button`
  min-height: var(--min-tap-height);
`;
const TextInput = styled.input`
  min-height: var(--min-tap-height, 32px);
`;
```

- Instead of changing the individual properties in a media query. You can update the CSS variable, which will then update the default styles at runtime/realtime.
- Before being very direct, but when you specify a new value in a media query, all the `var()` keywords will re-run and discover they have a new value in the default style (mobile first or desktop first)

```HTML
<style>
  main {
    --spacing: 8px;
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: var(--spacing);
    padding: var(--spacing);
  }
  article {
    border-radius: var(--spacing);
    padding: var(--spacing);
  }

  @media (min-width: 350px) {
    main {
      /* Notice this is updating the css property, which re-runs the var keyword above */
      --spacing: 16px;
    }
  }

  @media (min-width: 500px) {
    main {
      --spacing: 32px;
    }
  }
</style>

<main>
  <article>Card 1</article>
  <article>Card 2</article>
  <article>Card 3</article>
</main>
```

### Variable Fragments

- CSS variables can be used as lego blocks.

```HTML
  <style>
  body {
    --standard-border-width: 4px;
  }

  strong {
    --border-details: dashed goldenrod;
    border:
      var(--standard-border-width)
      var(--border-details);
  }
</style>

<strong>Hello World</strong>

```

- You can combine multiple variables to form a single property value.
- The result of this property, `border: 4px dashed goldenrod`
- **This works because CSS variables are evaluated when they are used, NOT when they are defined.**
- You can take this a step further, and make Composible

```HTML

<style>
  body {
    --pink-hue: 340deg;
    --blue-hue: 275deg;
    --intense: 100% 50%;
    
    --color-primary: hsl(
      var(--pink-hue)
      var(--intense)
    );
    --color-secondary: hsl(
      var(--blue-hue)
      var(--intense)
    );
  }

  strong {
    color: var(--color-primary);
  }
  a {
    color: var(--color-secondary);
  }
</style>

<p>
  Hi <strong>Mario</strong>!
  <br />
  The princess is in <a href="">another castle</a>.
</p>

```

- This helps keep our code EDY and makes it possible to build rich structures that make it easy to tweak entire color schemes. themes.

## Dark Mode

- you can use the `prefers-color-scheme` media query to create an alternative set of colors.
- Your colors should use the dame values for `hue` and `saturation`
- This works off of your system preferences dark mode,

```CSS
 @media (prefers-color-scheme: dark) {
   /* when you change your system settings to dark mode, these styles are applied */

 }
```

- If you want to test it out , witout having to toggle system settings, then just use `prefers-color-scheme: light`, just be sure to toggle it back.
- What is the default? Light mode or dark mode

## The Magic of Calc

- CSS has the ability to do math!

```CSS
.something {
  width: calc(100px + 24px);
  height: calc(50px + 25px * 4);
}
```

- You can use 4 mathematical operators, `+ - * /`
- The real benefit of using `calc` is when we combine it with **CSS Variables**
- You can use your `--spacing` custome CSS attribute as an input, then transform it using `calc`

```CSS
article {
  --spacing: 4px;
  padding: var(--spacing);
  border-radius: calc(var(--spacing) / 2);
}
```

## Unit Conversion

- You can use `calc` to convert pixels to rems.

```CSS
h2 {
  /* 24 / 16 = 1.5 */
  font-size: 24px;
}
```

- Instead of doing the math ourselves, let `calc` do it for us

```CSS
h2 {
  font-size: calc(24 / 16 * 1rem);
}
```

## Calculating colors and gradients

- HSL color model allows us to manipulate the colors
- This seems like a bit of overkill

```HTML
<style>
:root {
  --red-hue: 0deg;
  --intense: 100% 50%;

  --red: hsl(
    var(--red-hue) var(--intense)
  );
  --orange: hsl(
    calc(var(--red-hue) + 20deg)
    var(--intense)
  );
  --yellow: hsl(
    calc(var(--red-hue) + 40deg)
    var(--intense)
  );
  --pinkred: hsl(
    calc(var(--red-hue) - 20deg)
    var(--intense)
  );
  --pink: hsl(
    calc(var(--red-hue) - 40deg)
    var(--intense)
  );
}

.row {
  display: flex;
  padding: 8px;
  gap: 8px;
}

.demo-box {
  width: 50px;
  height: 50px;
  border-radius: 4px;
}
</style>
  <div class="row">
    <div
      class="demo-box"
      style="background: var(--pink)"
    ></div>
    <div
      class="demo-box"
      style="background: var(--pinkred)"
    ></div>
    <div
      class="demo-box"
      style="background: var(--red)"
    ></div>
    <div
      class="demo-box"
      style="background: var(--orange)"
    ></div>
    <div
      class="demo-box"
      style="background: var(--yellow)"
    ></div>
</div>
```

- You can use this technique to build gradients
- Basic gradient example

```HTML
<style>
    .box {
    width: 150px;
    height: 150px;
    border-radius: 2px;
    background: linear-gradient(
      45deg,
      hsl(-30deg 100% 50%),
      hsl(30deg 100% 50%)
    );
    }
</style>

<div class="box"></div>
```

```HTML
<style>
:root {
  /*
    Try changing these values,
    to create new gradients!
  */
  --root-hue: 0deg;
  --range: 30deg;
}

.box {
  --start-color: calc(
    var(--root-hue) - var(--range)
  );
  --end-color: calc(
    var(--root-hue) + var(--range)
  );
  
  width: 150px;
  height: 150px;
  border-radius: 2px;
  background: linear-gradient(
    45deg,
    hsl(var(--start-color) 100% 50%),
    hsl(var(--end-color) 100% 50%)
  );
}
</style>

<div class="box"></div>
```

- Playground, fun with gradients

```HTML
<style>
  html {
    --box-size: 75px;
  }

  .box {
    width: var(--box-size);
    height: var(--box-size);
    /*
      Here's a quick example, to get you started!
      We use “--index”, a number from 1 to 16,
      to derive the “hue” for each square.
      
      If you're not sure where to start,
      try tweaking these numbers!
      
      One last tip: using a gradient instead
      of a solid color opens lots of exciting
      possibilities!
    */
    /*
    background: hsl(
      calc(var(--index) * -7deg) 100% 50%
    );
    */
    background: linear-gradient(
      45deg,
      hsl(calc(var(--index-start) * -7deg) 100% 50%),
      hsl(calc(var(--index-end) * -7deg) 100% 50%)
    );
  }

  .row {
    display: flex;
    flex-wrap: wrap;
    width: calc(var(--box-size) * 4);
    height: calc(var(--box-size) * 4);
  }

  /*
    Attach a unique index to each box.
    Normally, we would do this in JS.
  */
  .box:nth-of-type(1) {
    --index-start: 12;
    --index-end: 32;
  }
  .box:nth-of-type(2) {
    --index-start: 4;
    --index-end: 332;
  }
  .box:nth-of-type(3) {
    --index-start: 1;
    --index-end: 6;
  }
  .box:nth-of-type(4) {
    --index-start: 6;
    --index-end: 8;
  }
  .box:nth-of-type(5) {
    --index-start: 112;
    --index-end: 322;
  }
  .box:nth-of-type(6) {
    --index-start: 132;
    --index-end: 332;
  }
  .box:nth-of-type(7) {
    --index-start: 132;
    --index-end: 5;
  }
  .box:nth-of-type(8) {
    --index-start: 6;
    --index-end: 5;
  }
  .box:nth-of-type(9) {
    --index-start: 7;
    --index-end: 2;
  }
  .box:nth-of-type(10) {
    --index-start: 7;
    --index-end: 9;
  }
  .box:nth-of-type(11) {
    --index-start: 6;
    --index-end: 3;
  }
  .box:nth-of-type(12) {
    --index-start: 8;
    --index-end: -32;
  }
  .box:nth-of-type(13) {
    --index-start: -112;
    --index-end: 7;
  }
  .box:nth-of-type(14) {
    --index-start: 44;
    --index-end: -32;
  }
  .box:nth-of-type(15) {
    --index-start: 6;
    --index-end: 1;
  }
  .box:nth-of-type(16) {
    --index-start: 6;
    --index-end: 300;
  }
  * {
    box-sizing: border-box;
  }
  </style>

  <div class="row">
    <div class="box"></div>
    <div class="box"></div>
    <div class="box"></div>
    <div class="box"></div>
    <div class="box"></div>
    <div class="box"></div>
    <div class="box"></div>
    <div class="box"></div>
    <div class="box"></div>
    <div class="box"></div>
    <div class="box"></div>
    <div class="box"></div>
    <div class="box"></div>
    <div class="box"></div>
    <div class="box"></div>
    <div class="box"></div>
 </div>
```

## Viewport Units

- Every value that you might think to use, like 24px or 10%, has a type. It might be a `<lenght>` or a `<color>`.
- Teh `<lenght>` type is one of the most common. Properties like `<width>` or `<padding>` accept `<lenght>` values, and it contains units like px or em or rem.
- It also includes viewport units
- THERE ARE TWO MAIN VIEWPORT UNITS:
  - `vw` viewport width
  - `vh` viewport height
- `1vw` is equivalent to 1% fo the viewport width. For example.

```CSS
  .box {
    width: 10vw; /* 10% of the viewport width */
    height: 25vh; /* 25% of the viewport height */
  }
```

- You can use these units with teh width adn height properties
- But really cool thing, is we can use them with any property that accepts `<lenght>` units.
- For example, the distance between letters

```HTML
<style>
  .heading {
  letter-spacing: 2vw;
}
</style>
<h2 class="heading">Resize me!</h2>
```

## The mobile height issue

- The `vh` unit is often used to solve an annoying problem: making sure that an element is exactly as tall as the viewport. No taller, no shorter
- Unfortunately, this doesn't work on mobile.
- Modern mobile browsers have two views, and "expanded" view when the page is loaded.
  - Expanded view, when the webpage is loaded, the address bar is tall and buttons at the bottom.
  - Slide away view, making more room for content as users scroll.
- `vh` unit **always refers to the largest possible height**. The slide away view.
- So if you set an element to `100vh`, it won't fit on the screen.
- [See Demo](https://courses.joshwcomeau.com/demos/full-height-vh)
- **How to work around this?**
- You can use a JS based solution to change how `vh` units work. Not recommended unless you really really need it.
- [viewport-units-buggyfill](https://github.com/rodneyrehm/viewport-units-buggyfill)
- PREFERRED - use the [percent-based trick from Module 1](https://courses.joshwcomeau.com/css-for-js/01-rendering-logic-1/11-height), passing percentages down so that they can be usdd wher eyou need them.
- Tweak designs so that they don't need to fill the viewport exactly.

## The desktop scrollbar issue

- `vw` unit it's problems
- It refers to the viewport width NOT counting the scrollbar
- On mobile , this is fine because the scrollbar floats transpacent above the content
- On desktop, the scrollbar takes up it's own space, within the viewport. The exact width depents on the platform and styling.
- This means that if we set an element to stretch 100vw, and our scrollbar is 15px wide. We will end up with 15px of horizontal overflow.
- [See desktop example](https://courses.joshwcomeau.com/demos/100vw)
- MacOS treats scroll bars a little differ. It hides them by default. You have to update your system preferences to show always. System Preferences/General/Show scroll bars

## Tracking the scrollbar width

- Using some JS, you can calculate the amount of space eaten up my scrollbar with the following

```JS
const scrollbarWidth = window.innerWidth - document.documentElement.clientWidth;
```

- `window.innerWidth` refers to the viewport width, it doesn't care about scrollbars.
- `documentElement.clientWidth` refers to the usable space within the document.

- For example; our window is 500px wide and scrollbar taking up 20px. `window.innerWidth` wil be 500 and `clientWidth` will be 480. By subtracting we get teh difference of 20

- Now that we knwo how wide the scrollbar is, we can assign it to a CSS variable

```JS
document.documentElement.style.setProperty(
  '--scrollbar-width',
  `${scrollbarWidth}px`,
);
```

- By attaching the CSS variable to teh `documentElement`, ew make it globally available, same thing as targeting `html` in CSS
- Then, we can use `calc` to work the `vw` units without worrying about scrollbars

```CSS
.wrapper {
  width: calc(100vw - var(--scrollbar-width));
}
```

- You can take this a step further by assigning that `calc` expression to a variable.

```CSS
html {
  --full-width: calc(100vw - var(--scrollbar-width));
}

.wrapper {
  width: var(--full-width);
}
```

- To prevent scrollbar popping up when dynamic content loads. You can pre-emptively set it

```CSS
  body {
    overflow-y: scroll;
  }
```

- This is a good practice, prevents layout shifts

## Clamping Values

- `clamp` take 3 values:
- The minumum value
- The ideal value
- The maximum value

- Works like the seperate properties of `mind-width`, `width` and `max-width`, and combines into a single property value
- The two rules below are functionally identical

```CSS
/* Method 1 */
.column {
  min-width: 500px;
  width: 65%;
  max-width: 800px;
}
/* Method 2 */
.column {
  width: clamp(500px, 65%, 800px);
}
```

- By moving built in constraints to clamp, we free up `max-width`. This solution combines them

```CSS
.column {
  width: clamp(500px, 65%, 800px);
  max-width: 100%;
}
```

- In the snippet, we are applying two maximum widths `800px` and `100%`. Our `.column` element will never be larger then 800px or 100% of available space.
- `clamp` can be used with any property

## Min and Max

- There are `min` and `max` functions we can use as well

```CSS
  .box {
    padding: min(32px, 5vw);
  }
```

- This works jsut like `Math.min` in JS, it evaluates to whichever value is smaller
- In this example, our `.box` will have dynamic padding athta scales with the viewport width, but only until it reaches 32px, no larger then that

## Scrollburglars

- Growth Mindset and product failure
- Front loading the exercise, being asked to solve a problem before we've covered the technique.
- Why would Josh ask you to try and solve a problem you won't be able to solve?
- BECAUSE THEIR IS VALUE IN THE PROCESS. Struggling with a problem si teh best way to ensure that you learn.
- If you start with the explanation, and you breeze through  the exercises, that knowledge is less likely to be absorbed.
- This is known as [productive failure](https://www.nature.com/articles/s41539-019-0040-6)
- In productive failure, the conventional instruction process is reversed so that learners attempt to solve challenging problems ahead of receiving explicit instruction. While students often fail to produce satisfactory solutions, these attempts help learners encode key features and learn better from subsequent instructions.
- Khan Academy - [Growth Mindset](https://www.khanacademy.org/ela/cc-4th-reading-vocab/x5ea2e43787f7791b:cc-4th-growth-mindset/x5ea2e43787f7791b:building-knowledge/a/growth-mindset--unit-intro-4)

## Exercise 01-recut

- horizontal scrollbar present, because of image overflow issues
- great way to solve for that, `min` property
- `min-width: min(28rem, 100%)`
- pass two values, and it will pick the smallest one
- as the window gets smaller, it will use the smaller of the two values.
- Two different `max-width` that apply in two differ situations.
  - on small screens, we would like the max width to be 100%
  - on larger screens, that moment that max width is bigger then 28rem we want to stop it from growing any larger.
- use the `min()` keyword, it will pick the smallest value and pick that

## Exercise 02-warp and weave

- to apply a global fix, you can use `overflow: hidden`, however, if you have a position sticky or fixed further down in the DOM, it will not work.
- but sometimes you want some overlow for artistic affects.

## CSS samples

- Hero element wall to wall photo

```CSS
.hero {
  background: url('/course-materials/night-sky.jpg');
  background-size: cover;
  background-position: bottom center;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  text-align: center;
  text-shadow: 0px 0.3em 1em hsl(295deg 100% 10%);
```

- Stretched Card, make an element stretch wall to wall in it's container, just apply negative margins and put img at 100%

```HTML
<style>
  body {
  background: #222;
  padding: 32px;
}

.card {
  background-color: white;
  padding: 32px;
  border-radius: 8px;
}

.stretch {
  margin-left: 32px;
  margin-right: 32px;
}

img {
  display: block;
  width: 100%;
}

p, img {
  margin-bottom: 16px;
}
</style>

<div class="card">
  <p>
    Otters have long, slim bodies and relatively short limbs. Their most striking anatomical features are the powerful webbed feet used to swim, and their seal-like abilities holding breath underwater.
  </p>
  <div class="stretch">
   <img alt="A cute otter in water" src="/course-materials/otter.jpg" />
  </div>
  <p>
    More importantly, otters are glorious water dogs, playful and curious. The otter, no other, is the best animal.
  </p>
</div>
```

- Decorative Effect, [blob background](https://courses.joshwcomeau.com/css-for-js/02-rendering-logic-2/08-reducing-z-index)

- Sticky nav items, [make your sections stick with content](https://courses.joshwcomeau.com/css-for-js/02-rendering-logic-2/15-sticky)

- CREATE A DECORATIVE ELEMENT AND SKEW IT.
- Check out `skew()` property. You can do both x and y axis. [MDN Skew](https://developer.mozilla.org/en-US/docs/Web/CSS/transform-function/skew())

```HTML
<style>
h2 {
  position: relative;
  font-size: 2rem;
  font-weight: bold;
  margin-bottom: 16px;
  margin-top: 48px;
}

.heading-decoration {
  position: absolute;
  top: -25px;
  right: 0px;
  width: 75px;
  height: 75px;
  background: papayawhip;
  opacity: 1;
  transform: translateX(12px) skew(-24deg);
}

.heading-content {
  position: relative;
}
</style>
<h2>
  <span class="heading-decoration"></span>
  <span class="heading-content">
  Evaluating friendliness
  </span>
</h2>
```

## Exercise 03 - Blog

- Decorative element, parallelogram, on an element
- Add overflow hidden to the main, but introduces new problem.
- If you use position sticky on any ancestor element, it will no longer be sticky, social media icons in this case.
- Position sticky follow the scroll for a moment then becomes fixed, it starts relative and then becomes fixed.
- Position fixed doesn't have the same limitation with overflow hidden.
- An alternative, is to use media queries to change the element to overflow hidden

## Responsive Typography

- We generally want our font size to be 16px, anything less and users have to strain to read, or slows down comprehension.
- [Important Facts about reading](https://www.smashingmagazine.com/2011/10/16-pixels-body-copy-anything-less-costly-mistake/#important-facts-about-reading), Smashing Magazine
- Fun Fact, most web apps use the same font size regardless of display size. Facebook and Twitter and Google stick to the same font size, `16px` no matter how big the screen gets.
- Font size units, dont' use absolute units like `px`
- So taht users can pick a default font size in the browser
- When we say the font size should be `16px`, what we are really saying is that it should be `1rem`.
- `rem` is unit relative to teh root font size, which defaults to `16px` in all browsers

### Small text

- We also have small text for labels and captions
- Ok to reduce the size if the text is unimportant

```CSS
figcaption {
  font-size: 0.75rem;
  text-align: center;
  padding-top: 8px;
}
```

### Form Fields

- `input` and `select` field sare small by default. Hard to read on mobile devices.
- To compensate, iOS Safari will automatically zoon in to focus on form fields and small text. It makes the text eaier to read, but is tendious and harder to navigate the page
- The fix, is to just set all fields to 16px, then Safai wil no longer zoom.

```CSS
input, select, textarea {
  font-size: 1rem;
}
```

## Headings

- Headings need a differ approach from desktop to mobile
- Typically you can use media queries to reduce the font size

```CSS
h1 {
  font-size: 2.5rem;
}
@media (max-width: 550px) {
  h1 {
    font-size: 1.75rem;
  }
}
```

- Another option, is to use a fluid value to scale more smoothly

### Fluid Typography

- The idea behind fluid typography instead of creating discrete font size breakpoints, it scales smoothly based on viewport size.
- This is done with the `vw` unit
- [MDN](https://developer.mozilla.org/en-US/docs/Learn/CSS/Building_blocks/Values_and_units), `vw` is 1% of viewport width
- Neat trick but two problems, sizes get ridiculous on small and large screens.

```HTML
<style>
h1 {
  font-size: 6vw;
  margin-bottom: 0.5em;
}
</style>
<main>
  <h1>
    This is a fluid headline!
  </h1>
  <p>
    The heading will grow and shrink with the viewport.
  </p>
</main>
```

- We can solve this problem with the `clamp` to set bounds for big and small

```HTML
<style>
  h1 {
    font-size: clamp(1.5rem, 6vw, 3rem);
    margin-bottom: 0.5em;
  }
</style>
<main>
  <h1>
    This is a fluid headline!
  </h1>
  <p>
    The heading will grow and shrink with the viewport.
  </p>
</main>
```

- `clamp` lets us set a a hard boundary. In this example, text will always be between 1.5rem and 3rem, no matter what the viewport size is.
- The only problem is, you introduce an accessibility violation. WCAG, says that text should be scalable up to 200%.
- All kinds of crazy calc functions to get this to work. Not worth it.
- Use it responsibly, good for headings and decorative, but not body text.

### Fluid Calculator

- You can change the rate at which something changes.
- The trick is that e can play with the ratio between viewport and relative units.

```HTML
<style>
.fluid {
  font-size: clamp(
    2rem,
    5vw + 1rem,
    5rem
  );
}
.fluid-fast {
  font-size: clamp(
    2rem,
    14vw - 1.5rem,
    5rem
  );
}
</style>

<h2 class="fluid">Fluid Text</h2>
<h2 class="fluid-fast">Fluid Text</h2>
```

- Check out Josh's [fluid calculator](https://courses.joshwcomeau.com/css-for-js/05-responsive-css/16-fluid-calculator)
- You can also use fluid technique for spacing elements, for example a menu bar item, get the proportions you want from Josh's calculator.

```HTML
<style>
  /* template */
  ul {
    justify-content: center;
    list-style-type: none;
    padding: 0;
    margin: 0;
  }

  a {
    color: black;
    font-weight: 700;
    text-decoration: none;
  }

  a:hover {
    text-decoration: underline;
  }
  ul {
    display: flex;
    gap: clamp(
      1rem,
      11.7vw - 2rem,
      5rem
    );
  }
</style>

<nav>
  <ul>
    <li>
      <a href="/">News</a>
    </li>
    <li>
      <a href="/">Classifieds</a>
    </li>
    <li>
      <a href="/">Opinion</a>
    </li>
  </ul>
</nav>
```

## Fluid Design

- The responsive vs. fluid dynamic isn't just a typography thing; becoming increasingly common to use Flexbox/Grid to build "fluid layouts" instead of defining concrete breakpoints.
- Example of the two [side by side](https://courses.joshwcomeau.com/css-for-js/05-responsive-css/17-fluid-design)
- Each approach has differ pros and cons depending on what you want to accomplish. Example below.

```HTML
<style>
  /* TEMPLATE */
  .wrapper {
    padding: 8px;
    background: white;
    border-radius: 8px;
    margin: 16px 0;
  }

  .description {
    padding: 5px 16px 8px 8px;
  }

  .description h2 {
    margin-bottom: 8px;
  }

  .bibliography {
    background: hsl(250deg 20% 90%);
    padding: 8px;
    padding-left: 32px;
    border-radius: 0 4px 4px 0;
  }

  .bibliography ul {
    margin: 0;
    padding: 0;
  }

  .bibliography li {
    margin-bottom: 8px;
  }

  .bibliography a {
    color: hsl(250deg 100% 50%);
    text-underline-offset: 3px;
  }

  body {
    background: hsl(250deg 20% 20%);
  }
  /* RESPONSIVE APPROACH */
  .wrapper {
    display: flex;
  }
  .description {
    flex: 1;
  }
  .bibliography {
    flex: 1;
  }
  
  @media (max-width: 32rem) {
    .wrapper {
      flex-direction: column;
    }
    .bibliography {
      border-radius: 0 0 4px 4px;
    }
  }
  
  /* FLUID APPROACH */
  /*
  .wrapper {
    display: flex;
    flex-wrap: wrap;
  }
  .description {
    flex: 1;
    min-width: 15rem;
  }
  .bibliography {
    flex: 1;
    min-width: 20rem;
  }
  */
</style>

<div class="wrapper">
  <div class="description">
    <h2>Becky Chambers</h2>
    <p>
      Becky Chambers is an American science fiction writer, and the author of the Hugo-award winning Wayfarers series. She is known for her imaginative world-building and character-driven stories.
    </p>
  </div>
  <nav class="bibliography">
    <ul>
      <li>
        <a href="/">
          A Psalm For The Wild-Built
        </a>
      </li>
      <li>
        <a href="/">
          The Galaxy, And The Ground Within
        </a>
      </li>
      <li>
        <a href="/">
          To Be Taught, If Fortunate
        </a>
      </li>
    </ul>
  </nav>
</div>
<div class="wrapper">
  <div class="description">
    <h2>John Scalzi</h2>
    <p>
      John Michael Scalzi II is an American science fiction author and former president of the Science Fiction and Fantasy Writers of America. He is best known for his Old Man's War series, three novels of which have been nominated for the Hugo Award.
    </p>
  </div>
  <nav class="bibliography">
    <ul>
      <li>
        <a href="/">
          Old Man's War
        </a>
      </li>
      <li>
        <a href="/">
          Questions For A Soldier
        </a>
      </li>
      <li>
        <a href="/">
          The Ghost Brigades
        </a>
      </li>
    </ul>
  </nav>
</div>
```

## Advanced Flex Techniques

- You can use Flexbox to integrate some impressive tricks.
- This for example, [4 differ layout supported](https://courses.joshwcomeau.com/css-for-js/05-responsive-css/17-fluid-design).

## Workshop, add responsiveness to Sole & Ankle site

### Exercise 1, set up our breakpoints

- Add pre-defined breakpoints to the project.
- Convert them to relative units so the breakpoints scale with the browser settings
- Add it to a constants.js file and import it into your app

```Java
// CD - Add the breakpoints in px
export const BREAKPOINTS = {
  phone: 600,
  tablet: 950,
  laptop: 1300,
};

// CD - Create a query to convert to rems and make it easier to write/call
// To covert anything to rems, just divide by 16. Rems or relative units, allow the design to scale when users change their font size preferences.
export const QUERIES = {
  phoneAndSmaller: `(max-width: ${BREAKPOINTS.phone / 16}rem)`,
  tabletAndSmaller: `(max-width: ${BREAKPOINTS.tablet / 16}rem)`,
  laptopAndSmaller: `(max-width: ${BREAKPOINTS.laptop / 16}rem)`,
};
```

### Exercise 2: Mobile Header

## Exercise 6: CSS variables Benefits

- [Link to workshop](https://courses.joshwcomeau.com/css-for-js/05-responsive-css/19-workshop-solution)
- Using a platform standard, vs custom
- Easier to migrate if we need to use a differ tool in the fugure
- Easier to build differ color themes, we can swap out
- Being able to compose them in differ ways
- Strategy for interpellating the colors
- Use `hsl` format
- In your constants file, just use the values

```JS
export const COLORS = {
  white: '0deg 0% 100%',
  gray: {
    100: '185deg 5% 95%',
    300: '190deg 5% 80%',
    500: '196deg 4% 60%',
    700: '220deg 5% 40%',
    900: '220deg 3% 20%',
  },
  primary: '340deg 65% 47%',
  secondary: '240deg 60% 63%',
};
```

- Then within your `globalStyles.js`, import your constants.js and then create css variables.

```JS
html {
  --color-white: hsl(${COLORS.white});
  --color-primary: hsl(${COLORS.primary});
  --color-secondary: hsl(${COLORS.secondary});
  --color-gray-100: hsl(${COLORS.gray[100]});
  --color-gray-300: hsl(${COLORS.gray[300]});
  --color-gray-500: hsl(${COLORS.gray[500]});
  --color-gray-700: hsl(${COLORS.gray[700]});
  --color-gray-900: hsl(${COLORS.gray[900]});

  --color-backdrop: hsl(${COLORS.gray[700]} / 0.8);
}
```

## Module 6 - Typography and Images

- The secrets of text rendering, from kerning to rasterization
- Understanding and managing text overflow, and how to do single-line and multi-line ellipses.
- Two alternative layout modes: floats and columns
- Web fonts, and how to optimally load them for the best user experience
- Variable fonts, a magical new font format
- The best icon solutions in a modern JS context
- Responsive image-handling with srcset and the <picture> element
- Modern image formats like .avif, and how to use them while still supporting all browsers.
- Customizing image placement using object-fit and object-position
- The intersection of images and Flexbox, and how to sidestep common issues

### Kerning

- Kerning refers to the spacing between individual characters. Characters are nudged left or right so they feel right. Half art and half science.
- In CSS we can disable kerning `font-kerning: none`, but have no fine-grained control.
- `letter-spacing` allows us to increase/decrease space between individual characters, acts as a kerning multiplier, amplifies whatever krning the browser decides on.

### Text Rasterization

- The browsers operating system also affects how typography is rendered.
- Rasterization and anti-aliasing, bitmap vs. vector fonts
- Bitmap fonts, old school where each letter is a bitmap
- Vector font ost common format, ttf, otf, svg, woff/woff2.
- Main benefit of vector, it can be scaled to any size without letters becoming pixellated and blurry.
- But in order to take vector font onto the screen, browser has to figure out which color to make each pixel, process known as rasterization.
- This produce pixellated text, to make it appear smooth, the browser can apply anti-aliasing

### Font Smoothing

- `-webkit-font-smoothing` property
- Allows us to switch which aliasing algorithm the browsers use.
- But only works on MacOS, and only on Chrome/Safari/Edge (not Firefox)
- Lots of history on browsers

## Text Overflow

- Browser groups characters in to words
- Words are seperated by braking characters
- Called soft wrap opportunities. Each whitespace character is a soft wrap opportunity.
- When content would sipll outside teh containing block, browser looks for soft wrap opportunity

### Widows

- The current browser algorythm can cause widows.
- Adobe has made a CSS proposal to suppo rt an alternative text-placement algorithm. JS [polyfill](https://opensource.adobe.com/balance-text/demo/index.html).

- Waht happens it a single word is to long to fit in the container?
- The browser can only split based on "soft wrap opportunities", and the word `asdfdsafasdfsafadssad` has none.
- `overflow: auto`, to make is scroll
- `overflow: hidden` to truncate

### Wrapping on multiple lines

- With the `overflow-wrap` property, we can linewrap longer words/strings
- `overflow-wrap: break-word` tweaks the text placing algorithm. IF the browser cannot fit the current workd, and doesn't ahve any spare sofft wrap opportunies, this decloration gives teh browser persmissoin to break after any character.

```html
<style>
  .wrapper {
    border: 2px solid;
    padding: 16px;
  }
  p:not(:last-of-type) {
    margin-bottom: 1em;
  }
  p {
    overflow-wrap: break-word;
  }
</style>

<div class="wrapper">
  <p>
    This is a narrow column of text, with a very long word: antidisestablishmentarianism.
  </p>
  <p>
    The same problem happens with URLs: https://www.somewebsite.com/articles/a1b2c3
  </p>
</div>
```

### Hyphenation

- `overflow-wrap: break-word` splits long words across multiple lines without any visual indication.
- In print media, we would add a hyphen
- A hyphen is a dash character used to join two segments of the same word
- Adding hyphens is not part of the text-placement algorightm, but we can add it in with teh hyphens property.

```html
<style>
  p {
    overflow-wrap: break-word;
    hyphens: auto;
    
    /* Prefix for Safari */
    -webkit-hyphens: auto;
  }
</style>
```

- For best results, combine `hyphens` with `overflow-wrap`
- Hyphens may not always show up but the layout will not break
- Text selection, hyphens are not selectable. So URLs can be copy/pasted

### Ellipsis

- Another strategy is to trail off, leaving the sentence unfini...
- You need to use `overflow: hidden` in order for `text-overflow: ellispsis` to work.

```html
<style>
  p {
    overflow: hidden;
    text-overflow: ellipsis;
  }
</style>

<div class="wrapper">
  <p>
    This is a narrow column of text, with a very long word: antidisestablishmentarianism.
  </p>
  <p>
    The same problem happens with URLs: https://www.somewebsite.com/articles/a1b2c3
  </p>
</div>
```

### Single Line ellipsis

- When you want to prevent line wrapping, and add an ellipsis if the string can't fit on single line.
- `white-space: nowarp`
- For example, if you have a table, and want to truncate strudnes withlonger names.
- The overflow management kids in after the line-breaking algorithm.
- First the browser figures out where to put the line breaks. Then it figures out what to do about the overflow.
- In order to truncate the content, we need to disable line-wrapping altogether. We do that with `white-space: nowrap`
- Always consider the usability aspects, when truncating, is the user familiar with the values.

```CSS
tbody th {
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
  max-width: 250px;
}
```

### Multi-line ellipsis

- If you want to show a few short lines then add an allipsis afterwards.
- Modern way to solve this, with `-webkit-line-clamp` property.
- Works in all major brosers, but does requite some additional declarations

```HTML
<style>
  p {
    display: -webkit-box;
    -webkit-box-orient: vertical;
    -webkit-line-clamp: 3;
    overflow: hidden;
    margin-bottom: 1em;
  }
  main {
    border: solid;
    margin: 0 auto;
    padding: 16px;
  }
</style>

<main>
  <p>
    No matter how long this paragraph is, only 3 lines will be shown, the rest concealed, and an ellipsis character will be added to demonstrate that there is more text that is not shown here.
  </p>
  <p>
    Short paragraphs don't get an ellipsis.
  </p>
</main>
```

- Watch out, can be buggy with Flex/Grid. Will show thin slices of truncated text below the ellipsis
- To avoid this issue, apply clamping to the tag that isn't being used as part of flex/grid. You can always solve by putting a wrapper div

## Print-style Layouts
