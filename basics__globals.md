If you want to call a function in your twig file, you have the option to do this via a global.


First of all, I have made a class GeneralHelper (located in App/Helpers).
The only thing this class is doing is return the $_GET value.

```php

<?php

namespace App\Helpers;

class GeneralHelper
{

    public function getParameter($key)
    {
        return isset($_GET[$key]) ? $_GET[$key] : null;
    }

}

```

Now we have to register the global in the SiteService.php file. 

```php
$view->registerGlobal('app', new GeneralHelper());
```



Now you can call it in the twig file

```twig

{{ app.getParameter('searchBox') }}

```

  

