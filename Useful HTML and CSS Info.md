<img src="https://raw.githubusercontent.com/paulca55/markdown-docs/master/images/cassify-header-logo.png" alt="Cassify logo" width="300">

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
- Inline boxes _don’t affect_ vertical spacing. They’re not for determining layout — they’re for styling stuff inside of a block.
- The width of inline boxes is based on the content it contains, not the width of the parent element.

Note: The `vertical-align` CSS property specifies the vertical alignment of an **inline** or **table-cell** box.

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
<p>Paragraphs are blocks, too. <em>However</em>, &lt;em&gt; and &lt;strong&gt; elements are not. They are <strong>inline</strong> elements.</p>

<div style='padding-top: 1px'></div>  <!-- Add this -->

<p>Block elements define the flow of the HTML document, while inline elements
do not.</p>
```

The important part here is that only consecutive elements can collapse into each other. Putting an element with non-zero height (hence the `padding-top` on the `div`) between our paragraphs forces them to display both the top margin and the bottom margin.

Remember that padding doesn’t ever collapse, so an alternative solution would be to use padding to space out our paragraphs instead of the margin property. However, this only works if you’re not using the padding for anything else.

A third option to avoid margin collapse is to stick to a bottom-only or top-only margin convention. For instance, if all your elements only define a bottom margin, there’s no potential for them to collapse.

### Padding as a percentage

When padding is added to an element as a **percentage** (e.g. `padding-bottom: 50%;`) the amount of padding applied relates to the width of the **containing block**. See below for an example:

Say we had a `.container` div and a `.content` div inside of it. If we set `padding-bottom: 50%;` to the `.content` div, how many pixels of padding will be applied to the bottom of the div?

#### The HTML

```html
<div class="container">
  <div class="content">
    <p>The content</p>
  </div>
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

Note: If you are using `box-sizing: border-box;` and had `border: 10px solid #000;` applied to the `.container` div, then the height of `.content` would be `590px`. This is because with the `10px` border on the left and the right, the actual width of the content area of `.container` is `1180px`. So 50% of this is `590px`. However if you used `box-sizing: content-box` the border wouldn't affect this so the height of `.content` would be `600px` even with the borders.

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
  <p>This fake article was written by somebody at InternetingIsHard.com, which
     is a pretty decent place to learn how to become a web developer. This footer
     is only for the containing <code>&lt;article&gt;</code> element.</p>
  <address>
    Please contact <a href='mailto:troymcclure@example.com'>Troy
    McClure</a> for questions about this article.
  </address>
</footer>
```

By default, this will be styled the same way as <em>, but you can change that with a simple CSS rule.

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

## Web Typography

### Font Families and Font Faces

The only human-friendly keywords available for `font-weight` are `normal` (400) and `bold` (700). Any other boldness levels need to set numerically.

[css-tricks-scaled-content]: https://css-tricks.com/scaled-proportional-blocks-with-css-and-javascript/ 'Scaled/Proportional Content with CSS and JavaScript'
[pseudo-classes]: https://www.sitepoint.com/web-foundations/pseudo-classes/
