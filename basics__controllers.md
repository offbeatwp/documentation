# Controllers

Below a basic example of a controller:

```
<?php
namespace App\Controllers;

use OffbeatWP\Controllers\AbstractController;
use App\Models\PostModel;

class PostsController extends AbstractController {
    public function actionSingle(PostModel $post)
    {
        return $this->render('posts/single', ['post' => $post]);
    }

    public function actionArchive($posts)
    {
        return $this->render('posts/archive', ['posts' => $posts]);
    }
}
```

The action within the controller should do all the logic needed for the request. The action can return a `string` or an `array`. A string is been echoed to the user directly, and an array is encoded to JSON automatically first and than echoed to the user as well.

## Views

Within the controller you have the possibility to render and view with the `view` method. The `view` method accepts two arguments:
1. The view that needs to be rendered
2. The data that needs to be send to your view.

OffbeatWP is going to look for the view in the nearest `views` directory. If it doesnt find the given view there it will continue the search. If the view isn't found it will try to find the view in the theme' `views` directory. This can be found in `/resources/views/`. So practically:

1. Controllers in the `app/Controllers` directories will searching for the the views in `/resources/views`. 
2. Controllers in a module will check /modules/_YOUR\_MODULE_/views/ first and if it cant find the view there it will check `/resources/views/` 
 
## JSON

If you action return an array it will be converted to a JSON string and then echoed to the user. The content-type will be changed to `application/json` as well.