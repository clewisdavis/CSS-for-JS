# Continued Notes

Other file was getting way to large for my computer to handle. Makign a seperate one. Will combine later.

## Scrolling

### Scroll Snapping

- The second property is `scroll-snap-align`. This property lets us se the snap point for the children.
- Choose `start` when you want the left edge of the element to snap to the left edge of container, in a horizontal scroll situation.
- Center snap alignment helps when we want to see "previews" of sibling elements on either side:

```HTML
<style>
    html, body {
    height: 100%;
    padding: 0;
    }

    .wrapper {
    display: flex;
    display: flex;
    width: 100%;
    height: 100%;
    overflow: auto;
    }

    .box {
    height: 100%;
    display: grid;
    place-content: center;
    border-radius: 8px;
    }
    .box.one {
    background-color: peachpuff;
    }
    .box.two {
    background-color: lavender;
    }
    .box.three {
    background-color: navy;
    color: white;
    }
    .box.four {
    background-color: hotpink;
    }
  /* sample */
  .wrapper {
    scroll-snap-type: x mandatory;
    padding: 32px;
  }
  .box {
    margin-left: 16px;
    margin-right: 16px;
    min-width: calc(100% - 32px);
    scroll-snap-align: center;
  }
</style>
<div class="wrapper">
  <div class="box one">
    First Box
  </div>
  <div class="box two">
    Second Box
  </div>
  <div class="box three">
    Third Box
  </div>
  <div class="box four">
    Fourth Box
  </div>
</div>
```

- In this example, the `scroll-snap-align: center`, each element has an anchor int eh very middle. And hat anchor snaps to the center of the parent container.

### Exercises

- Musical Artists, you want to show a horizontal ist of related artists. When you scroll side to side, we want to snap it so each artist is centered in teh viewport:
- First, make sure the container is managing the scroll, via `overflow: auto`
- Then add the `scroll-snap-type` to it.
- Then you have to tell the children element, and add `scroll-snap-align` to it.
- Center is neat, you can tell the user and give them a preview of the next/previous elements.
- Cover art scroll design

```HTML
<style>
  /* Base Styles */
  .artists {
    max-width: 400px;
    padding: 16px 32px;
    display: flex;
    gap: 16px;
    background: white;
    border-radius: 4px;
    }
    .artist-card {
    position: relative;
    min-width: calc(100% - 32px);
    height: 400px;
    border-radius: 6px;
    /* Trim corners */
    overflow: hidden;
    }
    .cover-art {
    display: block;
    width: 100%;
    height: 100%;
    }
    .about {
    position: absolute;
    left: 0;
    right: 0;
    bottom: 0;
    height: 50%;
    display: flex;
    align-items: flex-end;
    padding: 16px 24px;
    font-size: 1.5rem;
    font-weight: 500;
    color: white;
    background: linear-gradient(
        to bottom,
        hsla(0, 0%, 0%, 0) 0%,
        hsla(0, 0%, 0%, 0.01) 8.1%,
        hsla(0, 0%, 0%, 0.037) 15.5%,
        hsla(0, 0%, 0%, 0.08) 22.5%,
        hsla(0, 0%, 0%, 0.135) 29%,
        hsla(0, 0%, 0%, 0.2) 35.3%,
        hsla(0, 0%, 0%, 0.271) 41.2%,
        hsla(0, 0%, 0%, 0.347) 47.1%,
        hsla(0, 0%, 0%, 0.423) 52.9%,
        hsla(0, 0%, 0%, 0.499) 58.8%,
        hsla(0, 0%, 0%, 0.57) 64.7%,
        hsla(0, 0%, 0%, 0.635) 71%,
        hsla(0, 0%, 0%, 0.69) 77.5%,
        hsla(0, 0%, 0%, 0.733) 84.5%,
        hsla(0, 0%, 0%, 0.76) 91.9%,
        hsla(0, 0%, 0%, 0.77) 100%
    );
   }
  /* Snappy Time */
  .artists {
    overflow: auto;
    scroll-snap-type: x mandatory;
  }
  
  .artist-card {
    scroll-snap-align: center;
  }
  
  
</style>

<section class="artists">
  <article class="artist-card">
    <img
      class="cover-art"
      alt=""
      src="/cfj-mats/cover-art-water.jpg"
    />
    <div class="about">
      <p>Silk Stream</p>
    </div>
  </article>
  <article class="artist-card">
    <img
      class="cover-art"
      alt=""
      src="/cfj-mats/cover-art-lemons.jpg"
    />
    <div class="about">
      <p>Sour Patch Grift</p>
    </div>
  </article>
  <article class="artist-card">
    <img
      class="cover-art"
      alt=""
      src="/cfj-mats/cover-art-neon.jpg"
    />
    <div class="about">
      <p>はらじゅく CELEBRATION</p>
    </div>
  </article>
  <article class="artist-card">
    <img
      class="cover-art"
      alt=""
      src="/cfj-mats/cover-art-abstract.jpg"
    />
    <div class="about">
      <p>Ethereal Engine</p>
    </div>
  </article>
  <article class="artist-card">
    <img
      class="cover-art"
      alt=""
      src="/cfj-mats/cover-art-dogflowers.jpg"
    />
    <div class="about">
      <p>Sunday Whispers</p>
    </div>
  </article>
  <article class="artist-card">
    <img
      class="cover-art"
      alt=""
      src="/cfj-mats/cover-art-body-art.jpg"
    />
    <div class="about">
      <p>Temple</p>
    </div>
  </article>
</section>
```

### Scrollbar Colors

- Scrollbar styling is somewhat controversial.
- Nothing wrong with theming the scrollbar of our application, help it to blend in.
- You can choose more subtle colors, make it still recognizable but not standing out.
- Scrollbar is made up of 2 components: the thumb and the track.
- Every OS has it's own scrollbar, and used for all apps. They are not browser specific, the are OS specific.

### Changing Colors

- The CSS spec dees provide a nifty CSS property to tweak the scrollbar colors:

```CSS
body {
  scrollbar-color: color1 color2;
}
```

- `scrollbar-color` accepts two color values, the first color is for the thumb, the second for the track.
- But, this is only supported in Firefox at the moment. For all other browsers, you will need to rely on legacy venfor prefixed alternatives.
- Instead of a unique property, you will have to use `background-color` property

```CSS
::-webkit-scrollbar {
  /* Track color */
  background-color: color2;
}
::-webkit-scrollbar-thumb {
  /* Thumb color */
  background-color: color1;
}
```

- Here is a complete demo of both in action

```HTML
<style>
  body {
    padding: 24px;
    background: white;
  }
  p {
    line-height: 1.5;
    margin-bottom: 24px;
  }
  html {
    --color-thumb: red;
    --color-track: white;

    /* Official styles (Firefox) */
    scrollbar-color:
      var(--color-thumb)
      var(--color-track);
    scrollbar-width: thin;
  }

  /* Vendor prefix for other browsers */
  ::-webkit-scrollbar {
    background-color: var(--color-track);
  }
  ::-webkit-scrollbar-thumb {
    background-color: var(--color-thumb);
  }
</style>

<p>
  Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since the 1500s, when an unknown printer took a galley of type and scrambled it to make a type specimen book.
</p>
<p>
  Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since the 1500s, when an unknown printer took a galley of type and scrambled it to make a type specimen book.
</p>
<p>
  Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since the 1500s, when an unknown printer took a galley of type and scrambled it to make a type specimen book.
</p>
<p>
  Lorem Ipsum is simply dummy text of the printing and type
```

- On Firefox, the result looks good, but on other browsers, it looks clucky.
- Turns out, when you specify a custom color, we reset all of the scrollbars native properties. You modify one property, the all disappear.
- But you can use other CSS properties inside of `-webkit-scrollbar` pseudo-elements
- By using `border` and `border-radius` we can create something that looks roughly the same across all browsers.

```HTML
<style>
  body {
    padding: 24px;
    background: var(--background);
    color: var(--text);
  }
  p {
    line-height: 1.5;
    margin-bottom: 24px;
  }
  html {
    --background: hsl(210deg, 15%, 6.25%);
    --text: hsl(210deg, 10%, 90%);
    --gray-300: hsl(210deg, 10%, 40%);
    --gray-500: hsl(210deg, 8%, 50%);

    /* Official styles (Firefox) */
    scrollbar-color:
      var(--gray-300)
      var(--background);
    scrollbar-width: thin;
  }

  ::-webkit-scrollbar {
    width: 10px;
    background-color: var(--background);
  }
  ::-webkit-scrollbar-thumb {
    border-radius: 1000px;
    background-color: var(--gray-300);
    border: 2px solid var(--background);
  }
  /*
    Little bonus: on non-Firefox browsers,
    the thumb will light up on hover!
  */
  ::-webkit-scrollbar-thumb:hover {
    background-color: var(--gray-500);
  }
</style>

<p>
  Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since the 1500s, when an unknown printer took a galley of type and scrambled it to make a type specimen book.
</p>
<p>
  Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since the 1500s, when an unknown printer took a galley of type and scrambled it to make a type specimen book.
</p>
<p>
  Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since the 1500s, when an unknown printer took a galley of type and scrambled it to make a type specimen book.
</p>
<p>
  Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since the 1500s, when an unknown printer took a galley of type and scrambled it to make a type specimen book.
</p>
<p>
  Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since the 1500s, when an unknown printer took a galley of type and scrambled it to make a type specimen book.
</p>
```

- We can't use `padding` to increase the space around the thumb, but we can fake it with a boarder that matches the track color.
- A `:hover` pseudoselector allows us to brighten teh color on mouse-over.

### Mobile scrollbar styles

- In Josh's experiments, can't tweak teh scrollbar styles on iOS.
- In Android, the scrollbar styles work as you would expect.
- Should we mess with mobile scrollbars?
- Our custom styles may do more hard them good on mobile.
- So wrap your scrollbar styles in a media query:

```CSS
@media (min-width: 500px) {
  html {
    scrollbar-color: /* ... */;
  }
  ::-webkit-scrollbar {
    /* ... */
  }
  ::-webkit-scrollbar-thumb {
    /* ... */
  }
}
```

## Scroll Optimization

- Couple more handy optimization we can add to improve scroll experience.

### Scroll margin

- Clicking a anchor link will scroll to that part of the page. So the header matchign the link will be at the top of the page.
- But what if we have a fixed or sticky header? In that case, teh heading is hidden behind the element.
- You can use the `scroll-margin-top` property to solve this.

```CSS
h2 {
  scroll-margin-top: 6rem;
}
```

- We are defining the distance that element should sit from the top of the viewport when it's scrolled into view.
- And has very good browser support.

### Avoiding scroll-based layout shifts

- CLS, Cumalative Layout Shift, metric
- Created by Google, CLS isa  measure of how much movement there is on the page, typically in the first few seconds as the page is loading
- Two reasons to optimize for CLS
  - Layout shift are jarring and chaotic, they can cause you to accidentally click on the wrong thing.
  - Starting in 2021, Gogole has incorporated CLS into it's search ranking algorithm
- CLS metric measures two things
  - how many items move
  - and how significant the shift is. A small icon moving by a few pixels won't be judged as harshly as a big element popping into view and pushing all of the content down.
- Optiming for CLS is a huge topic, but one small thing you can do:

```CSS
body {
  overflow-y: scroll;
}
```

- This property ensures the page will always have a visible scrollbar, even if the page isn't tal enough to warrent one.
- This is a good thing, when the scrollbar pops into view, it causes a layout shift. Even element on the page shifts a few pixels to the left. To make room for the scrollbar.
- This small change can improve your CLS score.
- A better solution on the way, `scrollbar-gutter` property, to make room for the scrollbar without having to mess with overflow

## Other CLS wins

- Other tricks for optimizing for CLS

### Fixed Image Sizes

- Unless you give images a widht and height, the browswer won't know the dimentions unitl the image finished lading. As a result, images will default to being 0px wide and 0px tall, and a big layout shift will occur.
- To prevent this, we need to specify two of the CSS properties:
  - width
  - height
  - aspect-ratio
- `aspect-ratio` means that we can solve this problem even if the image is fliud/scales with the container.

### Grouped loading

- In some cases each section loads independently because they each have their own data sources.
- You can improve that by "grouping" things together. For example, wait until all stories are loaded before showing any of them in the NY Times example;

```JAVASCRIPT
function App() {
  const [mainStory, setMainStory] = React.useState(null);
  const [secondaryStories, setSecondaryStories] =
    React.useState(null);
  const [opinionStories, setOpinionStories] = React.useState(null);
  const areAllStoriesLoaded =
    !!mainStory &&
    !!secondaryStories &&
    !!opinionStories;
  if (!areAllStoriesLoaded) {
    return <Spinner />
  }
  return (
    /* Regular app here */
  );
}
```

- The tradeoff, we reduce the number of layout shifts, but means the user won't get to see any stories until they all loaded. On slow connections this can make a big differ.

## Focus Improvements

- Some user navigate exclusively with non-pointer devices, like keyboard, or a sip and puff switch

### Focus Visible

- AT any given moment, exactly one element on the page wil be focused.
- Always at least two ways to change which element is focused:
  - Hitting the "Tab" key will cycle to the next interactive element
  - Clicking an interactive element will focus it
- For a long time, User-Agent sytle would add visual "focus rings" to any interactive element that has focus

```CSS
button:focus {
  outline: 5px auto -webkit-focus-ring-color;
}
```

- Focus indicators vary between browsers and OS. But generally blue glow or black outline
- These indicators are important, without someone navigating without a pointer device, woudl have no way of knowing which element is selected, or where they are on the page.
- But these visual outlines can be a pet peeve for designers, blue rings clash with the brand aesthetic.
- To help with this, a new pseudo-class was added, `focus-visible`.
- This is very similar to `:focus`, btu it only matches when the element is focused and the user is using a non-pointer input devices (keyboard, paddles, sip and puff)
- The idea was that devs could wipe out the default focus styles, and re-add them to `:focus-visible`, so the wouldn't be shown to folks using a mouse, trackpad or touchscreen.
- A year or two ago, browsers started updating their User-Agent stylesheets. Now, focus indicators are applied to `:focus-visible` instead of `:focus`.

```CSS
/* This is what browsers do nowadays: */
button:focus-visible {
  outline: 5px auto -webkit-focus-ring-color;
}
```

- In other words, those annoying blue rings are already removed for people using a pointer device. We don't need to do anything as developers anymore.
- Focus rings no longer show up when clicking links and buttons.
- They do still show up on text inputs, but that seems like a good thing as you need to know what which element is focused when typing.
- Thanks to modern web, **no need to remove the focus outlines**, this code should not exist in your code base. Unless you are replacing the default focus indicator wtih an even higher contrast one.

```CSS
button {
  outline: none;
}
```

- TIP: you can keep track of the focused element with JS, `document.activeElement`.
- [Chrome devtools](https://developer.chrome.com/docs/devtools/console/live-expressions/) for more info

### Focus Within

- Using child selecotr, it's possibel to style a descendant when an ancestor is focused:

```HTML
<style>
  a {
    color: black;
    text-decoration: none;
    outline-offset: 4px;
  }
  .highlighted {
    display: inline-block;
    padding: 4px;
    margin: 0 -4px;
    border-radius: 4px;
  }
  a:focus .highlighted {
    background: hsl(55deg 100% 75%);
  }
</style>

<a href="/">
  Focus me and <span class="highlighted">see the magic!</span>
</a>
```

- When a parent has a hover/focus/active state, apply some CS to a child
- But what id we want to do the opposite? Apply a style to the parent when a child is focused?
- Put down that JS, we can solve this with CSS now, using the `:focus-within` pseudo class
- And has good [browser support](https://caniuse.com/?search=focus-within)

### In Practice

- The most common use case for `:focus-within` is forms

```HTML
<style>
  body {
    background-color: hsl(210deg, 55%, 92%);
  }

  form {
    background-color: white;
    padding: 32px;
    border-radius: 8px;
  }
  .row {
    margin-bottom: 16px;
  }
  label {
    display: block;
    margin-bottom: 4px;
  }
  input {
    padding: 4px 8px;
    font-size: 1rem;
  }
  button {
    display: block;
    width: 50%;
    padding-top: 4px;
    padding-bottom: 4px;
    margin: 32px auto 0;
    font-size: 1rem;
  }
  form {
    transform: translateY(0px);
    filter: drop-shadow(
      1px 2px 4px hsl(0deg 0% 0% / 0.2)
    );
    transition:
      filter 300ms, transform 300ms;
    will-change: transform;
  }
  /* focus within */
  form:focus-within {
    transform: translateY(-4px);
    filter: drop-shadow(
      2px 4px 16px hsl(0deg 0% 0% / 0.2)
    );
  }
</style>

<form>
  <div class="row">
    <label for="full-name">
      Name:
    </label>
    <input
      id="full-name"
      type="text"
      placeholder="Jane Doe"
    />
  </div>
  <div class="row">
    <label for="email">
      Email Address:
    </label>
    <input
      id="email"
      type="email"
      placeholder="jane@domain.com"
    />
  </div>
  <button>Submit</button>
</form>
```

- In this example, we apply some CSS to the parent <form> tage whenever any of it's descendants are focused. We are increasing the prominence of the shdow, and simulating a page lift with a vertical translate.

### Focus Outlines

- The `outline` property is a bit sneaky
- When we apply outline styles to a non-interactive element, like a `<div>` or a `<p>`, it essentially acts like a borer. It takea  on a solid color wiht hard edges.

```HTML
<style>
  .with-outline {
    outline: 2px solid blue;
  }
</style>

<div class="with-outline">
  This div has an outline.
</div>
```

- non-interactive outlines will look the same across all browsers and devices, just like a border.
- But, when we focus an interactive element, we are treated toa  browser specific "focus outline". This outline is different and changes depending on the browser and device

#### Customizing focus outlines

- What happens if we cahnge the `outline-color` property of a focus outline?

```HTML
<style>
  a {
    outline-color: red;
  }
</style>

<a href="/">Typical link</a>
```

- If you are suing Chrome, you should see a "focus outline", but with a red color instead of blue.
- On Firefox and Safari, this property has no effect.
- The `outline-color` property has broad support, but only with typical outlines, not focus outlines.
- Is there a way to "force" focus outlines to behave liek typical outlines, sot hat we can apply a custom color? We can but prob shouldn't.

```HTML
<style>
  a:focus {
    outline: 2px solid red;
  }
</style>

<a href="/">Typical link</a>
```

- Here is why this is usually a bad idea, focus outlines are tried and true convention, oen that users have come to expect. The default styling is instantly recognizable as a focus indicator. The non-focus outlines look more like borders adn people don't associate borders with focus.
- For browswer that suppor ti, changing the `outline-color` along is a happy compromise. We can tailer the focus indicator to our app's theme without fundamentally changing it.

## Floats

- The float property allows us to wrap text around images and other media.
- Before we had Flexbox, floats were critical tool for layouts. We don't need floats for layouts, but they still have a use.
- Even the CSSWG certainly hasn't fogotten about floats. And continue to build on the API.
- How do floats fit into modern CSS?
- Quick reminder, here is how floats wrap text around an image

```HTML
<style>
  p {
    margin-bottom: 1em;
  }
  img {
    width: 150px;
  }
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
<img src="/cfj-mats/cat-300px.jpg" />
<p>
  It has survived not only five centuries, but also the leap into electronic typesetting, remaining essentially unchanged. It was popularised in the 1960s with the release of Letraset sheets containing Lorem Ipsum passages, and more recently with desktop publishing software like Aldus PageMaker including versions of Lorem Ipsum.
</p>
<p>
  Contrary to popular belief, Lorem Ipsum is not simply random text. It has roots in a piece of classical Latin literature from 45 BC, making it over 2000 years old.
</p>
```

- We can position a floated element on either side, `float: left` or `float: right`.
- In the future we can use logical values `inline-start` and `inline-end`

### Shapes

- Historically, a floated element would "block out" a rectangle. Text would wrap around that rectangle.
- Recently, floats have gained an additional superpower, they can not specify a shape for text to wrap around.

```HTML
<style>
  .floated {
    float: left;
    shape-outside: circle();
    margin-right: 24px;
  
    /* Cosmetic tweaks: */
    width: 125px;
    border-radius: 50%;
  }
</style>

<div>
  <p>
    <img class="floated" src="/cfj-mats/cat-avatar-250px.jpg" alt="Yawning kitten" />
    Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since the 1500s, when an unknown printer took a galley of type and scrambled it to make a type specimen book.
  </p>
</div>
```

- With another seldom used value, `text-align: justify` we can create magazine style layouts.

```HTML
<style>
  .floated {
    float: right;
    shape-outside: circle();
    margin-left: 24px;
    width: 125px;
    border-radius: 50%;
  }
  
  p {
    text-align: justify;
    hyphens: auto;
  }
</style>

<div>
  <p>
    <img class="floated" src="/cfj-mats/cat-avatar-250px.jpg" alt="Yawning kitten" />
    Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since the 1500s, when an unknown printer took a galley of type and scrambled it to make a type specimen book.
  </p>
</div>
```

- `shape-outside` lets us specify a shapre that text should wrap around. `circle` si the most straightforward valule. But it accepts many differ shapes.
  - `clip-path` polygons
  - SVG-style paths, to define a complex straight and curved shapes
  - Auto-detection, by passing a URL to an image with transparency

- This is pretty magical.

```HTML
<style>
  .floated {
    --breathing-room: 16px;
    float: left;
    shape-outside:
      url(/cfj-mats/me-light.png);
    margin-right: var(--breathing-room);
    shape-margin: var(--breathing-room);
    width: 125px;
  }

  /* Cosmetic styles */
  .wrapper {
    max-width: 600px;
    padding: 32px;
    margin: 0 auto;
    background: white;
    border-radius: 8px;
  }
  body {
    padding: 16px;
  }
  p {
    text-align: justify;
    hyphens: auto;
  }
</style>
<div class="wrapper">
  <p>
    <img class="floated" src="/cfj-mats/me-light.png" alt="3D avatar" />
    Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since the 1500s, when an unknown printer took a galley of type and scrambled it to make a type specimen book. It was popularised in the 1960s with the release of Letraset sheets containing Lorem Ipsum passages, and more recently with desktop publishing software like Aldus PageMaker including versions of Lorem Ipsum.
  </p>
</div>
```

- In order to make this work, we add `shape-margin` a special property that add a gap between the opaque pixels in an images shape adn the surrounding content.
- We also ned to add `margin-right` since the `shape-margin` can't push teh content beyond the image's content size.
- `shape-outside` is a hidden gem. Most developers assuem floats are not relevant anymore, and miss out.
- Supported in all major browsers.

### Clearfixing

- Floats are notorious for breaking layouts.
- When you float an image, we take it out of flow. The parent wrapper is trying to determine how tall it should be. It ignores the floated elements, just like it would absolute position elements.
- We need to use the CS property `clear` to fix this.

```HTML
<style>
  .floated {
    --breathing-room: 16px;
    float: left;
    shape-outside:
      url(/cfj-mats/me-light.png);
    margin-right: var(--breathing-room);
    shape-margin: var(--breathing-room);
    width: 125px;
  }

  /* Cosmetic styles */
  .wrapper {
    max-width: 600px;
    padding: 32px;
    margin: 0 auto;
    background: white;
    border-radius: 8px;
  }
  body {
    padding: 16px;
  }
  /* clear */
  .clear {
    clear: left;
  }
</style>

<div class="wrapper">
    <img class="floated" src="/cfj-mats/me-light.png" alt="3D avatar" />
  <p>
    Lorem Ipsum is simply dummy text.
  </p>
  <p class="clear">
    This paragraph appears below the image.
  </p>
</div>
```

- This is called clearfix, typically used like this:

```HTML
<style>
  .floated {
    --breathing-room: 16px;
    float: left;
    shape-outside:
      url(/cfj-mats/me-light.png);
    margin-right: var(--breathing-room);
    shape-margin: var(--breathing-room);
    width: 125px;
  }

  /* Cosmetic styles */
  .wrapper {
    max-width: 600px;
    padding: 32px;
    margin: 0 auto;
    background: white;
    border-radius: 8px;
  }
  body {
    padding: 16px;
  }
  /* clearfix */
  .clearfix::after {
    content: '';
    display: block;
    clear: both;
  }
</style>

<div class="wrapper clearfix">
  <img class="floated" src="/cfj-mats/me-light.png" alt="3D avatar" />
  <p>
    Lorem Ipsum is simply dummy text.
  </p>
</div>
```

- Our parent wrapper element now renders pseudoelent that applies `clear: both` and clears both left and right after the content.
- It doesn't actually matter that this element is empty; the fact that it exists causes the parent to grow to include the entire floated element, and the 0px-tall element below.

## Conclusion

- March 20, 2022, completed this course. Over 200+ lessons and many many hours.
- Still more stuff to check out in the [video archive](https://courses.joshwcomeau.com/css-for-js/video-archive) and [treasure trove](https://courses.joshwcomeau.com/css-for-js/treasure-trove).

## Bonus Material

- Intro to Figma
- Figma is a design tool, and accessible enough for developers to use it.
- Limited set of things to do when not have create account. But you can sign up for free
- [Intro to React](https://courses.joshwcomeau.com/css-for-js/bonus/02-intro-to-react)
- Other resoruces
  - Ali Spittel's, [The beginners Guide to React 2020](https://welearncode.com/beginners-guide-react-2020/)
  - FreeCodeCamp, [React Beginner's Handbook](https://www.freecodecamp.org/news/react-beginner-handbook/)
  - [Official Docs](https://reactjs.org/docs/getting-started.html)
