# Configuration

When you have installed Wordpress initiated the OffbeatWP theme your good to go. There is no configuration to make OffbeatWP work. But below there are some configurations you need to know:

## Developing

By default, OffbeatWP assumes you are in `production` mode. This means for example that the twig-templates are compiled to `/wp-content/caches/twig`. During development, you don't want this of course. You need to tell OffbeatWP you are in development mode. This is easily done by adding this to your `wp-config.php`:

```
define('WP_ENV', 'development');
```

## Defining menu locations:

Open the file `config/menus.php`. You can easy defined a new menu location by adding this to the array:
```
'{slug}' => '{name}',
```

## Defining sidebars:

Open the file `config/sidebars.php`. You can easy defined a new sidebar by adding this to the array:
```
    '{id}' => [
        'name'          => '{name}',
        'description'   => '{description}',
        'before_widget' => '<div id="%1$s" class="widget %2$s">',
        'after_widget'  => '</div>',
        'before_title'  => '<h4 class="widgettitle">',
        'after_title'   => '</h4>',
    ]
```

You have the same parameters available like with using [`register_sidebar`](https://codex.wordpress.org/Function_Reference/register_sidebar), except `id`.

## Defining additional image sizes:

Open the file `config/images.php`. You can easy defined an image size by adding this to the array:
```
    '{name}' => [
        'width' => {width | int},
        'height' => {height | int},
        'crop' => {true|false}
    ]
```

## Adding services

Open the file `config/services.php`. You can easily add a service by adding it to the array:
```
    OffbeatWP\Services\ServiceScripts::class,
```

The order of the services defines the order of when the services are initiated.