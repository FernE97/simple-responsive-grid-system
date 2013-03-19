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

The main idea behind this is that the parent container `.container-grid` get's a padding-left of the set padding, which by default is 30px. Then Each column get's a padding-right of the set padding. By setting the padding-left on the parent container, you don't have to worry about zeroing out the last column's margin or padding.

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
