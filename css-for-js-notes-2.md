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

-
