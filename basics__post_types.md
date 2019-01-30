# Post types

Post and post types are one of the core elements of Wordpress, and one of the reasons Wordpress is so flexible. 

Even though the default Wordpress way of registering post types will still work with OffbeatWP, we would encourage you to use the OffbeatWP method to do it. It makes registering a post type a lot more declarative. 

This is how registering a post-type in OffbeatWP looks like:

```
offbeat('post-type')::make('download', 'Downloads', 'Download')
    ->model(Models\DownloadModel::class)
    ->supports(['title', 'editor'])
    ->icon('dashicons-format-aside')
    ->notPubliclyQueryable()
    ->inRest(false)
    ->public()
    ->set();
```

Basically the first and last line are the most important. The first line:

`offbeat('post-type')::make('download', 'Downloads', 'Download')`

has three arguments, the `post_type`, `Plural label` a `Single label`

The last line (`->set()`) performs the actual "register_post_type".

This line in between are settings of the post_type.

## Register in service

Post types should be registered in a Service or Module (what basically is a Service as well). We recommend it by doing it like this:

```
class Downloads extends AbstractModule
{
    public function register()
    {
        add_action('init', [$this, 'registerContentTypes']);
    }

    public function registerContentTypes()
    {
        offbeat('post-type')::make('download', 'Downloads', 'Download')
            ->model(Models\DownloadModel::class)
            ->supports(['title', 'editor'])
            ->icon('dashicons-format-aside')
            ->notPubliclyQueryable()
            ->inRest(false)
            ->public()
            ->set();

...
```

## Register the related model

When you register the post_type you can set the related model with it. By the OffbeatWP knows how to map the posts the right model.

`->model(Models\DownloadModel::class)`


## Available methods for settings

`rewrite($rewrite)`

`labels($labels)`

`model($modelClass)`

`supports($support)`

`notPubliclyQueryable()`

`public($public = true)`

`excludeFromSearch($exclude = true)`

`showUI($showUI = true)`

`icon($icon)`

`inMenu($menu)`

`inRest($showInRest = true)`

`position($position = null)`

For more information about register post type check the Wordpress documentation about [register_post_type](https://codex.wordpress.org/Function_Reference/register_post_type)


