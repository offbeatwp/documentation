# Forms

The `\OffbeatWP\Form\Form` is an abstract implementation that can be mapped to the right structure depending on the implementation you're using. The forms are currently used for Components and SiteSettings. 

## Form Structure

The current structure of a form is like this:
```
- Form
    - Tab
        - Section
            - Field
        - Repeater
            - Field
```

The use of tabs in a Component context is mandatory, but for SiteSettings, it isn't. A Section is not mandatory but really helps to structure your fields.

A more advanced example of a form:
```
$form = new Form();

$columnsField = \OffbeatWP\Form\Fields\Select::make('title2', 'Title');
$columnsField->addOptions(['2' => '2', '3' => '3', '4' => '4'])

$form
    ->addTab('general', 'General')
        ->addSection('general', 'General')
            ->addField(\OffbeatWP\Form\Fields\Text::make('title', 'Title'))
            ->addField(\OffbeatWP\Form\Fields\Editor::make('content', 'Content'))
    ->addTab('Appearance', 'Appearance')
        ->addSection('appearance', 'Appearance')
            ->addField($columnsField)
        ->addRepeater('pros_list', 'Pro list')
            ->addField(\OffbeatWP\Form\Fields\Text::make('pro', 'Pro'));
```


## Fields

Below the fields that are currently been integrated:

### Text

```php
\OffbeatWP\Form\Fields\Text::make($id, $label)
```

### Textarea

```php
\OffbeatWP\Form\Fields\TextArea::make($id, $label)
```

### Editor

```php
\OffbeatWP\Form\Fields\Editor::make($id, $label)
```

### Select

```php
\OffbeatWP\Form\Fields\Select::make($id, $label)
```

To define options you first construct the field and then assign the options:

```php
$selectField = \OffbeatWP\Form\Fields\Select::make($id, $label);
$selectField->addOptions(['key' => 'value']);

// or add single option:
$selectField->addOption($key, $value]);
```

### Image

```php
\OffbeatWP\Form\Fields\Image::make($id, $label);
```

### TrueFalse

```php
\OffbeatWP\Form\Fields\TrueFalse::make($id, $label);
```

### Post

Selecting a post

```php
$postField = \OffbeatWP\Form\Fields\Post::make($id, $label);

// if you only want from specific post types
$postField->fromPostTypes(['post']);
```

### Posts

Selecting multiple posts

```php
$postsField = \OffbeatWP\Form\Fields\Posts::make($id, $label);

// if you only want from specific post types
$postsField->fromPostTypes(['post']);
```

### Term

Selecting a term

```php
$termField = \OffbeatWP\Form\Fields\Term::make($id, $label);

// if you only want from specific taxonomies
$termField->fromTaxonomies(['post']);
```

### Terms

Selecting multiple terms

```php
$termsField = \OffbeatWP\Form\Fields\Terms::make($id, $label);

// if you only want from specific taxonomies
$termsField->fromTaxonomies(['post']);
```

### NavMenu

Selecting a nav menu

```php
\OffbeatWP\Form\Fields\NavMenu::make($id, $label);
```

### User

Selecting a user

```php
\OffbeatWP\Form\Fields\User::make($id, $label);
```

### Users

Selecting multiple users

```php
\OffbeatWP\Form\Fields\Users::make($id, $label);
```

### Breakpoints

Selecting one of the default bootstrap breakpoints

```php
\OffbeatWP\Form\Fields\Breakpoint::make($id, $label);
```

### TextAlign

Select box with text-align options

```php
\OffbeatWP\Form\Fields\TextAlign::make($id, $label);
```

### HorizontalAlign

Select box with horizontal align options

```php
\OffbeatWP\Form\Fields\HorizontalAlign::make($id, $label);
```

### VericalAlign

Select box with vertical-align options

```php
\OffbeatWP\Form\Fields\VericalAlign::make($id, $label);
```

## Creating your own fields

In some cases, it could be interesting to create your own fields by extending OffbeatWP Fields so you can reuse them. The right place to this is in an `app/Form/Fields` folder from the root of your theme.

If for example, you want to have a field to define a rating create a file named `Rating.php` in your `app/Form/Fields` directory, containing:

```php
<?php
namespace App\Form\Fields;

use \OffbeatWP\Form\Fields\Select;

class Rating extends Select {

    public function __construct()
    {        
        $this->addOptions([
            ''         => __('No Rating', 'offbeatwp'),
            '1'        => __('No Way', 'offbeatwp'),
            '2'        => __('Mwah', 'offbeatwp'),
            '3'        => __('It\'s oke', 'offbeatwp'),
            '4'        => __('Pretty awesome actually', 'offbeatwp'),
            '5'        => __('Awesomsaus', 'offbeatwp'),
        ]);

        parent::__construct();
    }
    
}
```

Within the form you do:

```php
$form->.......->addField(\App\Form\Fields\Rating::make($id, $label))
```

## Field Collections

Field collections are a combination of fields that can be reused, current collections available:

Adding a fields collection to a form must be done with the `->addFields` method.

```php
$form->.......->addFields(\OffbeatWP\Form\FieldsCollections\Heading::make())
```

### Heading

The heading fields collection automatically adds the following fields to your form:
- Title (text field)
- Heading Type (select box is h1-h6)
- Heading Style (select box is h1-h6)

```php
\OffbeatWP\Form\FieldsCollections\Heading::make();
```

### Link

The Link fields collection automatically adds the following fields to your form:
- Link label (text field)
- Link url (text field)
- Link target (selectbox is \_blank, \_self, \_top)

```php
\OffbeatWP\Form\FieldsCollections\Link::make();
```

## Defining your own Collections

In some cases, it could be interesting to create your own fields collection so you can reuse them. The right place to this is in an `app/Form/FieldsCollections` folder from the root of your theme.

```php
namespace App\Form\FieldsCollections;

use \OffbeatWP\Form\FieldsCollections\AbstractFieldsCollection;
use \OffbeatWP\Form\Fields\Text;

class SocialLinks extends AbstractFieldsCollection {
    public function __construct()
    {
        $this->addField(Text::make('facebook_link', __('Facebook link', 'offbeatwp')));
        $this->addField(Text::make('instagram_link', __('Instagram link', 'offbeatwp')));
        $this->addField(Text::make('twitter_link', __('Twitter link', 'offbeatwp')));
    }
}
```

To use this within the form:

```php
$form->.......->addFields(\App\Form\FieldsCollections\SocialLinks::make())
```
