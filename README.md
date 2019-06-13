# Best time proven css practices 
Here you can read my own list of advice for UI developers, that will bring you to the next level of coding.

## Use ems instead of pixels
Seriously. Stop coding like it's still 1990s. Using pixels is so much extra work for a developer.
Ems let you control component size with one line of code, so you don't need to override each property for each element inside component.
It saves hours and hours of your time.

## Use icon fonts or any other working vector solutions
Using png icons is very outdated approach. It becomes a problem when client asks you to change icon size or color.
You need to draw it again or ask a designer to do it.
Using SVG icons is much better, especially when you use iconMoon app to generate your own icon font from them.

## Use classes instead of element selectors and IDs
Do not add style to element selectors, like form, article, ul, a and others (normalize css is exception).
This clutters the global namespace and you come up with a situation, where you add pure html element to the page and it gets cluttred with bunch of styles from other pages, that you'll have to override.
This turns project into developer's hell. But you can avoid it by using classes.

## Use BEM
BEM turned out to be the best css methodology for any project, no matter small or big.
Personally I use simplified version, that covers the basics of BEM usage.
Follow this link  for details https://ru.bem.info/methodology/quick-start/

## USE namespacing prefixes
- Component	[c- like c-card c-checklist] Form the backbone of an application and contain all of the cosmetics for a standalone component.
- Layout module	[l- like l-grid l-container] hese modules have no cosmetics and are purely used to position c- components and structure an application’s layout.
- Helpers	[h- like h-show h-hide] These utility classes have a single function, often using !important to boost their specificity. (Commonly used for positioning or visibility.)
- States	[is- / has-	like is-visible has-loaded]	Indicate different states that a c- component can have.

## Separate component positionong from its layout
Whan it means is that you need to add extra markup around componenrs to set its layout.
For example you have product card and you want to make a search results grid:

    <ul class="l-search-results-list">
        <li class="l-search-results-list__item">
            //Import c-producr card here
        </li>
        <li class="l-search-results-list__item">
            //Import c-producr card here
        </li>
    </ul>

If this list needs to look differently in another page or block, just change the layout. No need for stiles overriding.

## Use helpers and modifiers
Imagine you have similar looking forms with different contents used allover the site.
Most form has button, but each time the button background/size/positioning is a bit different for design needs.
You can use BEM mix and add "c-signup-form__btn" to style button's position, but i fing it more helpfull not to tie button modefecations to particular form, but create modifiers and helpers and reuse them when needed.
Look at this button:

    <button type="submit" class="c-btn c-btn--primary c-btn--bold c-btn--width-xl h-marg-v-20">Next</button>

It has 3 reusable modifiers and one helper, that sets vertical margins to 2em. You don't have to copy and paste same set of styles from form to form.
If you think it's a bad idea - read BEM and Atomic CSS. This approach is taken from these 2 methodologies.

##