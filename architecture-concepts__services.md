# Service

A service is a  script that contains code to bootstrap a specific functionalitiy of the website. The service is also the place to define bindings to the container.

All the functionality to your website is initiated through services. So your website will contain multiple services, but also external functionality (pulled through composer) will be added to your theme as as service.

You have to register a service to have it bootstrapped. A service is registered in the `config/services.php` file, like this:

```
    OffbeatWP\Services\ServiceScripts::class,
```

# Writing a Service

A service needs to be extended from  `use OffbeatWP\Services\AbstractService`. A service can contain a `register` method. The register method is being executed right after all the services are registered. At the point all the bindings already exists.

You can easy scaffold a service by executing this CLI command:

```
wp offbeatwp make-service {name}
```

Make sure the service is in CamelCase.

This will create you an empty service in the `app/services.php` folder. You have to manually add it to `config/services.php`.
