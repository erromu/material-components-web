<!--docs:
title: "Image List"
layout: detail
section: components
excerpt: "An RTL-aware Material Design image list component."
iconId: card
path: /catalog/image-lists/
-->

# Image List

<!--<div class="article__asset">
  <a class="article__asset-link"
     href="https://material-components-web.appspot.com/image-list.html">
    <img src="{{ site.rootpath }}/images/mdc_web_screenshots/image-list.png" width="320" alt="Image list screenshot">
  </a>
</div>-->

MDC Image List provides a RTL-aware Material Design image list component, representing an evolution of the
[Material Design Grid List spec](https://material.io/guidelines/components/grid-lists.html).
An Image List consists of several items, each containing an image and optionally supporting content (i.e. a text label).

## Design & API Documentation

<ul class="icon-list">
  <li class="icon-list-item icon-list-item--spec">
    <a href="https://material.io/guidelines/components/grid-lists.html">Material Design guidelines: Grid lists</a>
  </li>
  <li class="icon-list-item icon-list-item--link">
    <a href="https://material-components-web.appspot.com/image-list.html">Demo</a>
  </li>
</ul>

## Installation

```
npm install --save @material/image-list
```

## Basic Usage

### HTML Structure

The HTML structure for a Standard Image List is as follows:

```html
<ul class="mdc-image-list my-image-list">
  <li class="mdc-image-list__item">
    <div class="mdc-image-list__image-aspect-container">
      <img class="mdc-image-list__image" src="...">
    </div>
    <div class="mdc-image-list__supporting">
      <span class="mdc-image-list__label">Text label</span>
    </div>
  </li>
  ...
</ul>
```

### Styles

The structure above would be combined with an invocation of the `mdc-image-list-standard-columns` mixin, to establish how many
columns should be displayed per line:

```scss
.my-image-list {
  @include mdc-image-list-standard-columns(5);
}
```

Images in a Standard Image list are constrained to 1:1 aspect ratio by default; this can be overridden using the
`mdc-image-list-aspect` mixin documented below.

## Style Customization

### CSS Classes

CSS Class | Description
--- | ---
`mdc-image-list` | Mandatory. Indicates the root Image List element.
`mdc-image-list--with-text-protection` | Optional. Indicates that supporting content should be positioned in a scrim overlaying each image (instead of positioned separately under each image).
`mdc-image-list__item` | Mandatory. Indicates each item in an Image List.
`mdc-image-list__image-aspect-container` | Optional. Parent of each item's image element, responsible for constraining aspect ratio. This element may be omitted entirely if images are already sized to the correct aspect ratio.
`mdc-image-list__image` | Mandatory. Indicates the image element in each item.
`mdc-image-list__supporting` | Optional. Indicates the area within each item containing the supporting text label, if the Image List contains text labels.
`mdc-image-list__label` | Optional. Indicates the text label in each item, if the Image List contains text labels.

### Sass Mixins

Mixin | Description
--- | ---
`mdc-image-list-aspect($width-height-ratio)` | Styles the aspect container elements within an Image List to conform to the given ratio, where 1 is 1:1, greater than 1 is wider, and less than 1 is taller.
`mdc-image-list-standard-columns($column-count, $gutter-size)` | Styles a Standard Image List to display the given number of columns. `$gutter-size` is optional and overrides the default amount of space between items.

### Additional Information

#### Constraining width

The `mdc-image-list-standard-columns` mixin will grow and shrink items based on the Image List's overall width. Depending on
placement, this could be directly related to the viewport width, and images could become exceedingly large compared to
their actual rendered size. This can be restricted by using any of `min-width`, `width`, or `max-width` on the Image
List:

```scss
.my-image-list {
  @include mdc-image-list-standard-columns(5);
  max-width: 960px;
}
```

> **Note:** Remember that any specified width will apply to the _entire_ list, so be sure to account for the gutters
as well.

#### Changing number of columns across breakpoints

Presenting a different number of columns for different viewport sizes is straightforward, since the only thing that
needs to be changed are styles:

```scss
.my-image-list {
  @include mdc-image-list-standard-columns(5);
}

@media (max-width: 599px) {
  .my-image-list {
    @include mdc-image-list-standard-columns(3);
  }
}
```

#### Using div in place of img to enforce aspect ratio

Images in an Image List typically use the `img` element. However, if your assets don't have the same aspect ratio as
specified for list items, they will become distorted. In these cases, you can use a `div` element in place of `img`,
and set the `background-image` of each.

> **Note:** Ensuring your images are appropriately-sized prior to serving them to browsers is the most efficient and
ideal approach to using MDC Image List. The `div` alternative is provided as a convenience. If you use this alternative,
make sure to also include the `mdc-image-list__image-aspect-container` element around each item's image.
