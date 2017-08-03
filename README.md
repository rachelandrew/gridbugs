# GridBugs

Inspired by [Flexbugs](https://github.com/philipwalton/flexbugs) this list aims to be a community curated list of CSS Grid Layout bugs, incomplete implementations and interop issues. [Grid shipped into browsers](https://gridbyexample.com/browsers) in a highly interoperable state, however there are a few issues - let's document any we find here.

While I'd like to focus on issues relating to the [Grid Specification](https://drafts.csswg.org/css-grid/) here, it is likely that related specs such as Box Alignment will need to be referenced. If you think you have spotted an issue and it seems to relate to Grid, [post it](https://github.com/rachelandrew/gridbugs/issues). We can work out the details together and make sure browser or spec issues get logged in the right place.

_Also, please raise an issue if I am wrong about any of these_ or you have more info or examples to add. Quite possibly I've pointed the finger at the wrong UA or missed a change in the spec. Help to make the list accurate appreciated!

## This is not CSS Grid technical support

Please raise issues about interop issues where you have already been through the process of creating a **Reduced Test Case** to check that the issue isn't something in your code. If you want to learn about CSS Grid Layout then check out [Grid by Example](https://gridbyexample.com) where I have video tutorials, small examples and links to other resources. I will answer more general grid questions on my [AMA](https://github.com/rachelandrew/cssgrid-ama) when time allows. I also have information regarding [fallbacks for older browsers](https://rachelandrew.co.uk/archives/2017/07/04/is-it-really-safe-to-start-using-css-grid-layout/).


## The bugs

1. [`grid-auto-rows` and `grid-auto-columns` should accept a track listing](#1-grid-auto-rows-and-grid-auto-columns-should-accept-a-track-listing)
2. [Repeat notation should accept a track listing](#2-repeat-notation-should-accept-a-track-listing)
3. [Fragmentation support](#3-fragmentation-support)
4. [Sizing of items with an intrinsic size inside fixed size grid tracks](#4-sizing-of-items-with-an-intrinsic-size-inside-fixed-size-tracks)
5. [Items with an intrinsic aspect ratio should align start](#5-items-with-an-intrinsic-aspect-ratio-should-align-start)
6. [The `grid-gap` property should accept percentage values](#6-the-grid-gap-property-should-accept-percentage-values)
7. [Grid gaps should behave as auto-sized tracks?](#7-grid-gaps-should-behave-as-auto-sized-tracks)
8. [Setting max-height to a percentage should scale down a larger image inside a grid track](#8-setting-max-height-to-a-percentage-should-scale-down-a-larger-image-inside-a-grid-track)
9. [`min-content` and `max-content` in track listings](#9-min-content-and-max-content-in-track-listings)
10. [Some HTML elements can't be grid containers](#10-some-html-elements-cant-be-grid-containers)
11. [A textarea that is a grid item collapses to zero width](#11-a-textarea-that-is-a-grid-item-collapses-to-zero-width)
12. [Space distributed to empty tracks spanned by an item with content](#12-space-distributed-to-empty-tracks-spanned-by-an-item-with-content)


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

In Firefox images with an intrinsic size are scaling down to fit into a fixed size grid track, rather than overflowing.

I believe that the correct behavior is to overflow, as per the CSS WG resolution of [Issue 523](https://github.com/w3c/csswg-drafts/issues/523#issuecomment-300539109).

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

#### Workaround

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
     Safari 10 (fixed in <a href="https://developer.apple.com/safari/technology-preview/release-notes/#r29">Technical Preview 29</a>)
       </td>
    <td>
      <a href="https://bugs.webkit.org/show_bug.cgi?id=170764">WebKit #170764</a>
    </td>
  </tr>
</table>


Currently percentage values of `grid-gap` are marked as **at-risk** in the Level 1 specification. A strong use case for percentage values is that of adding some grid layout features to a layout which already uses a float, or flexbox-based grid system [see tweet from @minamarkham](https://twitter.com/minamarkham/status/891029296604618752). These systems have to use percentages for spacing in order to create a 'grid'.

### 7. Grid gaps should behave as auto-sized tracks?

There is also an interop issue with regard to percentage `grid-row-gap` values, where the height of the grid is not a fixed size. Chrome and Safari TP, plus Edge Preview collapse the row gap to 0. Firefox is using a percentage of the total height, I think. 

- [Example 7.1](https://codepen.io/rachelandrew/pen/xLZbMm)
- [CSS WG discussion](https://github.com/w3c/csswg-drafts/issues/509#issuecomment-318812608)

### 8. Setting max-height to a percentage should scale down a larger image inside a grid track

<table>
  <tr>
    <th align="left">Demos</th>
    <th align="left">Browsers affected</th>
    <th align="left">Tracking bugs</th>
  </tr>
  <tr valign="top">
    <td>
      <a href="https://codepen.io/rachelandrew/pen/YxqVNz">8.1</a> &mdash; <em>bug</em>
    </td>
    <td>
    Chrome
       </td>
    <td>
      <a href="https://bugs.chromium.org/p/chromium/issues/detail?id=750631">Chromium #750631</a>
    </td>
  </tr>
</table>

Using `max-height` on an image inside a fixed size track should resolve so that the image scales down to fit inside the track. Currently in Chrome this does not work and so the image overflows. Using `max-width` works when the image is constrained by the column track sizing, setting a fixed height works as expected as does setting a max-height using a length unit such as `px`.

### 9. `min-content` and `max-content` in track listings

<table>
  <tr>
    <th align="left">Demos</th>
    <th align="left">Browsers affected</th>
    <th align="left">Tracking bugs</th>
  </tr>
  <tr valign="top">
    <td>
      <a href="https://codepen.io/rachelandrew/pen/eEzbpN">9.1</a> &mdash; <em>bug</em>
    </td>
    <td>
     Safari 10 (fixed in Technology Preview)
    </td>
    <td><a href="https://bugs.webkit.org/show_bug.cgi?id=169195">WebKit #169195</a></td>
  </tr>
</table>

In Safari 10, the values `min-content`, `max-content` and `fit-content` were prefixed. These have now been unprefixed in Safari Technology Preview.

#### Workaround

The workaround for this is to use the prefixed `-webkit-min-content`, `-webkit-max-content` and `-webkit-fit-content`.

### 10. Some HTML elements can't be grid containers

<table>
  <tr>
    <th align="left">Demos</th>
    <th align="left">Browsers affected</th>
    <th align="left">Tracking bugs</th>
  </tr>
  <tr valign="top">
    <td>
      <a href="https://codepen.io/rachelandrew/pen/dzXwRJ">10.1</a> &mdash; <em>bug (fieldset)</em><br>
      <a href="https://codepen.io/rachelandrew/pen/dzXwRJ">10.2</a> &mdash; <em>bug (button)</em>
    </td>
    <td>
    Chrome<br>
     Safari 10 (fieldset fixed in Technology Preview)
    </td>
    <td><a href="https://bugs.chromium.org/p/chromium/issues/detail?id=375693">Chromium #375693</a></td>
  </tr>
</table>

In Chrome (and Safari 10) fieldset elements with `display: grid` do not act as grid containers. The button element only functions as a grid container in Firefox. This is related to the same issue in Flexbox, [detailed on the Flexbugs site](https://github.com/philipwalton/flexbugs#9-some-html-elements-cant-be-flex-containers).

### 11. A textarea that is a grid item collapses to zero width

<table>
  <tr>
    <th align="left">Demos</th>
    <th align="left">Browsers affected</th>
    <th align="left">Tracking bugs</th>
  </tr>
  <tr valign="top">
    <td>
      <a href="https://yuheiy.github.io/pub/textarea-in-grid.html">11.1</a> &mdash; <em>bug</em>
    </td>
    <td>
    Chrome (on OSX only)
    </td>
    <td><a href=" https://bugs.chromium.org/p/chromium/issues/detail?id=727076">Chromium #727076</a></td>
  </tr>
</table>

On OS X Chrome, if a textarea is a grid item it collapses to 0 width when text is typed into it. _Linked to test case from the Chromium issue as due to the way CodePen loads into an iframe this doesn't seem to happen there._

### 12. Space distributed to empty tracks spanned by an item with content

<table>
  <tr>
    <th align="left">Demos</th>
    <th align="left">Browsers affected</th>
    <th align="left">Tracking bugs</th>
  </tr>
  <tr valign="top">
    <td>
      <a href="https://codepen.io/rachelandrew/pen/vJXJQr">12.1</a> &mdash; <em>bug 1</em><br>
      <a href="https://codepen.io/rachelandrew/pen/aymLmq">12.2</a> &mdash; <em>bug 2</em>
    </td>
    <td>
    Firefox
    </td>
    <td><a href="https://bugzilla.mozilla.org/show_bug.cgi?id=1386921">Firefox #1386921</a><br>
    <a href="https://bugzilla.mozilla.org/show_bug.cgi?id=1386932">Firefox #1386932</a></td>
  </tr>
</table>

If you have a grid with empty tracks which are spanned by an item on the grid, those tracks should not be assigned extra space due to the spanning item. Firefox is assigning extra space (bug 1), related is the fact that Firefox does different things depending on source order (bug 2).

Thanks to everyone who helped to isolate these issues [here](https://github.com/rachelandrew/gridbugs/issues/2). The discussion is useful if you want to understand exactly what is going on.

## Acknowledgments

Gridbugs is maintained by [@rachelandrew](https://twitter.com/rachelandrew) and was heavily inspired by the excellent [Flexbugs](https://github.com/philipwalton/flexbugs). 

## Contributing

In the first instance [raise an Issue](https://github.com/rachelandrew/gridbugs/issues), include a Reduced Test Case that demonstrates the problem clearly. If you are aware of a workaround for the problem, add that too.
