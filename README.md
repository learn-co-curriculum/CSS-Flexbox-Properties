# Customizing Flexbox

## Objectives

1.  Identify and Use Flex Properties

### Setting Up Child Elements with Flex

So, we've gotten pretty far with flexbox just by defining properties on the
container, but we can go even further by setting CSS properties within the
children of the container.

#### `flex-basis`

So far, we've been setting the size of our child elements in a flex container by
using the `width` and `height` properties. We can achieve the same effect using
the `flex-basis` property, which determines the initial width of an element in a
flex container. Width, in this case, refers to the length of an element in the
`flex-direction` assigned, so if `flex-direction` is set to `column`,
`flex-basis` affects the `height` of each element. There are a few settings for
`flex-basis` we can use, allowing us to handle sizing in different ways:

- `flex-basis: 100px;` - will give elements an initial width of `100px`, if the container is set to `row`, or an initial height of `100px`, if the container is set to `column`. Other units can be used here, such as `em`.
- `flex-basis: --%` - will set the element to a percentage of a container size. Setting `flex-basis` to 50% on one child element, for instance, will cause that child to take up half of a container row. Set to 100%, the child will fill the entire row, causing it to wrap if there are other children in the flex container.
- `flex-basis: content;` - will set the element's size based on the `width` or `height` properties if they are defined. Otherwise, the element will be sized based on the content inside the element.

#### `flex-grow`

The `flex-grow` property specifies how much space the element should take up
within a flex container. By default, `flex-grow` is equal to `0`, meaning
elements that do not have `flex-grow` specifically defined will not grow larger
than the `width`, _for rows_, `height`, _for columns_, or `flex-basis` they are
set to, producing the wrapping effect we've seen so far - all of our child
elements remain the same size, and spill over into a new line if they don't fit.

Assigning a `flex-grow` value greater than `0` changes this behavior, allowing a
child element to expand. The higher the number, the more space an element will
take up, relative to its siblings. For instance, if we had just two child
elements, the first with `flex-grow` set to `1`, and the second with `flex-grow`
set to `2`, the second element will be twice as wide as the first.

One way to think of this: in total, the sum of all `flex-grow` values, `1` and
`2` equals 3, so `flex-grow: 1;` is 1/3 of the row; if the sum of all
`flex-grow` values was 12, `flex-grow: 1;` would be 1/12 of the row.

The `flex-grow` property can be used in conjunction with a set width which can
create a variety of layouts. For instance, let's create a new CSS class,
`setWidth`, with `flex-basis` set to `100px`, and `flex-grow` set to `1`, like
so:

```
.setWidth {
  flex-basis: 100px;
  flex-grow: 1;
}
```

Then, for all of the pink child divs in our flex container, set the classes to
be `class="item setWidth"`, we get a cool effect - elements will still wrap if
the container size can't fit them in a line, but all elements will expand in
size to fill any empty space, so if one pink box is on a new line, it fills 100%
of the space, while all other boxes will fit evenly on their row.

If no divs have a set width, but have `flex-grow` set greater than `0`, elements
_will not_ wrap, instead, shrinking to fit all into one row.

#### `flex-shrink`

The `flex-shrink` determines how much an element in a flex container will
shrink; the larger the number, the more the element will shrink in relation to
other elements in the container, with the default set to `1`. To see this in
action, let's go back to our the first flex container where `<header>`,
`<main>`, and `<footer>` are the children. Currently, although we've set the
height of `header` and `footer`, if the page is shortened, these sections will
still shrink to fit.

In your CSS file, under `header`, add `flex-shrink: 0`, and under `footer`, add
`flex-shrink: 3`. Check out `index.html` in your browser and you can see that
our `<header>` is no longer changing size. Setting `flex-shrink` to `0` will
stop an element from shrinking to fit.

But what about our `<footer>`? Adjusting the height of the browser window will
now cause the `<footer>` to shrink much more than before until it disappears
entirely. Setting `flex-shrink` to `3` causes the `<footer>` to shrink _3_ times
as much as normal.

#### `flex`

Using `flex-grow`, `flex-shrink`, and `flex-basis` in combination allows us to:

1.  Set how much that element expands to fill space
2.  Set how much the element will shrink to fit
3.  Set how large the item is to start

These three settings tend to go together, and because of this, CSS has provided
a shorthand alternative to set all three: `flex`. The `flex` attribute can take
three settings:

```
flex: <flex-grow value> <flex-shrink value> <flex-basis value>
```

Alternatively, you can also use `auto`, `initial` and `none`:

- `flex: auto` - equal to `flex-grow: 1; flex-shrink: 1; flex-basis: content;`, elements set to this will grow and shrink evenly to fit the container.
- `flex: initial` - equal to `flex-grow: 0; flex-shrink: 1; flex-basis: content;`, elements with this settings will shrink to fit, but will not grow beyond their set width or the size of their content.
- `flex: none` - will prevent shrinking and growing, keeping elements to a set size or the size of their content.
- `flex: 1` - or any value greater than `0` - will act the same as `flex-grow: 1`.
- `flex: 100px` - or any valid width - will act the same as `flex-basis: 100px`.

It is recommended that you use `flex` over the individual `grow`, `shrink` and
`basis` properties. Since `flex` automatically handles some of the settings if
they aren't provided, it is less prone to conflicting behavior. Try assigning
our pink boxes different values for `flex` to see how they work.

#### `align-self`

Flexbox offers a way for us to change individual element positions, in the event
that we want one or more elements in a flex container to be positioned
differently than the rest. For instance, if we create a new class, assign
`align-self` to `flex-end` and add that class to one of our pink boxes, when we
take a look at it in browser, we will see that while that pink box will remain
in order relative to other boxes, it will appear at the bottom of the flex
container, while all others remain at the top.

#### `order`

Flexbox has one property which is slightly different than the rest: `order`. The
`order` takes in a positive or negative number value, and will cause flex
container children to rearrange based on ascending numerical value.

On a simple webpage like the one we've created during this lesson, `order` isn't
necessary (we could always just manually rearrange the order of elements we
want, right?). However, if you're building a fully responsive website, you may
realize your page layout needs to change depending on the screen size of a
visitor. For instance, on mobile, say you want to emphasize one element, such as
moving a submit button for ease of use, but on a computer screen, the button can
stay in the original order it is written in the HTML. We could accomplish this
using `order` in conjunction with [`@media`](https://developer.mozilla.org/en-US/docs/Web/CSS/@media).

It should be noted that modifying the order of elements may negatively affect
users who use assistive technology such as screen readers.

## Moving On

When you're ready to leave this lab, run `learn` from the command line. If the
test pass, enter `learn submit`. You'll then be prompted to move on!
