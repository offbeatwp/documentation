# Compiling assets

OffbeatWP has an assets builder based on webpack. It builds sass, es6 javascript and images. Besides of that the builder contains browsersync to have a easier workflow during development.

The first time you have to get the dependencies by running to following command from the root of you OffbeatWP theme

```
yarn install    |or|    npm install
```

To run the builder for development:

`yarn offbeatwp dev`

To run the builder for production:

`yarn offbeatwp production`


## Sass

Your sass files should be in `resources/sass/` The `main.scss` file is the entry-file for you sass

## Javascript

Your js files should be in `resources/js/` The `main.js` file is the entry-file for you javascript. Javascript can be written in ES6.

## Icon font

The builder can created icon fonts for you. Just create an `icons` folder in `/resources/` and move some `.svg` files into to. Next run the command from the route of your OffbeatWP Theme folder:

```
yarn offbeatwp icons
```

Next add the following line to your `resources/sass/main.scss` file:

```
@import "../fonts/icons/icons";
```

Check this file how to show the icon in your html.

