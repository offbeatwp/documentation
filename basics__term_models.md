## Term models

Models are one of the cool features of OffbeatWP. It gives a much more intuitive way of getting data from a post or term like the title, content or url.

OffbeatWP has two types of models:
1. [Post models](basics__post_models.md)
    A post model represents a post in a specific post type
2. Term Models
    A term model represents a term in a specific taxonomy

A term model represents a term of a specific taxonomiy. Below an example of a term model:

```
<?php
namespace App\Models;

use OffbeatWP\Content\Taxonomy\TermModel;

class TagModel extends TermModel {
    const POST_TYPE = 'tag';
    const ORDER_BY  = 'menu_order';
    const ORDER     = 'ASC';
}
```

## Creating a model

To create a model you can use the CLI-command:

```
wp offbeatwp make-termmodel {name} --taxonomy="{taxonomy}"
```

If you want to create a model for a module you can do this by adding `--module={module_name}` to the command like:

```
wp offbeatwp make-termmodel {name} --taxonomy={taxonomy}--module={module_name}
```

## Associating a taxonomy to a model

OffbeatWP maps terms to the related model. But to make this possible we have to register the models. When you register the taxonomy within your theme you can do this all at once as [explained here](basics__taxonomies.md). But if the taxonomy is buildin (like category , post_tag), or is defined within a plugin you have to do this by:

```
offbeat('taxonomy')->registerTermModel('post_tag', \App\Models\PostTagModel::class);
```

## Getting data from a model

By default the PostModel comes with the following methods to get data from the post:

#### `getId()`

Get the id of the term

#### `getName()`

Get the name of the term

#### `getSlug()`

Get the slug of the term

#### `getDescription()`

Get the description of the term

#### `getLink()`

Get the link of the term

#### `getParentId()`

Get the parent id of the term

#### `getParent()`

Get the parent term (model) of the term

#### `getMeta($key, $single = true)`

Get a meta value of the term. The first attribute is the key of the meta. The second parameter is if you desire a single or multiple response. Single is default.

#### `setMeta($key, $value)`

Setting a meta to the term. The argument is the key, the second the value of the meta.

#### `setMeta($key, $value)`

Setting a meta to the term. The argument is the key, the second the value of the meta.

#### `getPosts()`

Returns an instance of WpQueryBuilder so you are able to use functionals like `->all()`, `->take()` or `->first()`

## Macro

You can extend any term model from outside the model itself. This is called a macro. We have a [independent service](https://github.com/offbeatwp/acf) to integrate [Advanded Custom Fields }(https://www.advancedcustomfields.com/pro/) with OffbeatWP. Within the term model we want to be able to easily get an ACF field. The service contains the following `macro`:

```
TermModel::macro('getField', function ($name, $format = true) {
    return get_field($name, $this->wpTerm, $format);
});
```

Now we can easily access the term' ACF field be doing:

```
term.getField('key')
```

## Getting terms

You can get the terms of the model just by doing the following:

```
TermModel::all();
```

or to take a maximum number of terms:

```
TermModel::take(5);
```

or return just the first match.

```
TermModel::first();
```

***

Find term by id:
```
TermModel::findById($id);
```

Find term by slug
```
TermModel::findBySlug($slug);
```

Find term by name
```
TermModel::findByName($name);
```

### Filter results

Like with the post models you can chain some methods to filter terms:

`where($args)`

The arguments are equal to [WP_Term_Query::\__construct](https://developer.wordpress.org/reference/classes/WP_Term_Query/__construct/). But since this wont make your code very readable we do not recommend this filter.

`whereMeta($key, $value = '', $compare = '')`

Filter the terms by meta.

`whereRelatedToPost($postIds)`

Filter the terms by related posts. $postIds can by an array of integer.

`excludeEmpty($hideEmpty = true)`

Exclude empty terms

***

Example:

```
TermModel::whereMeta('isAwesome', 'totally')->excludeEmpty()->take(5);
```

This will get the terms where meta "isAwesome" equals to "totally", empty terms are excluded and just take 5 terms.

### Order terms

Ordering terms can be done by adding `->order($order_by, $order)` to the chain, like:

```
TermModel::whereMeta('isAwesome', 'totally')->order('term_id', 'ASC')->take(5);
```

This will get you the first 5 results of all posts the the tag "awesome", ordered by id (ascending).

To order by *meta* give as first argument `meta:{meta_key}` or to order as number `meta_num:{meta_key}`

