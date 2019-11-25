# Frontend Guidelines Questionnaire
A one-page questionnaire to help your team establish effective frontend guidelines, so that you can write consistent & cohesive code together.

## HTML

Liberally "borrowing" from [Gravity Depot's HTML Manual](https://manuals.gravitydept.com/code/html/)

## HTML Style

### Formatting
Tag names and attributes should always be lowercase. Attribute values should use double quotes.

```html
<img src="image.png" alt="My Image with a thing happening">
```

### Attributes
When your element has more than 3 or so attributes, it might be a good idea to break the attributes into separate lines for readability and source control tracking.

```html
<button
  type="button"
  class="button"
  id="coordinates-button"
  data-loading="Loading..."
  data-x="123"
  data-y="789"
>
  Send Coordinates
</button>
```
### Indentation

Let's argue

### Closing tags

Always close tags, even when they're optional (`<ul>`, `<li>`)

Don't add closing `/`s to "void" elements (unless your template language requires it). They are no longer needed. 

```html
<img>
<!-- not -->
<img />
```

### Comments

Although it is fine to use HTML comments, if your template language allows it, try to use comments that that won't render in the final HTML. 

That being said, comment if you feel it's necessary to provide context or help visually identify blocks when debugging.

*Be mindful that HTML comments are possible visible to the user.*

If you're using comments to temporarily "Comment Out" something, try to remember to remove that thing later if no longer needed (once the task is nearing completion).

### Nesting, line breaks, and indenting

Indenting nested elements in your HTML is usually preferable, but elements with little content and no attributes are an exception.

```html
<p>The quick brown fox jumps.</p>

<!-- vs -->

<p class="lead">
    The quick brown fox jumps.
</p>
```

### Blank Lines

Use blank lines when some visual separation would aid in understanding the document, but stick to one or two lines so stylistic differences between team members doesn't lead to more confusion.

## HTML Principles

### HTML Semantics, Accessibility and Landmarks
HTML, as a content markup language, adds additional meaning to the content. An understanding of HTML elements and the meaning they add, is expected by HTML authors.  This is an ongoing process, there is not a minimum or maximum of required knowledge.

Although this is typically not visible to most users, it is integral to software, like browsers, web crawlers and screen readers (and other assistive technologies). 

All those authoring HTML should have an understanding of [HTML tags that imply structure and meaning](https://www.w3.org/TR/wai-aria-practices/examples/landmarks/HTML5.html). Using them correctly will correspond to common accessibility landmarks with no extra effort.

https://keithjgrant.com/posts/2018/03/html5-sectioning-and-landmark-elements/

http://html5doctor.com/avoiding-common-html5-mistakes/

### Use Appropriate Elements

The basics of semantic HTML is using the most appropriate element for the content. Familiarity with headings (`<h1>`), HTML5 elements (`<article> <aside> <figure> <figcaption> <header> <footer> <main> <nav> <section>`), and using the appropriate form elements is expected.

It is still encouraged to identify these elements with classes for styling, rather than relying on element selectors that could cause issues in the future.

For example, headings should be structured in a predictable 1-6 order, whereas the visual hierarchy put in place by the designer may not perfectly correspond.

### Enhancing with JavaScript

Although we'll discuss use of JavaScript more below, keep in mind that JavaScript is supposed to be an enhancement to the page, and any HTML that relies on it's functioning needs to have considerations regarding what happens when it doesn't work, and what elements are appropriate to use. 

Write as little markup in your JavaScript as possible. Putting markup in JS makes it harder to find and refactor.

#### Buttons vs Links

The anchor tag `<a>` is effectively invalid if it does not have a valid href attribute. Capturing the click of an anchor tag with JavaScript is inappropriate and bad for accessibility and SEO, unless it's specifically designed as a fallback. For instance, hijacking a link for tracking purposes is common (we usually let Google Tag Manager handle this), because in the end, we want the link to work like a link, and if JavaScript is unavailable, the link would still work. 

Setting a `#` as a self-referential, or fake, link should only be done for development purposes when you don't have the correct link yet, and not as a way to neuter a link you intend to hijack.

The `<button>` element is the correct element to use if you are wanting to capture clicks to fire off event handlers. There is some style baggage with buttons, but these can be overcome easily, and it is easier to add proper aria attributes for accessibility purposes. Just make sure if it is not a button that is submitting a form, that you add the "type" attribute (the default type is "submit"). 

```html
<button type="button"></button>
```

### Sections and Document Hierarchy

Landmark roles established with HTML should have their own heading hierarchy. 

```html
<div class="primary">
    <h1>Page Title</h1>

    <article>
        <h1>Article Title</h1>
        <p>Llorem ipsum dolor sit amet.</p>

        <h2>Article Subtitle</h2>
        <p>Curabitur vulputate, ligula lacinia scelerisque tempor.</p>

        <h2>Article Subtitle</h2>
        <p>Curabitur vulputate, ligula lacinia scelerisque tempor.</p>
    </article>

    <article>
        <h1>Article Title</h1>
        <p>Nulla facilisi. Duis aliquet egestas purus in blandit.</p>
    </article>
</div>

<aside>
    <h1>Related Articles</h1>
    ...
</aside>
```

### HTML Structuring for styling

If everything goes correctly, we would be able to achieve our desired UI designs based on a purely semantic document structure. However, it's likely you will need to add extra `<div>`s and `<span>`s to help you properly and robustly style your content. 

These elements should be free of landmark roles. Never use something like a `<section>` or `<article>` just for styling. Ideally, if the UI were to be redesigned, these containers could be removed or reworked easily, without affecting any semantic meaning.

Do keep in mind that excessive DOM elements do affect browser performance, SEO, and accessibility. 

### Using IDs

Use IDs on major points of interest for hash linking purposes, especially on larger pages. But remember, IDs should be unique, and generally _NOT_ used for styling. 

They can also be used as javascript selectors, since if they are unique, the `getElementById` method is a reliable way to reference a single DOM node.

### HTML Meta tags

The following tags should be a part of all HTML documents.

- Doctype should be present on line 1: `<!doctype html>`
- HTML tag should have a lang attribute: `<html lang="en-us">`
- UTF-8 Character set should be set: `<meta charset="utf-8">`
- Viewport Meta should be set: `<meta name="viewport" content="width=device-width, initial-scale=1">`

### Including CSS and JS

Generally, CSS should be loaded in the head of your document via the `<link>` tag, and JS should be loaded via a `<script>` tag before the closing `</body>` tag. However, there are valid reasons to break this pattern.

CSS loading is render blocking, so delaying some of your less necessary CSS to later in the document is a valid approach.

Some JS must load in the head. Analytics often need this, as well as anything that manipulates the DOM on load, like `modernizr`. 

What's important is that you pay attention and only include items in head of the document that you absolutely need to.

### HTML Tools

There are currently no defined HTML preprocessor or templating engine do's or don'ts. Use Pug or Handlebars if you'd like.



- **Does your backend architecture influence the frontend markup in any way** (for example, WordPress will add `wp-paginate` to a class in your markup)? If so, can you highlight these conventions? 



---------------

## CSS 

### CSS Principles

#### Property ordering

No specific rules will be in place for the ordering of properties. However, there are some general guidelines that will make your code cleaner and easier to read. 

When using Scss, it is proper to nest pseudo classes, pseudo elements, and media queries, but put all of your properties above these, then list pseudo classes, then leave media queries for last. 

```scss
.class {
    property: value;
    property: value;
    property: value;

    &:hover {
        property: value;
    }

    &::after {
        property: value;
    }

    @media screen {
        property: value
    }
}
```

Always use two `::` for pseudo elements. 

Things aren't always this simple though, so just make sure you keep related things as close together as possible, even if it violates this ordering. 

#### Formatting

Add empty lines between declarations, unless they are closely related. 

```scss
.class1 {

}
.class1__item {

}
.class1--super {

}

.class2 {

}
```

Be consistent in spacing, it makes your code more predictable, readable, and searchable. 

- One space after selector
- Opening curly-bracket on the same line as the selector
- Closing bracket on new line
- One space after colon
- Semi-colon after every value

##### Good

```scss
.class {
    property: value;
}
```

##### Bad

```scss
.class{
    property:value;
}
```

Never put properties and all brackets on the same line! The only exception to this is when there is only one property in a declaration. 

##### Bad

```scss
.class { property: value; property: value; property: value; }
```

This ruins your git history and is generally hard to read.

##### OK, but not required or even necessarily encouraged

```scss
.class { property: value; }
```

When grouping selectors, break them into multiple lines to be more readable: 

```scss
.class1, 
.class2 {
    property: value;
}
```

In Attribute selectors, use single quotes, unless you can't...

```scss
[attr='value'] {}
[attr="When It's Necessary"] {}
```

Space around combinators:

```scss
.parent > .child {}
.sibling + .sibling {}
```



#### Commenting

When using Sass, most comment should be the `//` type. These do not get compiled to your final CSS. Standard CSS comments (`/* */`) do get compiled, so only include comments like this if you want them to be in the final CSS.

Add `*` for important comments, `!` for warnings, `?` for questions, `TODO` for todos. 

```scss
// * I'm important
// ! Watchout
// ? What is going on here?
// TODO I will do this someday
```

#### Naming

Detailed naming conventions are below under CSS Methodology. 

But for the basics, selectors, which means your classes as well, should always be lowercase and never being with an number.

#### Colors

If using Scss, try to always use variables for colors. The exception might be the named color `white`, because it's just white. 

// TODO examples, aliases

##### HEX, HSL, RGB, RGBA

There is no particular preference for how colors are set. It might have to do how the colors were specced by the designer. Remember, in Sass, these are often interchangeable. 

// TODO naming, spacing, using in Sass

- **What are some general principles your team should follow when writing CSS?** *(For example, modularity, avoiding long selector strings, etc. See [these](http://cssguidelin.es/) [resources](http://www.yellowshoe.com.au/standards/#css) [for](http://manuals.gravitydept.com/code/css) [inspiration](http://codeguide.co/#css))*

### CSS Methodology
- **Is your team using a CSS methodology** *(such as [SMACSS](https://smacss.com/), [BEM](https://en.bem.info/method/), or [OOCSS](http://oocss.org/))*? If yes, where is the documentation for that methodology?
- **Are you deviating from the methodology in any way?** If so, can you highlight these conventions?

### CSS Tools
- **Is the team using a preprocessor** *(such as [Sass](http://sass-lang.com/) or [Less](http://lesscss.org/))*?
- **What are the guidelines for using that preprocessor** *(check out [Sass Guidelines](https://sass-guidelin.es/) for inspiration)*?
- **Are you using a CSS base** *(such as [Normalize](https://necolas.github.io/normalize.css/) or a [reset](http://meyerweb.com/eric/tools/css/reset/))*?
- **Are you using any CSS postprocessors** *(such as [Prefixfree](https://leaverou.github.io/prefixfree/) or [Autoprefixer](https://github.com/postcss/autoprefixer))*?
- **Are there specific CSS techniques you're utilizing** *(such as [critical CSS](https://www.smashingmagazine.com/2015/08/understanding-critical-css/))*?

### Media Queries

### CSS Frameworks
- **Is the team using a framework** *(such as [Bootstrap](https://getbootstrap.com/) or [Foundation](http://foundation.zurb.com/))*? If yes, where is the documentation for that framework?
- **Are you deviating from the framework in any way?** If so, can you highlight these conventions?

### CSS Style
- **Spaces or Tabs?**
- **Spacing around rules?**
- **[Grouping](https://smacss.com/book/formatting#grouping) properties?**
- **What does CSS commenting look like?** 

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


From: https://yellowshoe.com.au/standards/#js

Best practices:

    Favour the framework & DRY
    Avoid inline & embedded js
    Keep global scope clean, put code into namespaces Page, Util, Controls
    Be defensive, feature detect
    Test performance in all browsers mentioned above - use console.time to track down bottlenecks.
    Minimise number of event listeners on a page, use event delegation
    Keep components as independent as possible
    var every variable 


Cookies - keep em small, they're sent every request

---------------

## Media
- **How are you handling icons** *(such as using SVG, icon fonts, etc)*?
- **How are you handling responsive images** *(such as using `srcset` & `<picture />`)*?
- **Are you using any [tools](https://addyosmani.com/blog/image-optimization-tools/) to optimize and serve images**?

### SVG

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




## Browser Support

## Testing
- 404
- my whole checklist