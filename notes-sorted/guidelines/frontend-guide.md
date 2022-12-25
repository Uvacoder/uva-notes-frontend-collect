# Frontend Guidelines
A one-page document to help your team establish effective frontend guidelines, so that you can write consistent & cohesive code together.

## HTML
## HTML Principles
- **What are some general principles your team should follow when writing HTML?** *(for example, authoring semantic HTML5 markup, accessibility, etc. See [these](http://www.yellowshoe.com.au/standards/#html) [resources](http://codeguide.co/#html) for [inspiration](http://manuals.gravitydept.com/code/html))*


## HTML Tools
- **Sass preprocessor** and **SCSS syntax** for stylesheet files, using `.scss` extension
- **[Nunjucks](https://mozilla.github.io/nunjucks/)** for templating engine
- **Gulp** to run a helpful tasks such as: compiling your Sass files to CSS, processing assets files (JS, images,icons), optimizing and building files for production and more
- **[Fractal](https://fractal.build)** for components library and style guide

## HTML Style
- Indent yout code using 2 spaces, not tabs
- Use comments carefully defining start and end of a block in a way like: `<!-- BLOCK NAME - Start --> <!-- BLOCK NAME - End -->`

---------------

## CSS

## Principles
- **What are some general principles your team should follow when writing CSS?** *(For example, modularity, avoiding long selector strings, etc. See [these](http://cssguidelin.es/) [resources](http://www.yellowshoe.com.au/standards/#css) [for](http://manuals.gravitydept.com/code/css) [inspiration](http://codeguide.co/#css))*

## Methodology
We adopt [BEM](https://en.bem.info/method/) methodology.
- **Are you deviating from the methodology in any way?** If so, can you highlight these conventions?

## Tools
- **Is the team using a preprocessor** *(such as [Sass](http://sass-lang.com/) or [Less](http://lesscss.org/))*?
- **What are the guidelines for using that preprocessor** *(check out [Sass Guidelines](https://sass-guidelin.es/) for inspiration)*?
- **Are you using a CSS base** *(such as [Normalize](https://necolas.github.io/normalize.css/) or a [reset](http://meyerweb.com/eric/tools/css/reset/))*?
- **Are you using any CSS postprocessors** *(such as [Prefixfree](https://leaverou.github.io/prefixfree/) or [Autoprefixer](https://github.com/postcss/autoprefixer))*?
- **Are there specific CSS techniques you're utilizing** *(such as [critical CSS](https://www.smashingmagazine.com/2015/08/understanding-critical-css/))*?


## Syntax

1. [Intending](#indenting)
2. [Declaration sorting](#declaration-sorting)
3. [Encoding](#encoding)

### Common rules
- two (2) spaces indents, no tabs;
- 80-characters wide lines;
- *one space* before the opening brace of declaration blocks for legibility
- Place closing braces of declaration blocks on a new line
- Include one space after `: `for each declaration
- Each declaration should appear on its own line for more accurate error reporting
- End all declarations with `;`. The last declaration's is optional, but your code is more error prone without it.
- Comma-separated property values should include a space after each comma
- Lowercase all hex values, e.g., `#fff`
- Use shorthand hex values where available, e.g., `#fff` instead of `#ffffff`.


```css
/* Bad CSS */
.selector, .selector-secondary, .selector[type=text] {
  padding:15px;
  margin:0px 0px 15px;
  background-color:rgba(0, 0, 0, 0.5);
  box-shadow:0px 1px 2px #CCC,inset 0 1px 0 #FFFFFF
}

/* Good CSS */
.selector,
.selector-secondary,
.selector[type="text"] {
  padding: 15px;
  margin-bottom: 15px;
  background-color: rgba(0,0,0,.5);
  box-shadow: 0 1px 2px #ccc, inset 0 1px 0 #fff;
}
```

### Declaration sorting
Related property declarations should be grouped together following the order:
1. Positioning
2. Box model
3. Typographic
4. Visual
5. Misc

```scss
.declaration-order {
  /* Positioning */
  position: absolute;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  z-index: 100;

  /* Box-model */
  display: block;
  float: right;
  width: 100px;
  height: 100px;

  /* Typography */
  font: normal 13px "Helvetica Neue", sans-serif;
  line-height: 1.5;
  color: #333;
  text-align: center;

  /* Visual */
  background-color: #f5f5f5;
  border: 1px solid #e5e5e5;
  border-radius: 3px;

  /* Misc */
  opacity: 1;
}
```

Positioning comes first because it can remove an element from the normal flow of the document and override box model related styles. The box model comes next as it dictates a component's dimensions and placement.

Everything else takes place inside the component or without impacting the previous two sections, and thus they come last.

Use [PostCSS VSCode Plugin](https://github.com/hudochenkov/postcss-sorting#options) to automatically sorting your code with [this configuration](postcss-settings.json). Copy settings in your VSCode *settings.json*.


### Indenting
When indenting in Sass, stick **two(2) spaces** and **leave a blank line** before and after the nested ruleset:
```scss
foo {
  color: red;

  .bar {
    color: blue;
  }

}
```

### Selector Nesting in Sass
**Avoid selector nesting as much as possible.** The problme is that it makes code more difficult to read.
- Don't nest more than 3 leves deep, following the [Inception Rule](http://thesassway.com/beginner/the-inception-rule)
- Use along with BEM naming convention to generate `.block_element`



### Encoding
To avoid any potential issue with character encoding, it is highly recommended to force UTF-8 encoding in the main stylesheet using the @charset directive. Make sure it is the very first element of the stylesheet and there is no character of any kind before it.
```css
@charset 'utf-8'
```

### Quotes
Wrap Sass strings in single quotes.
```scss
// Yep
$direction: 'left';

// Nope
$direction: left;
```

### Strings as CSS values
Specific CSS values (identifiers) such as initial or sans-serif require not to be quoted
```scss
// Yep
$font-type: sans-serif;

// Nope
$font-type: 'sans-serif';
```

### Strings containing quotes
If a string contains one or several single quotes, one might consider wrapping the string with double quotes (") instead, in order to avoid escaping characters within the string.

```scss
// Yep
@warn "You can't do that.";
```

### URLs
URLs should be quoted as well, for the same reasons as above:
```scss
// Yep
.foo {
  background-image: url('/images/kittens.jpg');
}

// Nope
.foo {
  background-image: url(/images/kittens.jpg);
}
```

### Units & Numbers
- Numbers shouldn't display leading zeros before a decimal value less than one. 
- When dealing with lengths, a `0` value should never ever have a unit (e.g., `margin: 0;` instead of `margin: 0px;`)
- Don't prefix property values or color parameters with a leading zero (e.g., `.5` instead of` 0.5` and `-.5px` instead of `-0.5px`)
```scss
// Yep
.foo {
  padding: 2em;
  opacity: .5;
  margin: 0;
}

// Nope
.foo {
  margin: 0em;
  padding: 2.0em;
  opacity: 0.5;
}
```

#### Calculations
Top-level numeric calculations should always be wrapped in parentheses.
```scss
// Yep
.foo {
  width: (100% / 3);
}

// Nope
.foo {
  width: 100% / 3;
}
```

### Colors
Respect the following order of preference for color formats:

1. HSL notation;
2. RGB notation;
3. HEX notation (lowercase and shortened);

```scss
// Yep
.foo {
  color: hsl(0, 100%, 50%);
}

// Also yep
.foo {
  color: rgb(255, 0, 0);
}

// Meh
.foo {
  color: #f00;
}

// Nope
.foo {
  color: #FF0000;
}

// Nope
.foo {
  color: red;
}
```
When using HSL or RGB notation, always add a single space after a comma (,) and no space between parentheses ((, )) and content.
```scss
// Yep
.foo {
  color: rgba(0, 0, 0, 0.1);
  background: hsl(300, 100%, 100%);
}

// Nope
.foo {
  color: rgba(0,0,0,0.1);
  background: hsl( 300, 100%, 100% );
}
```

#### Color Variables

Store color variables in another variable with a name explaining how it should be used:
```scss
$main-theme-color: $sass-pink;
```

#### Maps
Maps should be written as follows:

- space after the colon (:);
- opening brace (() on the same line as the colon (:);
- quoted keys if they are strings (which represents 99% of the cases);
- each key/value pair on its own new line;
- comma (,) at the end of each key/value;
- trailing comma (,) on last item to make it easier to add, remove or reorder items;
- closing brace ()) on its own new line;
- no space or new line between closing brace ()) and semi-colon (;).
```scss
// Yep
$breakpoints: (
  'small': 767px,
  'medium': 992px,
  'large': 1200px,
);

// Nope
$breakpoints: ( small: 767px, medium: 992px, large: 1200px );
```


---------------

## JavaScript

### JavaScript Principles
- **What are some general principles your team should follow when writing JavaScript?** *(See [these](https://github.com/airbnb/javascript) [resources](https://github.com/rwaldron/idiomatic.js) for [inspiration](https://github.com/styleguide/javascript))*


### JavaScript tools
- **Are you using a JavaScript framework** *(such as [jQuery](https://jquery.com/), [Ember](http://emberjs.com/), [Angular](https://angularjs.org/), etc)*?
- **Where is the documentation for those frameworks?**
- **Are you using any polyfills or shims** *(such as [any of these](https://github.com/Modernizr/Modernizr/wiki/HTML5-Cross-Browser-Polyfills))*?
- **What third-party scripts are dependencies for your project** *(such as scripts for form validation, graphs, animation, etc)*?
- **Do you test your JavaScript?** If so, what tools do you use *(such as [Jasmine](https://jasmine.github.io/), [Karma](https://github.com/karma-runner/karma), [Selenium](http://docs.seleniumhq.org/), etc)*?

### JavaScript Style 
*(See [these](https://github.com/airbnb/javascript) [resources](https://github.com/rwaldron/idiomatic.js) for [inspiration](https://github.com/styleguide/javascript))*
- **Spaces or Tabs?**
- **What does JS commenting look like?** 
- **What patterns are you following?** *(See [these](https://addyosmani.com/resources/essentialjsdesignpatterns/book/) [resources](https://shichuan.github.io/javascript-patterns/))*

---------------

## Media
- **How are you handling icons** *(such as using SVG, icon fonts, etc)*?
- **How are you handling responsive images** *(such as using `srcset` & `<picture />`)*?
- **Are you using any [tools](https://addyosmani.com/blog/image-optimization-tools/) to optimize and serve images**?

---------------

## Fonts
- **How do you load custom fonts?**
- **Do you use any tools to help implement web fonts** *(such as [Font Squirrel](https://www.fontsquirrel.com/), etc)*?
- **Do you use a service to manage and serve custom fonts** *(such as [Fonts.com](https://www.fonts.com/), [Typekit](https://typekit.com/), etc)*?


---------------

## Performance
- **Do you use performance budgets?** If so, what [metrics](https://timkadlec.com/2014/11/performance-budget-metrics/) are you using to determine budgets? Where are you keeping track of performance budgets?
- **How are you measuring your project's speed** *(such as [Pingdom Speed Test](http://tools.pingdom.com/) or [Google PageSpeed](https://developers.google.com/speed/pagespeed/))*?
- **What techniques are you using to decrease file size** *(such as [Gzip](https://css-tricks.com/snippets/htaccess/active-gzip-compression/), [Image Optimization](https://developers.google.com/web/fundamentals/performance/optimizing-content-efficiency/image-optimization))*?
- **What performance-related tools are you using in your workflow?** *(such as [WebPagetest](http://www.webpagetest.org/), [BigRig](https://aerotwist.com/blog/bigrig/) [Speedcurve](https://speedcurve.com/))*?


---------------

## Accessibility
- **Are you following the accessibility recommendations laid out in [this checklist](http://a11yproject.com/checklist.html)?**
- **What accessibility-related [tools](http://a11yproject.com/resources.html) are you using in your workflow?**

---------------

## Tooling
- **Are you using a task runner** *(such as [Grunt](http://gruntjs.com/) or [Gulp](http://gulpjs.com/))*?
- **Are you using a dependency manager** *(such as [Bower](http://bower.io/) or [Composer](https://getcomposer.org/))*?
- **Are you using any scaffolding tools** *(such as [Yeoman](http://yeoman.io/))*?
- **Are you using any tools to reinforce frontend style** *(such as [Editor Config](http://editorconfig.org/) or [linters](https://github.com/CSSLint/csslint))*?
- **Are any other specific pieces of software that are needed to work on this project?**

---------------

## Version control
- **What version control system are you using for your frontend code** *(such as [Git](https://git-scm.com/) or [Subversion](https://subversion.apache.org/))*?
- **Where is your version-controlled code hosted** *(such  as [Github](https://github.com/) or [Bitbucket](https://bitbucket.org/))*?
- **Do you use a version control workflow** *(such as [gitflow](http://nvie.com/posts/a-successful-git-branching-model/), [centralized](https://www.atlassian.com/git/tutorials/comparing-workflows/centralized-workflow), [feature-branch](https://www.atlassian.com/git/tutorials/comparing-workflows/feature-branch-workflow), etc)*?
- **Who's responsible for managing and governing the version controlled code?**?
- **Where are issues tracked?**

-----------

## Support and Optimization
It's important to recognize the difference between ["support" and "optimization"](http://bradfrost.com/blog/mobile/support-vs-optimization/). You should do your best to support as many environments as possible while simultaneously optimizing for the environments that make the most sense for your business and users. 

- **What browsers are you *optimizing* for?** 
- **What devices are you *optimizing* for?** 
- **Are you using a [graded browser support](https://github.com/yui/yui3/wiki/Graded-Browser-Support) system?**
- **Are there specific components that require [more specific grading](https://www.filamentgroup.com/lab/grade-the-components.html)?** 

-----------

## Localization
- **Is your website served in different languages?** If so, what considerations do you need to address when localizing for other languages?

-----------

## Deployment/Integration
- **How is your front-end code integrated into a production environment?**

-----------

## Documentation
- **Are you using a [pattern library tool](http://styleguides.io/tools.html) to document your front-end architecture?**
- **Where does your documentation live?** What are the links to the documentation?
- **Who's responsible for maintaining and governing the documentation?**
- **What happens when the guidelines are updated?**

-----------

*Feel free to modify or extend (such as adding specific sections for performance, accessibility, etc) this document for your own organization's needs. For questions, comments, additions, and corrections, please open an issue on Github and/or reach out to [@brad_frost](https://twitter.com/brad_frost) on Twitter.*
