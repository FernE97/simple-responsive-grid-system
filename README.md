# Simple Responsive Grid System

A responsive grid system based off of Chris Coyier's [Don't Overthink It Grids](http://css-tricks.com/dont-overthink-it-grids/).

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

Each column gets a padding-right of the set padding which by default is 30px. The parent container `.container-grid` gets a padding-left of the set padding. I have include a 12 & 16 column grid layout by default, so the layout can take advantage of a 3 or 4 column layout.

## Class Names

The class names for the columns consist on the amount or rows to span and the total amount of columns `.col-4-12`. There are also 'simple fraction' helper classes like `.col-1-2` which can make more sense once you start nesting columns. Since the content is floated, each column should be wrapped in a `.grid-row` div, or an element of your choice, as long as it contains the floats.

## Nesting

If you need to nest columns, add a class of `grid-nested` alongside the parent `col-x-x` class.

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

    </div>

    <div class="col-4-12 grid-nested">

        <div class="grid-row">
            <div class="col-1-2"></div>
            <div class="col-1-2"></div>
        </div>

    </div>
</div>
```

## Includes

If you prefer to keep your markup free of grid classes, you can use an `@include col()` on your own class. For Example..

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

**scss**

```scss
.container {
    max-width: 1020px;
    margin: 0 auto;
    padding-left: $grid-gutter;
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
