# Design System

The goal of this project is to have a sytem where you can spin up a new astro project and start writing HTML and have a mostly styled site, right out of the box.

This is a custom design system based on the Webflow Client-First approach by {Finsweet}. This approach allows for scalability and full customization without being tied to a system like Bootstrap, and will not have overly complicated output like Tailwind- Its just the basics. This system can be implemented with vanilla CSS, or with a preprossesor like SASS.

## TYPICAL PAGE STRUCTURE

```html
<html>
  <!-- REM: all sizes are based on the root's font size. 1rem = 16px by default. .5rem = 8px, 2rem = 32px, etc. This is ideal for accessibility, as the user can override the defaults if needed, and it will respect browser zooming. Use px values if a size is less than .25rem or 4px (borders, small spacing rules, etc.)
  TYPOGRAPHY & COLORS: Typography and Color rules are generally simple and apply to all page content. As such, they can be applied to the :root element. This system uses typescale variables at the root level to set the sizes of the H1, H2, etc. If needed, these can be overridden at the <h1>, <h2>, etc. tag levels. --->
  <body>
    <!-- Body should receive only typography and color styles. margin: 0; and box-sizing: border-box; can be used here to get children to cooperate by resetting the browser defaults  -->
    <div class="page-wrapper">
      <!-- page wrapper should not be heavily styled, though is a good utility for adding styles to the entire page when needed -->
      <nav></nav>
      <main class="main-wrapper">
        <!-- This will be the primary content area. NAV and FOOTER will be outside of this. Also this is good practice for accessibility -->
        <section class="section_[section-identifier]">
          <!--// Styles: Avoid applying styles to section_[section-identifier]. Instead, use a global add-on class like section-style-dark to control global styles across all sections. Each section_ class is custom, so we don't want to repeat CSS properties for each section. For example, if we need a "dark section", we can apply color: white and background-color: black classes to section-style-dark as a global add-on to our custom section_ class. This will also help describe the content i.e. class="section_main-hero" or class="section_our-team section-theme-dark" -->
          <div class="padding-global">
            <!-- padding-global controls left and right padding only
          CSS class padding-left and padding-right will be the only style on this class. This class can be used on children elements as well -->
            <div class="container-[size]">
              <!-- container-[size] controls the width of the content. We will use margin: 0 auto; to auto center the div, then width: 100%; to take up all available space, finally set a max-width: [width]; to set the size of the container. examples: "container-sm", "container-md", "container-lrg", etc -->
              <div class="padding-section-[size]">
                <!-- padding-section-[size] controls the top and bottom padding only
              CSS class padding-top and padding-bottom will be the only style on this class. -->
                <h1>Header</h1>
                <p>Paragraph</p>
                <div class="button">Button</div>
              </div>
            </div>
          </div>
        </section>
        <section class="section_[section-identifier]">
          <p>Some content</p>
        </section>
      </main>
      <footer></footer>
    </div>
  </body>
</html>
```

## SPACING STRADEGY

Spacing is the vertical space between elements and will be intelligently derived
from two methods: Utility Classes, and Custom Classes.
Utility classes will be used for the most common spacing rules, and custom
classes will be used for unique spacing rules. This will allow for a consistent
and predictable spacing system, while also allowing for unique spacing rules
when needed. Use padding-top or padding-bottom in rems for spacing rules.
##spacing-blocks spacing-blocks are empty divs that will not affect the
readability or accessibility of the page. They will be used to create space
between other divs and elements. They will be given a class that will control
the size of the space. For example, a class of ".spacer-lrg" will create a large
space, and a class of ".spacer-sm" will create a small space. To control the
size of the space, we will use padding-top in rems. EXAMPLE:

```html
<div class="spacer-lrg"></div>
<div class="spacer-sm"></div>
```

### spacing-wrappers

spacing-wrappers have the same goal of spacing-blocks, but are a bit more flexible.
These are utility classes that can be its own div, with children content, or applied
directly to an element as a utility class. For example, using .spacing-global to an
element will add padding to the top and bottom of the element.
This is useful for adding space to a section, or even to a button. EXAMPLE:

```html
<div class="spacing-global"></div>
or
<button class="spacing-global">Button</button>
etc.
```

### Custom spacing classes

Custom spacing classes will be used for unique spacing rules. For
example, if we need a unique spacing rule for a specific section, we can
create a custom class like ".spacing-[identifier]-[size]" and apply it to the
section. This will allow us to create unique spacing rules for specific
sections, while still maintaining a consistent and predictable spacing system.
USE:

```html
<section class="spacing-section-lrg">#</section>
or
<div class="spacing-section-sm"></div>
```

### responsive spacing

Adding custom classes inside media queries
to control the spacing rules for different screen sizes is a good idea.
For example, if we need a unique spacing rule for a specific section on
mobile, we can create a custom class like
".spacing-[identifier]-[size]-[device]" and apply it to the section inside a
media query. This will allow us to create unique spacing rules for
specific sections on mobile, while still maintaining a consistent and
predictable spacing system. EXAMPLES:

```html
<section class="spacing-section-lrg-mobile">
  or
  <div class="spacing-section-sm-mobile">, etc.</div>
</section>
```

## STRUCTURE

This will define the core structure we can use globally

### Global Padding

Global horizontal padding manages the left and right padding of a page's content.

- .padding-global

### Container Size

Global max width values that serve as max-width containers for content.

- ‍.container-tiny
- .container-xs
- .container-sm
- .container-std
- .container-lg
- .container-xl
- .container-xxl
- .container-xxxl

### Section Padding

Section padding manages a global vertical spacing system for sections. Inherits scale from $spaceScale.

- .padding-section-xs
- .padding-section-sm
- .padding-section-base //global padding value
- .padding-section-large

## TYPOGRAPHY

### The Typescale System

The Typescale System is the default system used to define all of the typography sizes and and global measurments. This system gives us a direct relationship between all of our text and sizing elements. This will help facilitate balance and harmony in the design right out of the box. The Fundemental frequencies found in nature are a great starting point to help us create the scale. If inclined: you can define your own frequency.

> minorSecond: 1.067;
> majorSecond: 1.125;
> minorThird: 1.2;
> majorThird: 1.25;
> perfectFourth: 1.333;
> tritone: 1.414;
> perfectFifth: 1.5;
> minorSixth: 1.6;
> goldenRatio: 1.618;
> majorSixth: 1.667;
> minorSeventh: 1.75;
> majorSeventh: 1.875;
> octave: 2;
> myFavoriteFrequency: 1.31459;

### HTML TAGS

Always use semantic html tags to define headings and text!

#### Custom Properties

You can always call the default style with classes, too. With custom properties and variables, the semantic tags and the utility classes will always provide the same base style.

- .heading-style-h1
  ...
- .heading-style-h6

### Text-size

utility classes for text size:

- .text-size-xl
- .‍text-size-lg
- .‍text-size-md
- .‍text-size-base
- .‍text-size-sm
- .‍text-size-tiny

### Text-style

Utility classes for text styles

- .text-style-normal
- .‍text-style-italic
- .‍text-style-link
- .‍text-style-caps
- .text-style-lower
- .‍text-style-nowrap
- .‍text-style-quote
- .‍text-style-strike
- .‍text-style-underline

### Text-weight

Utility classes for text weight

- .text-weight-xbold
- .text-weight-bold
- .text-weight-semibold
- .text-weight-normal
- .text-weight-thin
- .text-weight-light

## SPACING

### Margin size

- .‍margin-0
- .margin-tiny
- .margin-xxsmall
- .margin-xsmall
- .margin-small
- .margin-medium
- .margin-large
- .margin-xlarge
- .margin-xxlarge
- .margin-huge
- .margin-xhuge
- .margin-xxhuge
- .margin-custom1
- .margin-custom2
- .margin-custom3

### Margin direction

- .‍margin-top
- .margin-bottom
- .margin-left
- .margin-right
- .margin-horizontal
- .margin-vertical

### Padding Direction

- .padding-top
- .padding-bottom
- .padding-left
- .padding-right
- .padding-horizontal
- .padding-vertical

### Padding Size

- .padding-0
- .padding-tiny
- .padding-xxsmall
- .padding-xsmall
- .padding-small
- .padding-medium
- .‍padding-large
- .padding-xlarge
- .padding-xxlarge
- .padding-huge
- .padding-xhuge
- .‍padding-xxhuge
- .padding-custom1
- .padding-custom2
- .padding-custom3

## OTHER UTILITY CLASSES

### Responsive Hide

- .hide - hides on all devices
- .hide-tablet - hides element on tables and smaller
- .hide-mobile-landscape - hides elements on mobile landscape and smaller
- .hide-mobile-portrait - hides elements on mobile portrait

### Flex

- .display-inlineflex:

The inline version of flex allows the element, and it's children, to have flex properties while still remaining in the regular flow of the document/webpage. Basically, you can place two inline flex containers in the same row, if the widths were small enough, without any excess styling to allow them to exist in the same row. This is pretty similar to "inline-block."

- .display-flex:

The container and it's children have flex properties but the container reserves the row, as it is taken out of the normal flow of the document. It responds like a block element, in terms of document flow. Two flexbox containers could not exist on the same row without excess styling.

### Max Width

Add max-width to any element on the page, primarily children in a container
Use container-[size] classes to set the width of the container

- .‍max-width-xxlarge
- .max-width-xlarge
- .max-width-large
- .max-width-medium
- .max-width-small
- .max-width-xsmall
- .max-width-xxsmall

#### Max Width Full

Sets max-width: none.

- .‍max-width-full - sets max-width to none
- .max-width-full-tablet - sets max-width to none on tablet
- .max-width-full-mobile-landscape - sets max-width to none on landscape
- .max-width-full-mobile-portrait - sets max-width to none on portrait

### Others

- .z-index-1 - setsz-index: 1
- .z-index-2 - sets z-index: 2
- .align-center - sets margin-left and margin-right to auto, centers an element inside its parent div.
- .layer - sets position: absolute with 0% on all sides. Add this class to a div to make it expand the entire size of the parent element. Make sure the parent div has a position that is any other than static.
- .pointer-events-none - sets pointer-events: none, which prevents all click and hover interaction with an element.
- .pointer-events-auto - sets pointer-events: auto, which enables all click and hover interaction with an element
- .overflow-hidden - sets overflow: hidden
- .overflow-scroll - sets overflow: scroll
- .overflow-auto - sets overflow: auto
- .aspect-ratio-square - sets aspect-ratio: 1 / 1
- .aspect-ratio-portrait - sets aspect-ratio: 2 / 3
- .aspect-ratio-landscape - sets aspect-ratio: 3 / 2
- .aspect-ratio-widescreen - sets aspect-ratio: 16 / 9

## COLORS

Colors will require some leg work to initialize.
Most of the coloring set-up will be in the :root selector. This way the color variables will be accessible to every element that may need them.

Out of the box, the color system responds to user device preference:

```scss
@media (prefers-color-scheme: dark) {
  :root {
    background-color: #212121;
    color: #fafafa;
  }
}
```

### Palette

Palettes will lay out every possible color your design may use and set them as variables to reuse. Your pallet may only use 3 or 4 colors, or hundreds. I recomend using a token-weight naming convention to distinguish the colors:

```scss
:root {
  //NEUTRALS
  --outerspace-100: hsl(210, 10%, 96%);
  --outerspace-200: hsl(210, 10%, 84%);
  --outerspace-300: hsl(208, 10%, 72%);
  --outerspace-400: hsl(210, 10%, 60%);
  --outerspace-500: hsl(211, 10%, 48%);
  --outerspace-600: hsl(213, 10%, 36%);
  --outerspace-700: hsl(210, 10%, 24%);
  --outerspace-800: hsl(210, 10%, 12%);
  --outerspace-900: hsl(225, 13%, 6%);

  //SECONDARY
  --cadet-100: hsl(180, 14%, 96%);
  --cadet-200: hsl(180, 15%, 84%);
  --cadet-300: hsl(182, 21%, 73%);
  --cadet-400: hsl(180, 15%, 72%);
  --cadet-500: hsl(180, 15%, 60%);
  --cadet-600: hsl(180, 15%, 48%);
  --cadet-700: hsl(182, 16%, 37%);
  --cadet-800: hsl(182, 22%, 26%);
  --cadet-900: hsl(180, 15%, 12%);

  //BRAND
  --bluey-100: hsl(193, 90%, 96%);
  --bluey-200: hsl(193, 90%, 84%);
  --bluey-300: hsl(193, 90%, 72%);
  --bluey-400: hsl(193, 90%, 60%);
  --bluey-500: hsl(193, 90%, 48%);
  --bluey-600: hsl(193, 90%, 36%);
  --bluey-700: hsl(193, 90%, 24%);
  --bluey-800: hsl(193, 90%, 12%);
  --bluey-900: hsl(193, 90%, 4%);

  //ACCENT
  --cosmic-100: hsl(280, 90%, 96%);
  --cosmic-200: hsl(280, 90%, 84%);
  --cosmic-300: hsl(280, 90%, 72%);
  --cosmic-400: hsl(280, 90%, 60%);
  --cosmic-500: hsl(280, 90%, 48%);
  --cosmic-600: hsl(280, 90%, 36%);
  --cosmic-700: hsl(280, 90%, 24%);
  --cosmic-800: hsl(280, 90%, 12%);
  --cosmic-900: hsl(280, 90%, 4%);

  //UI
  --alert: hsl(338, 62%, 48%);
  --warning: hsl(39, 100%, 50%);
  --success: hsl(120, 100%, 25%);
  --info: hsl(240, 100%, 50%);
  --error: hsl(0, 100%, 50%);
  --white: hsl(210, 10%, 96%);
  --black: hsl(225, 13%, 6%);
}
```

### Themeing

This is where colors can get a little tricky. This can be as simple or as complicated as you need. First we define our base theme:

```scss
:root {
  /****** Background Color ******/

  --bg-color-100: var(--outerspace-100);
  --bg-color-200: var(--outerspace-200);
  --bg-color-300: var(--outerspace-300);
  /* add as nessesary */

  --bg-color-alt-100: var(--cadet-600);
  --bg-color-alt-200: var(--cadet-700);
  /* add as nessesary */

  /****** Main colors ******/

  --text-color-100: var(--outerspace-900);
  --text-color-200: var(--outerspace-800);
  --text-color-300: var(--outerspace-700);

  --brand-color-300: var(--bluey-300);
  --brand-color-400: var(--bluey-400);
  --brand-color-500: var(--bluey-500);
  --brand-color-600: var(--bluey-600);
  --brand-color-700: var(--bluey-800);

  --accent-color-300: var(--cosmic-300);
  --accent-color-400: var(--cosmic-400);
  --accent-color-500: var(--cosmic-500);
  --accent-color-600: var(--cosmic-600);
  --accent-color-700: var(--cosmic-700);
}
```

Then we will adjust for the dark theme: This can be a whole new set of colors, or just reversing the weight values:

```scss
:root {
  @media (prefers-color-scheme: dark) {
    /****** Background Color ******/

    --bg-color-100: var(--outerspace-900);
    --bg-color-200: var(--outerspace-800);
    --bg-color-300: var(--outerspace-700);
    /* add as nessesary */

    --bg-color-alt-100: var(--cadet-200);
    --bg-color-alt-200: var(--cadet-300);
    /* add as nessesary */

    /****** Main colors ******/

    --text-color-100: var(--outerspace-100);
    --text-color-200: var(--outerspace-200);
    --text-color-300: var(--outerspace-700);

    --brand-color-300: var(--cosmic-700);
    --brand-color-400: var(--cosmic-600);
    --brand-color-500: var(--cosmic-500);
    --brand-color-600: var(--cosmic-400);
    --brand-color-700: var(--cosmic-300);

    --accent-color-300: var(--bluey-700);
    --accent-color-400: var(--bluey-600);
    --accent-color-500: var(--bluey-500);
    --accent-color-600: var(--bluey-400);
    --accent-color-700: var(--bluey-300);
  }
}
```

### Using Colors

There are several methods used to set your colors:

1. Element Selectors
2. Custom Classes
3. Scoped Styles

#### Set Colors with Element Selectors:

Target global selectors and set the colors

```scss
body {
  background-color: var(--bg-color-100);
}
h1. h2,
h3,
h4,
h5,
h6,
p {
  color: var(--text-color-100);
}
```

#### Custom Color Classes

Set up custom classes to style items on the fly:

```scss
.text-color-100 {
  color: var(--text-color-100);
}
```

#### Scoped Colors:

Depending on your framework you can override colors in various ways. Refer to your framework docs on Scoped Style.

Otherwise, use inline styles or ID selectors to override colors as needed.
