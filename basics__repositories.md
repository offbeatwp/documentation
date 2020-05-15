If you want to get data from different places and want to reuse this functionality within the project. Is it possible to use a repository within offbeatwp. This is useful when editing data before sending it to the controller. It is good practice to create a repository for somewhat more difficult logic. 

It is recommended to add repositories in one way.

## Inside a module

Modules group a certain kind of functionality. For example an agenda, quote module and so on. You can create a repository within a module and use its functionality.

As you may have seen in the [basic module](basics__modules.md). 
You need to create repository file. This is what it would look like: 

```php

<?php

namespace Modules\Agenda\Repositories;

use App\Models\PostModel;
use Modules\Agenda\Models\EventModel;

class AgendaRepository
{

    public function getAgendaOverviewItems($settings)
    {
        $taxonomy = 'agenda_category';
        // Some logic
        return $postModel->paginated()->get();
    }


}

```
### Binding the repository
You also have to bind the repository. So you can use it. To so this, you have to add the next to the [main file](basics__modules.md).
The main file is `agenda.php` in the [example](basics__modules.md).

In the file you need to add this:

```php

    public $bindings = [
        'agenda' => Repositories\AgendaRepository::class,
    ];
    
```

### Using the repository.

You can call the repository anywhere using
```
$AgendaRepository = offbeat('agenda');

```

To call a methode

```
$AgendaRepository->getAgendaOverviewItems() or offbeat('agenda')->getAgendaOverviewItems()
```


