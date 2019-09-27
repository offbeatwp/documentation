# Post Models

Models are one of the cool features of OffbeatWP. It makes "The Loop" obsolete and gives a much more intuitive way of getting data from a post or term like the title, content or url.

OffbeatWP has two types of models:
1. Post models 
    A post model represents a post in a specific post type
2. [Term Models](basics__term_models.md)
    A term model represents a term in a specific taxonomy

A post model represents a post of a specific post type. Below an example of a post model:

```
<?php
namespace App\Models;

use OffbeatWP\Content\Post\PostModel as OffbeatWpPostModel;

class PostModel extends OffbeatWpPostModel {
    const POST_TYPE = 'post';
    const ORDER_BY  = 'menu_order';
    const ORDER     = 'ASC';
}
```

It is easy to extend the model so you can get the data of a post in a readable and intuitive way. If you have a post type for `events` it would be great to have a getter just for this:

```
<?php
namespace App\Models;

use OffbeatWP\Content\Post\PostModel as OffbeatWpPostModel;

class EventModel extends OffbeatWpPostModel {
    const POST_TYPE = 'event';

    public function getEventDate()
    {
        return $this->getMeta('event_date');
    }
}
```

Now you can can easy get the post' event date by doing `$event->getEventDate();`. In twig it even shorter: `{{ event.eventdate }}`

## Creating a model

To create a model you can use the CLI-command:

```
wp offbeatwp make-postmodel {name} --post_type="{post_type}"
```

If you want to create a model for a module you can do this by adding `--module={module_name}` to the command like:

```
wp offbeatwp make-postmodel {name} --post_type={post_type}--module={module_name}
```

## Getting data from a model

By default the PostModel comes with the following methods to get data from the post:

#### `getPreviousPost(false, '', '')`

Get the previous post

#### `getNextPost(false, '', '')`

Get the next post (you can use all the methods below)

#### `getId()`

Get the id of the post

#### `getTitle()`

Get the title of the post

#### `getContent()`

Get the content of the post

#### `getSlug()`

Get the post' post_name / slug

#### `getPermalink()`

Get the post' url

#### `getPostDate($format = '')`

Get the id of the post

#### `getExcerpt()`

Get the excerpt of the post

#### `getAuthor()`

Get the author of the post

#### `getMeta($key, $single = true)`

Get a meta value of the post. The first attribute is the key to the meta. The second parameter is if you desire a single or multiple responses. Single is the default.

#### `setMeta($key, $value)`

Setting a meta to the post. The argument is the key, the second the value of the meta.

#### `getTerms(taxonomy, $args = [])`

Get the terms of the post by taxonomy. The first argument is the taxonomy. With the second parameter, you can set some additional arguments. These arguments are equal to the [WP_Term_Query::\__construct](https://developer.wordpress.org/reference/classes/wp_term_query/__construct/) method.

#### `hasFeaturedImage()`

Check if the post has a featured image. Returns true or false.

#### `getFeaturedImage($size = 'thumbnail', $attr = [])`

Returns html (img-tag) of the post' featured image. With the first argument you can define the size, the second you send arguments which are equal to [get_the_post_thumbnail](https://developer.wordpress.org/reference/functions/get_the_post_thumbnail/)

#### `getFeaturedImageUrl($size = 'thumbnail')`

Get the post' featured image url

#### `getFeaturedImageId()`

Get the post' featured image id. Returns false if the post has no featured image.

#### `setup()`

If some plugin or other implementation requires a post to be in "the loop" you can run this method. 

#### `emd()`

Ends "The loop"

### Default post type ordering

You can add the constant `ORDER` and `ORDER_BY` to a model. Now every time you are getting posts this ordering is applied.

## Macro

You can extend any post model from outside the model itself. This is called a macro. We have a [independent service](https://github.com/offbeatwp/acf) to integrate [Advanded Custom Fields }(https://www.advancedcustomfields.com/pro/) with OffbeatWP. Within the post model, we want to be able to easily get an ACF field. The service contains the following `macro`:

```
PostModel::macro('getField', function ($name, $format = true) {
    return get_field($name, $this->getId(), $format);
});
```

Now we can easily access the post' ACF field be doing:

```
post.getField('key')
```

## Associating a post-type to a model

OffbeatWP maps posts to the related model. But to make this possible we have to register the models. When you register the post type within your theme you can do this all at once as [explained here](basics__post_types.md). But if the post_type is Building (like post and page), or is defined within a plugin you have to do this by:

```
offbeat('post-type')->registerPostModel('post', \App\Models\PostModel::class);
```

The first argument is the post_type and the second the PostModel.

## Getting posts

You can get posts from the model just by doing the following:

```
PostModel::all();
```

This will get you the number of posts as configured in the WordPress settings (Settings > Reading).

```
PostModel::all();
```

This will get you all the posts.

```
PostModel::take(5);
```

This will get you the first 5 posts. 

```
PostModel::first();
```

This will get you the first post.

```
PostModel::findbyId($id);
```

Find a post by id.

### Filtering posts

OffbeatWP comes with a variety of methods to filter your posts:

`where($args)`

The arguments are equal to [WP_Query](https://codex.wordpress.org/Class_Reference/WP_Query). But since this won't make your code very readable we do not recommend this filter.

`whereTerm($taxonomy, $terms = [], $field = 'slug', $operator = 'IN')`

Filter the posts by a term. 

`whereDate($args)`

Filter the posts by date. Arguments are equal to [WP_Query::data_query](https://codex.wordpress.org/Class_Reference/WP_Query#Date_Parameters)

`whereMeta($key, $value = '', $compare = '=')`

Filter the posts by meta.

***

Those filters can be chained like:

```
PostModel::whereTerm('tags', 'awesome')->whereMeta('great', 'NOT', '!=')->all();
```

This will get you *all* the posts having the tag "awesome" and where meta "great" is not equal to "NOT". The `->all()` could also be substitued by `->take(5)`, `->first()` or just `->get()`.

### Ordering posts

Ordering posts can be done by adding `->order($order_by, $order)` to the chain, like:

```
PostModel::whereTerm('tags', 'awesome')->order('id', 'ASC')->take(5);
```

This will get you the first 5 results of all posts the tag "awesome", ordered by id (ascending).

To order by *meta* give as first argument `meta:{meta_key}` or to order as number `meta_num:{meta_key}`

### Collections

The `get`, `take` and `all` methods return a Collection. OffbeatWP uses the [Laravel Collection](https://laravel.com/docs/5.7/collections) which gives you an awesome toolset.

A collection is iterable, meaning that you can just loop over it in a foreach loop. This is really helpful within your template. Just can just send the collection to your view and loop over it with twig-like:

```twig
{% for event in events %}
    <h3>{{ event.title }}</h3>
{% endfor %}
```

## Relationships (beta)

With a more advanced website, you often want to create relationships between posts. With OffbeatWP this is really simple.

First, we have to install a service, this to your `config/services.php` file:

```
OffbeatWP\Content\Post\Relations\Service::class,
```

To make these queries run quickly we have to install an extra table in our database. This is done through WP-CLI, run from your terminal:

```bash
wp post-relations:install
```

### Defining relationships

In your model, you can define the relationship like this

```
<?php
namespace App\Models;

use OffbeatWP\Content\Post\PostModel as OffbeatWpPostModel;

class EventPostModel extends OffbeatWpPostModel {
    const POST_TYPE = 'event';
        
    public function locations()
    {
        $this->hasMany('{key}');
    }
}
```

The key is something you make up yourself to identify the relationship. We recommend something declarative like the post type "event_location".

Besides `->hasMany` you can use `->hasOne()`, `->belongsTo()` or `->belongsToMany()`

### Attaching and Detaching relationships (for hasOne and hasHany)

Now you can attach another post by doing:

```
$event->locations()->attach($id);
```

If you also use an array of ids to attach multiple posts at once. By default, the relations are appended to existing relationships. If you what to replace the existing relationships, you just have to add a second parameter with the value `false` like:

```
$event->locations()->attach([1,2,3], false);
```

You can detach an relationship by doing:

```
$event->locations()->detach($id);
```

or to detach all relationships.

```
$event->locations()->detachAll();
```

### Associating and Dissociating relationships (for belongsTo and belongsToMany)

Now you can associate another post by doing:

```
$location->events()->associate($id);
```

If you also use an array of ids to associate multiple posts at once. By default, the relations are appended to existing relationships. If you what to replace the existing relationships, you just have to add a second parameter with the value `false` like:

```
$location->events()->associate([1,2,3], false);
```

You can dissociate an relationship by doing:

```
$event->locations()->dissociate($id);
```

or to dissociate all relationships.

```
$event->locations()->dissociateAll();
```


### Using relationships
```
$event->locations()->get();
```
