# What is OffbeatWP

OffbeatWP is a component-based (more on this later) theming framework for Wordpress. But actually it's a bit more than that. It uses the most modern wordpress technologies including:

- Composer
- Dependency Injection (using [PHP-DI](http://php-di.org/))
- Webpack for compiling assets
- MVC (model-view-controller)

It's our mission to create a more professional and standardised way of developing Wordpress themes. Because Wordpress doesn't really guides you how to structure your theme, themes get's messy and every often really slow.

Besides of that every developer has it's own habits which makes it hard to onboard new developers on the project of transfer the codebase to another developer.

## For who is OffbeatWP

OffbeatWP is made for agencies and other profesionals who makes custom websites for themselfs and clients. Espessially when you have a website with a large codebase and a wide variety of post-types and taxonomies you will expierence OffbeatWP as a blessing.

If you are a creator of templates in order to sell theme (on ThemeForest for example) OffbeatWP is not (yet) the best choice because it doens't support child themes yet. 
 
## Component based

In a world where every pages on a website is a 'landingpage', it's importart to have the ability to make every page attractive. Wordpress by default offers templates, shortcodes, widgets and blocks (Gutenberg) to build your website's pages. But very often you want to use the element in your template, as shortcode and as widget. Here components comes in place. Compoments are abstract elements that can be called within a template, but also been mapped to a shortcode, widget, block (soon) of any other pagebuilder element. This makes your theme much more maintainable.

[More on how to use components](basics__components.md)