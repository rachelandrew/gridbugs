# Gridbugs

Inspired by [Flexbugs](https://github.com/philipwalton/flexbugs) this list aims to be a community curated list of CSS Grid Layout bugs, incomplete implementations and interop issues. [Grid shipped into browsers](https://gridbyexample.com/browsers) in a highly interoperable state, however there are a few issues - let's document any we find here.

While I'd like to focus on issues relating to the [Grid Specification](https://drafts.csswg.org/css-grid/) here, it is likely that related specs such as Box Alignment will need to be referenced. If you think you have spotted an issue and it seems to relate to Grid, post it. We can work out the details together and make sure browser or spec issues get logged in the right place.


## The bugs

1. [`grid-auto-rows` and `grid-auto-columns` should accept a track listing](#1-grid-auto-rows-and-grid-auto-columns-should-accept-a-track-listing)
2. [Repeat notation should accept a track listing](#2-repeat-notation-should-accept-a-track-listing)
3. [Fragmentation support](#3-fragmentation-support)
4. [Sizing of items with an intrinsic size inside fixed size grid tracks](#4-sizing-of-items-with-an-intrinsic-size-inside-fixed-size-tracks)
5. [Items with an intrinsic aspect ratio should align start](#5-items-with-an-intrinsic-aspect-ratio-should-align-start)
6. [The `grid-gap` property should accept percentage values](#6-the-grid-gap-property-should-accept-percentage-values)
7. [Grid gaps should behave as auto-sized tracks?](#7-grid-gaps-should-behave-as-auto-sized-tracks)


### 1. `grid-auto-rows` and `grid-auto-columns` should accept a track listing

<table>
  <tr>
    <th align="left">Demos</th>
    <th align="left">Browsers affected</th>
    <th align="left">Tracking bugs</th>
  </tr>
  <tr valign="top">
    <td>
      <a href="https://codepen.io/rachelandrew/pen/Bdoome">1.1</a> &mdash; <em>bug</em>
    </td>
    <td>
     Firefox
    </td>
    <td>
      <a href="https://bugzilla.mozilla.org/show_bug.cgi?id=1339672">Firefox #1339672</a>
    </td>
  </tr>
</table>

The properties `grid-auto-rows` and `grid-auto-columns` enable an author to set the size of tracks created in the implicit grid. The spec says:

> "If multiple track sizes are given, the pattern is repeated as necessary to find the size of the implicit tracks. The first implicit grid track before the explicit grid receives the first specified size, and so on forwards; and the last implicit grid track before the explicit grid receives the last specified size, and so on backwards." - [7.6 Implicit Track Sizing](https://www.w3.org/TR/css-grid-1/#auto-tracks)

### 2. Repeat notation should accept a track listing

<table>
  <tr>
    <th align="left">Demos</th>
    <th align="left">Browsers affected</th>
    <th align="left">Tracking bugs</th>
  </tr>
  <tr valign="top">
    <td>
      <a href="https://codepen.io/rachelandrew/pen/prjjLy">2.1</a> &mdash; <em>bug</em>
    </td>
    <td>
     Firefox
    </td>
    <td>
      <a href="https://bugzilla.mozilla.org/show_bug.cgi?id=1341507">Firefox #1341507</a>
    </td>
  </tr>
</table>

Repeat notation can accept a single track sizing to repeat, eg:

`repeat(3,200px);`

Or a track listing:

`repeat(3, 200px 100px);`

This includes when the number of repeats is `auto-fill` or `auto-fit` to create as many tracks as will fit. 

> "The first argument specifies the number of repetitions. The second argument is a track list, which is repeated that number of times." - [Syntac of `repeat()`](https://www.w3.org/TR/css-grid-1/#auto-repeat)

### 3. Fragmentation Support

<table>
  <tr>
    <th align="left">Demos</th>
    <th align="left">Browsers affected</th>
    <th align="left">Tracking bugs</th>
  </tr>
  <tr valign="top">
    <td></td>
    <td>
     Firefox
     <br>Chrome
     <br>Safari
    </td>
    <td>
      <a href="https://bugzilla.mozilla.org/show_bug.cgi?id=1266265">Firefox #1266265</a><br>
      <a href="https://bugs.chromium.org/p/chromium/issues/detail?id=614667">Chrome #614667</a></td>
  </tr>
</table>

There is limited fragmentation support across browsers at present, therefore features such as the `break-*` properties are unlikely to work reliably. For details of how fragmentation should work in Grid Layout see [12. Fragmenting Grid Layout](https://www.w3.org/TR/css-grid-1/#pagination). 

### 4. Sizing of items with an intrinsic size inside fixed size tracks

<table>
  <tr>
    <th align="left">Demos</th>
    <th align="left">Browsers affected</th>
    <th align="left">Tracking bugs</th>
  </tr>
  <tr valign="top">
    <td>
      <a href="https://codepen.io/rachelandrew/pen/eEpeXW/">4.1</a> &mdash; <em>bug</em>
    </td>
    <td>
     Firefox
    </td>
    <td>
      <a href="https://bugzilla.mozilla.org/show_bug.cgi?id=1385410">Firefox #1385410</a>
    </td>
  </tr>
</table>

### 5. Items with an intrinsic aspect ratio should align start

<table>
  <tr>
    <th align="left">Demos</th>
    <th align="left">Browsers affected</th>
    <th align="left">Tracking bugs</th>
  </tr>
  <tr valign="top">
    <td>
      <a href="https://codepen.io/rachelandrew/pen/LjprNE">5.1</a> &mdash; <em>bug</em><br>
      <a href="https://codepen.io/rachelandrew/pen/prjQRz">5.2</a> &mdash; <em>workaround</em>
    </td>
    <td>
     Safari 10 (fixed in Technical Preview)
    </td>
    <td></td>
  </tr>
</table>

In Safari 10, a grid item that has an intrinsic aspect ratio was defaulting to `stretch`, rather than `start`.

The workaround for this is to declare `align-self: start` and `justify-self: start` on the item.

### 6. The `grid-gap` property should accept percentage values

<table>
  <tr>
    <th align="left">Demos</th>
    <th align="left">Browsers affected</th>
    <th align="left">Tracking bugs</th>
  </tr>
  <tr valign="top">
    <td>
      <a href="https://codepen.io/rachelandrew/pen/QMjPXq">6.1</a> &mdash; <em>bug</em>
    </td>
    <td>
     Safari 10 (fixed in Technical Preview)
       </td>
    <td></td>
  </tr>
</table>


Currently percentage values of `grid-gap` are marked as **at-risk** in the Level 1 specification. A strong use case for percentage values is that of adding some grid layout features to a layout which already uses a float, or flexbox-based grid system [see tweet from @minamarkham](https://twitter.com/minamarkham/status/891029296604618752). These systems have to use percentages for spacing in order to create a 'grid'.

### 7. Grid gaps should behave as auto-sized tracks?

There is also an interop issue with regard to percentage `grid-row-gap` values, where the height of the grid is not a fixed size. Chrome and Safari TP, plus Edge Preview collapse the row gap to 0. Firefox is using a percentage of the total height, I think. 

- [Example 7.1](https://codepen.io/rachelandrew/pen/xLZbMm)
- [CSS WG discussion](https://github.com/w3c/csswg-drafts/issues/509#issuecomment-318812608)

## Acknowledgments

Gridbugs is maintained by @rachelandrew and was heavily inspired by the excellent [Flexbugs](https://github.com/philipwalton/flexbugs). 

## Contributing

In the first instance raise an Issue, include a Reduced Test Case that demonstrates the problem clearly. If you are aware of a workaround for the problem, add that too.
