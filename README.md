# Best time proven CSS practices 
Here you can read my own list of advice for UI developers, that will bring you to the next level of coding.

## Use ems instead of pixels
Seriously. Stop coding like it's still 1990s. Using pixels is so much extra work for a developer.
Ems let you control the component size with one line of code, so you don't need to override each property for each element inside the component.
It saves hours and hours of your time.
Imagine you have a small statistics block like this https://www.screencast.com/t/2h2GaoYZF7Z2
You did all the CSS than the client tells you that he wants this block to be also used on another page, but it should be 2 times bigger.
If you use pixels, then you need to create a modifier for this block and override all sizes.
But, if you used em, you only need to create modifier and write 1 line of code - "font-size: 2em". That's it.
Each time you need something sized differently - you write 1 line of code.
You can even resize the whole site if you want to. So use pixels for borders and shadows and leave everything else for em.

## Use icon fonts or any other working vector solutions
Using raster icons, such as PNG is a very outdated and time-consuming approach. It becomes evident when the client asks you to change icon size or color and you have to draw it again or ask a designer to do it.
It is preferable to use vector icons, such as SVG or icon fonts, where you can change size or color with one line of CSS code.
I find it more comfortable to use icon fonts because they are easy to use, well supported and do not require any javascript. You can generate your own icon font from SVG icons using IconMoon web app. 

## Use classes instead of element selectors and IDs
Do not add style to element selectors, like form, article, ul, a and others (normalize CSS is an exception).
This clutters the global namespace and you come up with a situation, where you add pure html element to the page and it gets cluttered with a bunch of styles from other pages and components and you'll have to override them.
This turns the project into developer's hell. But you can avoid it by using unique class names.

## Don't go crazy with ruleset nesting
Ruleset nesting in CSS is bad for many reasons.
It slows down CSS parsing, makes CSS dependent on markup structure and makes your code not reusable.
So this is bad:

    .menu-list {
        list-style-type: none;
        padding-left: 0;

        .menu-list__item {
            border-bottom: 1px solid #ccc;

            .menu-list__item-icon {
                color: var(--text-color-base);

                &:hover {
                    color: var(--text-color-primary);
                    text-decoration: none;
                }
            }
        }

        &.is-open {
            height: auto;
        }
    }

This is a bit better because generated CSS will be flat. But searching for ".menu-list__item" will give you 0 results:

    .menu-list {
        list-style-type: none;
        padding-left: 0;

        &__item {
            border-bottom: 1px solid #ccc;
        }

        &__item-icon {
            color: var(--text-color-base);

            &:hover {
                color: var(--text-color-primary);
                text-decoration: none;
            }
        }

        &.is-open {
            height: auto;
        }
    }

This is much better:

    .menu-list {
        list-style-type: none;
        padding-left: 0;

        &.is-open {
            height: auto;
        }
    }

    .menu-list__item {
        border-bottom: 1px solid #ccc;
    }

    .menu-list__item-icon {
        color: var(--text-color-base);

        &:hover {
            color: var(--text-color-primary);
            text-decoration: none;
        }
    }

## Use CSS Variables
They’re live, native and already well supported so I highly recommend start using them now!
https://www.jonathan-harrell.com/unlocking-benefits-css-variables/

## Use BEM
BEM turned out to be the best CSS methodology for any project, no matter small or big.
Personally, I use the simplified version, that covers the basics of BEM usage.
Follow this link for details https://ru.bem.info/methodology/quick-start/

## USE namespacing prefixes
Namespacing makes code readable and clear. And they're also are the lifesavers when you have to redesign old project with a clattered global namespace.
E.g. once you add a ".button" or ".modal" element to the page you are redesigning, they instantly get old styles you don't need. Adding "c-" prefix to them saves the situation, because ".c-button" does not exist in old stylesheets and you can style from scratch.
Common prefixes are:
- Component	[c-]  like "c-card, c-checklist". Form the backbone of an application and contain all of the cosmetics for a standalone component.
- Layout module	[l-] like "l-grid l-container". These modules have no cosmetics and are purely used to position c- components and structure an application’s layout.
- Helpers	[h-] like "h-show h-hide". These utility classes have a single function, often using !important to boost their specificity. (Commonly used for positioning or visibility.)
- States	[is- / has-] like "is-visible has-loaded". Indicate different states that a component can have.

There are more prefix types and you always can add more or made up your own.

## Separate component styles from its layout
What it means is that you need to add extra markup around component to set its layout.
For example, you have a reusable navigation component and you want to position its items vertically:

    <div class="l-nav">
        <ul class="c-nav-list">
            ...
        </ul>
    </div>

    .l-nav .c-nav-list__item {
        display: block;
        width: 100%;
    }

If this list needs to look different in another page or block, just change the layout markup. No need for styles overriding.

## Use helpers and modifiers
Imagine you have similar looking forms with different contents used all over the site.
Most forms have a button, but each time the button background/size/positioning is a bit different for design needs.
You can use BEM mix and add "c-signup-form__btn" to style the button, but in this case, it is better not to tie button modifications to a particular form, but create modifiers and helpers to that can be reused when needed. BEM mixes are good when the styles are component specific, and won't be reused in other components.
Look at this button:

    <button type="submit" class="c-btn c-btn--primary c-btn--bold c-btn--width-xl h-marg-v-20">Next</button>

It has 3 reusable modifiers and one helper, that sets vertical margins to 2em. You don't have to copy and paste the same set of styles from form to form.
I took these approaches from BEM and Atomic CSS methodologies.

Here is my LESS mixin that generates spacing helpers:

    //Margins and Paddings
    .spacer-loop(@i) when (@i >= 0) {
        .spacer-loop((@i - 1)); // next iteration
        .h-marg-l-@{i} {
            margin-left: (0em + (0.1*@i)) !important;
        }

        .h-marg-r-@{i} {
            margin-right: (0em + (0.1*@i)) !important;
        }

        .h-marg-t-@{i} {
            margin-top: (0em + (0.1*@i)) !important;
        }

        .h-marg-b-@{i} {
            margin-bottom: (0em + (0.1*@i)) !important;
        }

        .h-marg-v-@{i} {
            margin-top: (0em + (0.1*@i)) !important;
            margin-bottom: (0em + (0.1*@i)) !important;
        }

        .h-marg-h-@{i} {
            margin-left: (0em + (0.1*@i)) !important;
            margin-right: (0em + (0.1*@i)) !important;
        }

        .h-marg-all-@{i} {
            margin: (0em + (0.1*@i)) !important;
        }

        .h-pad-l-@{i} {
            padding-left: (0em + (0.1*@i)) !important;
        }

        .h-pad-r-@{i} {
            padding-right: (0em + (0.1*@i)) !important;
        }

        .h-pad-t-@{i} {
            padding-top: (0em + (0.1*@i)) !important;
        }

        .h-pad-b-@{i} {
            padding-bottom: (0em + (0.1*@i)) !important;
        }

        .h-pad-v-@{i} {
            padding-top: (0em + (0.1*@i)) !important;
            padding-bottom: (0em + (0.1*@i)) !important;
        }

        .h-pad-h-@{i} {
            padding-left: (0em + (0.1*@i)) !important;
            padding-right: (0em + (0.1*@i)) !important;
        }

        .h-pad-all-@{i} {
            padding: (0em + (0.1*@i)) !important;
        }
    }

    .spacer-loop(30); // launch the loop


## Split your LESS files into smaller
For example, you have site.less or whatever where you put all your components styles. It'll become bigger with time and you're gonna have to use search tool for finding the component you need.
Searching will be easier if you move each component style into a separate file like "c-button", "c-product", etc. Splitting mixins, helpers and variables files would also be usable.
Third-party component overrides should be stored in third-party.less file. 


# Syntax and Formatting
Сode that looks clean feels clean. It is a much nicer environment to work in and prompts other team members to maintain the standard of cleanliness that they found. The gly code sets a bad precedent.

High-level recommendations:

- two (2) space indents, no tabs;
- 80 character wide columns;
- multi-line CSS;
- meaningful use of whitespace.

## 80 Characters Wide
Where possible, limit CSS files’ width to 80 characters. Reasons for this include:

- the ability to have multiple files open side by side;
- viewing CSS on sites like GitHub, or in terminal windows;
- providing a comfortable line length for comments.

There will be unavoidable exceptions to this rule—such as URLs, or gradient syntax—which shouldn’t be worried about.


## Titling
Begin every new major section of a CSS project with a title:

    /*------------------------------------*\
      #SECTION-TITLE
    \*------------------------------------*/

    .selector { }    

The title of the section is prefixed with a hash (#) symbol to allow us to perform more targeted searches: instead of searching for just SECTION-TITLE which may yield many results — a more scoped search of #SECTION-TITLE should return only the section in question.

Leave a carriage return between this title and the next line of code (be that comment, some Sass, or some CSS).

If you are working on a project where each section is its own file, this title should appear at the top of each one. If you are working on a project with multiple sections per file, each title should be preceded by five (3) carriage returns. This extra whitespace coupled with a title makes new sections much easier to spot when scrolling through large files:

    /*------------------------------------*\
      #A-SECTION
    \*------------------------------------*/

    .selector { }



    /*------------------------------------*\
    #ANOTHER-SECTION
    \*------------------------------------*/

    /**
    * Comment
    */

    .another-selector { }

## Multi-line CSS
CSS should be written across multiple lines. There are a number of benefits to this:

 - A reduced chance of merge conflicts, because each piece of functionality exists on its own line.
 - More "truthful" and reliable diffs, because one line only ever carries one change.

 Exceptions to this rule should be fairly apparent, such as similar rulesets that only carry one declaration each, for example:

    .icon {
        display: inline-block;
        width:  16px;
        height: 16px;
        background-image: url(/img/sprite.svg);
    }

    .icon--home     { background-position:   0     0  ; }
    .icon--person   { background-position: -16px   0  ; }
    .icon--files    { background-position:   0   -16px; }
    .icon--settings { background-position: -16px -16px; }

These types of ruleset benefit from being single-lined because:

 - they still conform to the one-reason-to-change-per-line rule;
 - they share enough similarities that they don’t need to be read as thoroughly as other rulesets—there  - is more benefit in being able to scan their selectors, which are of more interest to us in these cases.

 ## Meaningful Whitespace
 - One (1) empty line between closely related rulesets.
 - Five (3) empty lines between entirely new sections.

 For example:

    /*------------------------------------*\
    #FOO
    \*------------------------------------*/

    .foo { }

    .foo__bar { }



    /*------------------------------------*\
    #BAR
    \*------------------------------------*/

    .bar { }

    .bar__baz { }

    .bar__foo { }
