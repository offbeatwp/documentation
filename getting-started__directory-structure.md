# Directory structure

The directory structure of an OffbeatWP look like this:

- app
    - Controllers
        - ErrorsController.php
        - PagesController.php
        - PostsController.php
        - SearchController.php
    - Models
        - PageModel.php
        - PostModel.php
    - Services
        - SiteService.php
- assets
    _Empty by default, the compiled assets will be in here_
- components
    _Empty by default will contain the website\` components_
- composer.json
    _This file stores the PHP dependencies_
- config
    - app.php 
        _(Website settings)_
    - images.php
        _(Additional image sizes)_
    - menus.php
        _(Menu locations)_
    - services.php
        _(Services of the website)_
    - sidebars.php
        _(Define sidebars for your website)_
- functions.php
    _This is a default Wordpress theme file. OffbeatWP uses it the spin up the framework._
- index.php
    _This is a default Wordpress theme file. OffbeatWP uses it as an entry of the view._
- modules
    _Empty by default will contain the website\` modules_
- package.json
    _This file stores the NPM dependencies_
- resources
    - config.js
        Config file for the Webpack builder
    - img
        Containing your website' images
    - js
        Containing your website' javascript
    - sass
        Containing your website' styles
    - views
        Containing your website' views (or partly)
- routes
    - ajax.php
        (Routes for ajax)
    - api.php
        (Routes for API call)
    - web.php
        ((Routes for normal pages)
- screenshot.png
    _Is used as preview image in the overview of the available themes_
- style.css
    _This is a default Wordpress theme file, only used for the basic theme information like name, author, license, etc. _
- tests
    _Will contain your website' unit tests (still needs to be implemented)_
- vendor
    _Will contain the fetched libraries through composer_
