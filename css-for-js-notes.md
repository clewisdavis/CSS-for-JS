
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

```HTML
<style>
html, body {
  height: 100%;
}
.wrapper {
  min-height: 100%;
  border: solid;
}
</style>

<div class="wrapper">
  <p>
    I fill the viewport now!
  </p>
</div>
```

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

```CODE
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

```CODE
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
- For example, if you have a table, and want to truncate students with longer names.
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

- What if you wanted to layout a page like print, in multiple columns?
- You would use an additional layout mode, Multi-Column Layout
- This layout mode can automatically split content across multiple columns, in a manner that allows the parent container to grow and shrink.
- Tweak the sample blow to 3 columns. It breaks it into three columns.

```HTML
<style>
  .wrapper {
  columns: 2;
  column-gap: 16px;
  padding: 16px;
}

p {
  margin-bottom: 16px;
}
</style>
<main class="wrapper">
  <p>
    Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since the 1500s, when an unknown printer took a galley of type and scrambled it to make a type specimen book.
  </p>
  <p>
    It has survived not only five centuries, but also the leap into electronic typesetting, remaining essentially unchanged. It was popularised in the 1960s with the release of Letraset sheets containing Lorem Ipsum passages, and more recently with desktop publishing software like Aldus PageMaker including versions of Lorem Ipsum.
  </p>
  <p>
    Contrary to popular belief, Lorem Ipsum is not simply random text. It has roots in a piece of classical Latin literature from 45 BC, making it over 2000 years old.
  </p>
  <p>
    Richard McClintock, a Latin professor at Hampden-Sydney College in Virginia, looked up one of the more obscure Latin words, consectetur, from a Lorem Ipsum passage, and going through the cites of the word in classical literature, discovered the undoubtable source.
  </p>
  <p>
    Lorem Ipsum comes from sections 1.10.32 and 1.10.33 of "de Finibus Bonorum et Malorum" (The Extremes of Good and Evil) by Cicero, written in 45 BC. This book is a treatise on the theory of ethics, very popular during the Renaissance. The first line of Lorem Ipsum, "Lorem ipsum dolor sit amet..", comes from a line in section 1.10.32.
  </p>
</main>
```

- If you want to make sure a child isn't broken across columns, you can use `break-inside: avoid;`
- This will prevent the layout algorithm from splitting the paragraph across multiple columns.

```CSS
p {
  break-inside: avoid;
}
```

## Floats

- Floats are old school, web of the 00's / early 10s. Damn I feel old.
- Flexbox pretty much took over floats, much more elegant solution
- But Floats still have a place on the web.
- Floats allow content to wrap around an embedded element. Text wrapping around an image.
- Floated elements is like a boulder in a stream, all teh other content flows smoothly around it.
- And you can change the side with `left` or `right` property.
- Add a little margin to the element to create a little space.

```HTML
<style>
  img {
    float: left;
    margin-right: 16px;
  }
</style>

<p>
  Lorem Ipsum is simply dummy text of the printing and typesetting industry.
  Lorem Ipsum has been the industry's standard dummy text ever since the 1500s, when an unknown printer took a galley of type and
  scrambled it to make a type specimen book.
</p>
<img src="/course-materials/cat-300px.jpg" />
<p>
  It has survived not only five centuries, but also the leap into electronic typesetting, remaining essentially unchanged. It was popularised in the 1960s with the release of Letraset sheets containing Lorem Ipsum passages, and more recently with desktop publishing software like Aldus PageMaker including versions of Lorem Ipsum.
</p>
<p>
  Contrary to popular belief, Lorem Ipsum is not simply random text. It has roots in a piece of classical Latin literature from 45 BC, making it over 2000 years old.
</p>
```

## Indentation

- Like reading books, the first line of each paragraph is inset. So our eyes can distiguish one paragraph from another.
- On the web, we can accomplish this in a couple ways.
- pseudo element selector of the first word, `:first-letter` and a bit of margin.
- Useful for drop caps effects

```HTML
<style>
p::first-letter {
  margin-left: 2rem;
}

p {
  max-width: 500px;
  margin: 0 auto;
}
</style>
<p>
  This is a paragraph that has been indented, using the <em>first-letter</em> pseudo-element. Normally, we can't apply CSS directly to text, but this pseudo-element acts as an invisible "span" that wraps around the first character.
</p>
<p>
  Indentation isn't super common on the web, but it's everywhere in print media! Most published books will use indentation like this, and will only add space between paragraphs at the end of a "section" or sub-chapter.
</p>
```

- Or, use th  `text-indent` CSS property

```CSS
p {
  text-indent: 2rem;
}

p {
  max-width: 500px;
  margin: 0 auto;
}
```

## Justified alignment

- In print, common for text to be justified, spacing between each word is tweaked so that heach line fill the available horizontal space.

```HTML
<style>
  p {
    text-align: justify;
    padding: 16px;
  }
</style>

<p>
  This paragraph has been justify-aligned. The goal with justify-aligned text is to create a sharp block of text that aligns both on the left and right edges. It accomplishes this goal by tweaking the spacing between each word. Historically, this process was painstakingly done by typographers, using their intuition and a hearty amount of hyphens to create well-formatted text.
</p>
```

- Good book reference on [Typogrpahic styles](https://www.goodreads.com/book/show/44735.The_Elements_of_Typographic_Style)

## Exercise, Creating a Book

- Create a book layout with these techniques
- Initial Letter, in the future drop caps will be a single CSS property `initial-letter: 2;` 2 is number of lines to span

```HTML

<style>
.wrapper {
  max-width: 64rem;
  margin: 32px auto;
  border: 2px solid hsl(35deg 10% 40%);
  
  columns: 2;
  column-gap: 152px;
  padding: 50px;
  background: linear-gradient(
    to right,
    hsl(35deg, 30%, 90%),
    hsl(35deg, 30%, 90%) 47%,
    hsl(35deg, 30%, 70%) 49.5%,
    hsl(35deg, 20%, 50%) 50%,
    hsl(35deg, 30%, 70%) 50.5%,
    hsl(35deg, 30%, 90%) 53%,
    hsl(35deg, 30%, 90%)
  );
}

h2 {
  margin-bottom: 2em;
  font-size: 2rems;
}

p {
  text-align: justify;
}

p:not(:first-of-type) {
  text-indent: 2em;
}

p:first-of-type:first-letter {
  color: red;
  font-size: 3em;
  float: left;
  line-height: 1em;
  margin-right: 0.2em;
}

* {
  font-family: 'Merriweather', serif;
}
</style>

<main class="wrapper">
  <h2>Chapter 1</h2>
  <p class="drop-cap">
    Outside the space-warp chamber, Rizal's great green sun had already set. Thick olive dusk eddied through the interplanetary transit center. I swore under my breath and slammed shut the warp-hatch switch.
  </p>
  <p>
    Locking bars whispered back. The hatch revolved on its axis, slow as an asteroid eroding. I threw another quick glance at my chrono. It still read the same as before: six Earth hours more… six hours to ferret out the truth or be forever reconditioned.
  </p>
  <p>
    —Six hours, that is, if Controller Alfred Kruze didn't cut it shorter.
  </p>
  <p>
    And if he did, Rizal might very well change status. Today, it was billed as the FedGov's outermost bastion against the Kel. Tomorrow, it could prove man's fatal flaw, the Achilles heel in our whole system of defenses.
  </p>
  <p>
    In which case—
  </p>
  <p>
    Involuntarily, I shivered.
  </p>
  <p>
    “Agent Traynor—?”
  </p>
  <p>
    The voice came from the shadows. A dull, phlegmatic, tranquilized, conditioned voice. I stopped short; turned fast. “Who's asking?”
  </p>
  <p>
    The man shrugged stolidly, not even picking up my tension. “I'm a port rep, Agent Traynor. Port rep second, that is—”
  <p>
    “So who told you to come out here? Who said you should meet me?”
  </p>
  <p>
    “Oh…” A pause. “Well, you see, there's this sigman, Agent Traynor. Up in the Interworld Communications section. He had a regular 7-D clearance report that a FedGov Security investigation agent was warping in—you have to file a 7-D on all warpings, you know, Agent Traynor, on account of restrictives. So—well, the rep first was out to eat, so I just notified Rizal Security, just a routine report, and the unit controller there, an Agent Gaylord, he said for me to meet you, and—”
  </p>
  <p>
    I bit down hard and shifted my weight, both at once, wondering if a broken jaw would interfere with the work of a port rep second.
  </p>
  <p>
    Only then, all at once, I caught the unmistakable whish of a grav-car sweeping in.
  </p>
  <p>
    The lights hit us almost in the same instant. Two seconds later a man who said he was Agent Gaylord was jumping down and locking wrists with me in Rizal's traditional greeting.
  </p>
  <p>
    Even that wrist-lock set my teeth on edge. It was too solid, too stolid, too thorough a job of conditioning.
  </p>
  <p>
    Or was it maybe, just a trifle over-done?
  </p>
</main>
```

## Masonary Layout with Columns

- Made popular by Pinterest and Unsplash, stacking elements in an asymmetric grid
- Just one property `column-count: 3` will get you most of the way there.
- For the column gap, use the `column-gap: 16px` property
- And for the bottom spacing, just apply it to the li

### Limitations

- Items are laid out from top to bottom
- We generally read things left to right on the web, not top to bottom
- This can be jarring for the tab order
- Adding content dynamically, new content is added to the very last column and everything else is re-distributed

-

```HTML
<style>
/* Quick lil' CSS reset */
body, ul, li {
  padding: 0;
  margin: 0;
}
ul {
  list-style-type: none;
}

/* Real code starts here */
ul {
  --gap: 16px;
  column-count: 3;
  column-gap: var(--gap);
  padding: var(--gap);
}

li {
  break-inside: avoid;
}

img {
  display: block;
  width: 100%;
  margin-bottom: var(--gap);
}
</style>
<ul>
  <li>
    <a href="">
      <img src="/course-materials/night-sky.jpg" />
    </a>
  </li>
  <li>
    <a href="">
      <img src="/course-materials/nasa-earth-shot.jpg" />
    </a>
  </li>
  <li>
    <a href="">
      <img src="/course-materials/cat-four-300px.jpg" />
    </a>
  </li>
  <li>
    <a href="">
      <img src="/course-materials/wall-art.jpg" />
    </a>
  </li>
  <li>
    <a href="">
      <img src="/course-materials/article-image-balloons.jpg" />
    </a>
  </li>
  <li>
    <a href="">
      <img src="/course-materials/article-image-standing.jpg" />
    </a>
  </li>
  <li>
    <a href="">
      <img src="/course-materials/article-image-spot.jpg" />
    </a>
  </li>
  <li>
    <a href="">
      <img src="/course-materials/otter.jpg" />
    </a>
  </li>
</ul>
```

### The Future of Masonry

- Browsers are working on a special version of grid for this
- [No browser support yet](https://caniuse.com/mdn-css_properties_masonry)

```CSS
.container {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-template-rows: masonry;
}
```

## Line Length

- Long line length makes it hard on our eyes. Fatique on our eyes. And when you reach the end of the line, it's hard to figure out which line is next.
- Research on line length is a bit mixed, but most agree somewhere between 50 and 75 characters per line.
- And CSS has a built in unit for this. the `ch` unit:
- `1ch` is equal to the width of teh 0 character at current font size.
- Depending on your font, can have differ line length.
- Jsut need to be somewhere between 50-75 characters long

```CSS
p {
  max-width: 50ch;
  margin-bottom: 1em;
}
```

## Text Align

- What role does `text-align` still have to play with grid / flexbox world
- So what is the difference? Between centering something with `text-align` and `align-items`
- They do two differ things
- `text-align` moves all teh individual characters to the middle of each line. Like a RTE.
- flex box and `align-items` is more about layout alignment. And positions the paragraph as a block. Not individual characters.

## Font Stacks

- `font-family` property is how we change the font for a given elements.
- You can give multiple comma-seperated values

```CSS
.title {
  font-family: 'Lato', Futura, Helvetica, Arial, sans-serif;
}
```

- This acts as a preference list. In priority order, and teh last being the category for the font. Like `serif`, `sand-serif`, `monospace`, `cursive`
- If font is unavailable, it isn't installed on the suer's device, or the font is a web font, and not yet been downloaded
- Handfull of universally available fonts like
  - Arial, Courier New, Georgia, Helvetica, Tahoma, Times New Roman
- [CSS Font Stack](https://www.cssfontstack.com/), to show how common each font is between Windows and MacOS
- The goal is to provide a font stack to provide a list of fonts that the browser can pick from, making sure everyone ses an acceptable font and and no one sees the ugly default font.

## System Font Stacks

- A stack of fonts that default to the nicest default option for each platform
- Looks like this
- MacOS and iOS both use the San Francisco font
- -apple-system and BlinkMacSystemFont are aliases for the current system font on Mac
- Windows 10 users, won't recongnize the first fonts but will recognize the Segoe UI, Segoe UI is the default font for Windows 10
- System font stack is nice, because it automatically matches the conventions of the users's device. And modern operating systems use well designed fonts.

```CSS
p {
  font-family:
    -apple-system, BlinkMacSystemFont, avenir next, avenir, segoe ui,
    helvetica neue, helvetica, Ubuntu, roboto, noto, arial, sans-serif;
}
```

- CSS Variables to the rescue, make a lot easier to manage.

```CSS
html {
  --font-sans-serif:
    -apple-system, BlinkMacSystemFont, avenir next, avenir, segoe ui,
    helvetica neue, helvetica, Ubuntu, roboto, noto, arial, sans-serif;
  --font-serif:
    Iowan Old Style, Apple Garamond, Baskerville, Times New Roman,
    Droid Serif, Times, Source Serif Pro, serif, Apple Color Emoji,
    Segoe UI Emoji, Segoe UI Symbol;
  /* Set a global default */
  font-family: var(--font-sans-serif);
}
/* Apply different fonts as needed */
p {
  font-family: var(--font-serif);
}
```

## Web Fonts

- If you want to use a font that isn't on the users system, we can download a system font.

### Google Fonts

- Free online repository of open-source fonts
- Served from a CDN, they serve from their own servers

```HTML
<link rel="preconnect" href="https://fonts.gstatic.com">
<link href="https://fonts.googleapis.com/css2?family=Open+Sans:ital,wght@1,400;1,600&display=swap" rel="stylesheet">
```

- Drop that in the `head` of your HTML file.
- This snippet will download a stylesheet which downloads a font
- Then we can access that font in our CSS

```CSS
.thing {
  font-family: 'Open Sans', sans-serif;
}
```

- Web fonts should be wrapped in quotes `'Open Sans'` not `Open Sans`
- It's a helpful convention that indecates which fonts in stack are web fonts vs system fonts.

### Web font performance concerns

- Some downsides to webfonts, lots of great fonts are not available on Google
- and self-hosted fonts can perform better
- [Gatsby creator Kyle Matthews discovered that self hosting fonts can save 300ms on desktop and 1second plus on mobile 3G](https://bricolage.io/typefaces-easiest-way-to-self-host-fonts/)

## Using modern tooling

- Host a open source font bundled within a npm package, [Fontsource](https://fontsource.org/)
- Built for modern JS applications, letting you npm install fonts you want to use

## The manual way

- What if your font isn't available on google fonts or fontsource?
- You can add web fonts from scratch.
- Skipping over this content, but Josh explains the process as always.
- [The manual way](https://courses.joshwcomeau.com/css-for-js/06-typography-and-media/08-web-fonts)

## Font Loading UX

- When a person visits your site for the first time, they will need to download the web font files you are using.
- Some cases, the HTML will load before the fonts
- You have two main options:
  - 1. Wait until the web font has been downloaded before showing any text.
  - 2. Render the text in fallback font, on that is already loaded on the users system.
- Both options have issues.
  - 1. we are drpriving the user of the taxt they care about, FOIT, Flash of Invisible Text
  - 2. Jarring experience, flipping fonts can cause layout shifts, FOUT, Flash of Unstyled Text.
- As long as a user needs to download web fonts, this problem will exist, but we can improve things with modern CSS

### Works on my machine

- You may have never seen this happen. It's likly that.
  - On localhost, fonts are downloaded instantly
  - In prod, user will only notice this the first time you vist a page
  - You may have already have the font locally
  - Good internet connection
- For more realistic picture, [throttle your network speeds](https://developer.chrome.com/docs/devtools/network/#throttle), [disable your local fonts](https://developer.chrome.com/blog/new-in-devtools-86/#emulate-local-fonts)

## The font-display property

- The `font-display` property can control how a font should be rendered before it's avail.
  
```CSS
@font-face {
  font-family: 'Great Vibes';
  src: url('/fonts/great-vibes.woff2') format('woff2');
  font-weight: 400;
  font-style: normal;
  font-display: swap; /* 👈👈👈 */
}
```

- To understand how this works, we have to look at the font-display timeline, block, swap, failure timline
- Block period, text painted in an invisible ink, no text is visible. Render the font ASAP if becomes avail during this period
- Swap period, during this time, fallback font is rendered, first avail font in the stack. If the web font becomes avail, it gets swapped
- Failure period, during this time, if font isnt' lodaded during the blcok or swap, it stops trying and will keep showing the fallback font no matter what happens.

- How long does each of these last? The `font-dispaly` property is a way to contorl the length of each window.

### Block

- `font-display: block` prioritizes the use of the font over all others, has long block period and infinite swap period. , the block period should be no more then 3 seconds.
- Should only be used is font is absolutely critical. For example, if you use an icon font, you don't want the text to be shown before the icon.
- Icons fonts should generally be avoided.

### Swap

- with `font-display: swap` there is little to no block period
- The goal is to render text as quickly as possible
- This is the value that Google Fonts uses, it's a good option, but there is a better one for most cases

### Fallback

- `font-display: fallback` is a good balance for most cases
- Has very short block period, 100ms, and moderate swap period, about 3s
- This is Josh's preferred value
- On speedy connections, it's likely that th efont can be downloaded within the block peroid, preventing the flash between font families
- On slow or intermitten connections, the fallback font is used forever, preventing the random flash between fonts, seconds or minutes after the page has loaded.

### Optional

- `font-display: optional` is a great choice when the font is a subtle improvement, but not really that important. Short block period, 100ms and no swap period at all
- If the font doesn't load immediately, it will not load at all
- Mean,s users will see the fallback font for their first page, but the webfont for all following pages
- The first page view loads teh font in the background, to be applied on teh next page

### Font matching

- When using font-display, with a swap period, good chance rendered text will flip from one font to another.
- If fonts are differnt size/shape, this can cause wonky layout shifts
- One solution, align the two fonts to be as close as posssible, with CSS properties, font-size, letter-spacing, line-height
- [Check out the font style matcher](https://meowni.ca/font-style-matcher/)
- Tricky, we need these properties to apply before our font is loaded. No way to do that with pure CSS, but can be done with [JS Loading API](https://developer.mozilla.org/en-US/docs/Web/API/CSS_Font_Loading_API). But is this worth it? Not really.
- However, browsers are working on a new feature called "font descriptors", f-mods.

## Font Optimization

- Let Google do all the hard work for us, little known fact that Gogle Fonts are heavily optimized.
- For example, the popular font Inter, when downloaded from official site. Each font file is about 99kb to 151kb. That adds up.
- The same 3 weight fonts on Google Fonts, squeezes them down to one file, at 37kb, 90% smaller
- [You can self host Google optimized fonts](https://courses.joshwcomeau.com/css-for-js/06-typography-and-media/10-font-optimization). It's a bit of a trick, watch Josh's video to go through the steps.
- In your browser, dev tools > network tab, see what fonts you are loading and how much it being downloaded.
- [Google fonts helper](https://google-webfonts-helper.herokuapp.com/fonts), although not sure what this does exaclty. Looks like you can select the fonts you want, and then self host and it gives you the snippets of css.
- Additional resources, [Reduce WebFont Size](https://web.dev/reduce-webfont-size/)

## Variable Fonts

- With web fonts, each weight and style is it's own file. That can add up and cause unstyled text to flash.
- Variable Fonts, The idea with variable font is that parameters can be tweaked to control the rendered output. FOnt weight for example.
- With standard fonts, you can pick 2 or 3 weights, but with variable fonts, there are hundreds of valid values.
- And it's supported in major browsers.
- This is a lot of control, and really going down a rabit hole.
- [Book marking for future reference.](https://courses.joshwcomeau.com/css-for-js/06-typography-and-media/11-variable-fonts)

## Icons

- Two common way sto implement icons: use an icon font or use SVG
- Of the two, Josh prefer's SVG approach.
  - SVGs tend to look more crisp and sharp
  - The are easier to position an duse width instead of font-size
  - They can be more accessible
  - They can be multi-color
  - They can be tweaked and animated.
- What's an SVG? SVG is a vector image format. This means that instead of storing info about the colors of specific pixels, it stores teh instructions for how to draw the image.
- You can save it as a file, and reference it like any other iamge format. `<img src="/circle.svg" />, or you can copy and past code directly into your HTML, know as inline SVG
- WHEN WE INLINE OUR SVGs, we can target sub elements with CSS and JS

### Popular Icon sets

- [Feather icons](https://feathericons.com/)
- [iconmoon](https://icomoon.io/)
- [Material Design icons](https://github.com/google/material-design-icons)

### Using icons

- Each icon pack, option to download indivisual SVG files
- If using React, you need to convert each of the SVG files to JSX, so you can use with React components
- This tool can help, [SVG 2 JSX](https://svg2jsx.com/)
- In Rewct for example Feathre's creator has created an NPM package, `react-feather`

```CODE
import React from 'react';
import { HelpCircle } from 'react-feather';

funtion Somthing() {
  return (
    <div>
      <HelpCircle />
    </div>
  )
}
```

- Similar packagers for [Vue](https://www.npmjs.com/package/vue-feather), [Angular](https://www.npmjs.com/package/angular-feather), and [Svelte](https://www.npmjs.com/package/svelte-feather-icons)

### Icons and Accessibility

- Screen readers don't know how to deal with SVG icons
- You have to additional text info for folks using a screen reader.
- See [hiding from screen lesson](https://courses.joshwcomeau.com/css-for-js/02-rendering-logic-2/18-hidden-content#hiding-from-screens)

```HTML
<button>
  <HelpCircle />
  <span class="visually-hidden">
    Visit the help center
  </span>
</button>
```

### Spacing issues

- Lots of benefits of SVG, but one frustrating issue with them.
- There is a noticible amount of bottom spacing
- The problem is SVG elements have a defualt valueof `display: inline`, and inline elements have [magic space](https://courses.joshwcomeau.com/css-for-js/01-rendering-logic-1/09-flow-layout#inline-elements-have-magic-space).
- Usign an icon pack makes this tricky, no access to underlying SVG element.
- YOu can solve my using a decendant selector

```JS
import { Home } from 'react-feather';

function Header() {
  return <Button><Home /></Button>;
}

const Button = styled.button`
  padding: 0;

  & > svg {
    display: block;
  }
`;

render(<Header />);
```

- Is this bad practice? Gererally not a fan of nesting. Makes it harder to understand where the style is coming from.
- But with syled-components, all elemtns styles are colocated in one spot.

## Images

- Lots of advancements on working with images in CSS
- Basics, `img` tage has two required attributes, `src` and `alt`
- `alt` is a property that allow you to specify alternative text, is teh image fails to load for for folks that cannot see images.
- Not all images require `alt` attribute, only if the image is purley decorative
- How do you know when image is decorative? Imagine what the UX would be like if image failed to load. If you cannot see the image, would the product be harder to use?
- [Smashing Mag article, Your image is probably not decorative](https://www.smashingmagazine.com/2021/06/img-alt-attribute-alternate-description-decorative/)

### Writing effective alt text

- The goal of with alternative text should be to convey the smantic meaing of the image to the user.
- For example, logo at the top left corner. Instead of alt text saying, brand logo, it should be something like "Return to home".
- Good alt text helps users understand teh context that the image is in.
- Check out WebAIM, [guide on writing alt text](https://webaim.org/techniques/alttext/).

### Image vs background-image

- background-image, meant to be used for decorative images in the background. For example, on the spacejam site, the star background texture.
- Do not use background-image for semantically meaninful imags because they can't be given alt text.

### Fit and Position

- `img` tag is a little strange
- `img` is known as a replacement element.
- Images are inline elements, and usually go with the flow. And come with their own size based on demensions of the image file.
- Images also have intrinsic aspect ratios, you supply one dimension, either width or height, and the other scales up or down as needed to preserve teh aspect ratio
- What if we provide both a width and height, the image will distort
- To make images fit, you cuold crop the image, trimming off any excess that can't fit within the specified rectangle.
- With modern CSS, some tools to help with this, `object-fit`
- `object-fit` allow us to change what we want to prioritize
- Three priorities we can have, but we can only ever pick two.
- 1. aspect ratio
- 2. see all image data, every pixel
- 3. can fill the avail space
- Object Fit, `default`, fills the avial space but doesn't retain aspect ratio
- `Contain`, preserves the aspect ratio, but does not fil the entire space, scales the img down proportionally until it fits in the box, then just leaves a gap at either end.
- `Cover`, preserves aspect ratio and fills the entire space, but you cannot see the entire image, crops it.
- `None`, never used but exist, scales img to be natural size and just crops what doesn't fit

### Object Position

- When using `object-fit: cover` the browser wil crop our image to see the center of the image and trim off edges.
- But in some cases we want to use a differ anchor point.
- `object-position` lets us specify how the image should be translated or cripped within the space. Similar to `background-position`
- Object position takes two numbers, one for horizontal offset and one for vertical offset.
- We can also use keywords

```CSS
.thing {
  /* Anchor to the top-left corner */
  /* Same as "0% 0%" */
  object-position: left top;
}
```

- Good browser support, supported in every major browser except IE

Exercises

- Make a svg image scale with the monitor size. And crop itself on smaller screens
- [Link to exercise](https://courses.joshwcomeau.com/css-for-js/06-typography-and-media/14-img-fit)

```HTML
<style>
  body {
    margin: 0;
    padding: 0;
  }

  img {
    width: 100%;
    min-height: 150px;
    /* TODO */
    object-fit: cover;
    object-position: left center;
  }
</style>
<img
  alt=""
  src="/course-materials/swoops.svg"
/>
```

- Scaling and vector images, no need to worry about loss in quality like `jpg`, `gif`, `png` bitmap or raster image formats. SVG contains instructions for how to draw the image.

-

### Images and Flexbox

- Because the image is weird, sometimes it doesn't play nicely with layout algorythms.
- Expecially Flexbox
- When you have a cross axis in flex, the default alignment is stretch
- When you have two children of the same row, by default flex stretches the shorter one to be the height of the tallest one.
- The flex algorythm does this to all elements, even images
- You can add `align-items: flex-start` to the shorter item to solve the stretch problem.
- Hypethetical width and min-width for images, you can override that by adding min-width: 0
- You can get around this, think of image as content, does not belong as a direct child of flex parent.
- Flex Container, that has blocks of content, with content inside like images, content etc.
- Wrap the iamges as containers
- Add a wrapper, then add `width: 100%` to the image itself, as the column changes shape, so does the image. The container controls the image.

``` HTML
<style>
body {
  margin: 0;
  padding: 0;
}

main {
  display: flex;
  gap: 8px;
}

.col {
  flex: 1;
}
.twice-as-big {
  flex: 2;
}

img {
  width: 100%;
}
</style>

<main>
  <div class="col">
    <img
      alt=""
      src="/course-materials/size-200-300.png"
    />
  </div>

  <div class="col twice-as-big">
    <img
      alt=""
      class=""
      src="/course-materials/size-200-300.png"
    />
  </div>

</main>
```

### Exercises

- Simple layout with Image on the left that scales and blockquotes o the right.
- Display `flex` on the main, and add `flex: 1` to the child notes to create equal space for the two.
- Add `min-width` to each child node to prevent from going to small
- And `flex-wrap: wrap` on the main to wrap the nodes once it hits the min width size.

```HTML
<style>
  main {
    display: flex;
    gap: 32px 0;
    flex-wrap: wrap;
  }

  .book-img-wrapper, .reviews {
    flex: 1;
  }

  .book-img-wrapper img {
    width: 100%;
    min-width: 300px;
    object-position: -32px 0;
  }

  .reviews {
    text-align: center;
    min-width: 300px;
  }

  .average-rating {
    font-size: 1.25rem;
    margin-top: 32px;
    color: gold;
    font-style: italic;
  }
  body {
    margin: 0;
    padding: 0;
    color: white;
  }

  .book-img {
    /*
      We'll learn more about this fancy
      property in a future module!
    */
    filter:
      drop-shadow(
        -8px
        32px
        10px
        hsl(260deg 50% 4% / 0.5)
      );
  }
</style>
<main>
<div class="book-img-wrapper">
<img
  alt=""
  class="book-img"
  src="/course-materials/whispering-owl.png"
/>
</div>
<div class="reviews">
  <blockquote class="review">
    A magnificent story about a majestic creature.
    <footer>
      <cite class="author">KitKat99</cite>
    </footer>
  </blockquote>
  <blockquote class="review">
    From the first flap of the wings, it was clear that this book would soar above my expectations. Just terrific.
    <footer>
      <cite class="author">TheEagle</cite>
    </footer>
  </blockquote>
  <blockquote class="review">
    Some have said that it is a real book, but I see no evidence of that.
    <footer>
      <cite class="author">Skeptic1977</cite>
    </footer>
  </blockquote>
  <blockquote class="review">
    If you only read one book about an owl this month, this should be the one.
    <footer>
      <cite class="author">knuckles</cite>
    </footer>
  </blockquote>
  <blockquote class="review">
    A magnificent story about a boy and an owl!
    <footer>
      <cite class="author">KitKat99</cite>
    </footer>
  </blockquote>
  <blockquote class="review">
    A magnificent story about a boy and an owl!
    <footer>
      <cite class="author">KitKat99</cite>
    </footer>
  </blockquote>
  <blockquote class="review">
    A magnificent story about a boy and an owl!
    <footer>
      <cite class="author">KitKat99</cite>
    </footer>
  </blockquote>
  <div class="average-rating">
    ★★★★☆
    <br />
    Average Amazon Rating
  </div>
</div>
</main>
```

### Aspect Ratio

- Images have an intrinsic aspect ratio, so you can end up with drastically differ image sizes because of the natural aspect ratios
- What if we wnated them to have the same aspect ratio?
- You can do this by giving them all same `width` and `height` and use the `object-fit: cover` to avoid stretching
- How can we scale our images proportionally, as a certain aspect ratio?
- You can do that with `aspect-ratio: 1/1` property
- takes to values like `4/3` or `7/11`
- This is the ratio of width to height
- And aspect ratio of `2/1` meand teh image will be twice as wide as it is tall `width / height`
- Aspect ratio isn't specific to images, can work on any element, even `<video>`
- Note: not fully supported, [about 79% caniuse](https://caniuse.com/mdn-css_properties_aspect-ratio)

### Padding Fallback

- Aspect ratio isn't fully supported, can we add a fallback?
- You can do it with padding-bottom, but a bit hacky
- Kind of a pain, not taking notes on this

### Progressive enhancement

- In most cases, `aspect-ratio` is used to add some polish
- Since most browsers support it, can we start using it?
- Yes, you can use progressive enhancement
- `@supports` is a feature query, works like a media query but instead of targeting window sizes, it targets specific CSS declorations

```HTML
<style>
  section {
  display: flex;
  gap: 8px;
  }
  .image-wrapper {
    flex: 1;
  }
  img {
    width: 100%;
    height: 200px;
    object-fit: cover;
  }

  @supports (aspect-ratio: 1 / 1) {
    img {
      height: revert;
      aspect-ratio: 1 / 1;
    }
  }
</style>

<section>
  <div class="image-wrapper">
    <div class="padding-hack">
      <img
        alt="A wide-open outdoor concrete area. Architecture"
        src="/course-materials/architecture-hugo-sousa.jpg"
      />
    </div>
  </div>
  <div class="image-wrapper">
    <div class="padding-hack">
      <img
        alt="A modular building against a blue sky. Architecture"
        src="/course-materials/architecture-joel-filipe.jpg"
      />
    </div>
  </div>
  <div class="image-wrapper">
    <div class="padding-hack">
      <img
        alt="A unique building with inset curves. Architecture"
        src="/course-materials/architecture-julien-moreau.jpg"
      />
    </div>
  </div>
</section>
```

## Responsive Images

- Modern screen come in all sorts of configurations
- A new iPhone has a 3 to 1 ratio between hardware and sortware pixels. Known as high-DPI displays
- If we render an image at it's native size on high-DPI display, it's going to be fuzzy.
- To keep things crisp, we need to serve differ images based on screen's pixel ratio
- When exporting, common to export 2 or three differ versions, `cat.jpg`, `cat@2x.jpg` or `cat@3.jpg`

### Note

- Image optimization tools like [next/image](https://nextjs.org/docs/api-reference/next/image) or [gatsby-image](https://www.gatsbyjs.com/plugins/gatsby-image/) offer a lot of out of the box features.

### The srcset attribute

- The quickets way to get started with responsive images is to use the `srcset` HTML attribute

```HTML
<img
  alt=""
  src="/course-materials/responsive-diamond.png"
  srcset="
    /course-materials/responsive-diamond.png 1x,
    /course-materials/responsive-diamond@2x.png 2x,
    /course-materials/responsive-diamond@3x.png 3x
  "
/>
```

- `srcset` is basically a plural version of `src`, the browser will scan thorugh thlist and apply the first one that matches.
- We keep a redundant `src` property for older browsers.
- `srcset` enjoys a universal support in modern browsers and the `src` ensures that IE users will see our images.
- In devTools, it will let you know which one is being served if you hover over the URL in elements pane

### The picture element

- Another way to solve for this problem, the `<picture>` element

```HTML
<picture>
  <source
    srcset="
      /course-materials/responsive-diamond.png 1x,
      /course-materials/responsive-diamond@2x.png 2x,
      /course-materials/responsive-diamond@3x.png 3x
    "
  />
  <img
    alt=""
    src="/course-materials/responsive-diamond.png"
  />
</picture>
```

- Similar to the solution above, but moved the `srcset` solution to a new `<source>` element and wrap the whole thing in a `<picture>`
- The benefit here, is that we can apply differ formats.

```HTML
<picture>
  <source
    type="image/avif"
    srcset="
      /course-materials/responsive-diamond.avif 1x,
      /course-materials/responsive-diamond@2x.avif 2x,
      /course-materials/responsive-diamond@3x.avif 3x
    "
  />
  <source
    type="image/webp"
    srcset="
      /course-materials/responsive-diamond.webp 1x,
      /course-materials/responsive-diamond@2x.webp 2x,
      /course-materials/responsive-diamond@3x.webp 3x
    "
  />
  <img
    alt=""
    src="/course-materials/responsive-diamond.png"
  />
</picture>
```

- AVIF format, based on lessons learned form video compression, creates dramatically smaller images
- Currently low browser support, Chrome and Opera.
- `<picture>` allows us to use modern image formats in a safe way, providing fallbacks
- When the browser sees a `<picture>` tag, it scans through the `<source>` children, and the individual `srcset`.
- The order matters, when the browser finds a match, it will download it and serve to user
- We want our smallest AVIF files to be at the top
- Resources articles for more learning:
  - [AVIF has landed](https://jakearchibald.com/2020/avif-has-landed/)
  - [Squoosh](https://squoosh.app/), a web app by Google
  - [Modern Image Formats](https://www.joshwcomeau.com/performance/embracing-modern-image-formats/)

### Why so funky?

- For backwards compatibility, if a browswer doesn't recognize the tag, it just renders it as a plain ole div

### Styling the targeting picture elements

- Because `<picture>` breaks it into multiple elements, how do we style it? `<picture>`, `<source>`, `<img>`
- Ignore the `<source>` tags for styling, they are just meta data and not visible.
- Important to note, no matter which source is selected, the `<img>` tag will always be used. And acts like any other image tag.
- The souce exist to swap out, the `src` attribute.
- We want to add additional properties like `alt` text to teh `<img>` tage and not the `<source>` or `<picture>`
- Finally the `<picture>` element acts liek a `<span>`, inline wrapper around the `<img>` tag
- The `<picture>` wrapper comes in handy, for example we can use  it inside a Flex container.

```HTML
<style>
  main {
    display: flex;
    gap: 8px;
  }

  picture {
    flex: 1;
    padding: 8px;
    border: 2px solid;
  }

  picture img {
    display: block;
    width: 100%;
  }

  p {
    flex: 2;
    border: 2px solid;
  }
</style>
<main>
  <picture>
    <source
      srcset="/course-materials/responsive-diamond@2x.png 2x"
    />
    <source
      srcset="/course-materials/responsive-diamond@3x.png 3x"
    />
    <img
      alt=""
      src="/course-materials/responsive-diamond.png"
    />
  </picture>
  <p>Hello World</p>
</main>
```

### Deciding which to use

- Have to decide which is the best approach for you
- Exporting all those images manually is tedious and a lot of work
- Tools do exist, but have their own barier to entry

### Background Images

- The `<img>` tag is powerful, but it still cannot tile an image
- We need CSS background iamge to do that, example

```HTML
<style>
  body {
    background-image:
      url('/course-materials/geometric-pattern.png');
  }
  main {
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  }
  h1 {
    font-size: 2rem;
  }
  body {
    margin: 0;
    padding: 0;
  }
</style>

<main>
  <h1>Hello World</h1>
</main>

```

- This will be rendered at it's native size, tiels across the element
- Problem is, high DPI, it will look blurry and fuzzy
- To keep this crisp, we provide differ images for differ divices, scaling up based on pixel ratio.
- Can do this with media query, `<min-resolution>`

```HTML
<style>
  main {
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  }
  h1 {
    font-size: 2rem;
  }
  body {
    margin: 0;
    padding: 0;
  }
  body {
    background-image:
      url('/course-materials/geometric-pattern.png');
    background-size: 450px;
  }
  
  @media
    (-webkit-min-device-pixel-ratio: 2),
    (min-resolution: 2dppx)
  {
    body {
      background-image:
        url('/course-materials/geometric-pattern@2x.png');
    }
  }
  
  @media
    (-webkit-min-device-pixel-ratio: 3),
    (min-resolution: 3dppx)
  {
    body {
      background-image:
        url('/course-materials/geometric-pattern@3x.png');
    }
  }
</style>

<main>
  <h1>Hello World</h1>
</main>
```

- `min-resolution` is supported across all major browsers except Safari
- For Safari, use webkit for support, `--webkit-min-device-pixel-ratio`
- You have to specify a `background-size` in pixels, or high DPI images will render in their native size, producing much larger images without any additional clarity.
- The background size shuold match the width of the stardard 1x image.

### Fit and positioning

- The `background-size` property also accepts keywords, `object-fit` for example, can have our background image cover the element

```HTML
<style>
  body {
    background-image:
      url('/course-materials/geometric-pattern.png');
    background-size: cover;
  }
  main {
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  }
  h1 {
    font-size: 2rem;
  }
  body {
    margin: 0;
    padding: 0;
  }
</style>

<main>
  <h1>Hello World</h1>
</main>
```

### Background repeat

- By default, the background iamge will be tiled side-by-side, top to bottom.
- But the pattern wil be truncated at the bottom and on the right.
- `background-repeat` property allows us to tweak this algorithm, two additional options that can be used.
- `background-repeat: round`, will scale the image up or down, avoid having the image cut off at bottom or right, and preserves the aspect ratio.
- `background-repeat: space`, won't tweak the size of the image, btu will leave gaps between the images.

### Generative background

- I addtition to accepting URL to an image file, the `background-image` property accpets gradients
- Resoruce, pure-CSS background patterns
- [Magic Pattern, CSS background patterns](https://www.magicpattern.design/tools/css-backgrounds)
- Adding some ornamental design to your backgrounds

## Workshop: Unsprinkle

### Optimize the Fonts

- Replace the self hosted large font, with the Google version via using `<link>` tag
- Then self host the optimized Google Font, Network tab > Open in new tab to download > Put in your font directory and rename it
- Then use the `style` tag to point to the self hosted optimized font
- Go to Network tab and make sure it's using the local version

```HTML
<style>
      @font-face {
        font-family: 'Inter';
        font-style: normal;
        font-weight: 300 900;
        font-display: fallback;
        src: url(/fonts/Inter-variable-optimized-Google.woff2) format('woff2');
      }
    </style>
```

### Improve Images

- Loading your images in a React app with styled components
- You can use the `replace()` JS method to load your differ image names, as long as they follow same naming convensions.

```HTML
<script>
<picture>
  <source
    type="image/jpeg"
    srcSet={`
              ${src} 1x,
              ${src.replace('.jpg', '@2x.jpg')} 2x,
              ${src.replace('.jpg', '@3x.jpg')} 3x,
            `}
  />
  <Image src={src} />
</picture>
</scipt>
```

- File size, you can try the avif image source to optimize image size
- `.avif` format retains same quality as `.jpeg` but at much smaller file size
- Converting from `jpeg` to `avif` format reduced the size dramatically, from over 120KB to 10KB

```HTML
<script>
<picture>
          <source 
            type="image/avif"
            srcSet={`
              ${src} 1x,
              ${src.replace('.jpg', '@2x.avif')} 2x,
              ${src.replace('.jpg', '@3x.avif')} 3x,
            `}
          />
          <Image src={src} />
        </picture>
</script>
```

- Hardest part of these formats, is the time it takes to generate the alternative versions
- You can use nextjs or gatsby, but nothing in react native as of yet
- You can write it into your build script, `avif npm` package
- [avif-cli](https://www.npmjs.com/package/avif)
- You can write a script to generate the images when you build the site

### Accessibility Issues

- Use the [WebAIM extension](https://addons.mozilla.org/en-US/firefox/addon/wave-accessibility-tool/) to audit any issues with the site.

### Tag overflow

- How do you truncate the tags
- You could use the ellipsis overflow trick

```CSS
  .tag {
    overflow: hidden;
    text-overflow: ellipsis;
    white-space: nowrap;
  }
```

- this doesn't play well with flexbox
- more of a flow layout thing
- make the element tag an `display: inline` element
- on the parent DOM element, add padding to give elements space
- and margin right to add space between

```HTML
<style>
  ul {
    overflow: hidden;
    text-overflow: ellipsis;
    white-space: nowrap;
    padding: 4px 0;
  }

  li {
    display: inline;
    padding: 4px 8px;
    background: var(--color-gray-300);
    font-size: 0.875rem;
    font-weight: 475;
    color: var(--color-gray-800);
  
  }
  li:not(:last-of-type) {
    margin-right: 8px;
  }
</style>
```

## CSS Grid

- Grid is similar to Flexbox, but instead of one dimensional layouts, it can distrubute children across two dimensions.
- Sort of like Flexbox's older cousin.
- In this module will contain
  - How to be backwards compatible
  - Create complex layouts, responsive and fliud
  - Recipes for common CSS Grid Challenges

### Mental Model

- With grid, each elements content box is sliced into rows and columns.
- If a column is 250px wide, then each cell in that column is 250px
- Grid doesn't support zig-zag columns, every cell int he same column needs to have the asme width. The same is tru for rows, have the same height.
- Every row needs to hav ethe same number of columns
- We can't have a grid where the first row has 1 column and the second row has 2 columns, Holy Grail layout for example.
- But how is this possible?

### Rows/columsn are invisible markers

- On the web, every layout can be broken down into a combination of divs, spans, sections etc.
- The web is made up of boxes inside of boxes inside of boxes.
- For example, this table layout

```HTML
<table>
  <thead>
    <tr>
      <th>Name</th>
      <th>Email</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Axel Duproprio</td>
      <td>axel@gmail.com</td>
    </tr>
    <tr>
      <td>Beatrice Bouchard</td>
      <td>beatrice@gmail.com</td>
    </tr>
  </tbody>
</table>
```

- This table ends up being two rows, with two columns if you add a red outline to it.
- Grid is different because the structure happens in CSS.
- No DOM nodes that represent the rows and columns.
- They are invidible markers, tools our HTML elemetns can use to position themselvdes.
- Rows and columns are like the lines painted in a parking lot. The lines are guides and the driver decides.
- This analogy works in a number of ways:
  - The driver can choose how many spots to take up. Elements can choose to span multiple cells.
  - Driver can fit into an assigned sport, or only part of it.
  - A spot can be completely empty, a parking lot with 50 spots and 1 car.
  - A single grid can have multiple items. 3 motorcycles parked in the same spot.
- What makes grid so powerful, is the structure can be selectively ignored if you want. This makes all kinds of layouts possible.

### Browser Support

- Not bleeding ege anymore, has good support
- Check out caniuse for latest support numbers
- If you apps can use modern browsers, you are good to go!
- If you have to support the old stuff, you can use progressive enhancement

### Progressive enhancement with feature queries

- Doesn't mean the app has to look the same across all browsers
- Or the experience has to be equally as good.
- It means that user is able to accomplish the same tasks.
- If the app allos us to book vaccine appointments, then all users should be able to book vaccine appointments
- That's the core idea behind progressive enhancement
- We start with a baseline experience that works for everybody, and is good enough, and enhance it to be better experieince for modern browsers
- What this means for grid, give a simplidied layout using flow or flexbox, and improve the layout with grid on modern browsers
- Can do this with feature queries

```CSS
.wrapper {
  display: flex;
}
@supports (display: grid) {
  .wrapper {
    display: grid;
    grid-template-columns: 1fr 1fr;
  }
}
```

- A feature query is like a media query
- Anythign inside the `@supports` statement will be applied if the browser recognizes the decloration. Otherwise it will be ignored.
- Has to be a real decloration, for example, `spaghetti` will be ignored.

```CSS
@supports (display: spaghetti) {
  /*
    Any CSS put in this block will never be applied,
    because (at this time of writing) no browser
    has a "spaghetti" layout mode.
  */
}
```

## Grid Flow and Layout Modes

- Like Flexbox, we enable Grid layout mode with the `display` property

``` CSS
.wrapper {
  display: grid;
}
```

### Implicit Grid

- If you don't specify what the rows and columns will be, grid will come up with it's own based on the children.
- For example, the markup below, by default it creates one new row for each eleemnt, because our grid parent is given 3 children, we end up with a 1x3 grid.

```HTML
<style>
  .wrapper {
    display: grid;
  }
  
  header, section, footer {
    border: 1px solid;
  }
</style>

<div class="wrapper">
  <header>Hello World</header>
  <section>Stuff here</section>
  <footer>Copyright notice</footer>
</div>
```

- Implicit grids want to fill all available space
- If you give your grid a fix height, notice each row will behave the same
- Because our grid is 300px tall, each row ends up being 100px.

```HTML
<style>
  header, section, footer {
    border: 1px solid;
  }
  .wrapper {
    display: grid;
    height: 300px;
  }
</style>

<div class="wrapper">
  <header>Hello World</header>
  <section>Stuff here</section>
  <footer>Copyright notice</footer>
</div>
```

### Inspecting grids in the devtools

- CSS grid adds an invisible layer of how things are laid out
- Firefix and Chrome now have grid and inspection tools
- You should see the grid pill, clicking on it, will show you the grid layout
- Elements are not always 1 to 1 with their columns
- In grid, the lines are the primary things we track by
- Spanning to row line 1 to row line 2

### Grid auto flow

- What is you want to change the flow direction of a grid, from vertical to horizontal?
- `grid-auto-flow` property `row` (default) and `column`
- Isn't this like flexbox, flow direction? In flexbox, we are changing which axis is the primary axis, and which one is the cross axis.
- CSS Grid has no concept of primary or cross axis
- Instead, CSS Grid has rows and columns.
- Rows are always arranged in the vertial axis, rows are always stacked on on top of the other
- Columns are always arranged along the inline axis, horizontally.
- CSS Grid is like flow layout, Rows are distrubuted along teh block axis, just like block level elements in FLow
- When we change `grid-auto-flow` from `row` to `column` we are just changing our grid to have multiple columns insteaad of multiple rows.

### Layout modes

- Note: **`display: flex` and `display: grid` change the layout mode it's children use, not the element it's declared on**

### Grid Construction

- The real magic of grid happens when we **explicitly** define our own grids.
- Define some columns, with `grid-template-columns`

```HTML
<style>
  .wrapper {
    display: grid;
    grid-template-columns: 25% 75%;
  }
  aside, main {
  border: 1px solid;
  }
</style>

<div class="wrapper">
  <aside>On the side</aside>
  <main>Main content</main>
</div>
```

- This does two things
  - 1. The number of colums we want our grid to have
  - The individual widths of each column

- In thsi case, we hav ea 2-column grid, first column takes up 25% of space, and the second column takes up 75% of space.
- UNLIKE flexbox, these values are not **suggestions** they are hard limits.
- One problem is a column happens to have a large image, it will overflow by default.

### Flexible columns

- What if we wante our columns to grow to grow if their contents won't fit?
- For that, we use the `fr` unit
- In this example, we are saying the first column should take up ` unit of space, and the second column should take up 2 units.
- There are 3 units total, first column is 1/3, the second 2/3 space.

```HTML
<style>
  .wrapper {
    display: grid;
    grid-template-columns: 1fr 2fr;
  }
  aside, main {
  border: 1px solid;
  }
  img {
    display: block;
    width: 150px;
  }
</style>

<div class="wrapper">
  <aside>
    <img
      alt="Curious-looking dog"
      src="/course-materials/dog-one-300px.jpg"
    />
  </aside>
  <main>Main content</main>
</div>
```

- The `fr` unit brings Flexbox style flexibility ro CSS Grid, kinda like `flex-grow`
- Except it's operating on the columns and not on the actaul child elements
- `fr` stand for "fraction"
- Like `flex-grow`, the `fr` unit is flexible, in the example above, the first column wants to take up 1/3 space, but its child is to wide, so it grows to accommodate it.
- This only happens with the `fr` unit, as well as `auto`. Pixels, rems, and percentages are hard limits.
- the other thing to note, the `fr` unit distrubutes available space, consider the example below.

```HTML
<style>
  .wrapper {
    display: grid;
    grid-template-columns: 200px 2fr 1fr;
  }
  aside, main, section {
  border: 1px solid;
  }
</style>

<div class="wrapper">
  <aside>1</aside>
  <main>2</main>
  <section>3</section>
</div>
```

- First, the grid reserves 200px for the first column, then distrubutes whatever space remains to the other 2. This is how `flex-grow` works when we don't set `flex-basis` to 0.

### Implicit Rows

- CSS Gris is a two dimensional layout mode
- In this example, it's a 2-column grid, and given 7 children. The default behavior or grid, every child gets it's own cell. Our grid will implicitly create as many rows as it needs to.

``` HTML
<style>
  .wrapper {
    display: grid;
    grid-template-columns: 1fr 1fr;
  }
  .item {
    border: 2px solid;
    display: flex;
    justify-content: center;
    align-items: center;
    font-size: 2rem;
  }
</style>

<div class="wrapper">
  <div class="item">1</div>
  <div class="item">2</div>
  <div class="item">3</div>
  <div class="item">4</div>
  <div class="item">5</div>
  <div class="item">6</div>
  <div class="item">7</div>
</div>
```

- How tall will these rows be? Htey gro and shrink as needd based on the children content.
- Implicit rows are handy when we are rendering base on some data, like search results. We can throw a bunch of data into our grid and trust each row will be the right size for content.
- But what if we want more control?

### Explicit rows

- When creating whole layouts in Grid, it's common to give each row an explicit height.
- You can do this with `grid-template-rows` property.
- Here, we have created three rows, 64px header, 100px tall footer, and a main content area that fills the remaining space.
- Note: to fill the entire page, we can use our [min-height percentage trick](https://courses.joshwcomeau.com/css-for-js/01-rendering-logic-1/11-height) from mondule 1

```HTML
<style>
  .wrapper {
    display: grid;
    grid-template-rows: 64px 1fr 100px;
    min-height: 100%;
  }
</style>

<div class="wrapper">
  <header>My Website</header>
  <main>Content goes here</main>
  <footer>Copyright notice</footer>
</div>
```

### Out of bounds items

- Imagine you create an explicit Grid with 1 column and 3 rows.
- What happens if you create more than 3 children?

```HTML
<style>
  .wrapper {
    display: grid;
    grid-template-rows: 1fr 1fr 1fr;
    height: 100vh;
  }
</style>

<div class="wrapper">
  <div class="item">1</div>
  <div class="item">2</div>
  <div class="item">3</div>
  <div class="item">4</div>
</div>
```

- for the 4th row, the browser creates it and squeezes it in. It doesn't create an overflow, just mean less space for the other elements.
- Misleading to think the entire grid is "implicit" or "explicit", more accurate to say individual rows/columns are implicit or explicit.
- An explicit grid can still generate implicit columns or rows if we add additional children.

### Gap

- As with Flexbox, we can build gutters into our gird with `gap`

```HTML
<style>
  .wrapper {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 8px;
  }
</style>

<div class="wrapper">
  <div class="item">1</div>
  <div class="item">2</div>
  <div class="item">3</div>
  <div class="item">4</div>
  <div class="item">5</div>
  <div class="item">6</div>
  <div class="item">7</div>
</div>
```

- What if we want there to be a gap between rows and not columns?
- You can specify two values `gap: 8ps 0px`

### The repeat function

- Say you had a 6 column layout, a calender with some meta data for example.
- You could lay out the CSS like this.

```CSS
.calendar {
  grid-template-columns:
    250px 1fr 1fr 1fr 1fr 1fr;
}
```

- But that is annoying to have to repeat for each column
- For this, you can use `repeat()` function

```CSS
.calendar {
  grid-template-columns: 250px repeat(5, 1fr);
}
```

- We are saying, give me 6 columns, the first one is 250px, and the rest 1fr

## Exercises with Grid

- Build a [Mondrifans style](https://courses.joshwcomeau.com/css-for-js/07-css-grid/05-grid-construction) site with grid

```HTML
<style>
html, body {
  height: 100%;
}
.wrapper {
  --blue: hsl(250deg 100% 55%);
  --yellow: hsl(50deg 100% 50%);
  --red: hsl(350deg 100% 45%);
  --white: hsl(0deg 0% 100%);
  display: grid;
  grid-template-columns: 200px 1fr;
  grid-template-rows: 200px 1fr;
  gap: 32px 16px;
  min-height: 100%;
}
body {
  background: hsl(0deg 0% 2%);
  padding: 0;
  margin: 0;
}
.blue-box {
  background: var(--blue)
}
.red-box {
  background: var(--red);
}
header {
  background: var(--yellow);
  display: flex;
  justify-content: flex-end;
  align-items: flex-end;
  padding: 8px 16px;
}
main {
  background: var(--white);
}
</style>

<div class="wrapper">
  <div class="blue-box"></div>
  <header>
    <h1>Mondrifans</h1>
  </header>
  <div class="red-box">asdfasdf</div>
  <main></main>
</div>
```

- Build a Calendar Component

```CODE
function Calendar() {
  return (
    <Wrapper>
      {DAYS.map(day => (
        <Day key={day}>
          {day}
        </Day>
      ))}
    </Wrapper>
  );
}
const Wrapper = styled.div`
  border: 3px solid;
  display: grid;
  grid-template-columns: repeat(7, 2rem);
  gap: 4px;
  width: max-content;
  padding: 16px;
`;
const Day = styled.div`
  border: 2px solid;
  border-radius: 4px;
  height: 2rem;
  display: flex;
  justify-content: center;
  align-items: center;
`;
const DAYS = [
  1,
  2,
  3,
  4,
  5,
  6,
  7,
  8,
  9,
  10,
  11,
  12,
  13,
  14,
  15,
  16,
  17,
  18,
  19,
  20,
  21,
  22,
  23,
  24,
  25,
  26,
  27,
  28,
  29,
  30,
];
render(<Calendar />);
```

## Alignment

- CSS Grid is kinda similar to flexbox alignment `justify-content` and `align-items` but work a little different.
- The default behavior in Grid is to stretch the clumns to take up all available space.
- `justify-content: center` will overide this behaviour
- In order to center the column, is has to look at the contents of each row and figure out which one is the widest.
- Only if you don't specify an explicit width
- Similar to Flexbox, you can use `start` and `end` but without the `flex-` part
- We also have distrubuted options, like flexbox, `space-between`, `space-around`, and `space-evenly`. For when our grid has multiple columns
- `justify-content` allos us to cahnge hwo our columns are distrubuted, but there is another property we need to know.
- `justify-items`, at first glance this seems strange, columns aren't supposed to change their width across different rows. It should be consistent width
- Looking closer, the columns are full width, just the items within the columns have been shrunk down and centered
- Normally, a grid child will stretch across the entire width of it's column.
- `justify-items` changes this behavior so the child elements moves aroudn within it's cell
- In othe  words:
  - `justify-content` applies to teh grid structure, changing the columns
  - `justify-items` applies to the child elements, without affecting the shape of the grid
- Different value  for `-content` and `-items`; don't have any "space" variants with `justify-items`
- `space-` variants only work when trying to distribute multiple thigns in a shared space. `justify-items` is only concerned with a single item within it's own cell.

## Aligning rows

- In Grid, `align-content` is how we align rows in our grid.

```HTML
<style>
  header, section, footer {
    border: 1px solid;
  }
  .wrapper {
    display: grid;
    align-content: space-between;
    height: 300px;
  }
</style>

<div class="wrapper">
  <header>Hello World</header>
  <section>Stuff here</section>
  <footer>Copyright notice</footer>
</div>
```

- Because `align-content` is set to `space-between`, the grid has shifted the rows to be as far apart from each other as possible. And because we haven't specified a height, the rows are given an "explicit" height.
- Note, this only works because we geve our grid a fix height

- What about `align-items`, it controls the elements vertical position within the row
- With `align-items`, we control the placement of individual elements within each cell

```HTML
<style>
  header, section, footer {
    border: 1px solid;
  }
  .wrapper {
    display: grid;
    height: 300px;
    align-items: center;
    border: 2px solid pink;
  }
</style>

<div class="wrapper">
  <header>Hello World</header>
  <section>Stuff here</section>
  <footer>Copyright notice</footer>
</div>
```

## Self-alignment

- In flexbox, the `align-items` is used on the parent to control the cross axis position for all child elements.
- But you can use `align-self` to overrule it:

```HTML
<style>
  .wrapper {
    display: flex;
    align-items: center;
    gap: 16px;
    height: 100%;
    padding: 16px;
    border: 2px solid;
  }

  /*
    The last child should sit at the top
    of the row, instead of the center
  */
  .box:last-of-type {
    align-self: flex-start;
  }

  .box {
    width: 80px;
    height: 80px;
    background: black;
  }

  html, body {
    height: 100%;
  }
</style>
<div class="wrapper">
  <div class="box"></div>
  <div class="box"></div>
  <div class="box"></div>
  <div class="box"></div>
</div>
```

- In CSS Grid, `align-self` works pretty muc hteh same way. We apply it to a specific grid children, and it changes the vertical (cross axis) position wihtin the grid cell.
- We also have `justify-self` which changes an elements *horizontal* position within a grid cell

```HTML
<style>
  .wrapper {
    display: grid;
    grid-template-columns: 1fr 1fr;
    grid-template-rows: 1fr 1fr;
    align-items: center;
    justify-items: center;
    height: 100%;
    border: 2px solid;
  }

  /*
    The last child should move to the
    bottom-right corner of its cell,
    instead of the center.
  */
  .box:last-of-type {
    align-self: end;
    justify-self: end;
  }

  .box {
    width: 80px;
    height: 80px;
    background: black;
  }

  html, body {
    height: 100%;
  }
</style>
<div class="wrapper">
  <div class="box"></div>
  <div class="box"></div>
  <div class="box"></div>
  <div class="box"></div>
</div>
```

## When to use item vs content

- With CSS Grid, by default, the children will fill the space
- If you want to position items within each grid cell, then use `align-` and `justify-`
- When to use `-items`, when you want to change how they are positioned relative to each other, use `-items`
- If you want to change the entire group is positioned, then use `-content` property
- Playground, play with the `-content` and `-items` to see the difference

```HTML
<style>
body {
  background: silver;
}

.card {
  background: white;
  padding: 16px;
  border-radius: 8px;
}

.card h2 {
  margin-bottom: 8px;
}
.wrapper {
  display: grid;
  grid-template-columns: 250px 250px;
  justify-content: center;
  align-items: start;
  gap: 16px;
}
</style>

<div class="wrapper">
  <article class="card">
    <h2>This card has a heading</h2>
    <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Fusce finibus lorem ac risus tincidunt vulputate. Aenean aliquet ultricies mauris sed interdum. Vestibulum faucibus condimentum porta.</p>
  </article>
  <article class="card">
    <h2>This one does too!</h2>
    <p>Curabitur vel tempus odio. Nunc et aliquet lectus, a ultrices metus. Nam scelerisque porta metus, vitae ultricies nisi mollis nec.</p>
  </article>
  <article class="card">
    <h2>So does this one</h2>
    <p>Integer at venenatis nunc. Sed in dui viverra, facilisis metus sed, varius risus. Interdum et malesuada fames ac ante ipsum primis in faucibus. Vivamus elementum tempor enim non maximus. Sed tellus ipsum, sollicitudin sit amet aliquam quis, semper sit amet eros.</p>
  </article>
  <article class="card">
    <h2>Yep, another heading in this one</h2>
    <p>Sed accumsan sed orci vel tristique. Aliquam erat volutpat. Vivamus id eros eleifend, mattis velit non, feugiat leo. Maecenas rutrum felis erat, in malesuada felis placerat ut.</p>
  </article>
</div>
```

## Grid Exercises

- Diagonals, use grid alignment to create a diagonal set of boxes

```HTML
<style>
  .wrapper {
  display: grid;
  grid-template-rows: repeat(3, 1fr);
  min-height: 100%;
}

.box {
  width: 50%;
}

.box.one {
  background-color: pink;
  justify-self: end;
}
.box.two {
  background-color: lavender;
  justify-self: center;
}
.box.three {
  background-color: peachpuff;
  justify-self: start;
}

html, body {
  height: 100%;
}
</style>
<div class="wrapper">
  <div class="box one"></div>
  <div class="box two"></div>
  <div class="box three"></div>
</div>
```

## Grid Areas

- `grid-template-areas` and `grid-area` give you the ability to name regions of a grid and assign elements to them.
- `grid-template-areas`, you have quotes `''` and multiple lines. And each line represents a row
- NOTE: you still have to specify your `grid-template-columns` and `grid-template-rows`

```CSS
.wrapper {
  display: grid;
  grid-template-areas:
   ''
   '';
}
```

- Then you choose a name for your areas

```CSS
.wrapper {
  display: grid;
  grid-template-areas:
   'sidebar header'
   'sidebar main';
}
```

- Because `sidebar` area is used in multipe rows, it spans the rows
- The next thing, you have to assign elements to the areas with `grid-area`
- When you have areas with the same name, it will span those areas across columns

```HTML
<style>
.wrapper {
  display: grid;
  grid-template-areas:
   'sidebar header'
   'sidebar main';
}

aside {
  /* tells grid to span both cells in the same column */
 grid-area: sidebar; 
}

header {
 grid-area: header;
}

main {
  grid-area: main;
}
</style>

<div class="wrapper">
  <aside>Aside</aside>
  <header>Header</header>
  <main>Main<main>
</div>
```

## Exercise, Holy Grail Layout

- Try and create the holy grail layout
- NOTE: when using `grid-template-areas` you have to specify the `grid-template-columns` and `grid-template-rows`

```HTML
<!--
• The layout should span the entire page.
• A header should use a <header> tag, and be 4rem tall.
• The sidebar should use a <nav> tag, and be 200px wide.
• The main content area should use <main>, and fill the available space.
• The ad unit should use an <aside> tag, and be 150px wide.
• The footer should use a <footer> tag, and be 5rem tall.
-->

<style>
  /*
  These styles are purely presentational,
  to make your grid children more distinctive
  */
  header, nav, aside, main, footer {
    border: 3px solid;
    padding: 16px;
  }

  header {
    border-color: hsl(45deg 100% 50%);
    background-color: hsl(45deg 100% 50% / 0.2);
  }
  nav {
    border-color: hsl(170deg 100% 35%);
    background-color: hsl(170deg 100% 35% / 0.2);
  }
  main {
    border-color: hsl(220deg 100% 50%);
    background-color: hsl(220deg 100% 50% / 0.2);
  }
  aside {
    border-color: hsl(300deg 100% 45%);
    background-color: hsl(300deg 100% 45% / 0.2);
  }
  footer {
    border-color: hsl(350deg 100% 60%);
    background-color: hsl(350deg 100% 60% / 0.2);
  }

  body {
    padding: 0;
    margin: 0;
  }
  /* TODO */
  html, body {
   height: 100%;
  }
  
  .wrapper {
    display: grid;
    min-height: 100%:
    grid-template-columns: 200px 1fr 150px;
    grid-template-rows: 4rem 1fr 5rem;
    grid-template-areas:
     'header header header'
     'nav main aside'
     'footer footer footer'
     ;
  }
  
  header {
    grid-area: header;
  }
  
  nav {
    grid-area: nav;
  }
  
  main {
    grid-area: main;
  }
  
  aside {
    grid-area: aside;
  }
  
  footer {
    grid-area: footer;
  }
</style>

/* TODO */
<div class="wrapper">
  <header>Header</header>
  <nav>Nav</nav>
  <main>Main</main>
  <aside>Aside</aside>
  <footer>Footer</footer>
</div>
```

## Tracks and Lines

- `grid-template-areas` and `grid-area` is an API that is syntactic sugar, code that makes it easier to understand what is giong on.
- To truly understand how CSS Grid works, we need to understand how the algorithm sees the grid structure.
- Grids are composed of tracks and lines
- We can use grid lines to assign children

### How to control where an area sits in our grid, another way to do it

- Imagine a 4 column grid, think of it as starting at grid line 1, and stops at grid line 2
- If you want to place an item within a specific column, refer to the grid line numbers for column and row
- `grid-column: 3 / 4;` tells CSS Grid to put that item within the column numbers 3 and 4
- `grid-row: 2 / 3;` same as above, instructs CSS Grid to put this item within row numbers 2 and 3
- The `/` is confusing, it's not division, just a sperator `3 / 4` we are saying, start at this line `3`, seperator `/`, and end at this line `4`
- TRACK, in the specification, means either a row or column
- If you are not going to span multiple rows or columns, you can omit the `/`, and just specify the starting line number, `grid-column: 3` for example, will put the item within that part of the grid, NOTE: this is just shorthand for the `3 / 4`

### WHAT'S UP WITH THE NEGATIVE NUMBERS?

- Two differ labels, positive and negative `3 / 4` or `-3 / -4`
- The POSITIVE number start at top left corner and count down, left to right, top to bottom
- The NEGATIVE number, is the opposite, start at the right, and go to the left, right to left, bottom to top
- Why do we need two ways to do the same thing?
- You can mix and match the values
- For example, if you want to always span the entire width or height of something
- Span the entire height of a grid, `grid-row: 1 / -1`, this will span as many tracks as you want
- The lines, are always 0px thick
- How does `gap` push things? Imagine it as the line getting thicker
- The ability to span rows and columns, is a switch in mental model.

```HTML
<style>
  .wrapper {
    display: grid;
    height: 100vh;
    grid-template-columns: repeat(4, 1f);
    grid-template-rows: repeat(4, 1fr);
  }
  .box {
    background: pink;
    grid-column: 3 / 4;
    grid-row: 2 / 3;
  }
</style>
<div class="wrapper">
  <div class="box"></div>
</div>
```

### Keyboard gotchas

- Consider visually impaired users when layout your grid and positioning elements.
- With `grid-column` and `grid-row` you can position an element within a Grid and the DOM order doesn't matter.
- This can be disorienting for keyboard only visually impaired users.

## Fluid Grids

- One of the most famous CSS Grid snippets looks like this.
- This snippet, creates a Grid with a dynamic number of columns and it will try and pack as many in as it can staying above the min size 150px.
- This is also a complicated snippet

```HTML
<style>
  body {
  margin: 0;
  padding: 0;
}
.grid {
  padding: 16px;
  }
  .item {
    height: 225px;
    background: white;
    border-radius: 8px;
    padding: 16px;
  }
  .grid {
    display: grid;
    gap: 16px;
    grid-template-columns:
      repeat(auto-fill, minmax(150px, 1fr));
  }
</style>

<main class="grid">
  <div class="item"></div>
  <div class="item"></div>
  <div class="item"></div>
  <div class="item"></div>
  <div class="item"></div>
  <div class="item"></div>
</main>
```

### Clamping with minmax

- Ealier in the lesson we saw how `min`, `max` and `clamp` functions can be sued to contrain a value with upper and lower bounds.
- CSS Grid has a similar function: `minmax`
- Here is an example
- What's going on here: you have two equal columns `1fr`, but the first column should never shrink below 50px. While the second should never shrink below 250px.
- It's another way to set `min-width` on our grid columns.
- You can also use for height, to set a `min-height` with `grid-template-rows`
- NOTE: the flexible unit has to come last, because `1fr` isn't a valid minimum value, `minmax(250px, 1fr)`

```HTML
<style>
  body {
    margin: 0;
    padding: 0;
  }
  .grid {
    padding: 16px;
  }
  .card {
    height: 225px;
    background: white;
    border-radius: 8px;
    padding: 16px;
  }
  .grid {
    display: grid;
    gap: 16px;
    grid-template-columns:
      minmax(50px, 1fr)
      minmax(250px, 1fr);
  }
</style>

<main class="grid">
  <div class="card"></div>
  <div class="card"></div>
</main>
```

### Generating coluns with auto-fill

- Earlier we saw how `repeat` function can save you a bit of typing

```CSS
.grid {
  grid-template-columns: repeat(7, 1fr);
  /*
    ...is equivalent to:
    grid-template-columns: 1fr 1fr 1fr 1fr 1fr 1fr 1fr;
  */
}
```

- `repeat` is another neat trick, it accepts special keywords in addition to numbers
- Say ou have come cards that are 150px wide, and you want to fill the grid with as many cards as possible. You can do that with `auto-fill`
- `grid-template-columns: repeat(auto-fill, 150px);`

```HTML
<style>
  .grid {
    display: grid;
    gap: 16px;
    grid-template-columns:
      repeat(auto-fill, 150px);
  }
  body {
    margin: 0;
    padding: 0;
  }
  .grid {
    padding: 16px;
  }
  .card {
    height: 250px;
    background: white;
    border-radius: 8px;
    padding: 16px;
  }
</style>

<main class="grid">
  <div class="card"></div>
  <div class="card"></div>
  <div class="card"></div>
  <div class="card"></div>
  <div class="card"></div>
  <div class="card"></div>
</main>
```

- When the availabel space isn't perfect multiple of 150px, we have some leftover space, we can control that with `justify-content`

```HTML
<style>
  .grid {
    display: grid;
    gap: 16px;
    grid-template-columns:
      repeat(auto-fill, 150px);
    justify-content: space-evenly;
  }
</style>

<main class="grid">
  <div class="card"></div>
  <div class="card"></div>
  <div class="card"></div>
  <div class="card"></div>
  <div class="card"></div>
  <div class="card"></div>
</main>
```

- `auto-fill` allows us to implement fliod principles in CSS Grid.

### Putting them all together

- Now we can put it all together in our cool grid snippet
- `minmax` will let us clamp a value to a specific range
- `repeat` takes a special value
- `auto-fill` will generate a dynamic number of columns
- Put it all together to create the snazzy Grid Snippet

```HTML
<style>
  body {
  margin: 0;
  padding: 0;
  }
  .grid {
    padding: 16px;
  }
  .item {
    height: 225px;
    background: white;
    border-radius: 8px;
    padding: 16px;
  }

  body {
    margin: 0;
    padding: 0;
  }
  .grid {
    padding: 16px;
  }
  .item {
    height: 225px;
    background: white;
    border-radius: 8px;
    padding: 16px;
  }
  /* Famous Snippet */
  .grid {
    display: grid;
    gap: 16px;
    grid-template-columns:
      repeat(auto-fill, minmax(150px, 1fr));
  }
</style>

<main class="grid">
  <div class="item"></div>
  <div class="item"></div>
  <div class="item"></div>
  <div class="item"></div>
  <div class="item"></div>
  <div class="item"></div>
</main>
```

### auto-fill vs. auto-fit

- In addition to the `auto-fill` keyword, we also have `auto-fit`
- Mostly can be used interchangeably, on differnce though
- Le't pretend we are rendering a dynamic list of data, you could have 20 items, 40 or 2
- What should happen with the extra space?
- `auto-fill` you will have lots of empty columns
- `auto-fit` will stretch to ultra-wide columns

```HTML
<style>
  .grid {
    display: grid;
    justify-content: space-evenly;
    gap: 16px;
    /*
      Try changing “auto-fill” to
      ”auto-fit”, when fullscreened:
    */
    grid-template-columns:
      repeat(auto-fill, 150px);
  }
</style>

<main class="grid">
  <div class="card"></div>
  <div class="card"></div>
</main>
```

### Responsive Tweaks

- What happens if our minimum size is larger and causes an overflow situation?
- Notice on smaller screens, this causes an overflow

```HTML
<style>
  body {
  margin: 0;
  padding: 0;
  }
  .grid {
    padding: 16px;
  }
  .item {
    height: 225px;
    background: white;
    border-radius: 8px;
    padding: 16px;
  }
  .grid {
    display: grid;
    gap: 16px;
    grid-template-columns:
      repeat(auto-fill, minmax(400px, 1fr));
  }
</style>

<main class="grid">
  <div class="item"></div>
  <div class="item"></div>
  <div class="item"></div>
  <div class="item"></div>
  <div class="item"></div>
  <div class="item"></div>
</main>
```

- You can always use a media query to change the grid structure below a certain size
- When the viewport is smaller, we stick with simple grid layout, single column
- But on larger screens, we use Famous Snippet

```CSS
@media (min-width: 450px) {
    .grid {
      grid-template-columns:
        repeat(
          auto-fill,
          minmax(400px, 1fr)
        );
    }
```

- Or use the **fliud approach**
- What's going on here with this snippet?
- The first part to get evaluated, `min(400px, 100%)`, 100% refers to the `.grid` elements width, if viewing on a large monitor at 800px wide, then 100% resolves to 800px.
- `min()` picks the smaller of the two values, so on a large monitor, 400px is returned form the expression
- On smaller screen, 100% might only be 250px, in this case 100% is returned since it's smaller than the alternative 400px option
- Once we found which value is smaller, we plug it into the "Famous" snippet

```HTML
<style>
  body {
  margin: 0;
  padding: 0;
  }
  .item {
    height: 225px;
    background: white;
    border-radius: 8px;
    padding: 16px;
  }
  .grid {
    display: grid;
    padding: 16px;
    gap: 16px;
    /* Famous Snippet */
    grid-template-columns:
      repeat(
        auto-fill,
        minmax(min(400px, 100%), 1fr)
      );
  }
</style>

<main class="grid">
  <div class="item"></div>
  <div class="item"></div>
  <div class="item"></div>
  <div class="item"></div>
  <div class="item"></div>
  <div class="item"></div>
</main>
```

## Exercise - World Famous Snippet

- For this exercise, implement the world famous snippet without copy/paste
- The `min` inside of the `minmax` is tricky to follow.
- `min(320px, 100%)` is saying, pick the smaller of the two values based on size of the element. In cases with small screensizes, once it gets below 320px, it will choose the % value. Because the % value calculates smaller then 320px.
- Good way to prevent overflow, on small screen sizes.

```HTML
<!--
• 320px minimum column width
• 16px gap
• No overflow on smaller screens
-->

<style>
  body {
  margin: 0;
  padding: 0;
  }
  .grid {
    filter: drop-shadow(0px 2px 8px hsl(0deg 0% 0% / 0.25))
  }
  .item {
    height: 75px;
    background: white;
    border-radius: 4px;
  }
  .grid {
    /* variable to pick smaller of two values based on item size */
    --min-column-width: min(320px, 100%);
    display: grid;
    padding: 16px;
    /* World Famous Snippet */
    grid-template-columns: repeat(auto-fill, minmax(var(--min-column-width), 1fr));
    gap: 16px;
  }
</style>

<main class="grid">
  <div class="item"></div>
  <div class="item"></div>
  <div class="item"></div>
  <div class="item"></div>
  <div class="item"></div>
  <div class="item"></div>
</main>
```

## Subgrid

- One limitation of CS Grid v1, is every grid element must be a direct child of the grid parent.
- For example, we have a list of items, we want each list item to be assigned to our CSS Grid
- The grid children will be `header`, `aside` and `ul`
- The `li` cannot participate in the grid, since they are grandchildren
  
```HTML
<div class="grid">
  <header>Header</header>
  <aside>Sidebar</aside>
  <ul>
    <li>First Item</li>
    <li>Second Item</li>
  </ul>
</div>
```

- CSS Grid v2, introduces subgrid, a keyword to allow grandchildren to access the grid structure
- CANIUSE, this is only supported in Firefox, as I write this note, Jan, 8, 2022

## Grid Dividers

- Neat trick if you want to show some borders around your grid.
- Can't do this with showing grid lines
- Instead you use `background-color` and `gap` on the grid children and the entire grid
- The grid container is given a hot-pink background, but it only shows in small spaces between and around the grid children using `gap`

```HTML
<style>
  .wrapper {
  max-width: 550px;
  margin: 0 auto;
  }

  .story img {
    width: 100%;
    height: 200px;
    object-fit: cover;
    border-radius: 4px;
  }

  .featured.story {
    grid-column: 1 / -1;
  }
  .wrapper {
    --hot-pink: hsl(340deg 100% 50%);
    display: grid;
    grid-template-columns: 1fr 1fr;
    padding: 2px;
    gap: 2px;
    background-color: var(--hot-pink);
  }
  
  .story {
    background-color: white;
    padding: 24px;
  }
</style>

<div class="wrapper">
  <article class="featured story">
    <img src="/course-materials/meerkat.jpg" alt="A curious meerkat pops up" />
    <h2>
      Study: Meerkats unseat dolphins as nature's smartest animal
    </h2>
    <p>
      Meanwhile, humans come in 4th, right after the surprisingly-wiley platypus.
    </p>
  </article>
  <article class="story">
    <img src="/course-materials/night-sky.jpg" alt="A vibrant shot of the night sky" />
    <h2>
      The Search for Extra-Terrestrial Life
    </h2>
    <p>
      In Ukraine, a team of dedicated interdisciplinary professionals work to answer one of history's longest unanswered questions: what's going on, up there?
    </p>
  </article>
  <article class="story">
    <img src="/course-materials/wall-art.jpg" alt="A colorfully-lit hallway" />
    <h2>
      The TIFF's Must-Watch List
    </h2>
    <p>
      As the Toronto International Film Festival picks up, 5 intrepid reporters will dedicate the week to watching every available film. At the top of the list so far: “Ephemeral Hallway”.
    </p>
  </article>
</div>
```

## Inset Borders

- Another approach, you can apply borders to specific grid children
- And use padding to increase the distance

```HTML
<style>
  .wrapper {
  max-width: 550px;
  margin: 0 auto;
  }

  .story img {
    width: 100%;
    height: 200px;
    object-fit: cover;
    border-radius: 4px;
  }

  .featured.story {
    grid-column: 1 / -1;
  }
  .wrapper {
    --hot-pink: hsl(340deg 100% 50%);
    display: grid;
    grid-template-columns: 1fr 1fr;
    border: 2px solid var(--hot-pink);
    padding: 24px;
  }
  
  .featured.story {
    padding-bottom: 24px;
    margin-bottom: 24px;
    border-bottom:
      2px solid var(--hot-pink);
  }
  
  .story:nth-of-type(2n) {
    padding-right: 24px;
    border-right:
      2px solid var(--hot-pink);
  }
  .story:nth-of-type(2n + 3) {
    padding-left: 24px;
  }
</style>

<div class="wrapper">
  <article class="featured story">
    <img src="/course-materials/meerkat.jpg" alt="A curious meerkat pops up" />
    <h2>
      Study: Meerkats unseat dolphins as nature's smartest animal
    </h2>
    <p>
      Meanwhile, humans come in 4th, right after the surprisingly-wiley platypus.
    </p>
  </article>
  <article class="story">
    <img src="/course-materials/night-sky.jpg" alt="A vibrant shot of the night sky" />
    <h2>
      The Search for Extra-Terrestrial Life
    </h2>
    <p>
      In Ukraine, a team of dedicated interdisciplinary professionals work to answer one of history's longest unanswered questions: what's going on, up there?
    </p>
  </article>
  <article class="story">
    <img src="/course-materials/wall-art.jpg" alt="A colorfully-lit hallway" />
    <h2>
      The TIFF's Must-Watch List
    </h2>
    <p>
      As the Toronto International Film Festival picks up, 5 intrepid reporters will dedicate the week to watching every available film. At the top of the list so far: “Ephemeral Hallway”.
    </p>
  </article>
</div>
```

## Grid Recipes

### TWO LINE CENTER

- The good ole center horizontally and center vertically
- With Flexbox, this because a lot easier, we can just do

```HTML
<style>
/* Cosmetic styles */
.wrapper {
  height: calc(100vh - 16px);
  border: 3px solid;
}

.box {
  width: 100px;
  height: 100px;
  background: peachpuff;
}
.wrapper {
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>

<section class="wrapper">
  <div class="box"></div>
</section>
```

- In CSS Grid, we ues the same trick
- For consistency, we will use `align-content` instead of `align-items`

```HTML
<style>
  /* Cosmetic styles */
  .wrapper {
    height: calc(100vh - 16px);
    border: 3px solid;
  }

  .box {
    width: 100px;
    height: 100px;
    background: peachpuff;
  }
  .wrapper {
    display: grid;
    justify-content: center;
    align-content: center;
  }
</style>

<section class="wrapper">
  <div class="box"></div>
</section>
```

- SHORTHAND, because we are setting `justify-content` and `align-content` to the same value, we can take advantage of `place-content: center`

```HTML
<style>
  /* Cosmetic styles */
  .wrapper {
    height: calc(100vh - 16px);
    border: 3px solid;
  }

  .box {
    width: 100px;
    height: 100px;
    background: peachpuff;
  }
  /* Grid shorthand */
  .wrapper {
    display: grid;
    place-content: center;
  }
</style>
<div class="wrapper">
  <div class="box"></div>
</div>
```

- `place-content` property will set both `justify-content` and `align-content` at the same time. That means we have a 2 decloration centering trick. Modern CSS is really cool.

## Sticky Grids

- You don't have to choose just one grid layout mode. You can mix and match
- Super dense section, but here is the code for applying sticky elements wihtin a grid context
- [Video overview](https://courses.joshwcomeau.com/css-for-js/07-css-grid/14-sticky-grids)

```HTML
<style>
  .grid {
    --header-height: 5rem;
    display: grid;
    grid-template-areas:
      'header header'
      'sidebar main'
      'footer footer';
    grid-template-columns: 14rem 1fr;
    gap: 16px;
    max-width: 1200px;
    margin: 0 auto;
    isolation: isolate;
  }

  header {
    grid-area: header;
    position: sticky;
    z-index: 2;
    top: 0;
    display: grid;
    place-content: center;
    height: var(--header-height);
    border-bottom: 3px solid;
    background-color: white;
  }

  /*
    The “aside” child is positioned according to
    grid layout, filling the assigned grid area.
  */
  aside {
    grid-area: sidebar;
    position: relative;
    z-index: 1;
  }

  .sticky-sidebar {
    position: sticky;
    top: var(--header-height);
  }

  main {
    grid-area: main;
    /*
      Add a bunch of height, to simulate it
      being full of content
    */
    min-height: 180vh;
    border: 3px solid;
  }

  /*
    NOTE: In the video, I added the following
    CSS to the footer:

    position: relative;
    z-index: 2;

    I've removed it from this final solution,
    because our sidebar doesn't overlap the
    footer anymore, so it isn't necessary.
  */
  footer {
    grid-area: footer;
    display: grid;
    place-content: center;
    height: 5rem;
    border-top: 3px solid;
    background-color: white;
  }

  .grid > * {
    padding: 8px;
  }

  body {
    margin: 0;
    padding: 0;
  }
</style>
<div class="grid">
  <header>
    <h1>My Website</h1>
  </header>
  <aside>
    <div class="sticky-sidebar">
      <h2>Chicken Cacciatore</h2>
      <nav>
        <ol>
          <li>Introduction</li>
          <li>Prep</li>
          <li>Cooking</li>
          <li>Reviews</li>
          <li>Introduction</li>
          <li>Prep</li>
          <li>Cooking</li>
          <li>Reviews</li>
          <li>Introduction</li>
          <li>Prep</li>
          <li>Cooking</li>
          <li>Reviews</li>
          <li>Introduction</li>
          <li>Prep</li>
          <li>Cooking</li>
          <li>Reviews</li>
          <li>Introduction</li>
          <li>Prep</li>
          <li>Cooking</li>
          <li>Reviews</li>
          <li>Introduction</li>
          <li>Prep</li>
          <li>Cooking</li>
          <li>Reviews</li>
          <li>Introduction</li>
          <li>Prep</li>
          <li>Cooking</li>
          <li>Reviews</li>
          <li>Introduction</li>
          <li>Prep</li>
          <li>Cooking</li>
          <li>Reviews</li>
        </ol>
      </nav>
    </div>
  </aside>
  <main>
    Main Content
  </main>
  <footer>
    Copyright notice
  </footer>
</div>
```

## Full Bleed Layouts

- What if you had a blog layout, and you wanted some media to break free of the flow, and bleed to full window width?
- Having an element stretch edge to edge, "full-bleed", a term borrowed from the publishing world
- Very common layout, blog post, single column

```HTML
<style>
  /* Cosmetic baseline styles */
  img {
    max-width: 100%;
  }
  h1 {
    margin: 32px 0;
  }
  p {
    margin: 16px 0;
  }
  body {
    padding: 0;
    margin: 0;
  }
  .max-width-wrapper {
    max-width: 30ch;
    padding: 32px;
    margin-left: auto;
    margin-right: auto;
  }
</style>

<div class="max-width-wrapper">
  <h1>Some Heading</h1>
  <p>
    Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since the 1500s, when an unknown printer took a galley of type and scrambled it to make a type specimen book. It has survived not only five centuries, but also the leap into electronic typesetting, remaining essentially unchanged.
  </p>
  <img
    alt="a satisfied-looking cute meerkat"
    src="/course-materials/meerkat.jpg"
    class="meerkat"
  />
  <p>
    It was popularised in the 1960s with the release of Letraset sheets containing Lorem Ipsum passages, and more recently with desktop publishing software like Aldus PageMaker including versions of Lorem Ipsum.
  </p>
</div>
```

- In CSS Grid, offers a clever solution to this problem
- Here is a solution with Grid
- **Grid Contruction**
  - 3 explicit columns
  - `1fr` on the left and `1fr` on the right, this will center the middle column `min(30ch, 100%)`
  - `min(30ch, 100%)`, this function clamps this value so that it never grows above 100% of the available space.
  - The two side columns `1fr`, act like `auto margins` and take up remaining space, making sure the middle column is centered
- **Column Assignments**
  - We want all children of this grid to be assined to the middle column.
  - So we use the wild card selector `*`
  - `.wrapper > * { grid-column: 2;}`, this means every child will be assigned to the 2nd column
  - Every child element of the grid will create it's own implicit row, and occupy the center column
  - NOTE: urban legend that wildcard selectors are bad for performance.
- **Full Bleed Children**
  - We need a way to opt into the full bleed layout
  - Any child element with the `.full-bleed` class will stretch from the first column line to the last
  - Why the negative number? This tells grid to start at the first column on the left, and end on the first column on the right. And future proofs your grid, incase you want to add more columns in the fugure.
  - This can lead to some very tall images. So you need to combine it with `object-fit`

```CSS
.full-bleed {
  grid-column: 1 / -1;
}
```

```CSS
.meerkat {
  display: block;
  width: 100%;
  height: 300px;
  object-fit: cover;
}
```

```HTML
<style>
  /* Cosmetic baseline styles */
  h1 {
    margin: 32px 0;
  }
  p {
    margin: 16px 0;
  }
  body {
    padding: 0;
    margin: 0;
  }
  .wrapper {
    display: grid;
    grid-template-columns:
      1fr
      min(30ch, 100%)
      1fr;
  }
  .wrapper > * {
    grid-column: 2;
  }
  .full-bleed {
    grid-column: 1 / -1;
  }
  
  .meerkat {
    display: block;
    width: 100%;
    height: 300px;
    object-fit: cover;
  }
</style>

<main class="wrapper">
  <h1>Some Heading</h1>
  <p>
    Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since the 1500s, when an unknown printer took a galley of type and scrambled it to make a type specimen book. It has survived not only five centuries, but also the leap into electronic typesetting, remaining essentially unchanged.
  </p>
  <div class="full-bleed">
    <img
      alt="a satisfied-looking cute meerkat"
      src="/course-materials/meerkat.jpg"
      class="meerkat"
    />
  </div>
  <p>
    It was popularised in the 1960s with the release of Letraset sheets containing Lorem Ipsum passages, and more recently with desktop publishing software like Aldus PageMaker including versions of Lorem Ipsum.
  </p>
</main>
```

- **Adding Gutters**
  - Notice on small screens, things are very cramped
  - How do we add any gap or padding to our grid, without affecting the full bleed?
  - By adding some padding to the wrapper, our full bleed is no longer
  - You solve this by using negative margin on our full bleed children
  - The container adds 16px of padding, but the item you want to full bleed will undo that with the negative margin trick.

```CSS
.wrapper {
  display: grid;
  grid-template-columns:
    1fr
    min(30ch, 100%)
    1fr;
  padding-left: 16px;
  padding-right: 16px;
}

```CSS
.full-bleed {
    grid-column: 1 / -1;
    /* negative margin trick to undo the padding and make full-bleed */
    margin-left: -16px;
    margin-right: -16px;
  }
```

- Full snippet

```HTML
<style>
  /* cosmetic styles */
  .meerkat {
  display: block;
  width: 100%;
  height: 300px;
  object-fit: cover;
  }
  h1 {
    margin: 32px 0;
  }
  p {
    margin: 16px 0;
  }
  body {
    padding: 0;
    margin: 0;
  }
  /* CSS Grid styles */
  .wrapper {
    display: grid;
    grid-template-columns:
      1fr
      min(30ch, 100%)
      1fr;
    padding-left: 16px;
    padding-right: 16px;
  }
  .wrapper > * {
    grid-column: 2;
  }
  .full-bleed {
    grid-column: 1 / -1;
    margin-left: -16px;
    margin-right: -16px;
  }
</style>

<main class="wrapper">
  <h1>Some Heading</h1>
  <p>
    Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since the 1500s, when an unknown printer took a galley of type and scrambled it to make a type specimen book. It has survived not only five centuries, but also the leap into electronic typesetting, remaining essentially unchanged.
  </p>
  <div class="full-bleed">
    <img
      alt="a satisfied-looking cute meerkat"
      src="/course-materials/meerkat.jpg"
      class="meerkat"
    />
  </div>
  <p>
    It was popularised in the 1960s with the release of Letraset sheets containing Lorem Ipsum passages, and more recently with desktop publishing software like Aldus PageMaker including versions of Lorem Ipsum.
  </p>
</main>
```

- Using CSS Variables, the only problem is this creates a dependency between the parent's padding and the child's margin. We can address this with CSS Variables.

```CSS
.wrapper {
    --breathing-room: 16px;
    display: grid;
    grid-template-columns:
      1fr
      min(30ch, 100%)
      1fr;
    padding-left: var(--breathing-room);
    padding-right: var(--breathing-room);
  }
  .wrapper > * {
    grid-column: 2;
  }
  .full-bleed {
    grid-column: 1 / -1;
    margin-left: calc(
      var(--breathing-room) * -1
    );
    margin-right: calc(
      var(--breathing-room) * -1
    );
  }
```

## Managing Overflow

- Say you have a grid child that holds a list of images. On smaller screens, you want to add a horizontal scrollbar.
- `fr` units are a way to divvy up leftover space. But it also reacts based on it's contents
- If we put a really large element in a grid child, the `fr` unit will grow to contain it
- EXAMPLE; the fr unit grows to be 1000px wide in order to contain the element.

```HTML
<style>
  .grid {
    display: grid;
    grid-template-columns: 175px 1fr;
    gap: 16px;
  }
  
  .box {
    width: 1000px;
    height: 200px;
    background-color: peachpuff;
  }
</style>

<div class="grid">
  <div class="intro">
    <h2>My Photos</h2>
    <p>Here are some animals I saw on holiday:
  </div>
  <div class="box-container">
    <div class="box"></div>
  </div>
</div>
```
  
### Solution 1: Moving the overflow

- We can solve this problem by moving our `overflow: auto` to the grid child directly:
- Why does this work? Maybe `fr` has a exception built in: if the grid child has `overflow: auto`, it give it permission to shrink with the browser.

```HTML
<style>
  .grid {
    display: grid;
    grid-template-columns: 175px 1fr;
    gap: 16px;
  }
  
  .box-container {
    overflow: auto;
  }
  
  .box {
    width: 1000px;
    height: 200px;
    background-color: peachpuff;
  }
</style>

<div class="grid">
  <div class="intro">
    <h2>My Photos</h2>
    <p>Here are some animals I saw on holiday:
  </div>
  <div class="box-container">
    <div class="box"></div>
  </div>
</div>
```

- Here is the original probelem, with multiple images to fit and scroll a list of images.

```HTML
<style>
  .image-list img {
  height: 200px;
  }

  ul {
    list-style-type: none;
    padding: 0;
    margin: 0;
  }
  .grid {
    display: grid;
    grid-template-columns: 175px 1fr;
    gap: 16px;
  }
  
  .image-container {
    overflow: auto;
  }
  
  .image-list {
    display: flex;
    gap: 16px;
    /*
      No more 'overflow: auto' or
      'max-width: 100%' here.
    */
  }
</style>

<div class="grid">
  <div class="intro">
    <h2>My Photos</h2>
    <p>Here are some animals I saw on holiday:
  </div>
  <div class="image-container">
    <ul class="image-list">
       <li>
        <img src="/course-materials/cat-four-300px.jpg" />
      </li>
      <li>
        <img src="/course-materials/otter.jpg" />
      </li>
       <li>
        <img src="/course-materials/dog-three-300px.jpg" />
      </li>
       <li>
        <img src="/course-materials/meerkat.jpg" />
      </li>
    </ul>
  </div>
</div>
```

### Solution 2: Setting a minimum width

- You can use `minmax` to tell CSS Grid, we are ok with shrinking below the child elements width
- by changing `1fr` to `minmax(0, 1fr)` we are telling the column that it can be as small as it wants. Don't worry about trying to stretch around the child element.

```HTML
<style>
  .image-list img {
  height: 200px;
  }

  ul {
    list-style-type: none;
    padding: 0;
    margin: 0;
  }
  .grid {
    display: grid;
    gap: 16px;
    
    /* This is the changed line: */
    grid-template-columns:
      175px minmax(0, 1fr);
  }
  
  /* This stuff is unchanged: */
  .image-list {
    display: flex;
    gap: 16px;
    max-width: 100%;
    overflow: auto;
  }
</style>

<div class="grid">
  <div class="intro">
    <h2>My Photos</h2>
    <p>Here are some animals I saw on holiday:
  </div>
  <div class="image-container">
    <ul class="image-list">
       <li>
        <img src="/course-materials/cat-four-300px.jpg" />
      </li>
      <li>
        <img src="/course-materials/otter.jpg" />
      </li>
       <li>
        <img src="/course-materials/dog-three-300px.jpg" />
      </li>
       <li>
        <img src="/course-materials/meerkat.jpg" />
      </li>
    </ul>
  </div>
</div>
```

## Grid Quirks

- A handful of starnge quirks when working with CSS Grid

### Row Limit

- In Chrome, grids are limited to 1000 rows. If an implicit grid is gien 1002 children, the final three children will occupy the same cell. NOTE: This has been increase in Chrome 96, now it's 100,000 rows.

### Margin Collapse

- Just like Flexbox, the margin will not collapse on grid children, in either direction.
- Margin collapse is a feature of Flow layout

```HTML
<style>
  .wrapper {
    display: grid;
  }
  
  p {
    margin: 30px;
  }
</style>

<div class="wrapper">
  <p>Hello World!</p>
  <p>The margins on these paragraphs won't collapse.</p>
  <p>Check it out in the devtools.</p>
</div>
```

### z-index works with grid children

- Normally `z-index` only works in positioned layout. The element neesd to be set to `position` to `relative` / `fixed` / `sticky`.
- But an exception has been made for CSS Grid: A grid child can use `z-index` even if it doesn't change the `position` property.
- Chagne the example below, by setting `z-index` on a grid child, it will change the stacking context.
- NOTE: Keep this in mind when layering your design elements.

```HTML
<style>
  .box {
  width: 50px;
  height: 50px;
  border: 3px solid;
  }
  .box.grid {
    background: pink;
  }
  .box.absolute {
    background: silver;
  }
  .wrapper {
    display: grid;
  }
  
  .box.grid {
    /*
      Change me to '1' to see
      the difference!
    */
    z-index: 3;
  }
  
  .box.absolute {
    position: absolute;
    z-index: 2;
    top: 20px;
    left: 20px;
  }
</style>

<div class="wrapper">
  <div class="box grid"></div>
  <div class="box absolute"></div>
</div>
```

### Weirdness with "fr" on rows

- The `fr` unit allows us to divvy up extra space in a grid container.
- Fine in with rows and columns within a specified height container. Gets weird in other situatons.
- The default behavior of a grid child, is that is grows to span the available area.
- What is you have an unknown height?
- The `fr` unit only works when you have a known amount of space
- So it knows how much space to divide up.
- If no height is speficied for the grid, the calculated height of the first grid child will become the definition for `1fr`
- Which means, it will apply that to all the other `fr` rows
- In the context of a row, when you don't have a specific height on a container, it's clever, maps itself to the grid children, in a way to make sure the grid contains the children.
- Makes sure all our rows are big enough to contain the children.
- [Video explanation](https://courses.joshwcomeau.com/css-for-js/video-archive/010-fr-in-depth)

```HTML
<style>
  .grid {
    display: grid;
    grid-template-rows: 1fr 1fr 1fr;
    /* no height is specified on the this element, remember, this is a flow layout element */
    /* grid is only applied to child elements */
  }
  
  .box {
    border: 2px solid;
  }
  .box.one {
    /* remove this height and watch what happens */
    height: 100px;
  }
</style>
<div class="grid">
  <div class="box one"></div>
  <div class="box two"></div>
  <div class="box three"></div>
</div>
```

## Workshop, Grid Workshop

- Build an online newspaper with CSS Grid, the New Grid Times
- Just getting everything set up for the exercise, React app etc.

### Exercise 1: Header

- Make a desktop version of the header from a mobile first header
- React app, using styled components
- [Figma Design](https://www.figma.com/file/BDdNhCeVLye5mFHHxQhkgE/New-Grid-Times?node-id=0%3A1)
- Instead of modifying the mobile version of the header to be desktop. Just hide the entire header with a media query, and turn on a new mobile header
- Strategy for layout out the header, with logo in the center, and elements on the left and right.

```CSS
const MainHeader = styled(MaxWidthWrapper)`
/* mobile first by default */
  display: flex;
  align-items: center;
  justify-content: center;
  margin-top: 32px;
  margin-bottom: 48px;

  @media ${QUERIES.laptopAndUp} {
    /* desktop with a media query */
    display: grid;
    /* set three columns */
    grid-template-columns: 1fr auto 1fr;
    align-items: center;
    justify-content: start;
  }
`;
```

- Layout tricks for the subscribe button, to properly align the subscribe button
- Uses a mix of CSS Grid, Absolute positioning, and Flow layout

```CSS
const SubscribeWrapper = styled.div`
  display: none;
  
  /* desktop styles */
  @media ${QUERIES.laptopAndUp} {
    display: revert;
    position: relative;
    justify-self: end;
  }
`;

const SubLink = styled.a`
  /* absolute positioning for the link */
  position: absolute;
  width: 100%;
  text-align: center;
  margin-top: 8px;
  /* font properties */
  font-size: 0.875rem;
  color: var(--color-gray-900);
  font-style: italic;
  text-decoration: underline;
`;
```

### Exercise 2: Fit and Finish

#### Text Truncation

- Ellipsis strategy for responsive views on the story preview.
- `-webkit-line-clamp` with `overlfow: hidden`

```CSS
const Abstract = styled.p`
  font-size: 1rem;
  margin-bottom: 1em;
  white-space: pre-wrap;
  /* ellipsis strategy, truncates base on # of lines and adds ellipsis but doesn't hide overflow */
  display: -webkit-box;
  -webkit-box-orient: vertical;
  -webkit-line-clamp: 8;
  /* necessary for line-clamping */
  overflow: hidden;

  @media ${QUERIES.tabletAndUp} {
    -webkit-line-clamp: 16;
  }

  @media ${QUERIES.laptopAndUp} {
    -webkit-line-clamp: 10;
  }
`;
```

- Mixing CSS Grid and `line-clamp`, the two algorythms can conflict with one another. Leaving some unexpected results and partial lines being displayed after the ellipsis.
- To solve for this, seperate the layout algorythms, and make the item holding the `line-clamp` flow layout. And add a wrapper that uses the `grid-area` layout.

#### Story Borders

- For each story, apply a border for more seperation using `last-of-type`

```CSS
const VerticalStoryWrapper = styled.div`
  /* last of type, apply this style to all elements except the last one */
  &:not(:last-of-type) {
    border-bottom: 1px solid var(--color-gray-300);
    padding-bottom: 16px;
    margin-bottom: 16px;
  }
`;
```

### Opinion Avatars

- Laying out sections using the world famous snippet, responsive card layouts

```CSS
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(165px, 1fr));
  gap: 16px;
```

- Check out your [repo and branch](https://github.com/clewisdavis/new-grid-times/tree/feature/my-workshop-branch) for Grid and responive tricks

## Module 8 - ANIMATIONS

- Animations help to make products feel premium, and helps our brain comprehend and make sense of things.
- Just like the real world, things don't just appear and disappear. They pass by us, the come and go. Our brains are not built for things to just happen.
- Apple understands this, and every interaction is considered with animations. When you lock/unlock and switch between devices. It brings a lot of life to the products.

### Transforms

- `transform` allows us to change a specified element in some way. We can move and contort our elements in many differ ways

#### Transform Functions

- Translation allos us to move an item around, x, y axis
- `transform: translate(3px, -2px)`
- We can use `translate` to shift an item along either axis, `x` side to side, `y` up and down.
- *Note: the items in-flow poistion doesn't change. Layout algorithms are not changed.
- Very similar to how `top`, `left`, `right`, `bottom` work with a positioned layout
- When you want to move an item along a single axis, use `translateX`, and `translateY`

```CSS
.box {
  transform: translateY(20px);
  /* It's equivalent to: */
  transform: translate(0px, 20px);
}
```

- Using %'s is really powerful, the % refers to the elemetns own size, instead of the availael space in the parent container.

```CSS
.box {
  transform: translate(-100%, 0%);
}
```

- Setting `transform: translateY(-100%)` moves the box up by it's exact height, no matter what the height is, to the pixel.
- Example of how transforms compares with other CSS properties like `left` absolute

```HTML
<style>
  /* base styles */
  .relative.box {
  background: deeppink;
  }
  .transform.box {
    background: navy;
  }

  .box {
    width: 80px;
    height: 80px;
  }
  .wrapper {
    position: relative;
    width: 90%;
    max-width: 500px;
    border: 4px solid;
  }
  /* comparison */
  .relative.box {
    position: relative;
    left: 50%;
  }
  .transform.box {
    transform: translateX(50%);
  }
</style>

<div class="wrapper">
  <div class="relative box"></div>
  <div class="transform box"></div>
</div>
```

- Using `calc` you can even add a buffer, the size of the element plus some extra spacing

```CSS
.box {
  transform: translateX(calc(100% + -3px));
}
```

#### Scale

- Another transform function, `scale`, allow us to grow or shrink an element
- `transform: scale(1)`, scale uses a unitless value that represents a multiple, similar to line-height. `scale(2)` mean that the element should be 2x as big as it would be.
- We can also pass multiple values in to scale, for `x`, `y`, `transform: scale(1, 1)`
- NOTE, we are not just scaling up the element, but all it's children
- Since scale will stretch and squash all the elements contents. This make it useful for animation.

#### Rotate

- Yup, `rotate` will rotate our elements
- `transform: rotate(0deg);`
- Typically use `deg` as the unit for rotation, but there is another.
- The `turn` unit represents how many turns the element should make. 1 turn is equal to 360 degrees. It's obscure but well supported.

#### Skew

- Finally the `skew` function, seldom used
- `transform: skew(0deg);`
- Same as `translate`, we can skew along either axis
- Skew can be helpful for decorative element, like diagonal layouts, [see blog post](https://9elements.com/blog/pure-css-diagonal-layouts/)

#### Transform Origin

- Every element has an *origin*, the anchor point the transform functions execute from.
- Can take multiple values, `transform-origin: left top`, see [mdn](https://developer.mozilla.org/en-US/docs/Web/CSS/transform-origin) for full list

```CSS
.box {
  transform: rotate(0deg);
  transform-origin: center;
}
```

#### Combining multiple operators

- We can string together multiple transform funcitons by space-seperating them.
- `transform: translateX(0px) rotate(0deg);`
- The order is important, they will be applied in order, sequentially.
- The transform functions are applied from right to left.
- Example animation, moon circling a planet.

```HTML
<style>
  /* starter styles */
  .wrapper {
  position: relative;
}

  .planet {
    width: 80px;
    height: 80px;
    background: dodgerblue;
    border-radius: 50%;
  }

  .moon {
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    margin: auto;
    width: 20px;
    height: 20px;
    background: silver;
    border-radius: 50%;
  }
  /* animation */
  @keyframes orbit {
    from {
      transform:
        rotate(0deg)
        translateX(80px);
    }
    to {
      transform:
        rotate(360deg)
        translateX(80px);
    }
  }
  
  @media (
    prefers-reduced-motion: no-preference
  ) {
    .moon {
      animation:
        orbit 6000ms linear infinite;
    }
  }
</style>

<div class="wrapper">
  <div class="planet"></div>
  <div class="moon"></div>
</div>
```

### Inline Elements

- Gatcha with transforms, is they don't work with inline elements in Flow layout.
- Inline elements go with the flow, and wrap around some content.
- Easiest fix is to switch it to use `display: inline-block`, or a different layout mode (Flexbox, Grid).

```HTML
<style>
  .inline-fella {
    background: hsl(50deg 90% 80%);
    padding: 4px;
  }
  .inline-fella {
    /* Doesn't work :( */
    transform: rotate(-10deg);
  }
</style>

<p>
  Why
  <span class="inline-fella">Hello</span>
  there!
</p>
```

#### Exercises, Animation

- A simple modal window with a centered viewport, and the close button sitting on top of the modal.

```HTML
<style>
.dialog-wrapper {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: hsl(0deg 0% 0% / 0.75);
  /* Good center center shorthand */
  display: grid;
  place-content: center;
}

.dialog-content {
  width: 600px;
  max-width: 100%;
  height: 400px;
  background: white;
  border-radius: 6px;
  position: relative;
}

.close-btn {
  position: absolute;
  top: 0;
  right: 0;
  padding: 16px;
  background: transparent;
  border: none;
  font-weight: normal;
  /* Note the 100%, which moves it up to the exact height of the element */
  transform: translateY(-100%);
  color: white;
  border: 1px solid red;
}
</style>
<div class="dialog-wrapper">
  <div class="dialog-content">
    <button class="close-btn">
      Close
    </button>
  </div>
</div>
```

### CSS Transitions

- `transitions` allows us to smooth out the changes that happen in our applications. Instead of things happening instantly, they glide between the two states.
- Here is an example of a button without a transition

```HTML
<style>
  .btn {
    width: 100px;
    height: 100px;
    border-radius: 50%;
    border: none;
    background: slateblue;
    color: white;
    font-size: 20px;
    font-weight: 500;
    line-height: 1;
  }
  .btn:hover {
    transform: translateY(-10px);
  }
</style>

<button class="btn">
  Hello World
</button>
```

- We can instruct the browser to interpolate one state to another with `transition`

```HTML
<style>
  /* starter style */
  .btn {
    width: 100px;
    height: 100px;
    border-radius: 50%;
    border: none;
    background: slateblue;
    color: white;
    font-size: 20px;
    font-weight: 500;
    line-height: 1;
  }
  .btn {
    transition: transform 250ms;
  }
  
  .btn:hover {
    transform: translateY(-10px);
  }
</style>

<button class="btn">
  Hello World
</button>
```

- `transtion` is highly configurable, but only two values are required
  - Name of the property we want to animate
  - The duration of the animation
- If you want to animate multiple properties, you pass in a comma-seperated list

```CSS
  .btn {
    transition: transform 250ms, opacity 400ms;
  }
  .btn:hover {
    transform: scale(1.2);
    opacity: 0;
  }
```

- NOTE: `transition-property` takes a special value of `all`, if may be tempting to use this value. But it's recommended to specify each property. In the future, someone may want to add a property and not want it to animate.

#### Timing Functions

- When we talk about motion on the web, we are talking about simulated motion. Remember keyframes in flash? It's more like a flipbook, each frame draws the element in a slightly differ position. If we do this fast enough, it appaers like a fluid motion.
- Timing function, lenear timing function, when teh element moves at a constant pace. A circle moves the same amount each frame.
- There are several timing functions available in CSS, you can specify which one you want with `transition-timing-function` property.

```CSS
.btn {
  transition: transform 250ms;
  transition-timing-function: linear;
}
```

- Or we can pass it indirectly to the `transitino` shorthand

```CSS
.btn {
  transition: transform 250ms linear;
}
```

- `linear` is rately the best choice, nothing really moves like this in the real world.
- `ease-out` comes in fast, but slows down at the end. When to use ease-out, when something is entering from off screen like a modal appearing, or a mobile menu slide out.
- `ease-in`, opposite of `ease-in`, starts out slow and speeds up. Mostly used for when an element goes offscreen or invisible. Otherwise the sudden stop can be jarring.
- `ease-in-out`, the combination of the two, it's symmetrical, equal amount of acceleration and deceleration.
- `ease`, **default value**, very similar to `ease-in-out, the difference being it isn't symmetrical. Brief ramp up and lots of deceleration.
- NOTE: time is constant, these functions describe how a value gets from 0 to 1 over a fixed tiem interval. Not how quickly the animation should complete.

#### Custom Curves

- You can define your own custom easing curve, using the cubic bezier timing function.
- The values above are just presets of the `cubit-bezier` function.
- The `linear` value can be defined as `cubic-bezier(0, 0, 1, 1)`.
- Coming up with your own can be tricky, refer to [Josh's post](https://courses.joshwcomeau.com/css-for-js/treasure-trove/011-cubic-bezier), and this [tool](https://cubic-bezier.com/#.17,.67,.83,.67).
- Or you can just choose from this preset [list of easing functions](https://easings.net/).

#### Delays

- Have you ever treid to mouse over a neted nav menu items, only to have it close before you get there? Like a sub nav item within a drop down popup.
- This can be solved without reaching for JS, with `transition-delay`

```CSS
.dropdown {
  opacity: 0;
  transition: opacity 400ms;
  transition-delay: 300ms;
}
.dropdown-wrapper:hover .dropdown {
  opacity: 1;
  transition: opacity 100ms;
  transition-delay: 0ms;
}
```

- This allows us to keep things as they are for a brief interval. In the example above, when the user move their mouse outside or `.dropdown-wrapper`, nothing happens for 300ms. After that, the `transition` kids in normally.

#### Doom flicker

- When you hover an element and it flickers because the animation has moved the element outside the hover.
- Before code sample, flicker

```HTML
<style>
  .btn {
    width: 100px;
    height: 100px;
    border: none;
    border-radius: 50%;
    background: slateblue;
    color: white;
    font-size: 20px;
    font-weight: 500;
    line-height: 1;
    transition: transform 250ms;
  }
  
  .btn:hover {
    transform: translateY(-10px);
  }
</style>

<button class="btn">
  Hello World
</button>
```

- After solution, we seperate the trigger from the effect. We listen for the hovers on the parent `<button>` element and apply the animation to the child element. This ensures the hover target will not move outside the cursor.

```HTML
<style>
  .btn {
    width: 100px;
    height: 100px;
    border: none;
    background: transparent;
    padding: 0;
  }
  
  .btn:hover .btn-contents {
    transform: translateY(-10px);
  }
  
  .btn-contents {
    display: grid;
    place-content: center;
    height: 100%;
    border-radius: 50%;
    background: slateblue;
    color: white;
    font-size: 20px;
    font-weight: 500;
    line-height: 1;
    transition: transform 250ms;
  }
</style>

<button class="btn">
  <span class="btn-contents">
    Hello World
  </span>
</button>
```

#### Exercises, Translated cards

- Update the set of cards to slide up on hover.
- Solution

```HTML
<style>
.wrapper {
  display: grid;
  grid-template-columns:
    repeat(auto-fit, minmax(150px, 1fr));
  gap: 8px;
  padding: 16px;
}
.card {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  min-height: 200px;
  background: white;
  border-radius: 8px;
  border: 2px solid hsl(240deg 100% 75%);
}
.card img {
  width: 64px;
  height: 64px;
}

.card {
  transition: transform 250ms ease-out;
}

a.card-link:hover .card {
 transform: translateY(-12px);
}
</style>
<div class="wrapper">
  <a href="/" class="card-link">
    <article class="card">
      <img
        alt="Download Chrome"
        src="/images/logos/chrome.svg"
      />
    </article>
  </a>
  <a href="/" class="card-link">
    <article class="card">
      <img
        alt="Download Firefox"
        src="/images/logos/firefox.svg"
      />
    </article>
  </a>
  <a href="/" class="card-link">
    <article class="card">
      <img
        alt="Download Safari"
        src="/images/logos/safari.png"
      />
    </article>
  </a>
  <a href="/" class="card-link">
    <article class="card">
      <img
        alt="Download Edge"
        src="/images/logos/edge.svg"
      />
    </article>
  </a>
  <a href="/" class="card-link">
    <article class="card">
      <img
        alt="Download Opera"
        src="/images/logos/opera.svg"
      />
    </article>
  </a>
</div>
```

#### Exercise: Photo Zoom

- Zoom in on a set of photos, but the the photo should not go outside it's element.

```HTML
<style>
  /* TODO */
  .thumbnail {
    transition: transform 500ms;
  }
  /* use overflow to hide the elements excess when zoomed */
  .thumbnail-wrapper {
    overflow: hidden;
  }
  
  a.thumbnail-wrapper:hover .thumbnail {
    transform: scale(1.2);
  }
</style>

<div class="wrapper">
  <a href="/" class="thumbnail-wrapper">
    <img
      alt="A balloon store"
      class="thumbnail"
      src="/course-materials/article-image-balloons.jpg"
    />
  </a>
  <a href="/" class="thumbnail-wrapper">
    <img
      alt="A good-boy dog. Black and white."
      class="thumbnail"
      src="/course-materials/article-image-spot.jpg"
    />
  </a>
  <a href="/" class="thumbnail-wrapper">
    <img
      alt="A cardboard standing-desk tool."
      class="thumbnail"
      src="/course-materials/article-image-standing.jpg"
    />
  </a>
  <a href="/" class="thumbnail-wrapper">
    <img
      alt="A “tokyo drift” style sports car"
      class="thumbnail"
      src="/course-materials/article-image-car.jpg"
    />
  </a>
  <a href="/" class="thumbnail-wrapper">
    <img
      alt="A young man amongst daisies in a field"
      class="thumbnail"
      src="/course-materials/article-image-flower-boy.jpg"
    />
  </a>
</div>
```

### Keyframe Animations

- CSS keyframe animations are declated using the `@keyframes` at rule. You specify a transition from one set of CSS declarations to another
- Each `@keyframes` statement needs a name, think of it as a global variable
- Keyframe animations are meant to be general and reusable. We can apply them to specific selectors with the `animation` property

```CSS
@keyframes slide-in {
  from {
    transform: translateX(-100%);
  }
  to {
    transform: translateX(0%);
  }
}
```

- Same as the `transition` property, `animation` requries a duration. Below we are saying that the animation should last 1 second (1000ms)
- The browswer will interpolate the declarations with our `from` and `to` blocks, ov erthe duration defined.

```HTML
<style>
  /* starter styles */
  body {
  padding: 32px 0;
  }
  .box {
    width: 100px;
    height: 100px;
    background: slateblue;
    padding: 8px;
    display: grid;
    place-content: center;
    color: white;
    text-align: center;
  }
  @keyframes slide-in {
    from {
      transform: translateX(-100%);
    }
    to {
      transform: translateX(0%);
    }
  }

  .box {
    animation: slide-in 1000ms;
  }
</style>

<div class="box">
  Hello World
</div>
```

- You can animate multiple properties in the same animation decloration.

```HTML
<style>
  body {
  padding: 32px;
  }
  .box {
    width: 100px;
    height: 100px;
    background: slateblue;
    padding: 8px;
    display: grid;
    place-content: center;
    color: white;
    text-align: center;
  }
  @keyframes drop-in {
    from {
      transform:
        rotate(-30deg) translateY(-100%);
      opacity: 0;
    }
    to {
      transform:
        rotate(0deg) translateY(0%);
      opacity: 1;
    }
  }

  .box {
    animation: drop-in 1000ms;
  }
</style>

<div class="box">
  Hello World
</div>
```

#### Timing functions

- Same as `transitions`, keyframe animation default to an `ease` timing curve, but can be changed.
- You can do this with the `animation-timing-function` property

```HTML
<style>
  body {
  padding: 32px;
  }
  .box {
    width: 100px;
    height: 100px;
    background: slateblue;
    padding: 8px;
    display: grid;
    place-content: center;
    color: white;
    text-align: center;
  }
  @keyframes drop-in {
    from {
      transform: translateY(-100%);
    }
    to {
      transform: translateY(0%);
    }
  }

  .box {
    animation: drop-in 1000ms;
    animation-timing-function: linear;
  }
</style>

<div class="box">
  Hello World
</div>
```

#### Looped animations

- By default, keyframe animations will only run once, but we can control this with `animation-iteration-count` property

```HTML
<style>
  body {
  padding: 32px 0;
  }
  .box {
    width: 100px;
    height: 100px;
    background: slateblue;
    padding: 8px;
    display: grid;
    place-content: center;
    color: white;
    text-align: center;
  }
  @keyframes slide-in {
    from {
      transform: translateX(-100%);
      opacity: 0.25;
    }
    to {
      transform: translateX(0%);
      opacity: 1;
    }
  }

  .box {
    animation: slide-in 1000ms;
    animation-iteration-count: 3;
  }
</style>

<div class="box">
  Hello World
</div>
```

- Also a special value that comes in handy when creating spinners for loading. `animation-iteration-count: infinite;`

```HTML
<style>
  .spinner {
    display: block;
    width: 32px;
    height: 32px;
  }
  @keyframes spin {
    from {
      transform: rotate(0turn);
    }
    to {
      transform: rotate(1turn);
    }
  }
  
  .spinner {
    animation: spin 1000ms;
    animation-timing-function: linear;
    animation-iteration-count: infinite;
  }
</style>

<img
  class="spinner"
  alt="Loading…"
  src="/course-materials/loader.svg"
/>
```

#### Multi-step animations

- In addition to `from` and `to` keywords, we can also use percentages. Allows us to add more then 2 steps in the animation
- Each percentage refers to the progress through the animation. `from` is really just syntactic sugar for `0%`. `to` is sugar for `100%`

```HTML
<style>
  @keyframes fancy-spin {
    0% {
      transform: rotate(0turn) scale(1);
    }
    25% {
      transform: rotate(1turn) scale(1);
    }
    50% {
      transform: rotate(1turn) scale(1.5);
    }
    75% {
      transform: rotate(0turn) scale(1.5);
    }
    100% {
      transform: rotate(0turn) scale(1);
    }
  }
  
  .spinner {
    animation: fancy-spin 2000ms;
    animation-iteration-count: infinite;
  }
</style>

<img
  class="spinner"
  alt="Loading…"
  src="/course-materials/loader.svg"
/>
```

#### Altering animations

- Let's say you want an element to breathe, inflating and deflating.
- You can set up a 3-step animation for this
- It spend the first half of the duration growing to be 1.5x, once it reaches that peak, it spend the second half shrinking back down to 1x

```HTML
<style>
  @keyframes grow-and-shrink {
    0% {
      transform: scale(1);
    }
    50% {
      transform: scale(1.5);
    }
    100% {
      transform: scale(1);
    }
  }

  .box {
    animation: grow-and-shrink 4000ms;
    animation-iteration-count: infinite;
    animation-timing-function: ease-in-out;
  }
</style>

<div class="box"></div>
```

- This works, but there's a more elegant way, we can use the `animation-direction` property.
- `animation-direction` controls the order of the keyframes. The default value is `normal`, giong from 0% to 100% over the course of a specified duration.
- We can also set it to `reverse`, play the animation backwards, going from 100% to 0%.
- The interesting part, we can set it to `alternate`, which will ping pong between `normal` and `reverse` on iterations.

-

```HTML
<style>
  .box {
    width: 100px;
    height: 100px;
    background: slateblue;
  }
  @keyframes grow-and-shrink {
    0% {
      transform: scale(1);
    }
    100% {
      transform: scale(1.5);
    }
  }

  .box {
    animation: grow-and-shrink 2000ms;
    animation-timing-function: ease-in-out;
    animation-iteration-count: infinite;
    animation-direction: alternate;
  }
</style>

<div class="box"></div>
```

#### Shorthand values

- All those properties is a lot of typing, we can use the shorthand to combine all of them.
- The above animation can be re-written to the following.
- And the good thing is **the order doesn't matter**

```CSS
.box {
  /*
  From this:
    animation: grow-and-shrink 2000ms;
    animation-timing-function: ease-in-out;
    animation-iteration-count: infinite;
    animation-direction: alternate;
  ...to this:
  */
  animation: grow-and-shrink 2000ms ease-in-out infinite alternate;
}
```

- There is one excetion: `animation-delay`

```CSS
.box {
  animation: grow-and-shrink 2000ms ease-in-out infinite alternate;
  animation-delay: 500ms;
}
```

### Fill Modes

- We want our elements to fade out, but when it's over the element pops back into exsitence.
- Why does the element jump back to full visibility? Teh declarations in the `from` and `to` blocks apply while the animation is running.
- After the first 1000ms the animations is done. Leaving the with whatever CS declarations have been defined elsewhere.
- SInce we haven't set the `opacity` for this element anywhere else, it snaps back to it's default value `1`.
- Let's consider another approach, filling forwards

```HTML
<style>
  .box {
    width: 100px;
    height: 100px;
    background: slateblue;
    padding: 8px;
    display: grid;
    place-content: center;
    color: white;
    text-align: center;
  }
  @keyframes fade-out {
    from {
      opacity: 1;
    }
    to {
      opacity: 0;
    }
  }
  
  .box {
    animation: fade-out 1000ms;
  }
</style>

<div class="box">
  Hello World
</div>
```

#### Filling forwards

- Instead of relying on default declarations, another approach is `animation-fill-mode`
- `animation-fill-mode` lets us persist the final value from the animation, forward in time.
- The animation duration, and the final frame persist going forward. Sorta confusing.
- `animaiton-fill-mode: forwards` is basically copying the declarations form the `to` block and persisting them as we scrub forward in time.

```HTML
<style>
  .box {
    width: 100px;
    height: 100px;
    background: slateblue;
    padding: 8px;
    display: grid;
    place-content: center;
    color: white;
    text-align: center;
  }
  @keyframes fade-out {
    from {
      opacity: 1;
    }
    to {
      opacity: 0;
    }
  }
  
  .box {
    animation: fade-out 1000ms;
    animation-fill-mode: forwards;
  }
</style>

<div class="box">
  Hello World
</div>
```

#### Filling backwards

- By default, animations will run imediately as soon as the `animation` property is set.
- Like the `transition` we can specify a delay if we'd like the animation to start a bit later.
- But with this, we run into a similar issue, for the first half-second `animation-delay: 500` the element is fully visible.
- For the first 500ms, no CSS from the animation is applied.
- `animation-fill-mode` has another value, `backwards` which allows us to apply the animations initial state backwards in time.

```HTML
<style>
  body {
  padding: 32px 0;
  }
  .box {
    width: 100px;
    height: 100px;
    background: slateblue;
    padding: 8px;
    display: grid;
    place-content: center;
    color: white;
    text-align: center;
  }
  @keyframes slide-in {
    from {
      transform: translateX(-100%);
      opacity: 0.25;
    }
    to {
      transform: translateX(0%);
      opacity: 1;
    }
  }

  .box {
    animation: slide-in 1000ms;
    animation-delay: 500ms;
  }
</style>

<div class="box">
  Hello World
</div>
```

- Essentially what we've said is to copy al the declarations in the `from` block and apply them to the element ASAP, before the animation ahs started.

```HTML
<style>
  body {
  padding: 32px 0;
  }
  .box {
    width: 100px;
    height: 100px;
    background: slateblue;
    padding: 8px;
    display: grid;
    place-content: center;
    color: white;
    text-align: center;
  }
  @keyframes slide-in {
    from {
      transform: translateX(-100%);
      opacity: 0.25;
    }
    to {
      transform: translateX(0%);
      opacity: 1;
    }
  }

  .box {
    animation: slide-in 1000ms;
    animation-delay: 500ms;
    animation-fill-mode: backwards;
  }
</style>

<div class="box">
  Hello World
</div>
```

- What if we want to persist the animation forwards and backwards? We can use a third value, `both`, which does both directions.
- In general, you want the initial value in the keyframe to be applied during the delay. And the final value to be applied after the animation has ended.
- Apply `animation-fill-mode: both` in most situations. It's not the default, so you have to set it.
- Like all animation properties, it can be used in the shorthand.

```CSS
.box {
  animation: slide-in 1000ms ease-out both;
  animation-delay: 500ms;
}
```

## Dynamic Updates

- So far, we've just seen animation running directly on the page, on page load.
- More accurate way, is for an animation to start dynamically using JS at any point in time.
- When the page loads, the `animation` property is set to `undefined`, and nothing happens
- When the user clicks the "Enable Animation" button, that property is updated to `jump 1000ms infinate`.
- The moment the animation is set to a valid value, the animation begins.
- When the button is set again, `animation` is reverted back to `undefined`

```JAVASCRIPT
function App() {
  const [
    animated,
    setAnimated,
  ] = React.useState(false);

  return (
    <Wrapper>
      <Box
        style={{
          animation: animated
            ? 'jump 1000ms infinite'
            : undefined,
        }}
      />
      <button
        onClick={() => {
          setAnimated(!animated);
        }}
      >
        {animated
          ? 'Disable animation'
          : 'Enable animation'
        }
      </button>
    </Wrapper>
  );
}

const Wrapper = styled.div`
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  gap: 32px;
  height: 100vh;
`;

const Box = styled.div`
  width: 80px;
  height: 80px;
  background: slateblue;
`;

render(<App />);
```

```CSS
@keyframes jump {
  0% {
    transform: translateY(0%);
  }
  30% {
    transform: translateY(-50%);
  }
  50% {
    transform: translateY(0%);
  }
}

body {
  margin: 0;
  padding: 0;
}
```

### Playing and Pausing

- In the sample above, disabling the animation can lead to some jarring transitions.
- When we remove the `animation` property, all of the CSS in the `from` and `to` blocks dissapear immediately. The element wil revert back to it's default CSS.
- This is known as "interuption" `@keyframes` animations don't handle interruptions well.
- We can use **play states** to help in this situation.`animation-play-state`
- Reminder, styles are "camelCased" when setting them in JS.
- Before, we were dynamically applying and removing the animation altogether. In the updated example below, the animation is always applied, but we dynamically toggle between running and paused.
- `paused` works liek a pause button on a remote control. Everything freezes in place. Toggling back to `running` will pick up from where it left off.

```JAVASCRIPT
function App() {
  const [
    animated,
    setAnimated,
  ] = React.useState(false);

  return (
    <Wrapper>
      <Box
        style={{
          animationPlayState: animated
            ? 'running'
            : 'paused',
        }}
      />
      <button
        onClick={() => {
          setAnimated(!animated);
        }}
      >
        {animated
          ? 'Pause animation'
          : 'Start animation'
        }
      </button>
    </Wrapper>
  );
}

const Wrapper = styled.div`
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  gap: 32px;
  height: 100vh;
`;

const Box = styled.div`
  width: 80px;
  height: 80px;
  background: slateblue;
  animation: jump 1000ms infinite;
`;

render(<App />);
```

```CSS
@keyframes jump {
  0% {
    transform: translateY(0%);
  }
  30% {
    transform: translateY(-50%);
  }
  50% {
    transform: translateY(0%);
  }
}

body {
  margin: 0;
  padding: 0;
}
```

### Animations vs. transitions

- When do you use `@keyframes` and when do you use `transition`?
- Things only `@keyframes` can do:
  - Looped animations
  - Multi-step animations
  - Pauseable animations
- If an animation needs to run immediately when the page loads or a component mounts, it's easiest to use `@keyframes`
- Use `transitinos` when your CSS will cahgne as the result of some state or user action. Smooth out a harse transtion between values.

### With Styled-components

- When you write CSS with styled-components, all our styles are coupled with a specific component. The `@keyframe` is meant to be set declared globally, how do we reconcile?
- Easy, the library comes with a utility for this
- We can import `keyframes` from the styled-components package. Example...

```JAVASCRIPT
import styled, { keyframes } from 'styled-components';

function App() {
  return <FloatingCircle />;
}

const float = keyframes`
  from {
    transform: translateY(10px);
  }
  to {
    transform: translateY(-10px);
  }
`;

const FloatingCircle = styled.div`
  animation: ${float} 1000ms infinite alternate ease-in-out;
`;
```

- The `keyframes` funciton is called using the tagged tempalte literals
- To apply our animaiton, we interpolate it within the styles for a specific component
- The advantage, it removes the possibility of naming conflicts
- In vanilla CSS, `@keyframes` definitions are global. If we created a keyframe animaiton called `fadeIn`, any component in our app can use this animation. However, if another developer on our team decidees to name their animation `fadeIn`, one of the animations will overwrite the other
- In styled components, each animaiton is given a unique, random name. Just like our component classes

### Exercises, Popup help circle

- Animate the help circle to slide in from the bottom, after a short delay
- The solution...

```HTML
<!--
Acceptance criteria:

• Should have a 1000ms delay
• Should animate over 500ms
• Should have 32px of spacing from the
  bottom-right corner
-->

<style>
  /* default style */
  .help-circle {
    display: grid;
    place-content: center;
    width: 60px;
    height: 60px;
    color: white;
    background: slateblue;
    border-radius: 50%;
    border: 3px solid white;
    box-shadow:
      0px 2px 8px hsl(0deg 0% 0% / 0.1),
      0px 4px 16px hsl(0deg 0% 0% / 0.1),
      0px 8px 32px hsl(0deg 0% 0% / 0.1);
    cursor: pointer;
  }
  .help-circle img {
    width: 32px;
    height: 32px;
  }

  .visually-hidden {
    position: absolute;
    overflow: hidden;
    clip: rect(0 0 0 0);
    height: 1px;
    width: 1px;
    margin: -1px;
    padding: 0;
    border: 0;
  }

  /* Use calc to position the help circle off screen, with a CSS variable to account for the spacing */
  @keyframes slide-in {
    from {
      transform: translateY(
        calc(100% + var(--spacing))
      );
    }
    to {
      transform: translateY(0%);
    }
  }

  /* Use fixed positioning to put the circle where you want it */

  .help-circle {
    /* Any CSS variable defined here, can be used in the animation keyframe associated with it */
    --spacing: 32px;
    position: fixed;
    bottom: var(--spacing);
    right: var(--spacing);
    /* animate backwards to bring the icon up */
    animation: slide-in 500ms backwards;
    animation-delay: 1000ms
  }
</style>

<button class="help-circle">
  <img
    alt=""
    src="/course-materials/help-white.svg"
  />
  <span class="visually-hidden">
    Access help center
  </span>
</button>
```

### Exercises, Waving Hand

- Update the "waving hand" emoji so that it actually waves at the user.
- Animation doesn't work with inline elements, change it to a `inline-block` or `block` level element
- The hand rotates on a odd origin, use `transform-origin` to update the position
- Make it loop with with the `infinite` property
- Use `alternate` to make the animation from `to` and `from`

```HTML
<style>
  html, body {
  height: 100%;
  }
  body {
    display: grid;
    place-content: center;
  }
  .wave {
    font-size: 3rem;
  }

  @keyframes wave {
    from {
      transform: rotate(0deg);
    }
    to {
      transform: rotate(30deg);
    }
  }
  .wave {
     display: inline-block;
     animation: wave 500ms infinite alternate ease-in-out;
     transform-origin: 80% 75%;
  }
</style>

<p>
  <span
    class="wave"
    role="img"
    aria-label="Waving hand"
  >
    👋
  </span>
</p>
```

## Animation Performance

- Sluggish animations can ruin a good UX
- Not much room for error, in order for our brains to perceive motion as fluid and believeable, it need to run at 60 frams per second.
- If an animation is to computationally expensive, it can appear janky and choppy. The device cannot keep up and the framerate drops.
- Poor performance will often take the form of variable framerates.

### The pixel pipeline

- If we want to update the pixels on our screen, there is a pipeline of possible steps.

1. Recalculating style, first we nee dto figure otu which CSS declaration to apply to which elements.
2. Layout, next we need to figure out where each element sits on the page
3. Paint, once we know wher eeverythgn is, we can start to painting them, This is the process of figuring out which color every pixel shoudl be "rasterization" adn nfilling it in
4. Compositing, finally we can transform previously painted elements

- Different CSS properties will trigger different steps in the pixel pipeline. If we animate an element's `height`, we will need to recalculate the layout.
- For this reason, we try and avoid properties like `width`, `height`, `padding`, and `margin`
- Propteries like `background-color` will never affect layout,
- The `transform` property is special, it can animate a property without even triggering a paint step.
- Two properties that can be animated with compositing alone: `transform` and `opacity`.
- In Chrome, `filter` can also be composited.
- This doen't mean you can only use those properties, it's a judgement call.

### Hardware Acceleration

- Depending on your browser and OS, you may occasionally notice a curious flicker on certain animations.
- Sometiems you will notice elements glitch and the start and end of transitions.
- This happens because of a hand-off between the computers CPU and GPU.
- **Hardware Acceleration** when rasterizing the pixels in every frame, the computer will transfer everythign to the GPU as a texture. GPUs are very good at doing these kidns of texture based transformations, as a result we get a very slick and performant animation.
- But GPUs and CPUs render thigns slighly differ. When the CPU hands it to the GPU, and visa versa, you get a snap of things shifting slightly.
- We can change this by adding the property `will-change`

```CSS
.btn {
  will-change: tranform;
}
```

- `will-change` is a property that allos us to tell the browser we are going to animate the selected element. And to optimize for this case.
- It means, the browser will let the GPU handle this element all the time.
- `will-change` let's us be intentional about which elements should be hardware-accelerated.
- Check out MDN though, says to use it sparigly as a last resort.

## Designing Animations

- During the design to dev handoff, animation can get lost since most teams don't have a dedicated motion designer
- Here are some high level tips to make it easier to design animations.

### Types of Animations

1. Transitions chang ethe content on the page in a significant way, like moving from one page to another, a modal opening or closing, of a multi-step wizard moving to the next step.
2. Supplements add or remove informaiton from the page, without changing their location or task. For example a notification might pop up in the corner
3. Feedback helps the user understnd how the applicaiton has responded to user input. For ex; an error message appearing when submititng a form. Or a button sliding down on click to indicate it's being depressed.
4. Demonstrations are used fo reducation, a way of showing the user how something works. Like the animation demos in this course.
5. Decoration are aesthetic and dont' affect the information on the page. For ex; confetti to celebrate a piece of good news being delivered to the user.

- Every animaiton should have a purpose behind it. Don't just add animation for the sake of animating.
- Animations can make the product feel more polished, but only when it's more thoughtful.

### Animation Duration

- When creating an animation in CSS, we need to specify a duration in milliseconds. So how long should it be?
- A modal for example, if we pick a quick value (200ms) the motion is disorienting. To much to fast.
- If we pick a value to slow, feels like the app is taking to long. Imagine if you do something 10 times a day, it becomes annoying.
- A generally acceptable range of durations is from 200ms to 500ms.

### Additional Reading

- [Animation At Work](https://abookapart.com/products/animation-at-work) by Rachel Nabors
- [Improving the payment experience with animation](https://medium.com/bridge-collection/improve-the-payment-experience-with-animations-3d1b0a9b810e)

## Action Driven Animation

- When most of us think of animations, we think in terms of states. model is either `opacity: 1` or closed `opacity: 2`. We use CSS transitions to animate the changes in state.
- The problem with that, it doesn't distinguish between actions.
- The animation for opening the modal is teh same as it would be when closing the modal.
- [See the animation demo](https://courses.joshwcomeau.com/css-for-js/08-animations/10-action-driven-animation), try changing some of the properties.
- Modal actions for example
  - Enter duration: 500ms
  - Enter timing function: ease-out
  - Exit duration: 250ms
  - Exit timing function: ease-in
- How do we craete transitions based on actions?
- If the animation is base don a pseudo-selector, like `:hover` we can do it by using different `transition` values

```HTML
<style>
  .button {
    width: 200px;
    height: 50px;
    border-radius: 6px;
    border: 2px solid;
    will-change: transform;
  }
  .button {
    /* Exit animations */
    transition: transform 500ms;
  }
  .button:hover {
    transform: scale(1.1);
    
    /* Enter animation */
    transition: transform 150ms;
  }
</style>

<button class="button">
  Hello World
</button>
```

- When the mouse is resting atop the element, the `:hover` declarations apply, so the enter animation will be given the `transition: transform 150ms`. The moment the mouse leaves teh element, it falls back to the defualt `transition: transform 500ms` and uses that transition for the exit animation.
- For more on the subject, check out [Meaningful Motion with Action-Driven Animation](https://tobiasahlin.com/blog/meaningful-motion-w-action-driven-animation/)

## Exercises

### Pushable Button

- Action Driven animation
- Provide differ transitions for differ states
  - hover
  - active
- When you are exiting something, you don't want the animation to be to quick, a quick motion may distract them, happen slowly so it doesn't draw a lot of attention
- 4th state, process of hover:active to :active
- You can use JS events, onMouseDown, onMouseOut etc.
- Deeper dive into [building a 3D button](https://www.joshwcomeau.com/animation/3d-button/)

```HTML
<style>
  .pushable {
    background: hsl(340deg 100% 32%);
    border: none;
    border-radius: 12px;
    padding: 0;
    cursor: pointer;
  }
  .front {
    display: block;
    padding: 12px 42px;
    border-radius: 12px;
    font-size: 1.25rem;
    background: hsl(345deg 100% 47%);
    color: white;
  }
  .front {
    transform: translateY(-4px);
    /* default transition */
    transition: transform 500ms;
  }
  
  .pushable:hover .front {
    transform: translateY(-6px);
    /* hover transition */
    transition: transform 250ms;
  }

  .pushable:active .front {
    transform: translateY(-2px);
    /* active transition */
    transition: transform 50ms;
  }
</style>

<button class="pushable">
  <span class="front">
    Push me
  </span>
</button>
```

### Orchestration

- Instead of everything animating in at once, you sequence the elements, staggered.
- It may seem overkill, but this technique is critical for making next level animations. It's what makes a product feel more polished.
- Companies like Apple understand this, it's why their products feel so polished.

### Implementing orchestration

- So how do we take advantage or orchestrations? With a lot of ternaries, yikes
- Because we want seperate enter/exit animations, we need to set different values for a bunch of stuff base don `isOpen` is set to true or not.
- See full demo here [Modal transitions](https://courses.joshwcomeau.com/playground/modal-orchestrations)
- Check out some React libraries, [react-spring](https://react-spring.io/) and [GPAP](https://greensock.com/gsap/)

### Accessibility

- Animations are an imprtant part of UX, but not everyone experiences in the same way.
- For some folks, this can trigger physical symbtoms, like nausea, dizzines, and malaise.
- Modern operating systems offe ra remedy for this, they can opt out of animations.
- And now web apps and websites can acces this value and use it for our CSS and JS.

### Vestibular disorders

- The vestibular ssytem includes part of the inner ear and parts of the brain, and manages oru sense of balance.
- For example, when you spin really fast an it makes you dizzy. By spinning you are sloshing fluid around in yoru inner ear and the brain uses that fliud to determine which way is up.
- So when you are spinning, your brain receives incompatible info form differ sources. Your ear-fluid is claming one thing, while your eyes are claiming another. This is very disorienting.
- For some people, their vestibular system feeds the brain bad information.
- The most commonly known symptom of this is called vertigo; someone will feel gravity pulling them in the wrong diretion.
- Troubling, animations can be a trigger for some folks, leading to a range of unpleasant side-effects: vertigo, dizziness, nausea, headached, malaise.
- It can feel as it our website is reaching out and spinning the person in their office chair.
- Estimated that up to 35% of adults 40+ in teh US have experience smoe form of vestibular dysfunciton, with 5% reporting chronic problems.  

### Opting out of animations

- There is a media query for this in the app settings > accessibility > reduce motion
- Setting is in all mainstream OS
- You can just google reduce animaitons for your operating system to find the instructions
- Apple introduced the setting, `prefers-reduced-motion` and other browsers have followed suit.
- It has [good browser support](https://caniuse.com/?search=prefers-reduced-motion)

### Accessing in CSS

- To tell if they've reqeusted reduced motion, we can use a media query
- If a user selected "reduce animations" in their OS, `prefers-reduced-motion` will be set to `reduce`
- The CSS rules tn that media query will apply, disabling the trnsition on our `.fancy-box` selector

```CSS
.fancy-box {
  width: 100px;
  height: 100px;
  transform: scale(1);
  transition: transform 300ms;
}
.fancy-box:hover {
  transform: scale(1.2);
}
@media (prefers-reduced-motion: reduce) {
  .fancy-box {
    transition: none;
  }
}
```

- A better way to think about it, start without animations and enable them if the user wishes.
- `no-preference` is the default value, if a user hav never fiddled with their settings, `prefers-reduced-motion` will be set to `no-preference`
- By switching up sot hat `transition` is set from within a media query, we ensure that the animation is disabled by default for user on devices that don't support this property.

```CSS
.fancy-box {
  width: 100px;
  height: 100px;
  transform: scale(1);
  /* No more `transition` here! */
}
.fancy-box:hover {
  transform: scale(1.2);
}
@media (prefers-reduced-motion: no-preference) {
  .fancy-box {
    transition: transform 300ms;
  }
}
```

### Accessing in JS

- The media query shown above works great for animations that take place entirely from within CSS. But a lot of animations that cannot be done entirely through CSS.

  - Animations using spring physics
  - Animations involving the cursor coordinates, scroll positions
  - HTML5 Canvas Aaimations
  - Some SVG animations

```JAVASCRIPT
function getPrefersReducedMotion() {
  const mediaQueryList = window.matchMedia(
    '(prefers-reduced-motion: no-preference)',
  );
  const prefersReducedMotion = !mediaQueryList.matches;
  return prefersReducedMotion;
}
```

- This function nwill return `true` is the user prefers resduced motion.
- If it returns `false` it mean the user has no preference, and we should enable our animations
- We can also use event listeners to update this value when it changes

```JAVASCRIPT
const mediaQueryList = window.matchMedia(
  '(prefers-reduced-motion: no-preference)',
);
const listener = (event) => {
  const getPrefersReducedMotion = getPrefersReducedMotion();
};
mediaQueryList.addListener(listener);
// Later:
mediaQueryList.removeListener(listener);
```

- This listener will fire when the user toggles the "Reduce Motion" checkbox in their OS

### Motion vs. Animation

- Nnot all animations involve motion.
- The most common triggers for folks with vestibular disorders are multi-layered parallax animations, or page wide transition. Big sweeping motion
- Should we disable all animations, or only the ones with significant motion?
- If an element moves more then a few pixels, we can disable it using the techniques above.
- But you don't have to disable small fadin-in and fading-out color changes. Or if an element moves a few pixels.
- How much is to much? small bits of animation motion doesn't seem to bother most people with vvestibular issues. But err on the side of caution.

## Exercises, Update the Help Circle

- Update the help circle animation from earlier so it doesn't animate for users who have enabled the "reduced" motion setting.
- The default option for people unable to provide a preference, should be the safer one.
- You can optimize for both cases, for people with vestibular disorders, have it fade in, and for others, you have slide in.

```HTML
<style>
  /* starter styles */
  .help-circle {
    display: grid;
    place-content: center;
    width: 60px;
    height: 60px;
    color: white;
    background: slateblue;
    border-radius: 50%;
    border: 3px solid white;
    box-shadow:
      0px 2px 8px hsl(0deg 0% 0% / 0.1),
      0px 4px 16px hsl(0deg 0% 0% / 0.1),
      0px 8px 32px hsl(0deg 0% 0% / 0.1);
    cursor: pointer;
  }
  .help-circle img {
    width: 32px;
    height: 32px;
  }

  .visually-hidden {
    position: absolute;
    overflow: hidden;
    clip: rect(0 0 0 0);
    height: 1px;
    width: 1px;
    margin: -1px;
    padding: 0;
    border: 0;
  }
  
  @keyframes slide-in {
    from {
      transform: translateY(
        calc(100% + var(--spacing))
      );
    }
    to {
      transform: translateY(0%);
    }
  }
  /* fade in option by default */
  @keyframes fade-in {
    from {
      opacity: 0;
    }
    to {
      opacity: 1;
    }
  }
  
  .help-circle {
    --spacing: 32px;
    position: fixed;
    bottom: var(--spacing);
    right: var(--spacing);
    animation: fade-in 500ms backwards;
    animation-delay: 1000ms;
    /*
    animation: slide-in 500ms backwards;
    animation-delay: 1000ms;
    */
  }
  
  /* 
  @media (prefers-reduced-motion: reduce) {
    .help-circle {
      animation: none;
      animation-delay: none;
    }
  }
  */
  
  /* Media query for those for everyone else, reduce motion disabled in preferences */
  @media (prefers-reduced-motion: no-preference) {
    .help-circle {
      animation: slide-in 500ms backwards;
      animation-delay: 1000ms;
    }
  }
  
  
</style>

<button class="help-circle">
  <img
    alt=""
    src="/cfj-mats/help-white.svg"
  />
  <span class="visually-hidden">
    Access help center
  </span>
</button>
```

## Ecosystem World Tour Animation

- Take a look at the modern landscape of animaitons libraries and APIs.
- A little React heavy

### The Web Animations API

- The web animations API is a low-level animation API built into the browswer. We can build animation sequences and control them with JS.
- It mirros the `@keyframes` API

```JAVASCRIPT
const elem = document.querySelector('.box');
const frames = [
  { opacity: 0, transform: 'translateY(100%)' },
  { opacity: 1, transform: 'translateY(0%)' },
];
elem.animate(
  frames,
  {
    duration: 1000,
    iterations: Infinity,
  },
);
```

- This is equivalent to the following CSS

```CSS
@keyframes pop-in {
  from {
    opacity: 0;
    transform: translateY(100%);
  }
  to {
    opacity: 1;
    transform: translateY(0%);
  }
}
.box {
  animation: pop-in 1000ms infinite;
}
```

- Web Animations API can be thought of as "CSS keyframe animations in JS".
- There are some differences, the Web Animations API will let us apply a single timing fuction for the whole animation. Each step isnt' given it's own easing by default.
- You can provide custom timing functions to each step in the web animations API.

```HTML
<style>
.box {
  width: 50px;
  height: 50px;
  background: slateblue;
  margin: 64px;
  border-radius: 4px;
}

html {
  height: 100%;
}
body {
  height: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>
<div class="box"></div>

<script>
  const elem = document.querySelector('.box');

  const frames = [
    {
      transform: 'translate(-20px, -10px)',
      easing: 'ease-out',
    },
    {
      transform: 'translate(0px, 10px)',
      easing: 'ease-in',
    },
    {
      transform: 'translate(20px, -10px)',
      easing: 'ease-out',
    },
    { transform: 'translate(-20px, -10px)' },
  ]
  
  elem.animate(
    frames,
    {
      duration: 2000,
      iterations: Infinity,
      easing: 'ease',
    }
  )
</script>
```

- Pros
  - it's built into the browswer, so no hefty package needs
  - it has good performance
  - solid browswer support
  - bit more customization copared to CSS keyframe animations
- Cons
  - it' snot fundamentally differ from CSS keyframe animations
  - some parts are easy to get tripped up on vs. the CSS keyframe animations

- Resources
  - [MDN Animations API](https://developer.mozilla.org/en-US/docs/Web/API/Web_Animations_API/Using_the_Web_Animations_API)
  - [CSS Animations vs. Web Animations](https://css-tricks.com/css-animations-vs-web-animations-api/)
  - Note: [Motion One](https://motion.dev/)

### Framer Motion

- Framer Motion is not the same thing as Framer / Framer X, the design tool. It's produced by the same company but a differ thing.
- Framer Motion is a production-ready library for React. It can animate CSS properties that aren't normally able to be animated.
- Framer Motion works by calculating a sequence of transforms required to interpolate the start and end positions, sounds really hard.
- Because it uses tranforms, animations are highly performant.
- Framer Motion can animate just about any CSS change.
- For example, if your element goes from being a child in a grid continer to setting position absolute, Framer Motion can animate that transition.
- It can even animate between components

- Pros
  - Can animate all kidns of things tha twould normally not be animatable, leadin g o next level user experiences.
  - Uses hardware-accelerated transforms for performatne transitions
  - Supports using spring physics instead of Bezier curves
  - Ties in nicely with Rect. Can add sophisticated animations with small amount of code.
- Cons
  - All taht magic comes at a cost, package is ~32kb gzip
  - Runs in the main thread, so may become choppy is the thread is busy
  - Only works in React

- Resources
  - [Treasure Trove Framer Motion](https://courses.joshwcomeau.com/css-for-js/treasure-trove/009-framer-motion)
  - [Official Docs](https://www.framer.com/motion/)

### React Spring

- React SPring allows us to model our animations base don spring physics, rather then Bezier curves
- Entirely differ model for running animations.
- With spring physics, we don't pick a duaton for our animations; instead we configure the characteristics of a spring.
- Spring physics are modeled on the natual world, and convinces our breain in a way that Bezier curves can't fully imitate.
- React Spring is the most common way to animate using spring phusics in React.

- Pros
  - Fluid, organic motion compared with CSS transitions / keyframe animations.
  - Highly optimized performance.
  - Reletively small 18bg gzip
  - A rich APi with lots of advanced optoins,
  - Ties in with an ecosystem created by the same folks.
  - At it's core, React Spring is a number generator
- Cons
  - It can't do Magic animations like the way Framer Motion can. And Framer Motion does not support spiring physics.
  - The leanring curve is pretty steep, both with spring physics and this library.
  - Like all JS based animations libraries, teh animation might be janky if the main thread becomes occupied.
- Resources
  - [React Spring](https://react-spring.io/)
  - [Josh's intro to spring phycics](https://www.joshwcomeau.com/animation/a-friendly-introduction-to-spring-physics/)

### GreenSock GSAP

- GSAP is one of th oldest and most well known animation libraries.
- It offers advanced Bezier based easing. And a timeline to manage orchestration
- Bundle size is similar to other libraries. 24kb gzip
- Pros
  - Large active community
  - Can be used iwth any framework, not just React
  - Highly optimized for perf
  - RIch plugin ecosystem for things like adding scrol based triggers
- Cons
  - Does not support true spring physics
  - Because it is framework agnostic, it will not tie in as neatly as a framework specific solutions
- Resources
  - [Official site and docs](https://greensock.com/gsap/)
  - Sara Drasner, [How to animate on the web with greensock](https://css-tricks.com/how-to-animate-on-the-web-with-greensock/)

### Other libraries

- Lots of other options, but most try to replicate CSS transitions and keyframe animations.
- Focus on tools that do htings not otherwise possible in CSS.
- For small straightforward animations, CSS animations is your best bet.
- Reach for modern tools in two cases:
  - The naimation is too complet to be done with CSS
  - The animation is very prominent, and want to make it stand out a little more with sprint physics.

## Workshop, Add animation to our Sole and Ankle store

- [Check out my repo here](https://github.com/clewisdavis/sole-and-ankle-animated)

## Module 9 - Big Little Details

- Learn about the small details to add a lot of polish to your websites and apps

### CSS Filters

- CSS Filters allow us to leverage the power of SVG filters from within CSS.
- SVG's are an image file format that allows us to create vector graphics using an HTML like syntax
- One of the powerful thigns about SVGs, they have a rich filter API
- The cool thing, we can access a SVG filter from within CSS

```CSS
.box {
  filter: drop-shadow(4px 8px 5px hsl(0deg 0% 0% / 0.2));
}
```

- CSS has access to about a dozen common SVG filters, through the use of filter funcitons like `drop-shadow()`

### Color Manipulation

- A good chunk of CSS filters manipulate color in some way.
- Similar to Photoshop filters.
- Some examples

```CSS
img {
  width: 300px;
  border-radius: 8px;
}
.brightness {
  filter: brightness(150%);
}
.contrast {
  filter: contrast(60%);
}
.sepia {
  filter: sepia(100%);
}
.mixed {
  filter: contrast(200%) grayscale(90%);
}
section {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  gap: 16px;
}
```

- These color manipulating filters take a percentage. For example, `brightness` has a default value of `100%`, and we can make it less or more bright.
- We can apply multipele filters to the same element by space-seperating them:

```CSS
.image {
  filter:
    brightness(120%)
    contrast(110%)
    grayscale(50%);
}
```

- These filters are often used on images, but can work on any DOM nodes.
- For example, a button using transition to animate the effect.

```HTML
<style>
  .btn {
    padding: 16px 64px;
    border: none;
    border-radius: 6px;
    color: white;
    font-size: 1rem;
    font-weight: bold;
  }
  .btn {
    background: linear-gradient(
      to top,
      hsl(260deg 80% 40%),
      hsl(260deg 80% 50%)
    );
    transition: filter 600ms;
  }
  .btn:hover, .btn:focus {
    transition: filter 250ms;
    filter: brightness(150%);
  }
</style>

<button class="btn">
  Push me
</button>
```

- The effect is similar to animating `background-color` but more flexible since it works with teh gradients and background images as well.

### Hue rotation

- The `hue-rotate` filter funciton shifts the color of every pixel in the element.

```HTML
<style>
  .btn {
    padding: 16px 64px;
    border: none;
    border-radius: 6px;
    color: white;
    font-size: 1rem;
    font-weight: bold;
  }
  .btn {
    background: linear-gradient(
      to top,
      hsl(260deg 80% 40%),
      hsl(260deg 80% 50%)
    );
    transition: filter 600ms;
  }
  .btn:hover, .btn:focus {
    transition: filter 250ms;
    filter:
      brightness(110%)
      hue-rotate(60deg);
  }
</style>
```

### Blur Filter

- The CSS filter `blur` applies a Gaussian blur to the selected element.
- And example, hover over the image to unblur.
- However, blurring can be a very expensive operation, even with hardware acceleration.

```HTML
<style>
  img {
    display: block;
    width: 300px;
    border-radius: 8px;
  }
  img {
    filter:
      blur(6px)
      brightness(50%);
    transition: filter 800ms ease-in-out;
  }
  
  a:hover img,
  a:focus img {
    filter:
      blur(0px)
      brightness(100%);
    transition: filter 300ms;
  }
</style>

<a href="/">
  <img
    alt="A colourful busy street in Tokyo, Japan"
    src="/cfj-mats/akihabara.jpg"
  />
</a>
```

- A11y, blurring is comsmetic, we obfuscate it visually. It someone is using a screenreader, they will be abel to access the element and won't have any idea the content is meant to be concealed.
- This can be a problem if lurring serves a purpose, like a quiz ina game and answer is blurred. In this case use `aria-hidden` to hide the content from screen readers. And remove the blur and aria attribute at the same time.
- If you want a sharp edge on your element, you can use `overflow: hidden` on the parent container.

```HTML
<style>
  img {
    display: block;
    width: 300px;
    filter:
      blur(6px)
      brightness(50%);
    transition: filter 800ms ease-in-out;
  }
  a:hover img,
  a:focus img {
    filter:
      blur(0px)
      brightness(100%);
    transition: filter 300ms cubic-bezier(0.05, 0.66, 0.33, 1);
  }
  a {
    /* Crop the blurred edge */
    overflow: hidden;
    /*
      Move the border-radius up,
      to preserve the sharp corner
      as well
    */
    border-radius: 8px;
  }
</style>

<a href="/">
  <img
    alt="A colourful busy street in Tokyo, Japan"
    src="/cfj-mats/akihabara.jpg"
  />
</a>
```

### Blurred Glow

- Neat design secret to glow an element with the blur fitler.
- Take two elements and stack them on top of one another, then blur the background element.

```HTML
<style>
  body {
    overflow: hidden;
  }
  .wrapper {
    position: relative;
  }
  .gradient {
    position: relative;
    width: 200px;
    height: 200px;
    border-radius: 50%;
    background-image: linear-gradient(
      deeppink,
      red,
      coral,
      gold,
      white
    );
  }
  .blurry {
    position: absolute;
    filter: blur(40px);
    transform: scale(1.3) translateX(10%) rotate(30deg);
  }
  .regular {
    filter: drop-shadow(0px 0px 25px hsl(0deg 0% 0% / 0.3));
  }
</style>

<div class="wrapper">
  <div class="gradient blurry"></div>
  <div class="gradient regular"></div>
</div>
```

### Backdrop Fitlers

- The `filter` property wil apply an SVG filter to the selected element, btu what if we want to blur everything behind the element?
- For example, a card  in front of a photo, blurring the background.
- Unfortunately FireFox does not support this feature.
- You can accomplish this task using the `backdrop-filter` property.

```HTML
<style>
  img {
    position: fixed;
    top: 0;
    left: 0;
    width: 100vw;
    height: 100vh;
    object-fit: cover;
  }
  .blur-circle {
    position: absolute;
    top: 50vh;
    left: 0;
    right: 0;
    bottom: 0;
    margin-left: auto;
    margin-right: auto;
    width: 100vh;
    height: 100vh;
    border-radius: 50%;
    border: 4px solid white;
  }

  body {
    /*
      Don't allow the circle to
      introduce a scrollbar.
    */
    max-height: 100vh;
    overflow: hidden;
  }
  .blur-circle {
    backdrop-filter: blur(10px);
    /* Vendor prefix for Safari: */
    -webkit-backdrop-filter: blur(10px);
  }
</style>

<img
  alt="A colourful busy street in Tokyo, Japan"
  src="/cfj-mats/akihabara.jpg"
/>
<div class="blur-circle"></div>
```

- You can use `backdrop-filter` to obfuscate content behind a sticky header.

```HTML
<style>
  body {
  /* Make sure there's enough to scroll */
  min-height: 150vh;
}

  header {
    position: sticky;
    top: 0;
    padding: 32px;
    text-align: center;
  }

  main {
    padding: 32px;
  }

  h2 {
    margin-bottom: 16px;
  }

  .intro {
    font-size: 1.125rem;
    margin-bottom: 64px;
  }

  ol {
    font-size: 1.125rem;
    margin-bottom: 16px;
  }
  header {
    background: hsl(0deg 0% 100% / 0.5);
    backdrop-filter: blur(12px);
    -webkit-backdrop-filter: blur(12px);
  }
</style>

<header>
  <h1>Course Platform</h1>
</header>

<main>
  <h2>Module 1: Rendering Logic I</h2>
  <p class="intro">Flow layout is the “OG” layout algorithm of the web, and it's still used heavily today. In this module, we explore how to best use Flow layout in modern times. We'll also deepen our understanding of common fundamentals like the Box Model.</p>
  
  <ol>
    <li>
      Built-in Declarations and Inheritance
    </li>
    <li>
      The Cascade
    </li>
    <li>
      Directions
    </li>
    <li>
      The Box Model
      <ol>
        <li>
          Padding
        </li>
        <li>
          Border
        </li>
        <li>
          Margin
        </li>
      </ol>
    </li>
    <li>
      Flow Layout
      <ol>
        <li>
          Width Algorithms
        </li>
        <li>
          Height Algorithms
        </li>
      </ol>
    </li>
    <li>
      Margin Collapse
      <ol>
        <li>
          Rules of Margin Collapse
        </li>
        <li>
          Will It Collapse?
        </li>
        <li>
          Using Margin Effectively
        </li>
      </ol>
    </li>
    <li>
      Workshop: Agency page
    </li>
</main>
```

### Fallbacks

- `backdrop-filter` has decent browswer support but missing in Firefox.
- In cases where the effect causes legibility issues. You need a fallback.
- Use `@supports` query so that all users are served a decent experience.

```CSS
/*
  The fallback experience, for IE/Firefox users.
  MUCH less transparency.
*/
header {
  background: hsl(0deg 0% 100% / 0.95);
}
@supports (backdrop-filter: blur(12px)) {
  /*
    The main experience, for Chrome/Safari users.
    Blurry backdrops.
  */
  header {
    background: hsl(0deg 0% 100% / 0.5);
    backdrop-filter: blur(12px);
  }
}
```

### Lots of combinations

- `backdrop-filter` unlocks a lot of interesting possibilities. It supports all the filters, and be combined with multiple filters.

```CSS
.header {
  backdrop-filter:
    brightness(150%)
    hue-rotate(30deg)
    blur(5px);
}
```

## Border Radius

- The `border-radius` property lets us round corners of our boxes
- But that is just the start of it, you can do some cool things with `border-radius`

```HTML
<style>
  .card {
    width: 200px;
    height: 200px;
    background: white;
    border-radius: 16px;
  }
</style>

<article class="card"></article>
```

### Percentages

- Have you ever trid to use a percentage border-radius on a non-square element? You get some funky results.

```HTML
<style>
  .card {
    width: 300px;
    height: 150px;
    background: white;
    border-radius: 10%;
  }
</style>

<article class="card"></article>
```

- Border radius is shorthand for 4 distict CSS properties.
  - `border-top-left-radius`
  - `border-top-right-radius`
  - `border-bottom-left-radius`
  - `border-bottom-right-radius`

- Each of these properties accepts two values, horizontal and vertical radius.

```HTML
<style>
  .card {
    width: 300px;
    height: 150px;
    background: white;
    border-top-left-radius: 40px 20px;
  }
</style>

<article class="card"></article>
```

- The first value is used as the horizontal radiufor an ellipse. The second value is used as the vertical radius.
- This is how `border-radius` works under the hood. When we pass a value like `32px`, that single value is used 8 times.
- With %'s, it gets strange, the horizontal radius will be based on the width, and teh vertical radius wil be based on the height.
- The ellipse wil be proportional tot he element itself. If our element has a width of 300px and a eight of 150px, it will have an aspect ratio of 2:1.
- If we set the radisu to 50%, that mean sthe diameter is 100%. So we end up with an elipses that is the same width and height as the element itself.

### Full shorthand syntax

- `border-radius` actually takes 8 seperate values: 4 corners, and each corner can specify a horizontal and vertical radius.
- We can pass all 8 values to the `border-radius` shrohand with our friend the `/` delimiter

```CSS
.box {
  border-radius: 10% 20% 30% 40% / 50% 60% 70% 80%;
}
```

- The first 4 numbers are all horizontal radiuses. We specify then in clockwise orer, starting from the top-left corner.
- The last 4 numbers are the vertical radiuses, also specified in teh clockwise order from the top left.
- If on ly the first 4 numbers are provided, they are copied over to the last 4:

```CSS
.box {
  /* These two declarations are equivalent: */
  border-radius: 10% 20% 30% 40%;
  border-radius: 10% 20% 30% 40% / 10% 20% 30% 40%;
}
```

- And if only a single value is provided, it's copied over all 8 values:

```CSS
.box {
  /* These two declarations are equivalent: */
  border-radius: 100px;
  border-radius: 100px 100px 100px 100px / 100px 100px 100px 100px;
}
```

### Blobby shapes

- By using all 8 border-rdius values, ew can create some pretty neat blobby shapes.
- Check out this tool by [9Elements](https://9elements.github.io/fancy-border-radius/):
- You can use this tool to get some neat shapes with border radius.

## Nested Radiuses

- A common mistke people make, nesting radius.
- A rounded element in a rounded corner. We use the same border-radius for both parent and child.
- The corners dont' quite look right do they? They are uneven in the middle.

```HTML
<style>
  .card {
    width: min-content;
    background: white;
    text-align: center;
  }
  .avatar {
    display: block;
    width: 250px;
  }
  .card p {
    padding: 4px;
  }
  .card {
    border-radius: 16px;
    padding: 8px;
  }
  .avatar {
    border-radius: 16px;
  }
</style>

<article class="card">
  <img
    class="avatar"
    alt="Dog avatar"
    src="/cfj-mats/article-image-spot.jpg"
  />
  <h2>Spot</h2>
  <p>Perennial Good Boy. Parlimentary candidate, district 22. Dog park YIMBY.</p>
</article>
```

- By using the same `border-radius`, both orners are being rounde according to their own circles.
- Our corner would look more consistent if the two corners shared the same center point.
- How do we calculate this? We need to figure out the radius of the larger circle.
- To do that we need to sum pu teh inner circle's radius as well as any padding or other spacing
- In the case above, the correct outer radius is 24px (16px inner radius + 8px padding)
- We can use `calc` and CSS variables to do this calculation for us:

```HTML
<style>
  .card {
    --inner-radius: 16px;
    --padding: 8px;
    border-radius: calc(
      var(--inner-radius) + var(--padding)
    );
    padding: var(--padding);
  }
  .avatar {
    border-radius: var(--inner-radius);
  }
</style>

<article class="card">
  <img
    class="avatar"
    alt="Dog avatar"
    src="/cfj-mats/article-image-spot.jpg"
  />
  <h2>Spot</h2>
  <p>Perennial Good Boy. Parlimentary candidate, district 22. Dog park YIMBY.</p>
</article>
```

- What if the outer radius is known, and we want to calculat ethe inner radius?
- You do the same calculation except ew subtract the padding instead of adding it:

```HTML
<style>
  .card {
    width: min-content;
    background: white;
    text-align: center;
  }
  .avatar {
    display: block;
    width: 250px;
  }
  .card p {
    padding: 4px;
  }
    .card {
    --outer-radius: 24px;
    --padding: 8px;
    border-radius: var(--outer-radius);
    padding: var(--padding);
  }
  .avatar {
    border-radius: calc(
      var(--outer-radius) - var(--padding)
    );
  }
</style>

<article class="card">
  <img
    class="avatar"
    alt="Dog avatar"
    src="/cfj-mats/article-image-spot.jpg"
  />
  <h2>Spot</h2>
  <p>Perennial Good Boy. Parlimentary candidate, district 22. Dog park YIMBY.</p>
</article>
```

### Circular Radius

- The `border-radius` has a built in limit, it won't allow the corners to grow so large that they run into each other.
- If our element is 200 X 100, each corner will have a maximum radius of 50px. It cannot grow any larger.

```HTML
<style>
  .card {
    width: 200px;
    height: 100px;
    border: 3px solid hsl(225deg, 12%, 40%);
  }
  .card {
    /* Yowza! */
    border-radius: 6000px;
  }
</style>

<article class="card"></article>
```

### Asymmetric Circles

- What if you wanted to create a asymmtric shape?
- You can give the top corners a differ value then the bottom ones, creating a asymmetrical effect.

```HTML
<style>
  .card {
    width: 300px;
    height: 200px;
    border: 3px solid hsl(225deg, 12%, 40%);
    border-radius: 5000px 5000px 1000px 1000px;
  }
</style>

<article class="card"></article>
```

## Shadows

- Shadows give you app a sense of lighting and depth.
- And they are surprisingly deep.
- There are three main ways we can apply shadows in CSS: `box-shadow`, `text-shadow` and `filter: drop-shadow`

### box-shadow

- It's based on the box model. When you appy `box-shadow` to an element, that element's box will cast a simulated shadow behind it.

```HTML
<style>
  .card {
    box-shadow:
      2px 4px 8px hsl(0deg 0% 0% / 0.25);
  }
</style>

<article class="card">
  <h2>Hello World</h2>
</article>
```

- `box-shadow` is most commonly calded with 4 arguments:

1. Horizontal offset
2. Vertical offset
3. Blur radius
4. Color

- The blue radius is the strength of the blurring effect.
- The color can be any valid color value, but recommend using `hsl` or `hsla`. Using a solid color like black can be very aggressive shadow.

### filter: drop-shadow

- `filter` property allows us to access SVG filter mechanics rfom wihtin the CSS language.
- `fitler: drop-shadow()` is one of those filters.

```HTML
<style>
  .card {
    filter: drop-shadow(
      2px 4px 8px hsl(0deg 0% 0% / 0.25)
    );
  }
</style>

<article class="card">
  <h2>Hello World</h2>
</article>
```

- The API looks quite similar: it also accepts 4 values, of the same types in the same order.
- But the differnce is, under the hood, the `drop-shadow` filter funciton uses Gaussian blurring. This is a differnt mathematical way of blur. And produces slighly differ results.
- Instead of a simple blur radius, the third argumane specifies a "standard deviation".
- Compared to `box-shadow`, the `fitler` produces a softer, more blended shadow.

### text-shadow

- `text-shadow` is a shadow that applies only to the typography wihtin the selected element.

```HTML
<style>
  .card {
    width: 200px;
    max-width: 100%;
    background: white;
    border-radius: 4px;
    padding: 32px;
  }
  p {
    text-shadow:
      2px 4px 8px hsl(0deg 0% 0% / 0.25);
  }
</style>

<p>
  This text has a subtle shadow!
</p>
```

- One of the most common use case for `text-shadow` is to increase the contrast between light color text and a light background.

## Contoured Shadows

- Many CSS filters are designed ot work well with images. Like they were plucked out from PSD.
- For example, in Photoshop, when you add a drop shadow to layer, it applies that shadow to he opaque pixxels in thelayer. It doesn't do the rectangle itself.
- This means that if we use `filter: drop-shadow` on an image that aupports transparency, png, gif, svg, the shadow wil apply tot he non-transparent parts of the image:
- This effect isn't limeted to images, it works for any DOM node.
- We can apply `filter: drop-shadow` to an alement, and it contours that element and all of its descendants and applies the shadow tot hat shape.
- Example;

```HTML
<style>
  /* starter styles */
  body {
  overflow: hidden;
  }
  .card {
    position: relative;
    width: 200px;
    max-width: 100%;
    height: 250px;
    background: white;
    border-radius: 4px;
    padding: 32px;
    text-align: center;
  }
  .card h2 {
    font-size: 1rem;
  }
  .decoration {
    position: absolute;
    border: 4px solid white;
    border-radius: 50%;
  }
  .decoration.one {
    top: 0;
    right: 0;
    width: 80px;
    height: 80px;
    background: hotpink;
    transform: translate(50%, -50%);
  }
  .decoration.two {
    top: 50px;
    right: -70px;
    width: 50px;
    height: 50px;
    background: dodgerblue;
  }
  /* shadow */
  .card {
    filter: drop-shadow(
      2px 4px 8px hsl(0deg 0% 0% / 0.4)
    );
  }
</style>

<article class="card">
  <h2>Hi!</h2>
  <div class="decoration one"></div>
  <div class="decoration two"></div>
</article>
```

- We can even apply `filter: drop-shadow` to a group of elements, to make sure we don't have any shadow overlap. Like a stack of cards.
- This can prevent the overlap that happens when `box-shadow` is use don tightly grouped siblings.

```HTML
<style>
  body {
  margin: 0;
  padding: 0;
  }

  .item {
    height: 75px;
    background: white;
    border-radius: 4px;
  }

  .grid {
    display: grid;
    padding: 16px;
    grid-template-columns:
      repeat(auto-fill, minmax(100px, 1fr));
    gap: 8px;
    margin-bottom: 164px;
    max-width: 100vw;
    margin: 64px auto;
  }
  /*
    Apply the shadow to the grid parent,
    not the individual grid elements!
  */
  .grid {
    filter: drop-shadow(
      2px 4px 32px hsl(0deg 0% 0% / 0.4)
    );
  }
</style>

<main class="grid">
  <div class="item"></div>
  <div class="item"></div>
  <div class="item"></div>
  <div class="item"></div>
  <div class="item"></div>
  <div class="item"></div>
</main>
```

- When should you use `filter: drop-shadow` vs `box-shadow`, box-shadow still has some uses

## Single Sided Shadows

- Sometimes we want our shadows to be cast in a single direction. We want the shadow to be underneath the element, not spilling out in all directions.
- `box-shadow` is qualified to solve this problem. Because it alone takes an optional fifth argument: spead radius.

```CSS
.box {
  box-shadow: 0px 2px 4px 10px red;
  /*                       ^-- Spread! */
}
```

- The spread radius allows us to increase or decrease the size of the shadow.
- By default, the spread is 0, meaning the shadow is the same size as the element.
- A spread of `2px`, mean sthe shadow grows in every direction by 2px, becoming 4px wider and 4px taller.
- Example; Bottom Edge, the most common shadow

```HTML
<style>
  html, body {
  height: 100%;
  }
  body {
    padding: 0;
    display: grid;
    place-content: center;
  }

  .box {
    width: 200px;
    max-width: 100%;
    border-radius: 8px;
    background: white;
    padding: 16px 20px;
    display: grid;
    place-content: center;
    font-size: 2rem;
  }
  .box {
    --blur: 8px;
    --spread: calc(var(--blur) * -1);
    --offset: 12px;
    
    box-shadow:
      0px var(--offset)
      var(--blur) var(--spread)
      hsl(0deg 0% 0% / 0.2);
  }
</style>
<div class="box">
  Hello
</div>
```

- You can change the direction by tweaking the horiontal/vertical offsets.

```HTML
<style>
  html, body {
  height: 100%;
  }
  body {
    padding: 0;
    display: grid;
    place-content: center;
  }

  .box {
    width: 100px;
    height: 100px;
    border-radius: 8px;
    background: white;
  }
  .box {
    --blur: 8px;
    --spread: calc(var(--blur) * -1);
    
    box-shadow:
      12px 0px
      var(--blur) var(--spread)
      hsl(0deg 0% 0% / 0.2);
  }
</style>
<div class="box"></div>
```

- Teh `drop-shadow` filter function deos not take a `spread` argument, this feature is unique to `box-shadow`

## Inset Shadows

- One trick exlusive to `box-shadow`, we can use it to create inner shadows!
- The inset shadows allo wus to create the illusion that an element is lower than it's surrouding environment.

```HTML
<style>
  html, body {
  height: 100%;
  }
  body {
    padding: 0;
    display: grid;
    place-content: center;
  }

  .wrapper {
    background-color: hsl(0deg 0% 92%);
    border-radius: 16px;
    padding: 64px;
  }
  .wrapper {
    box-shadow:
      inset
      2px 2px 8px
      hsl(0deg 0% 0% / 0.33);
  }
</style>

<div class="wrapper">
  Hello World
</div>
```

- One cool trick, is to create a moat

```HTML
<style>
  html, body {
  height: 100%;
  }
  body {
    padding: 0;
    display: grid;
    place-content: center;
  }

  .wrapper {
    /* Using the nested radius trick discussed earlier! */
    --radius: 16px;
    --padding: 8px;
    background-color: hsl(230deg 80% 90%);
    padding: var(--padding);
    border-radius: var(--radius);
  }
  .box {
    width: 200px;
    max-width: 90vw;
    border-radius: calc(var(--radius) - var(--padding));
    background: white;
    padding: 16px 20px;
    display: grid;
    place-content: center;
    font-size: 2rem;
  }
  .wrapper {
    box-shadow:
      inset
      2px 2px 8px
      hsl(0deg 0% 0% / 0.33);
    /*
     The '.box' has a non-inset shadow.
     We don't want it to bleed beyond
     its wrapper.
    */
    overflow: hidden;
  }
  .box {
    box-shadow:
      2px 2px 8px
      hsl(0deg 0% 0% / 0.33);
  }
</style>

<div class="wrapper">
  <div class="box">
    Moat!
  </div>
</div>
```

## Exercises, Shadows

- Tooltip with shadow, we want the whole element to have a shadow, including the tip.

```HTML
<style>
  /* base styles */
  .tooltip {
    position: relative;
    width: 160px;
    padding: 16px;
    background: white;
    border-radius: 8px;
    text-align: center;
  }

  .tooltip::after {
    content: '';
    position: absolute;
    left: 0;
    right: 0;
    top: 0;
    margin: auto;
    background: inherit;
    width: 24px;
    height: 24px;
    transform: translateY(-100%);
    /*
      “clip-path” cuts out the triangle
      shape. We'll learn more about it
      later this module!
    */
    clip-path:
      polygon(0% 100%, 50% 0%, 100% 100%);
  }
  .tooltip {
  /*
    box-shadow:
      0px 0px 16px hsl(0deg 0% 0% / 0.5);
  */
  /* use filter instead of box-shadow to get the entire element */
  filter: drop-shadow(
    0px 0px 16px hsl(0deg 0% 0% / 0.4)
    );
  }
</style>

<div class="tooltip">
  Lorem ipsum dolor hello
</div>
```

- Scrapbooking, create an scrapbooking inspired UI

```HTML
<!--
Acceptance criteria:

• The <article> should be 90% or 500px wide,
  whichever is smaller. It should be centered.
• The inset shadow should have:
  • 1px horizontal offset
  • 2px vertical offset
  • 4px blur radius
  • Black color @ 30% opacity
• The “heart” sticker should have a shadow.
  (use your judgment for the params)
-->

<style>
  body {
  padding: 64px 32px;
  }
  .wrapper {
    background: peachpuff;
    padding: 64px;
  }
  .card {
    padding: 16px;
    background: white;
  }
  .sticker {
    font-size: 5rem;
  }
  .wrapper {
    width: 90%;
    max-width: 500px;
    margin: 0 auto;
    box-shadow: 
        inset 1px 2px 4px hsl(0deg 0% 0% / 0.3);
    border-radius: 1px;
  }
  .card {
  position: relative;
    box-shadow: 
       1px 2px 4px hsl(0deg 0% 0% / 0.3);
   border-radius: 1px;
  }
  .photo {
    display: block;
    width: 100%;
    border-radius: 1px;
  }
  .sticker {
    position: absolute;
    top: 0;
    left: 0;
    line-height: 5rem;
    transform: translate(-40%, -40%);
    filter: drop-shadow(
      1px 2px 6px hsl(0deg 0% 0% / 0.5)
    );
  }
</style>

<article class="wrapper">
  <div class="card">
    <img
      class="photo"
      alt="A girl sits on a boulder overlooking a mountain"
      src="/cfj-mats/girl-mountain.jpg"
    />
    <div
      class="sticker"
      role="img"
      aria-label="heart sticker"
    >
      💖
    </div>
  </div>
</article>
```

## Designing Shadows

- It's one thing to know hwo to use shadow CSS properties, it's another thing to create realistic, lush-looking shadows.
- Why even use shadows? Shadows allow us to create the illusion of depth, deffer element son the apge floating at differ levels.
- The best website and apps, feel tactile and genuine. Shadows help to sell that illusion.
- The benefit, is you can draw attention to elements that fee closest to us. So by elevating a dialog box, we make it more likely hat the user focuse on it first.
- When you use shadows, you eithe rwant to increase the prominence of a specific element, or I want to make my app feel more tactile and life-like.
- In order to do this, you need a holistic view of the shadows in our app.

### Creating a consistent environment

- Most of us are not using shadows correctly. When we want a shadow, we drop a `box-shadow` on an element and mess with the numbers.
- The problem is, we end up with a mess of inconsistent shadows. Our goal is to creat an illution of depth. We need each shadow to match, other wise it just looks like a blob of burry borders.
- In the real world, shadows are cast from a light source, the direction of the shadows depends ont he positino of the light.
- In general, we should decide on a single light soruce from all elements on the page. It's common for that light soruce to be above and slightly to the left.
- If CSS ha da real lighting system, we would specify a position for one or more lights. But CSS has no such thing.
- INstead we shift teh shadow around by specifying a horizontal offset adn a vertical offset.
- Here is the first trick: **Every shadow on teh page should share the same ratio**
- It makes it seem like, every element is lit fom the same very-far-away light source. Like the sun.
- **Elevation**, how can we create the illusion that an element is lifting up tward teh user?
- We need to tweak all 4 variables in tandom to creat a cohesive experience.
- `box-shadow: 2.0px 4.0px 4.0px hsl(0deg 0% 0% / 0.44);`
- The first two numbers, horizontal and vertical offset, scale together in tandem.
- *the vertical offset is always 2x the horizontal one*
- The two other things that happen
  - The blur radius get larger
  - The shadow becomes less opaque
- Think about what happens when you put your hand near your desk and slowly lift it up. Notice how the shadow changes, it moves further away from your hand (larger offset), it becomes fuzzier (larger blur radius) and starts to fade away (lower opacity).
- Apply your intuition when it comes to designing shadows.
- **Summarize**
  - Each element on the apge should be lit form the same global light source.
  - The `box-shadow` property represents the light soruce position using horizontal and vertical offsets. For consistency, each shadow should use hte same ratio between tehse two numebrs.
  - As an elemtn gets closer tot he user, the offset shold increase, teh blur radius should increase, and teh shadow's opacity should decrease.
  - Skip the calculations and use your intuition.

## Layering

- Modern 3D tools like Blender can produce realistic chadows and lighting by using a technique known as raytracing.
- Uses hundreds of beams of lights shot out from the camera, bouncing off of surfaces in the scene hundreds of times.
- `box-shadow` is much more simple, as a result shadows will never look photo-realistic, but we can use a technique called *layering*
- Instead of using a single box-shadow, we can stakk a handful on top of each other, slighly differ offsets and radiuses:

```HTML
<style>
  /* default */
  .wrapper {
    display: flex;
    gap: 32px;
  }

  .box {
    width: 100px;
    height: 100px;
    border-radius: 8px;
    background-color: white;
  }
  /* example */
  .traditional.box {
    box-shadow:
      0 6px 6px hsl(0deg 0% 0% / 0.3);
  }
  .layered.box {
    box-shadow:
      0 1px 1px hsl(0deg 0% 0% / 0.075),
      0 2px 2px hsl(0deg 0% 0% / 0.075),
      0 4px 4px hsl(0deg 0% 0% / 0.075),
      0 8px 8px hsl(0deg 0% 0% / 0.075),
      0 16px 16px hsl(0deg 0% 0% / 0.075)
    ;
  }
</style>

<section class="wrapper">
  <div class="traditional box"></div>
  <div class="layered box"></div>
</section>
```

- By layering multiple shadows, we create a more realistic shadow.
- More detail in this blog post by Tobias, Smoother and [Sharper Shadows with Layered box-shadow](https://tobiasahlin.com/blog/layered-smooth-box-shadows/)
- Also check out Josh's tool: [Shadow Palette](https://www.joshwcomeau.com/shadow-palette/)
- and his blog post on how to use it: [Intro to Shadow Palette Generator](https://www.joshwcomeau.com/css/introducing-shadow-palette-generator/)

### Color Matched Shadows

- So far we have used semi-transparent black, `hsl(0deg 0% 0% / 0.4`, this is less then ideal.
- When we layer black over a background color, it desaturates it quite a bit.
- Check out the two examples:

```HTML
<style>
  .wrapper {
    display: flex;
    gap: 32px;
  }
  .box {
    width: 100px;
    height: 100px;
    border-radius: 8px;
  }
  body {
    background-color:
      hsl(220deg 100% 80%);
  }
  .black.box {
    background-color:
      hsl(0deg 0% 0% / 0.25);
  }
  .darker.box {
    background-color:
      hsl(220deg 100% 72%);
  }
</style>

<section class="wrapper">
  <div class="black box"></div>
  <div class="darker box"></div>
</section>
```

- The box on the left uses a transparent black, the box ont he right matches the color's hue and stauration, but lowers the lighness. We end up with a much more vibrant box.
- A similar effect happens when we use a darker color for our shadows:

```HTML
<style>
  .wrapper {
    display: flex;
    gap: 32px;
  }
  .box {
    width: 100px;
    height: 100px;
    border-radius: 8px;
    background: white;
  }
  body {
    background-color:
      hsl(220deg 100% 80%);
  }
  
  .black.box {
    --shadow-color: hsl(0deg 0% 0% / 0.25);
  }
  .darker.box {
    --shadow-color: hsl(220deg 100% 55%);
  }
  .box {
    filter: drop-shadow(
      1px 2px 8px var(--shadow-color)
    );
  }
</style>

<section class="wrapper">
  <div class="black box"></div>
  <div class="darker box"></div>
</section>
```

- Still takes some experimenting to get it right:

```HTML
<style>
  .wrapper {
    display: flex;
    flex-direction: column;
    gap: 32px;
  }
  .box {
    width: 200px;
    height: 100px;
    border-radius: 8px;
    background: white;
    display: grid;
    place-content: center;
  }
  body {
    background-color:
      hsl(220deg 100% 80%);
  }
  .black.box {
    --shadow-color: hsl(0deg 0% 0% / 0.5);
  }
  .darker.box {
    --shadow-color: hsl(220deg 100% 50%);
  }
  .goldilocks.box {
    --shadow-color: hsl(220deg 60% 50%);
  }
  .box {
    filter: drop-shadow(
      1px 2px 8px var(--shadow-color)
    );
  }
</style>

<section class="wrapper">
  <div class="black box">Too grey</div>
  <div class="darker box">Too bright</div>
  <div class="goldilocks box">Just right</div>
</section>
```

- By matcing the hue and lowerin gthe saturatoin/lightness, we can create an authentic shadow that doesn't have that "washd out" grey quality.

### Puting it all together

- So far we have covered 3 distinct ideas.
  - Creating a cohesive environment by coordinating our shadows
  - Using layering to create more-realistic shadows
  - Tweaking the coolorsto prevent washed out shadows
- Example of all three:

```HTML
<style>
  body {
  background-color:
    hsl(220deg 100% 80%);
  }
  .wrapper {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 32px;
  }
  .box {
    border-radius: 8px;
    background: white;
    display: grid;
    place-content: center;
  }
  .first.box {
    width: 50px;
    height: 50px;
    box-shadow:
      0.5px 1px 1px hsl(220deg 60% 50% / 0.7);
  }
  .second.box {
    width: 100px;
    height: 100px;
    box-shadow:
      1px 2px 2px hsl(220deg 60% 50% / 0.333),
      2px 4px 4px hsl(220deg 60% 50% / 0.333),
      3px 6px 6px hsl(220deg 60% 50% / 0.333);
  }
  .third.box {
    width: 150px;
    height: 150px;
    box-shadow:
      1px 2px 2px hsl(220deg 60% 50% / 0.2),
      2px 4px 4px hsl(220deg 60% 50% / 0.2),
      4px 8px 8px hsl(220deg 60% 50% / 0.2),
      8px 16px 16px hsl(220deg 60% 50% / 0.2),
      16px 32px 32px hsl(220deg 60% 50% / 0.2);
  }
</style>

<section class="wrapper">
  <div class="first box"></div>
  <div class="second box"></div>
  <div class="third box"></div>
</section>
```

### Fitting into a design system

- With everyone moving toward design systems, can we "tokenize" our shadows?
- Yes, you can here is an example using styled components.

```JAVASCRIPT
const ELEVATIONS = {
  small: `
    0.5px 1px 1px hsl(var(--shadow-color) / 0.7)
  `,
  medium: `
    1px 2px 2px hsl(var(--shadow-color) / 0.333),
    2px 4px 4px hsl(var(--shadow-color) / 0.333),
    3px 6px 6px hsl(var(--shadow-color) / 0.333)
  `,
  large: `
    1px 2px 2px hsl(var(--shadow-color) / 0.2),
    2px 4px 4px hsl(var(--shadow-color) / 0.2),
    4px 8px 8px hsl(var(--shadow-color) / 0.2),
    8px 16px 16px hsl(var(--shadow-color) / 0.2),
    16px 32px 32px hsl(var(--shadow-color) / 0.2)
  `
}
```

- This uses a static `ELEVATIONS` object, which defines 3 dlevations. The color data for each shadow uss a CSS variable, `--shadow-color`

## Colors

- Color perception varies quite a lot form person to person. We need to consider how we can use color more respsible in our projects.
- Not just about contrast ratios, we need to make sure we aren't relying on colors that can' tbe distinguished by everybody.
- Coming up with a nice color palette? Take a look at [Josh's Color Palettes](https://courses.joshwcomeau.com/css-for-js/treasure-trove/014-color-palettes) article.

### Accessibility Color

- When using color in our interfaces, there are two questions we nee dto ask ourselves
  - Is there enough contrast between the text/UI and background?
  - Can folks who are color blind understand this UI?

#### Color Contrast

- In order for text to be legible, it needs to have significant amount of contrast between it and it's background.
- WCAG has a mathmatical number formula to checking contrast ratios.
- It accepts two colors, and spits our a number. The bigger the number, the greater the contrast
- The scale reanges from 1 (no contrast) to 21 (max contrast)
- What's the min acceptable number? Two things to consider
  - 1. How big is the text? Large text (headings) are allowed to hae lower contrast ratios than normal text (para)
  - 2. What elvel of support are you aimingfor? AA or AAA guideliens. AAA is more strict. Companies generally settl on AA.
- Here are the minumum acceptable contrast ratios:

|             | Normal text | Large text    |
| ----        |----         |          ---  |
| AA          | 4.5         | 3             |
| AAA         | 7           | 4.5           |

- You can check the color contrast with this handy tool: [Color Review](https://color.review/)
- If you color has low contrast, the rool will show you visually where the thresholds are.
- Chrome also has an inspector while hovering over the element selector.

### Color picking

- What if it isn't clear what the colors are, for example, text in front of image.
- You wil need to sample some colors to see what the contrast is like. You can find a colo r picker browsewr extensions to get pixel values of an image.
- Try and find h the low contrast parts of the photo to check.

### Color Blindness

- Color blindness is hte inability to see certain colors. It is estimated that between 5 to 10% of t people have some amount of color blindness.
- Ther are several categories of color blindness
  - Red/green color blindness (protanopia, deuteranopia)
  - Blue/yellow (tritanopia)
  - Complete colorblindness (monochromacy)
- The most common form of color blindness is red/green. To those individuals, red adn green both appear brownish
- Hard for us to know what thsi experience is like. So we need to simuate it. Check out [Josh's simulation tool](https://courses.joshwcomeau.com/css-for-js/09-little-big-details/04.01-color-accessibility)
- In our work, we have to be careful not to rely to heavily on color to communicate meaning. This is an easy mistake to make.
- For example, some people associate green with success and red with failure, but these two colors are identical from most colorblind folks.
- We can still use color as an enhancement, but it needs to be a secondary indicator. Not the only one.
- Browser dev tools allow us to simulate colorblindness.
- [Chrome Emulate vision deficiencies](https://developer.chrome.com/blog/new-in-devtools-83/#vision-deficiencies)
- [FireFox dev tools COlor vision simulation](https://developer.mozilla.org/en-US/docs/Tools/Accessibility_inspector/Simulation)

### Exercises, Colors Accessibility

- Fix this UI has several contrast and color issues.
- Use the browser dev tools to look for contrast issues.
- If you have an element that is partially transparent, take a screen grab, drop in Figma, draw a new square, and use color picker to grab any colors at pixel leve.
- Watch out for red and green combos. If a chart, you can use a differ line style, dotted to differentiate.

## Selection Colors

- How do you control the colors of other things within the DOM, text selection, scrollbars, native form controls.

### Selection colors

- By default, when you select text, a blue background is applied.
- We can tweak both the background and text color for the seleciton box using the `::selection` pseudo-element.
- Small details but can be surpisingly cool.

```HTML
<style>
  ::selection {
    color: hsl(25deg 100% 20%);
    background-color: hsl(55deg 100% 60%);
  }
</style>

<p>
  Try selecting some of the text in these paragraphs!
</p>
<p>
  Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since the 1500s.
</p>
```

### Tweaking selection styles by element

- Sometimes yo may wish to use different seleciton styles for difer elements on teh page, rather than a single global selection style.

```HTML
<style>
  p::selection {
    color: black;
    background-color: yellow;
  }
</style>

<p>
  This paragraph has <em>some emphasized text</em>, in the middle.
</p>
```

- Seleciotn styles are not inheritable, they should be, but no major browser implements it correctly. So you can do some neat stuff via CSS variables.

```HTML
<style>
  ::selection {
    color: var(--selection-color);
    background-color:
      var(--selection-background);
  }
  
  html {
    /*
      Define global defaults
      for selection colors…
    */
    --selection-color:
      hsl(25deg 100% 20%);
    --selection-background:
      hsl(55deg 100% 60%);
  }
  
  figure {
    /*
      …But then override those values
      for specific parts of the page!
    */
    --selection-color: hsl(0deg 0% 0%);
    --selection-background:
      hsl(333deg 100% 50%);
  }
</style>
```

- This example, every element on the page has the same `::selection` style, but they rely on CSS variables rather than hardcoded values. When we change the value of a CSS variable, the seleciotn styles change, for that element and all of its decendants.
- However, there are accessibility concerns, it can cause confusion, especially for people who are developing computer literacy.

### Accent Colors

- When styling certain types of UI (checkboxes, radio buttons, sliders), we typically have two choices
  - Use teh browser defaults pretty much as is
  - Rebuild the elemtn from scratch, suing more-flexible tags like `<buuton>`
- An upcomong addition to the CSS language is going to give us a thrid choice: `accent colors`
- With the `accent-color` property, we wil eb abelt o change the colors used in a handful of HTML elemtns.
- Post by [Adam Argyle and Joey](https://web.dev/accent-color/) Arhar on setting accent color
- Support is getting better, [Can I Use](https://caniuse.com/mdn-css_properties_accent-color)

## Gradients

- CSS has a surprisingly deep and sophisticated set of gradient functions:

### Linear Gradients

- If we provide two colors to `linear-gradient` it will interpolate between them, starting from the top and going down

```HTML
<style>
  .box {
    width: 200px;
    height: 200px;
    border: 3px solid;
    background-image: linear-gradient(
      deeppink,
      gold
    );
}
</style>
<div class="box"></div>
```

- If we want that gardient to run at a differ angle, we can pass that as an optional first argument.

```CSS
.box {
  width: 200px;
  height: 200px;
  border: 3px solid;
  background-image: linear-gradient(
    45deg,
    deeppink,
    gold
  );
}
```

- The default angel for gradients is `180deg`. If we set it to `0deg`, the gradeint would run from bottom to the top.
- We can also specify cardinal directions with the `to` keyword

```CSS
.box {
  background-image: linear-gradient(to right, color1, color2);
  /* Is equivalent to: */
  background-image: linear-gradient(90deg, color1, color2);
}
```

- We can pass more than two colors, to create richer gradients:

```HTML
<style>
  .box {
    width: 200px;
    height: 200px;
    border: 3px solid;
    background-image: linear-gradient(
      90deg,
      deeppink,
      red,
      coral,
      gold,
      white
    );
  }
</style>
<div class="box"></div>
```

- Gradients have color stops, points along the spectrum where the color is fully applied. By default, these colors will be equidistant:
- We can change their placement, thought, with percentages.

```CSS
.box {
  width: 200px;
  height: 200px;
  border: 3px solid;
  background-image: linear-gradient(
    90deg,
    deeppink,
    red 10%,
    coral 20%,
    gold 70%,
    white
  );
}
```

- We can use color stops to do something pretty neat and unexpected. We can create sharp lines by positioning the stops very close together.

```CSS
.box {
  width: 200px;
  height: 200px;
  border: 3px solid;
  background-image: linear-gradient(
    90deg,
    deeppink 0%,
    deeppink 9.99%,
    red 10%,
    red 19.99%,
    coral 20%,
    coral 29.99%,
    gold 30%,
    gold 39.99%,
    white 40%
  );
}
```

### Gradient Hints

- In addtition to color stops, we have color hints. A color hint allows us to move the midpoint between two colors

```HTML
<style>
  .box.one {
  background-image: linear-gradient(
    deeppink,
    30%,
    gold
  );
}
.box.two {
  background-image: linear-gradient(
    deeppink,
    80%,
    gold
  );
}

.box {
  width: 200px;
  height: 200px;
  border: 3px solid;
  margin: 16px;
}
</style>
<div class="box one"></div>
<div class="box two"></div>
```

## Radial Gradients

- A radial gradient emanates outwards in a circle from a single point.

```HTML
<style>
  .box {
  width: 200px;
  height: 200px;
  border: 3px solid;
  background-image: radial-gradient(
    deeppink,
    red,
    coral,
    gold,
    white
  );
}
</style>
<div class="box"></div>
```

- A few differences between radial and linear gradients.
- The optional first argument for radial gradients is a little differ.

```CSS
.box {
  width: 200px;
  height: 200px;
  border: 3px solid;
  background-image: radial-gradient(
    50% 100%,
    deeppink,
    gold
  );
}
```

- We are saying that the gradient core should span half teh available width and the full height. This creates a tall skinny ellipse.
- You can use the `circle at` prefeix, to simplify things. A sunset effect for example;

```HTML
<style>
  .box {
  width: 200px;
  height: 200px;
  border: 3px solid;
  background-image: radial-gradient(
    circle at 50% 100%,
    white 0%,
    yellow 10%,
    gold 20%,
    coral 30%,
    skyblue
  );
}
</style>
<div class="box"></div>
```

- More in-depth info on [MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/gradient/radial-gradient())

## Conic Gradients

- Cnic gradients are what whould happen if you took a straight line aith a linear gradient, and formed it into a cicle
- Similar to other gradient functions:

```HTML
<style>
.box {
  width: 200px;
  height: 200px;
  border: 3px solid;
  background-image: conic-gradient(
    deeppink,
    red,
    coral,
    gold,
    white
  );
}
</style>
<div class="box"></div>
```

### Smoothing it out

- By default, you end up with a harsh line running vertically through the top half. This is because our start and end colors are so different.
- If oru gradient ends with the same color it started with, we can create a smoother effect.

```HTML
<style>
 .box {
  width: 200px;
  height: 200px;
  border: 3px solid;
  background-image: conic-gradient(
    deeppink,
    coral,
    gold,
    coral,
    deeppink /* <-- same color! */
  );
}
</style>
<div class="box"></div>
```

- Or you can make all the lines harse, by shifting the colro stops to be adjacent.
- Really useful for creating pie charts.

```HTML
<style>
.box {
  width: 200px;
  height: 200px;
  border: 3px solid;
  border-radius: 50%;
  background-image: conic-gradient(
    deeppink 0%,
    deeppink 33.3%,
    gold 33.4%,
    gold 66.6%,
    slateblue 66.7%,
    slateblue 100%
  );
}
</style>
<div class="box"></div>
```

### Gradient angle and position

- Lineaer gradient are given an angle (`45deg`) and radial gradients are given a position `circle at 50% 100%`. Conic gradients take both.
- The format is: `from <angle> at <position>`

### Recipes

- Some things you can do with conic gradients

### Edge glow

- One of the most practical  cases is to create a glow effect.

```HTML
<style>
.box {
  width: 200px;
  height: 200px;
  border: 3px solid;
  background-image: conic-gradient(
    from 90deg at 50% 100%,
    hsl(220deg 80% 55%) 50%,
    hsl(220deg 90% 75%) 62.5%,
    hsl(220deg 100% 85%) 75%,
    hsl(220deg 80% 75%) 87.5%,
    hsl(220deg 80% 55%) 100%
  );
}
</style>
<div class="box"></div>
```

## Easing Gradients

- Timing funcitons like linear an ease-out used by the `transition` property.
- Those timing functions refer to how a value should be interpolated over time.
- Those same functions can also refer to how to interpolate something **over space**.
- Imaging we are moving a box by 100px over 10 seconds. In a linear timing function, it will move by 10px every second.
- Imagine we are drawing a gradient from a hue of 0 degrees, to a hue of 40 degres, over 10em. A lineear timing function, teh color changes by 4 degres every rem.
- **Just like you can choose different timing functions for motion, we can choose differ timing functions for gradients**
- No matter which timing funciton you choose, the start and end colors remain constant.

### Using Easing Gradients

- But, esing gradients is not part fo the CSS language yet.
- In the future, hopefully it will be as simple as adding in the property.
- For now, we will use a toll tha twill simulate these timing functions by generating a bunch of color stops:

```CSS
.box {
  /* Simulated "ease-in-out": */
  background-image: linear-gradient(
    to bottom,
    hsl(330, 100%, 45.1%) 0%,
    hsl(331, 89.25%, 47.36%) 8.1%,
    hsl(330.53, 79.69%, 48.96%) 15.5%,
    hsl(328.56, 70.89%, 49.96%) 22.5%,
    hsl(324.94, 63.52%, 50.4%) 29%,
    hsl(319.21, 54.99%, 50.3%) 35.3%,
    hsl(310.39, 46.14%, 49.68%) 41.2%,
    hsl(296.53, 39.12%, 49.7%) 47.1%,
    hsl(280.63, 42.91%, 53.43%) 52.9%,
    hsl(265.14, 47.59%, 56.84%) 58.8%,
    hsl(250.13, 52.52%, 59.88%) 64.7%,
    hsl(235.88, 59.2%, 60.91%) 71%,
    hsl(225.81, 68.23%, 57.85%) 77.5%,
    hsl(218.93, 74.97%, 54.21%) 84.5%,
    hsl(213.89, 79.63%, 49.97%) 91.9%,
    hsl(210, 100%, 45.1%) 100%
  );
}
```

- A easing tool you can use is by [Andreas Larsen](https://larsenwork.com/easing-gradients/#editor), also a[post-CSS version](https://github.com/larsenwork/postcss-easing-gradients)
- It's a small detail, but upgrading to easing gradients can really make a product feel polished.
- Note: the tool's snippet is incomplete. It produces a snippet that looks like...

```CSS
.forNow {
  linear-gradient(
    /* values here */
  );
};
```

- This is incomplete, linear-gradient is a value, but it's missing the property. Update it to use `background-image`

```CSS
.forNow {
  background-image: linear-gradient(
    /* values here */
  );
};
```

## Exercises

- Image overlay gradient with a figcaption using easing gradients

```HTML
<!--
  Acceptance criteria:
  
  • Image should be 300px by 200px.
  • Gradient should be 100px tall.
  • Gradient should max out at 85%
    opacity
-->

<style>
figure {
  position: relative;
  margin: 0;
  width: min-content;
}
figure .photo {
  display: block;
  width: 300px;
  height: 200px;
  object-fit: cover;
}
figcaption {
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
  height: 50%;
  padding: 16px;
  color: white;
  display: flex;
  align-items: flex-end;
  text-shadow: 0px 0px 3px hsl(0deg 0% 0% / 0.5);
  background: linear-gradient(
    to bottom,
    hsla(0, 0%, 0%, 0) 0%,
    hsla(0, 0%, 0%, 0.011) 10.8%,
    hsla(0, 0%, 0%, 0.041) 20.6%,
    hsla(0, 0%, 0%, 0.088) 29.5%,
    hsla(0, 0%, 0%, 0.149) 37.5%,
    hsla(0, 0%, 0%, 0.22) 44.8%,
    hsla(0, 0%, 0%, 0.299) 51.5%,
    hsla(0, 0%, 0%, 0.383) 57.6%,
    hsla(0, 0%, 0%, 0.467) 63.3%,
    hsla(0, 0%, 0%, 0.551) 68.7%,
    hsla(0, 0%, 0%, 0.63) 73.9%,
    hsla(0, 0%, 0%, 0.701) 78.9%,
    hsla(0, 0%, 0%, 0.762) 83.9%,
    hsla(0, 0%, 0%, 0.809) 89.1%,
    hsla(0, 0%, 0%, 0.839) 94.4%,
    hsla(0, 0%, 0%, 0.85) 100%
  )
}
</style>

<figure>
  <img
    class="photo"
    alt="Two upside-down dog heads"
    src="/cfj-mats/upside-down-dogs.jpg"
  />
  <figcaption>“Dogs From Above”</figcaption>
</figure>
```

### OVerlapping shapes

- Gradients can be used to create some pretty nifty patterns. Like overlapping triangles and circles.
- Need to stack gradients, two gradients, you can stack them as long as one is transparent.
- And how to draw the sharp lines.
- Can use `linear-gradient` and `radial-gradient` fuctions to create neat decorative effects.

```HTML
<style>
  /* base */
  html, body {
    height: 100%;
  }
  body {
    background: var(--blue-bg);
  }
  .background {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
  }
  html {
    --blue-bg: hsl(230deg 40% 20%);
    --blue-darker: hsl(230deg 40% 24%);
    --blue-dark: hsl(230deg 40% 28%);
  }
  
  .linear-slopes {
    background: linear-gradient(
      calc(180deg - 20deg),
      transparent 0%, 
      transparent 49.99%,
      var(--blue-dark) 50%,
      var(--blue-dark) 100%
    ), linear-gradient(
      calc(180deg + 20deg),
      transparent 0%, 
      transparent 49.99%,
      var(--blue-darker) 50%,
      var(--blue-darker) 100%
    );
  }
  
  .radial-slopes {
    background: radial-gradient(
      circle at 100% 120%,
      var(--blue-dark) 0%, 
      var(--blue-dark) 49.99%,
      transparent 50%,
      transparent 100%
    ), radial-gradient(
      circle at 0% 100%,
      var(--blue-darker) 0%, 
      var(--blue-darker) 49.99%,
      transparent 50%,
      transparent 100%
    );
  }
</style>

<div class="background radial-slopes"></div>
```

### Trophy Display

- Use Conic gradients to create a glow / spotlight effect on a trophy graphic.

```HTML
<style>
  body {
    padding: 64px 0;
  }
  html {
    --dark-gold: hsl(34deg 90% 45%);
    --gold: hsl(44deg 80% 70%);
    --light-gold: hsl(44deg 100% 85%);
  }
  .wrapper {
    position: relative;
    height: 325px;
    max-width: 550px;
    display: flex;
    justify-content: center;
    margin: auto;
    background-color: var(--gold);
    border-radius: 10000px 10000px 1000px 1000px;
    background-image: conic-gradient(
      from 90deg at 50% 100%,
      var(--dark-gold) 50%,
      var(--gold) 62.5%,
      var(--light-gold) 75%,
      var(--gold) 87.5%,
      var(--dark-gold) 100%
    );
  }
  
  .trophy {
    transform-origine: center bottom;
    transform: scale(1.4) translateY(16px);
    /* opacity: 0; */
  }
</style>

<div class="wrapper">
  <img
    class="trophy"
    alt="gold trophy"
    src="/cfj-mats/gold-trophy.png"
  />
</div>
```

### Gradient Dead Zones

- Sometimes gradients get a big "grey" in the middle?
- That happens because gradients in CSS are essentially like yoru car's GPS, they try to take the shortest most direct route between two colors, using RGB values.
- Imagine a color wheel, with a straight line from one color to the other.
- What is instead, if we curve around teh color wheel. We end up with a much nicer looking gradient.
- By picking the saturated midpiont colors, we create a much more vibrant gradient.
- How do you come up iwth teh right midpoint values? Tricky, but we have a tool for that.
- [Gradient Generators](https://courses.joshwcomeau.com/css-for-js/treasure-trove/013-gradient-generator)

## Mobile UX Improvements

- Mobile browsers are a little unique, look at some usability improvements.

### Tap rectangles and text selection

- When tapping an interactive elementon mobile devices, the browswer will flash a "tap rectangle" briefly.
- There is a grey rectangle that flashes quickly. The box can suerve as helpful feedback to confirm that you have successfully tapped an interactive element. But our button has plenty of feedback as is with the 3D effect.
- You can remove it with this declaration.

```CSS
.pushable {
  -webkit-tap-highlight-color: transparent;
}
```

- in iOS, if the button is held down for a second, the phone will try and select the text within teh button
- The `user-select` property allows us to set an element to be unselectable:

```CSS
.pushable {
  user-select: none;
}
```

### Increasing target sizes

- There are several categories of input devices:
  - fine pointers, like mouse or trackpad
  - coarse pointers, like a finger or a touchscreen
  - non-pointer devices, liek a keyboard

- With a coarse pointer, it's hard to be precise. Mobile users typically use a touchscren wtih a finger, we need to ensure a large enough tappable area.
- Apple recommends a minimum tap target of 44px by 44px. This is the minimum, though it's better to overshoot this target.
- Here is the thing, this doesn't mean we have to make everything visually bigger.

```HTML
<style>
  button {
    padding: 0 16px;
    background: hsl(230deg 80% 25%);
    color: white;
    border: none;
    border-radius: 4px;
    font-size: 1rem;
    cursor: pointer;
  }

  button:active {
    background: hsl(230deg 80% 10%);
  }
  button {
    position: relative;
    height: 32px;
  }
  
  button::after {
    --tap-increment: -8px;
    content: '';
    position: absolute;
    top: var(--tap-increment);
    left: var(--tap-increment);
    right: var(--tap-increment);
    bottom: var(--tap-increment);
  }
</style>

<button>
  Push me
</button>
```

- Our button has a pseudo-element that extends outwards by 8px in every direction. Our button may only be 32px tall, but the tap target size is 48px;
- How it Works:
  - Make sure the link/button is a containling block for positioned elements by setting the `position: relative`
  - Add a child pseudo-element, and make it absolutely-positioned.
  - Set `top` / `left` / `right` / `bottom` to a negative value, so that it extends outwards.
  - The trick allow you to increase the size of the tap target without eafecting the design.

- [CodePen on auto increase click targets](https://codepen.io/third774/pen/XWgXZRY)

## Pointer Events

- The `pointer-events` property allows us to get an element to be a hologram: you can see it , but you can't touch it.

```HTML
<style>
  button {
    pointer-events: none;
  }
</style>

<button>
  Try clicking me!
</button>
```

- We can still focus the button using the keyboard, and select the text. But click events pass right through.
- Here is the wild thing, we can undo pointer-events in descendants
- For example, if you have a toast or message that overlays a button. You can set a parent element (toast message) to ignore pointer events, but then restore the default value to a child. The child will support clicks/taps btu the parent won't.

```HTML
<style>
  .toast-wrapper {
    position: fixed;
    left: 0;
    right: 0;
    bottom: 0;
    padding: 32px;
    display: grid;
    place-content: center;
  }
  .toast {
    background: hsl(208deg 68% 45%);
    padding: 8px 32px;
    border-radius: 4px;
    color: white;
    font-size: 0.875rem;
  }
  .random {
    position: fixed;
    left: 16px;
    bottom: 16px;
  }
  .toast-wrapper {
    pointer-events: none;
  }
  
  .toast {
    pointer-events: auto;
  }
</style>

<button class="random">
  Random button
</button>

<div class="toast-wrapper">
  <div class="toast">
    Your tweet was sent.
  </div>
</div>
```

- The `.toast-wrapper` wil ignore clicks, so that we can click the `.random` button behind it.
- Being able to selectively ignore clicks without locking anything in for the element's descendants is a pretty wild power. A trick to keep in your back pocket.

## Clipping with Clip-Path

- One of the most underrated CSS properties is `clip-path`.
- `clip-path` allows us to trim a DOM node into a specific shape. For example, to make a triangle.

```HTML
<style>
  .triangle {
    width: 100px;
    height: 80px;
    background-color: deeppink;
    clip-path: polygon(
    0% 100%,
      50% 0%,
      100% 100%
    );
  }
</style>

<div class="triangle"></div>
```

- For a long time we had to rely on hacky tricks like using transparent borders to create shapes in CSS. These days it's way easier with `clip-path`
- Several ways to make a `clip-path`, the `polygon()` function is one of them.
- For clip path, the order matters, adn anything outside that is clipped out.
- You can clip out anything, a DOM element, image or video.
- Tool for helping you with clip paths, [Clippy](https://courses.joshwcomeau.com/css-for-js/treasure-trove/001-clippy)
