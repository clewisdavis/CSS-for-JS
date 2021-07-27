# CSS for JS Notes

## Absolute Positioning

- Trick for centering an element using absolute

```css
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
