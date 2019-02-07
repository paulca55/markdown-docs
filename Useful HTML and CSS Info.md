# Useful HTML and CSS Info

<!-- TOC depthFrom:2 depthTo:2 orderedList:false updateOnSave:true withLinks:true -->

- [Links and Images](#links-and-images)
- [Hello, CSS](#hello-css)
- [CSS Box Model](#css-box-model)
- [CSS Selectors](#css-selectors)
- [Semantic HTML](#semantic-html)
- [HTML Forms](#html-forms)
- [Web Typography](#web-typography)

<!-- /TOC -->

## Links and Images

### Absolute, Relative, and Root-relative Links

Root-relative links (e.g. `/images/bg.jpg`) won’t work for local file systems (i.e. `file:///Users/paul/Desktop/basic-web-pages/basics.html`) they need a local/remote server environment.

### Image Dimensions

The `width` attribute sets an explicit dimension for the image. There’s a corresponding `height` attribute, as well. Setting only one of them will cause the image to scale proportionally, while defining both can stretch the image. Dimension values are specified in pixels, and you should never include a unit (e.g., `width="75px"` would be incorrect).

The width and height attributes can be useful, but it’s usually better to set image dimensions with CSS so you can alter them with media queries.

## Hello, CSS

### The Cascade

The CSS hierarchy for every web page looks like this:

- The browser’s default stylesheet
- User-defined stylesheets
- External stylesheets _(that’s us)_
- Page-specific styles _(that’s also us)_
- Inline styles _(that could be us, but it never should be)_

CSS can be defined in 3 ways.

- External stylesheet
- Internal stylesheet (sometimes referred to as _embedded styles_ or _page-specific styles_)
- Inline styles

## CSS Box Model

### Block Elements and Inline Elements

- Block boxes always appear below the previous block element. This is the “natural” or “static” flow of an HTML document when it gets rendered by a web browser.
- The width of block boxes is set automatically based on the width of its parent container.
- The default height of block boxes is based on the content it contains. For example, when you narrow the browser window which only contains a `<h1>`, the `<h1>` gets split over two lines, and its height adjusts accordingly.
- Inline boxes _don’t affect_ vertical spacing. They’re not for determining layout — they’re for styling stuff inside of a block. When it comes to margins and padding, browsers treat inline elements differently. You can add space to the left and right on an inline element, but you cannot add height to the top or bottom padding or margin of an inline element.
- The width of inline boxes is based on the content it contains (including any left and right padding), not the width of the parent element.

_**Note:** The `vertical-align` CSS property specifies the vertical alignment of an **inline** or **table-cell** box._

### Margins

Margins and padding can accomplish the same thing in a lot of situations, making it difficult to determine which one is the “right” choice. The most common reasons why you would pick one over the other are:

- The padding of a box has a background, while margins are always transparent.
- Padding is included in the click area of an element, while margins aren’t.
- Margins collapse vertically, while padding doesn’t.
- If none of these help you decide whether to use padding over margin, then don’t fret about it - just pick one. In CSS, there’s often more than one way to solve your problem.

### Margins on Inline Elements

Inline boxes _completely ignore_ the top and bottom margins of an element. The rationale behind this goes back to the fact that inline boxes format runs of text inside of a block, and thus have limited impact on the overall layout of a page. If you want to play with the vertical space of a page, you must be working with block-level elements.

So, before you start banging your head against the wall trying to figure out why your top or bottom margin isn’t working, remember to check your display property.

### Preventing Margin Collapse

Sometimes you do want to prevent the margins from collapsing. All you need to do is put another invisible element in between them (_although this isn't very semantic_).

```html
<p>
  Paragraphs are blocks, too. <em>However</em>, &lt;em&gt; and &lt;strong&gt; elements are not. They
  are <strong>inline</strong> elements.
</p>

<div style="padding-top: 1px"></div>
<!-- Add this -->

<p>Block elements define the flow of the HTML document, while inline elements do not.</p>
```

The important part here is that only consecutive elements can collapse into each other. Putting an element with non-zero height (hence the `padding-top` on the `div`) between our paragraphs forces them to display both the top margin and the bottom margin.

Remember that padding doesn’t ever collapse, so an alternative solution would be to use padding to space out our paragraphs instead of the margin property. However, this only works if you’re not using the padding for anything else.

A third option to avoid margin collapse is to stick to a bottom-only or top-only margin convention. For instance, if all your elements only define a bottom margin, there’s no potential for them to collapse.

### Padding as a percentage

When padding is added to an element as a **percentage** (e.g. `padding-bottom: 50%;`) the amount of padding applied relates to the width of the **containing block**.

_**Note:** Also using a percentage for a **margin** will also relate to the width of the **containing block**._

Say we had a `.container` div and a `.content` div inside of it. If we set `padding-bottom: 50%;` to the `.content` div, how many pixels of padding will be applied to the bottom of the div?

#### The HTML

```html
<div class="container">
  <div class="content"><p>The content</p></div>
</div>
```

#### The CSS

```css
.container {
  width: 1200px;
}

.content {
  width: 800px;
  padding-bottom: 50%;
}
```

#### The Result

The answer is `600px`. This is because this is half (`padding-bottom: 50%;`) of the width of the containing block (`.container`). This is actually a good method to keep an element in proportion when scaling down the screen size (see [CSS Tricks][css-tricks-scaled-content] for more info).

_**Note:** If you are using `box-sizing: border-box;` and had `border: 10px solid #000;` applied to the `.container` div, then the height of `.content` would be `590px`. This is because with the `10px` border on the left and the right, the actual width of the content area of `.container` is `1180px`. So 50% of this is `590px`. However if you used `box-sizing: content-box` the border wouldn't affect this so the height of `.content` would be `600px` even with the borders._

### Constant width to height ratio

#### Example 1

_**Note:** This method requires the child element to be **absolutely position** inside the parent container._

##### HTML

```html
<div class="parent">
  <div class="child"></div>
</div>
```

##### CSS

```css
.parent {
  height: 0;
  padding-bottom: 56.25%; /* 16:9 */
  position: relative;
}

.child {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
}
```

#### Example 2

_**Note:** This method allows content to be placed inside the element normally._

##### HTML

```html
<div class="parent">
  <div class="child"></div>
</div>
```

##### CSS

```css
.parent {
  background: #333;
  width: 50%;
}
.parent::before {
  content: '';
  padding-top: 100%;
  float: left;
}
.parent::after {
  content: '';
  display: block;
  clear: both;
}
```

## CSS Selectors

### Pseudo-classes for Links

Some useful information can be found on [Sitepoint][pseudo-classes] about pseudo classes.

#### Visited Hover State

We can refine our links even more by stringing pseudo-classes together.

```css
a:visited:hover {
  color: orange;
}
```

This creates a dedicated hover style for visited links. Fantastic! Except for the fact that this breaks our `a:active` style due to some complicated CSS internals that you’ll never want to read about.

#### Visited Active State

We can fix that with `a:visited:active`. Note that the order in which these are defined in `styles.css` matters:

```css
a:visited:active {
  color: red;
}
```

These last two sections let you style visited links entirely separately from unvisited ones. It’s a nice option to have, but again, you’re welcome to stop at basic link styles if that’s all you need.

## Semantic HTML

### Sections

Each `<section>` element should contain at least one heading, otherwise it will add an “untitled section” to your document outline. For example, run the below code through the [outliner tool](https://gsnedders.html5.org/outliner/):

```html
<h2>Inline Semantic HTML</h2>
<section>
  <!-- This will be an "Untitled Section" -->
  <p>The <code>&lt;time&gt;</code> element is semantic, but it’s not sectioning content.</p>
</section>
```

This creates a new section, but since there’s no heading associated with it, the document outline doesn’t know what to call it. This should generally be avoided when using `<section>` elements.

### Address

The `<address>` element is like `<time>` in that it doesn’t deal with the overall structure of a document, but rather embellishes the parent `<article>` or `<body>` element with some metadata. It defines contact information for the author of the article or web page in question.

- `<address>` should _not_ be used for arbitrary physical addresses. To represent an arbitrary address, one that is not related to the contact information, use a `<p>` element rather than the `<address>` element.
- This element should not contain more information than the contact information, like a publication date (which belongs in a `<time>` element).
- Typically an `<address>` element can be placed inside the `<footer>` element of the current section, if any.

```html
<footer>
  <p>
    This fake article was written by somebody at InternetingIsHard.com, which is a pretty decent
    place to learn how to become a web developer. This footer is only for the containing
    <code>&lt;article&gt;</code> element.
  </p>
  <address>
    Please contact <a href="mailto:troymcclure@example.com">Troy McClure</a> for questions about
    this article.
  </address>
</footer>
```

By default, this will be styled the same way as `<em>`, but you can change that with a simple CSS rule.

### Figures and Captions

The `alt` attribute is closely related to the `<figcaption>` element. `alt` should serve as a text replacement for the image, while `<figcaption>` is a supporting description displayed with either the image or its text-based equivalent.

When using `<figcaption>` in the above manner, you can safely omit an image’s alt attribute without hurting your SEO. Depending on what kind of images you’re working with, it may be more convenient (and less redundant) to have visible `<figcaption>`’s that describe them opposed to invisible alt attributes.

## HTML Forms

### Radio buttons

Changing the type property of the `<input>` element to radio transforms it into a radio button. Radio buttons are a little more complex to work with than text fields because they always operate in groups, allowing the user to choose one out of many predefined options.

This means that we not only need a label for each `<input>` element, but also a way to group radio buttons and label the entire group. This is what the `<fieldset>` and `<legend>` elements are for. Every radio button group you create should:

- Be wrapped in a `<fieldset>`, which is labeled with a `<legend>`.
- Associate a `<label>` element with each radio button.
- Use the same `name` attribute for each radio button in the group.
- Use different `value` attributes for each radio button.

### Text Areas

The `<textarea>` tag isn’t self-closing like the `<input>` element, so you always need a closing `</textarea>` tag. If you want to add any default text, it needs to go _inside_ the tags opposed to a `value` attribute.

## CSS Text

### When to use `overflow-wrap` (or legacy `word-wrap`) vs `word-break`

`overflow-wrap` and `word-break` behave very similarly and can be used to solve similar problems. A basic summary of the difference, as explained in the CSS specification is:

`overflow-wrap` is generally used to avoid problems with long strings causing broken layouts due to text flowing outside a container.
`word-break` specifies soft wrap opportunities between letters commonly associated with languages like Chinese, Japanese, and Korean (CJK).
After describing examples of how `word-break` can be used in CJK content, the spec says: "To enable additional break opportunities only in the case of overflow, see `overflow-wrap`".

From this, we can surmise that `word-break` is best used with non-English content that requires specific word-breaking rules, and that might be interspersed with English content, while `overflow-wrap` should be used to avoid broken layouts due to long strings, regardless of the language used.

_**Note:** As appsosed to `word-break`, `overflow-wrap` will only create a break if an entire word cannot be placed on its own line without overflowing, unless `word-break` is set to `break-word` which is not fully supported._

#### The Historical `word-wrap` Property

`overflow-wrap` is the standard name for its predecessor, the `word-wrap` property. `word-wrap` was originally a proprietary Internet Explorer-only feature that was eventually supported in all browsers despite not being a standard.

`word-wrap` accepts the same values as `overflow-wrap` and behaves the same way. According to the spec, browsers "must treat `word-wrap` as an alternate name for the `overflow-wrap` property, as if it were a shorthand of `overflow-wrap`". Also, all user agents are required to support `word-wrap` indefinitely, for legacy reasons.

Both `overflow-wrap` and `word-wrap` will pass CSS validation as long as the validator is set to test against CSS3 or higher (currently the default).

### `white-space`

The `white-space` property has nothing to do with how text wraps/breaks inside it's container, it specifies how white-space inside an element is handled.

For example should white-space (spaces and line-breaks) in the code be trimmed (normal behaviour) or adhered to (such as when displaying code snippets).

### `hyphens`

The `hyphens` property controls hyphenation of text in block level elements. You can prevent hyphenation from happening at all, allow it, or only allow it when certain characters are present.

Note that `hyphens` is language-sensitive. Its ability to find break opportunities depends on the language, defined in the lang attribute of a parent element. Not all languages are supported yet, and support depends on the specific browser.

## Web Typography

### Font Families and Font Faces

The only human-friendly keywords available for `font-weight` are `normal` (400) and `bold` (700). Any other boldness levels need to set numerically.

## Useful to know

### Form inputs and pseudo elements

An `<input />` doesn’t allow the usage of `::before` or `::after` pseudo elements on it. None of the input types do.

Why can’t you use these pseudo elements on inputs? Because these pseudo elements are only allowed to be used on _container_ elements. So, elements like inputs, images and any other self closing element can’t use pseudo elements because they aren’t “container elements”. Meaning, they don’t allow any nested elements or content inside of them.

### `outline` and `outline-offset`

The `outline` property in CSS draws a line around the outside of an element. It's similar to border except that:

1. It always goes around all the sides, you can't specify particular sides
2. It's not a part of the box model, so it won't effect the position of the element or adjacent elements.

Other minor facts include that it doesn't respect `border-radius` (makes sense I suppose as it's not a border) and that it isn't always rectangular. If the outline goes around an inline element with different font-sizes, for instance, Opera will draw a staggered box around it all.

It is often used for accessibility reasons, to emphasize a link when tabbed to without affecting positioning and in a different way than hover. Read more detail about `outline` on [CSS Tricks][css-tricks-outline].

The `outline-offset` property adds space between an outline and the edge or border of an element. The space between an element and its outline is transparent.

## Using `em`

When `em` is used to specify a font-size, the `em` is measured relative to the font-size of the **parent** element.

When `em` is used to specify lengths (i.e. width, padding, margin etc.) the `em` is measured relative to the font size of the **current** element.

## Using percentages

When `%` is used to specify a font-size, the `%` is measured relative to the font-size of the **parent** element.

When `%` is used to specify lengths (i.e. width, padding, margin, etc.) the `%` is measured relative to their **parent's width**. However if specifying the height of an element in `%` it will be a percentage of the **parent's height**.

When `%` is used in `transform: translate()` the `%` is measured relative to the **width** (translateX) and **height** (translateY) of the current element.

## `z-index` and stacking order/stacking context

_**Note:** This majority of this information was taken from [Philip Walton's website][philip-walton-z-index] but has been edited in places._

### Stacking Order

z-index seems so simple: elements with a higher z-index are stacked in front of elements with a lower z-index, right? Well, actually, no. This is part of the problem with z-index. It appears so simple, so most developers don’t take the time to read the rules.

Every element in an HTML document can be either in front of or behind every other element in the document. This is known as the stacking order. The rules to determine this order are pretty clearly defined in the spec, but as I’ve already stated, they’re not fully understood by most developers.

When the z-index and position properties aren’t involved, the rules are pretty simple: basically, the stacking order is the same as the order of appearance in the HTML. (OK, it’s actually a little more complicated than that, but as long as you’re not using negative margins to overlap inline elements, you probably won’t encounter the edge cases.)

When you introduce the position property (**without specifiying a z-index**) into the mix, any positioned elements (and their children) are displayed in front of any non-positioned elements. (To say an element is “positioned” means that it has a position value other than static, e.g., relative, absolute, sticky, fixed, etc.)

Finally, when z-index is involved, things get a little trickier. At first it’s natural to assume elements with higher z-index values are in front of elements with lower z-index values, and any element with a z-index is in front of any element without a z-index, but it’s not that simple. First of all, z-index only works on positioned elements. If you try to set a z-index on an element with no position specified, it will do nothing. Secondly, z-index values can create stacking contexts, and now suddenly what seemed simple just got a lot more complicated.

### Stacking Contexts

Groups of elements with a common parent that move forward or backward together in the stacking order make up what is known as a stacking context. A full understanding of stacking contexts is key to really grasping how z-index and the stacking order work.

Every stacking context has a single HTML element as its root element. When a new stacking context is formed on an element, that stacking context confines all of its child elements to a particular place in the stacking order. That means that if an element is contained in a stacking context at the bottom of the stacking order, there is no way to get it to appear in front of another element in a different stacking context that is higher in the stacking order, even with a z-index of a billion!

New stacking contexts can be formed on an element in one of three ways:

- Root element of document (HTML).
- Element has a `position` value "absolute" or "relative" and `z-index` value other than "auto".
- Element has a `position` value "fixed" or "sticky" (sticky for all mobile browsers, but not older desktop).
- Element that is a child of a flex (`flexbox`) container, with `z-index` value other than "auto".
- Element has an `opacity` value less than 1.
- Element with a `mix-blend-mode` value other than "normal".
- Element with any of the following properties with value other than "none":
  - transform
  - filter
  - perspective
  - clip-path
  - mask / mask-image / mask-border
- Element with a `isolation` value "isolate".
- Element with a `-webkit-overflow-scrolling` value "touch".
- Element with a `will-change` value specifying any property that would create a stacking context on non-initial value (see this post).
- Element with a `contain` value of "layout", or "paint", or a composite value that includes either of them.

### Determining an Element’s Position in the Stacking Order

Actually determining the global stacking order for all elements on a page (including borders, backgrounds, text nodes, etc.) is extremely complicated and far beyond the scope of this article (again, I refer you to the [spec](http://www.w3.org/TR/CSS2/zindex.html).

But for most intents and purposes, a basic understanding of the order can go a long way and help keep CSS development predictable. So let’s start by breaking the order down into individual stacking contexts.

#### Stacking Order Within the Same Stacking Context

Here are the basic rules to determine stacking order within a single stacking context (from back to front):

1. The stacking context’s root element.
2. Positioned elements (and their children) with negative z-index values (higher values are stacked in front of lower values; elements with the same value are stacked according to appearance in the HTML).
3. Non-positioned elements (ordered by appearance in the HTML).
4. Positioned elements (and their children) with a z-index value of `auto` (ordered by appearance in the HTML). Note that an elements initial value for z-index is `auto` when z-index is not explicitly defined.
5. Positioned elements (and their children) with positive z-index values (higher values are stacked in front of lower values; elements with the same value are stacked according to appearance in the HTML).

_**Note:** positioned elements with negative z-indexes are ordered first within a stacking context, which means they appear behind all other elements. Because of this, it becomes possible for an element to appear behind its own parent, which is normally not possible. This will only work if the element’s parent is in the **same stacking context** and is not the root element of that stacking context. A great example of this is [Nicolas Gallagher’s CSS drop-shadows][nicolas-cs-drop-shadows] without images._

#### Global Stacking Order

With a firm understanding of how/when new stacking contexts are formed as well as a grasp of the stacking order within a stacking context, figuring out where a particular element will appear in the global stacking order isn’t so bad.

The key to avoid getting tripped up is being able to spot when new stacking contexts are formed. If you’re setting a z-index of a billion on an element and it’s not moving forward in the stacking order, take a look up its ancestor tree and see if any of its parents form stacking contexts. If they do, your z-index of a billion isn’t going to do you any good.

Read more about z-index on [MDN][mdn-z-index].

Watch this video about z-index on [Kevin Powell's YouTube channel][kevin-powell-z-index].

[css-tricks-scaled-content]: https://css-tricks.com/scaled-proportional-blocks-with-css-and-javascript/ 'Scaled/Proportional Content with CSS and JavaScript'
[css-tricks-outline]: https://css-tricks.com/almanac/properties/o/outline/ 'Outline'
[pseudo-classes]: https://www.sitepoint.com/web-foundations/pseudo-classes/ 'Pseudo Classes'
[philip-walton-z-index]: https://philipwalton.com/articles/what-no-one-told-you-about-z-index/ 'What No One Told You About Z-Index'
[mdn-z-index]: https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Positioning/Understanding_z_index 'MDN: Understanding CSS z-index'
[mdn-stacking-context]: https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Positioning/Understanding_z_index/The_stacking_context#The_stacking_context 'MDN: The Stacking Context'
[kevin-powell-z-index]: https://www.youtube.com/watch?v=uS8l4YRXbaw 'CSS Z-Index and Stacking Context'
[nicolas-cs-drop-shadows]: http://nicolasgallagher.com/css-drop-shadows-without-images/demo/ 'CSS drop-shadows without images'
