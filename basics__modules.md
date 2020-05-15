# Modules

Modules are basically just [services](architecture-concepts__services.md). What makes a module special is that it can contain it's own grouped functionality. This makes it useful for functionality that you easily want to share with other projects, are functionality that is so big that you want to have it all as a group.

## Creating modules

OffbeatWP has a CLI command to easily create a module for you:

`wp offbeatwp make-module {name}`

If you want to use the module you need to activate it. You can do this by editing the services.php file. It is located in the config folder and it looks like this.  

```php
return [
    OffbeatWP\Twig\Service::class,
    App\Services\SiteService::class,
    OffbeatWP\AcfLayout\Service::class,
    OffbeatWP\GravityForms\Service::class,
    OffbeatWP\GravityFormsBootstrapV4\Service::class,
    OffbeatWP\AcfSiteSettings\Service::class,
    Modules\KnowledgeBase\KnowledgeBase::class
];
```

As you can see, I have registered my module at the bottom line.

`Modules\KnowledgeBase\KnowledgeBase::class`

A simple module would look like this:

```
├── Agenda.php
├── Components
│   └── AgendaOverview
│       ├── AgendaOverview.php
│       └── views
│           └── agenda-overview.twig
├── Controllers
│   └── AgendaController.php
├── Models
│   ├── EventCategoryModel.php
│   └── EventModel.php
├── Repositories
│   └── AgendaRepository.php
└── views
    └── single.twig
```
