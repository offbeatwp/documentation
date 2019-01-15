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

## Why do you want to work with OffbeatWP?

Wordpress is an amazing open source CMS system. But Wordpress has some _bad_-sides, especcially for custom made websites. Below some _bad_-sides of Wordpress and how OffbeatWP is solving those (based on this [post](https://medium.com/track-changes/wordpress-without-shame-fedc1a2fef72)):

### #1: In WP “everything is a post”

Eventhough the "everthing is a post" approach gives Wordpress a lot of flexibility, sometimes it makes things a bit messy. OffbeatWP makes it possible to have a model per post-type helping you to structure your code and makes it really confinient to work with.

### #2: The Loop bites you in the ass at least a half dozen times per project.

Say goodbye to "The Loop". Since OffbeatWP uses Collections (from [Laravel](https://laravel.com/docs/5.7/collections)) and models you have easy access to the post\` data. For example if you want to get the permalink of the post you simple do:

```
post.permalink
```
### #3: It’s slow.

By default Wordpress isn't the slow at all. Most of the time it is a combination of bad written themes and plugins, and not really well configured hosting that makes Wordpress slow. OffbeatWP can help you with writing your theme in a proffesional way so only the code that needs to be executed is executed.

### #4: It’s really, really hard to get consistent caching logic.

In our humble opinion you shouldn't use any *page caching* at all. It's our goal that every request to Wordpress is handled and finished withing 200ms. That's our budget. If a request exceeds this budgets we have to optimize the request to make it happen.

### #5: There is no way of doing version control of any dependencies

OffbeatWP uses composer (for PHP pagckages) and npm (for asset building like scss, js, fonts, etc). These are version controlled libraries. We encourage plugin developers to make their plugins also available as a _Service_. With this all the dependencies of your website will be defined in your theme, all version controlled.

