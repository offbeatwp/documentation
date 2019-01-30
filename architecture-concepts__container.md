# Container

The container manages the dependencies and performs the dependency injection. OffbeatWP uses the powerful implementation from [PHP DI](http://php-di.org/). You'll find the documentation of PHP DI [here](http://php-di.org/doc/).

Example:
```
<?php
namespace App\Controllers;

use OffbeatWP\Controllers\AbstractController;
use App\Repositories\PageRepository;

class PagesController extends AbstractController {
    public function actionSingle($id, PageRepository $pageRepository)
    {
        $post = $pageRepository->find($id);
        echo $this->render('pages/page', ['post' => $post]);
    }
}
```

In this example, the `PageController` needs to get a specific page from the database. We can use a repository to do so. So we inject the repository, the container does this automatically. This is extremely useful in case of unit testing. When running a test we easily can swap the repository by a dummy implementation and run that method with dummy data.


## Binding

To be able to inject certain classes you need to bind them. You need to do this in a [service](architecture-concepts__services.md). You can easily do this by filling the bindings parameters in the service like this:

```
<?php
namespace OffbeatWP\AcfSiteSettings;

use OffbeatWP\Services\AbstractService;
use OffbeatWP\Contracts\SiteSettings as SiteSettingsContract;

class Service extends AbstractService {
    public $bindings = [
        SiteSettingsContract::class => SiteSettings::class
    ];
}
```

