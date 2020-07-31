# Views

OffbeatWP uses [Twig](https://twig.symfony.com/) as template engine by default. It is part of the Symfony project and is widely supported.

Check the website of Twig for the [documentation](https://twig.symfony.com/doc/2.x/)

## Added OffbeatWP Functionality

`{{ config($key) }}`
Get settings from one of the files in the `/config` folder.

`{{ assetUrl($file) }}`
Files that are compiled through the OffbeatWP asset builder (CSS, js and images) has a hashed name. To get the correct path you should use this method which checks the manifest and maps returns the correct URL.

`{{ component($name, $args = []) }}`
Getting and rendering a OffbeatWP Component (More about [components](basics__components.md))

`{{ setting($key) }}`
OffbeatWP has functiontality included for site settings. The only implementation now is through ACF. OffbeatWP has already implemented this. Check out the [documentation](https://github.com/offbeatwp/acf-sitesettings).

## Added Wordpress Functionality

Within your twig template, you'll have access to a `wp` global variable. Through this variable, you have access to a lot of the default Wordpress functionality. 

`{{ wp.head }}` -> wp_head();

`{{ wp.footer }}` -> wp_footer();

`{{ wp.title }}` -> wp_title();

`{{ wp.languageAttributes }}` -> get_language_attributes();

`{{ wp.navMenu($args) }}` -> wp_nav_menu($args);

`{{ wp.homeUrl }}` -> get_home_url();

`{{ wp.siteUrl }}` -> site_url();

`{{ wp.bloginfo($name) }}` -> get_bloginfo($name, 'display');

`{{ wp.bodyClass($class = '') }}` -> body_class($class);

`{{ wp.action($action) }}` -> do_action($action);

`{{ wp.shortcode($shortcode) }}` -> do_shortcode($shortcode);

`{{ wp.sidebar($name) }}` -> dynamic_sidebar($name);

`{{ wp.attachmentUrl($attachmentID, $size = 'full') }}` -> wp_get_attachment_image_src($attachmentID, $size);

`{{ wp.getAttachmentImage($attachmentID, $size = 'thumbnail', $classes = ['img-fluid']) }}` -> wp_get_attachment_image($attachmentID, $size, false, ['class' => implode(' ', $classes)]);

`{{ wp.formatDate($format, $date, $strtotime = false) }}` -> date_i18n($format, $date);

`{{ wp.resetPostdata() }}` -> wp_reset_postdata();

`{{ wp.isFrontPage() }}` -> is_front_page();

`{{ wp.templateUrl($path = null) }}` -> get_template_directory_uri();

`{{ __('{string}', '{textdomain}') }}` -> \__($string, $textdomain);

`{{ gf.form(settings.form.id, false, false, false, null, true) | raw }}` get gravity form

`{{ dump(wp.allPostMeta) }}` get all post meta from the current post or (wp.allPostMeta($postId) for a specefic post (you can add `<pre>` tags to make it more clear)

