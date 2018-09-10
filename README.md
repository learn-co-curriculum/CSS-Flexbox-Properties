# Building a Responsive Layout with CSS Flexbox

## Problem Statement

Using CSS to create a website that looks good to as many users as possible can
be a challenge. Your webpage may look great on the screen you designed it on,
but open the page up on a small laptop, and suddenly the page content is
squeezed, spilling over, or pushed out of place. Open that same page on a larger
monitor and you might have a ton of empty space.

CSS, however, has some powerful solutions for this, and in this lesson, we will
be discussing one of them: flexbox.

Flexbox makes it possible to build page layouts that are dynamic. As the
designer of a web page, you can designate some parts of your page to
automatically resize depending on window size, filling empty space in a way that
you specify. It is also very useful for displaying columns or rows of items,
keeping items evenly spaced regardless of their individual sizes, or allowing
them to _wrap_ to a new line cleanly.

In this lesson, we will discuss some of the common ways to use flexbox and the
associated properties you can use while coding through some examples. Feel free
to code along using the provided `index.html` and `index.css` files. You can
test out your page by either running `httpserver` if you are using the
in-browser Learn IDE, or by right clicking the `index.html` in Finder and
opening it in a browser.

## Objectives

1.  Setting up a Flex Container

## Setting Up a Flex Container

In order to use flexbox properties, we must first define a container where we
want flexbox to apply. In `index.html`, we've got a small amount of HTML in the
`<body>`: a `<div>` with a class `flex-container` that has three child elements,
`<header>`, `<main>` and `<footer>`, which will act as our first flex container.
In `index.css`, we've got some starter code, too: `background-color`, `width`
and `height` are pre-defined for the `header`, `main`, and `footer` elements.

First, create a block in `index.css` called `.flex-container`, which will define
CSS for our 'flex-container' class. To apply flexbox, we need to add `display: flex` as a property here and set a width and height of the container. We can
also set width and height to the full size of the window using `100vw`, and
`100vh`, so our CSS block will look like this:

```
.flex-container {
  display: flex;
  width: 100vw;
  height: 100vh;
}
```

## Identify and Use Flex Properties

Save `index.css` and check out `index.html` in your browser. Cool! We're taking
some inspiration from nature today, and going with colors that look like you're
oceanside. Looks like we're on our way! If you inspect the page, you'll see that
the three sections displayed are actually our `<header>`, `<main>` and
`<footer>` elements. Note, too, that the three sections are evenly dividing the
page. If you resize your browser window, the three sections will stay evenly
split, expanding and shrinking to fit. With just a little bit of CSS, we've
already got some responsiveness!

However, we've got a small issue.. it doesn't make much sense to have a
`<header>` on the left, and a `<footer>` on the right; they should be on the top
and bottom of our page. We'll need to add one more line of CSS for this,
`flex-direction`.

#### `flex-direction`

By default, flexbox will display content horizontally. If we want to change
this, we'll need to define a direction. In `index.css`, add the following line
to `.flex-container`:

```
flex-direction: column;
```

Refresh `index.html` to see the change. This time, our ivory `<header>` appears
along the top of our page, with `<footer>` at the bottom!

The `flex-direction` property has a few setting options:

- `row` - the default setting, organizes items from left to right
- `column` - organizes items from top to bottom
- `row-reverse` - organizes items from _right_ to _left_
- `column-reverse` - organizes items from _bottom_ to _top_

Switching `flex-direction` to the `column-reverse` setting, for instance, will
put our pale blue `<footer>` on top, and our ivory `<header>` on the bottom.

We'll go ahead and keep the setting as `column` so our elements are in logical
order, but our `<header>` and `<footer>` sections are quite large. Go back into
`index.css`, and in the `header` block, change the `height` property to `10%`,
then check the page out in your browser.

This time, our `<header>` is much shorter. More importantly, though, our
`<main>` and `<footer>` sections have actually expanded, evenly filling the
remainder of the page. The height of our `<header>` is now 10% of the parent
container, which, in this case, is the height of our window.

It probably makes more sense to set a specific height, as `<header>` will most
often contain navigation and a website logo that we want to keep at a consistent
height. Similarly, footers usually contain a small amount static links and
information, so let's go ahead and switch the height property in the `header`
and `footer` CSS blocks to `80px`.

Refresh the page and you'll see the effect: Our turquoise `<main>` section takes
up the majority of the page, and if you shrink the height of your browser
window, the height of `<main>` will change significantly. Our `<header>` and
`<footer>` sections will still adjust in height a little, but we'll take a look
at preventing that later on. Previously, to create this sort of layout, we would
have added the `position` property to the individual `<header>` and `<footer>`
elements, but with flexbox, the position is being handled by the _parent
container_, applying to all of its children.

Now that we've set up a basic layout using flexbox, we can go deeper into some
of its cool properties.

#### `flex-wrap`

Let's say we want to display a series of items in the `<main>` section of our
page. Make six `<div>` elements inside of `<main>` and assign them a class name
'item', adding the number 1 through 6 in them, like so:

```
<div class="item">1</div>
<div class="item">2</div>
<div class="item">3</div>
<div class="item">4</div>
<div class="item">5</div>
<div class="item">6</div>
```

In our CSS file, define a block for `.item` with `height` and `width` set to
`100px`, `margin` set to `5px`, and `background-color` set to `#FCF2EC`. Now, in
the `main` CSS block, set `display` to `flex`. The two classes should look like
the following:

```
main {
  display: flex;
  background-color: white;
  width: 100%;
  height: 100%;
}

.item {
  height: 100px;
  width: 100px;
  margin: 5px;
  background-color: #FCF2EC;
}
```

Refresh and you should see six pink boxes horizontally aligned. If you reduce
the width of your browser window, these boxes will evenly shrink to fit. Go back
into `index.css`, and in `.main`, add the following line:

```
flex-wrap: wrap;
```

Now, if you refresh the browser, grow and shrink the window, the boxes will stay
100 pixels wide, _and 'wrap' to a new line_ one by one when there is no more
space to fit! The `flex-wrap` property defines how items in a flex container
handle positioning when there are too many items to fit the space. By default,
`flex-wrap` is set to `nowrap`, which is what we saw initially. You can also try
changing `flex-wrap` to `wrap-reverse`, which will act similar to `wrap`, except
from the _bottom and up_, instead of top and down. We'll keep the property set
to `wrap` for now, though.

Let's add in the previous property we discussed, `flex-direction`. If you add
`flex-direction: column` to the `main` CSS block, flexbox will still _wrap_
items, but instead of in a new line underneath, the items will appear in a new
_column_ to the right of the first.

#### `flex-flow`

In our `.main` CSS block, we've now got `flex-direction` and `flex-wrap`
defined. These two properties often go hand in hand, so CSS provides a shorthand
property that defines both in one line: `flex-flow`. To implement this, in
`.main` replace `flex-direction` and `flex-wrap` with the following:

```
flex-flow: column wrap;
```

The `flex-flow` property takes in two settings, the first for direction and the
second for wrapping. If you only include one setting, the other will be set to
its default, `row` or `nowrap`.

Again, notice we've only defined flex properties in the parent element, using
`.main`. We're effectively letting our browser decide how to handle the
positioning of the child divs with these two lines of CSS for the parent. For
the next section, switch the direction back to `row` (so, either `flex-flow: row wrap;`, or just `flex-flow: wrap;`).

#### justify-content

Now that we've got wrapping and direction set up, we can define where we want
items positioned in more detail. The first property we will look at is
`justify-content`, which will define where items start and end, and how they are
spaced in between. In the `main` CSS block, add:

```
justify-content: center;
```

Now, our six pink boxes are centered together on the page. Wrapping will still
apply here, so if the page shrinks enough, some of the boxes will spill over,
but _remain centered on the next row_. Very cool! Getting HTML elements to
behave this way _without_ flexbox is actually fairly difficult, but we've got it
set up in short order.

The `justify-content` property has a number of settings:

- `center` - centers all elements while preserving the original spacing in-between
  each of them.
- `flex-start` - aligns all elements to the beginning of the container. This is
  the default setting, so we've actually already seen what this looks like.
- `flex-end` - aligns all elements to the end of the flex container. If you apply
  this setting, our pink boxes will align to the right side of the screen.
  However, if the page shrinks, the last flex elements will still wrap to the next
  row, so order is preserved.
- `space-around` - adds space in between each flex element so they fill the space
  they are in, evenly dividing the row and centering each element in each
  division. This white space in between will shrink as the page shrinks, and items
  will wrap when they no longer fit on the same row.
- `space-between` - similar to `space-around`, except this time, the _first_ and
  _last_ flex elements on a row will be aligned to the beginning and end of the
  row, removing white space on the edges of the container. On a new row, the first
  and last elements will again align to the beginning and end.

If you change `flex-flow` back to `column wrap`, the flex elements will act the
same way, _only vertically_, so `justify-content` will apply based on the
`flex-direction` you've defined.

#### `align-items`

Centering vertically is actually fairly non-intuitive using basic CSS. Flexbox
provides a solution, though, in the `align-items` property. In the `.main` CSS
block, make sure `flex-flow` is set to `row wrap` once again, and then add the
following line:

```
align-items: center;
```

Save, then refresh your page in the browser and take a look. Now, our pink boxes
are centered _vertically_ within our `<main>` element. If the window shrinks,
the elements will wrap as expected, and each row will center within its own
space. Now, go back to your `flex-flow` setting and change it from `row` to
`column`. Our flex elements will now be centered _horizontally_. So, where
`justify-content` will arrange flex elements in the same direction that you've
defined in `flex-direction` or `flex-flow`, `align-items` will arrange elements
in the direction **perpendicular** to your `flex-direction` setting.

Just like `justify-content`, the `align-items` property has a few different
settings:

- `center` - centers elements vertically if the `flex-direction` is set to `row`, and horizontally if the `flex-direction` is set to `column`.
- `flex-start` - aligns elements to the top of the flex container if `flex-direction` is set to `row`, and to the left of the container if `flex-direction` is set to `column`.
- `flex-end` - aligns elements to the bottom or right of the flex container, the opposite of `flex-start`.
- `stretch` - Stretches elements to fit the container. Try this by setting `align-items` to `stretch`, then make sure `flex-flow` is set to `row wrap`, and in the `.item` CSS block, remove `height: 100px`. Each element will now stretch to fit the height of the flex container. The `stretch` setting will have the same effect on flex columns if you add back in the `height` property but remove `width: 100px`.
- `baseline` - aligns elements based on the _text_ baseline inside each element. If you tried out the `stretch` setting, make sure your `flex-direction` is set back to `row` and that both `height` and `width` are set to `100px` in the `.item` CSS block. Now, set `align-items` to `baseline`, go to your `index.html` file and remove some of the numbers that are contained in our divs, leaving a few. Save both the HTML and CSS, and check out the page in your browser. Any div that is now empty is aligned normally, but any div that still has text in it will align _based on the bottom of the text_.

To perfectly center an element horizontally and vertically, with flex, we can
use a combination of both `justify-content` and `align-items` like so:

```
justify-content: center;
align-items: center;
```

#### `align-content`

The `align-content` property defines how multiple rows of elements will be
displayed. The effects of `align-content` will not apply if `nowrap` is set, and
won't be visible until more than one row or column of flex content is present.
Because of this, it is often best to use `align-content` in conjunction with
`align-items`, giving you a more nuanced control over the effects of wrapping.

- `center` - centers all rows in the container. Combined with `align-items: center`, this will keep all items and rows grouped together, instead of centering each row independently.
- `stretch` - similar to `align-items: stretch` when multiple rows are present.
- `space-around` - centers elements vertically on each row (or horizontally on each column) the same way as if you only used `align-items: center`.
- `space-between` - similar to `justify-content: space-between`, if two rows of elements are present, the first row will align to the top of the container, and the second row will align to the bottom. Any additional rows will be evenly centered and spaced in between.
- `flex-start` - aligns elements to the beginning of the flex container
- `flex-end` - aligns elements to the end of the flex container

### Conclusion

That covers all the properties of flexbox, but feel free to continue to practice
with various settings. It is possible to use flexbox to create very unique page
layouts, recreate some of the awesome modern layouts we see (i.g. the dynamic
columns you see on [pinterest.com](pinterest.com)), or just add a little more
responsiveness to make your site look good regardless of how big or how small
your user's screen is.
