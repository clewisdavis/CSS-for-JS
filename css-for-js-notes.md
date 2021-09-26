
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
- `mind-width` for mobile first
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
