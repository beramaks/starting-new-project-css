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
