StatSheet Frameless CSS framework v1.0
======================================

The StatSheet Frameless CSS framework is based on the [frameless grid](https://github.com/jonikorpi/Frameless/blob/master/frameless.scss). We have a responsive and non-responsive version of the grid.

This particular framework utilizes a 12 column grid for the desktop version and portrait tablet, a 4 column grid for a landscape mobile device and a 2 column grid for a portrait mobile device.

When shrinking from a larger grid to a smaller grid, any column greater than the max grid level for that layout be shrunk to the size of the max grid size...

Sample code:

  <div class="wrapper">
    <div class="col col1">1</div>
    <div class="col col1">1</div>
    <div class="col col1">1</div>
    <div class="col col1">1</div>
    <div class="col col4">4</div>
    <div class="col col2">2</div>
    <div class="col col2">2</div>
  </div>
  
This is how the sample code snippet above would translate as a responsive template:

  DESKTOP VERSION:
  
  *----*----*----*----*----------------*--------*--------*
  |    |    |    |    |                |        |        |
  | 1  | 1  | 1  | 1  |        4       |    2   |    2   |
  |    |    |    |    |                |        |        |
  *----*----*----*----*----------------*--------*--------*
  
  
  TABLET VERSION:
  
  *---*---*---*---*------------*------*------*
  |   |   |   |   |            |      |      |
  | 1 | 1 | 1 | 1 |     4      |  2   |   2  |
  |   |   |   |   |            |      |      |
  *---*---*---*---*------------*------*------*
  
  
  LANDSCAPE MOBILE:
  
  *---*---*---*---*
  |   |   |   |   |
  | 1 | 1 | 1 | 1 |
  |   |   |   |   |
  *---*---*---*---*
  |               |
  |       4       |
  |               |
  *-------*-------*
  |       |       |
  |   2   |   2   |
  |       |       |
  *-------*-------*
  
  
  PORTRAIT MOBILE:
  
  *---*---*
  |   |   |
  | 1 | 1 |
  |   |   |
  *---*---*
  |   |   |
  | 1 | 1 |
  |   |   |
  *---*---*
  |       |
  |   4   |
  |       |
  *-------*
  |       |
  |   2   |
  |       |
  *-------*
  |       |
  |   2   |
  |       |
  *-------*


The css files included are:

* frameless.scss `Responsive Sass`
* frameless.css `Responsive Grid` <- you will never need to edit this file
* frameless_default.css
* print.css
* reset.css
* style.css
* style_r.css `Responsive styles`


The Basics
-----
Every grid must be inside a container with the class `wrapper`. This wrapper will center the grid and make it the appropriate width:

Every column should have two classes... `col` and `col#` where # is replaced with a number between 1 and 12

`col#` determines the width of the column.

Every column has a 10 pixel margin on the left and the right.  These margins can cause layout probelms if you have nested columns like this:

  <div class="wrapper">
    <div class="col col12">
      <div class="col col6"> </div>
      <div class="col col3"> </div>
      <div class="col col3"> </div>
    </div>
  </div>

This presents a tiny issue... every nested column will add more padding to the container column.  We can account for this by getting rid of the left or right padding of a column by adding the class `alpha` or `omega` respectively. These naming conventions were adopted from the widely popular [960 Grid System](http://www.960.gs).

So the correct way to do nesting would be as follows:

  <div class="wrapper">
    <div class="col col12">
      <div class="col col6 alpha"> </div>
      <div class="col col3"> </div>
      <div class="col col3 omega"> </div>
    </div>
  </div>

That way, we get rid of the excess margins on the first and last elements of the nested columns

Conditional Responsiveness
----
The following styles will allow you to hide/show certain elements in specific layouts. These styles will only work on the responsive version of the grid.

* `show-default` -- Will only display element in the desktop version
* `show-tablet` -- Will only display element on a portrait tablet
* `show-mobile-wide` -- Will only display element on a landscape mobile device
* `show-mobile` -- Will only display element on a mobile device (Landscape or Portrait)

* `hide-default` -- Will hide element in the desktop version only
* `hide-tablet` -- Will hide element on a portrait tablet only
* `hide-mobile-wide` -- Will hide element on a landscape mobile device only
* `hide-mobile` -- Will hide element on a mobile device only (Landscape or Portrait)

These styles can come in handy:

  <div class="wrapper">
    <div class="col col12">

      <div id="banner-ad" class="hide-mobile">
        // AD CODE
      </div>

      <ul class="nav">
        <li><a href="#">Home</li>
        <li><a href="#">About</li>
        <li><a href="#">Contact</li>
      </ul>

    </div>
  </div>

The code above would show the banner ad on a desktop and tablet only and hide it on a mobile device.

Media Queries
-----
CSS3 media queries are useful for setting specific styling for elements on specific devices.  If the conditional classes discussed in the previous section aren't enough, you can add more specific styling in the `style_r.css` file under the appropriate media query:

  /* Mobile Layout */
  @media only screen and (max-width: 767px) {
    #logo {
      width:300px;
      height:40px;
      background-image:url('logo_small.png');
    }
  }

The snippet above would replace the background image for the `#logo` div on a mobile device.
