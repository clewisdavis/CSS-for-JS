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
