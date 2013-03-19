# Simple Responsive Grid System

Simple Responsive Grid System is based off of Chris Coyier's [Don't Overthink It Grids](http://css-tricks.com/dont-overthink-it-grids/). It is using Scss to create percentage based columns which can easily be modified by changing the variables. The variables let you set a max-width, # of columns, and the width of the gutters.

Each column gets a padding-right of the set padding which by default is 30px. The parent container `.container-grid` gets a padding-left of the set padding. I have included 12 and 16 column grids by default, so the layout can take advantage of three and four column layouts. [View the example page](http://ferne97.github.com/simple-responsive-grid-system/).

### Some Example Code

```html
<div class="container-grid">
    <div class="grid-row">

        <div class="col-2-3">
            <!-- main content -->
        </div>

        <div class="col-1-3">
            <!-- sidebar content -->
        </div>

    </div>
</div>
```

```scss
// Variables
$grid-column-12: 12;
$grid-gutter:    30px;
$max-width:      1340px;


// Loop
@for $n from 1 through $grid-column-12 {
    .col-#{$n}-#{$grid-column-12} {
        @extend .col;
        width: percentage($n / $grid-column-12);
    }
}
```

## Class Names

The class names for the columns consist of the amount or rows to span and the total amount of columns `.col-4-12`. `.col-100` is used for a full-width column. There are also 'simple fraction' helper classes like `.col-1-2` and `.col-1-3` which feel a little cleaner and can make more sense once you start nesting columns. Since the content is floated, each column should be wrapped in a `.grid-row` div, or an element of your choice, as long as it contains the floats.

## Nesting

If you need to nest columns, add a class of `grid-nested` alongside the parent `col-x-x` class. `grid-nested` simply adds `padding-right: 0` so the padding won't be doubled once a child column is added.

```html
<div class="grid-row">
    <div class="col-8-12 grid-nested">

        <div class="grid-row">
            <div class="col-1-2"></div>
            <div class="col-1-2"></div>
        </div>

        <div class="grid-row">
            <div class="col-1-3"></div>
            <div class="col-1-3"></div>
            <div class="col-1-3"></div>
        </div>

    </div><!-- end grid-nested -->

    <div class="col-4-12 grid-nested">

        <div class="grid-row">
            <div class="col-1-2"></div>
            <div class="col-1-2"></div>
        </div>

    </div><!-- end grid-nested -->
</div><!-- end grid-row -->
```

## Includes

You can use your own layout and class names.

```html
<div class="container">
    <div class="group">

        <div class="content-main">
            <!-- main content -->
        </div>

        <div class="sidebar">
            <!-- sidebar content -->
        </div>

    </div>
</div>
```

Then in your scss use an `@include col(x, x)` to have it generate the width of your columns.

```scss
.container {
    margin: 0 auto;
    padding-left: $grid-gutter;
    max-width: $max-width;
}

.group {
    @extend .clearfix();
}

.content-main {
    @include col(8, 12);
}

.sidebar {
    @include col(4, 12);
}
```

The mixin for a column uses two paramaters. `$n` for how many columns to span and `$cols` for the total amount of columns in the grid (i.e. 12 or 16).

```scss
@mixin col($n, $cols: $grid-column-16) {
    @include col-base();
    width: percentage($n / $cols);
}
```

The `col` mixin also includes the `col-base` mixin which adds the rest of the necessary styles.

```scss
@mixin col-base {
    position: relative;
    display: block;
    float: left;
    padding-right: $grid-gutter;
}
```

So this..

```scss
.content-main {
    @include col(8, 12);
}
```

Will output to this..

```css
.content-main {
    position: relative;
    display: block;
    float: left;
    padding-right: 30px;
    width: 66.66667%;
}
```
