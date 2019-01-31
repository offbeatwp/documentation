# Routing

OffbeatWP has a way of routing that makes it possible the use the default Wordpress rewrite rules and map them to OffbeatWP controllers. This is done by a "callback route". In the future, we will make it also possible to define routes based on the url.

## Callback routes

Example of a callback route:

```
offbeat('routes')->callback( 
    function () {
        return is_archive();
    },
    [PostsController::class, 'actionArchive']
);
```

The first attribute is the callback, this will be executed to find a match for the current request. If the callback returns true a match is found and it will not check any other later defined routes. If the callback returns false there was no match and it will check the next defined route. 

Routes can be defined everywhere, as long as they are registered before WordPress tries to render the page. But OffbeatWP has preferred two ways to define routes:

### 1. In your themes route folder

In the root of your theme, you'll find a folder named `routes`. This contains three files by default:
- ajax.php
- api.php
- web.php

Currently, there isn't a real difference between the files, but the helps you to group the routes.

### 2. In your modules service

When the controllers are in your module, it would make sense the define the routes into your module as well. The recommended way of doing this is by defining it into your Module-file. 

Add this to your `register` method:

```
add_action('before_route_matching', [ $this, 'registerRoutes' ]);
```

