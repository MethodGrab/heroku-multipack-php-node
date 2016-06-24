# Heroku Multipack PHP & Node.js
> An example multipack app that uses a PHP / Nginx backend with Node.js frontend package management / build.


## Usage

```sh
# Clone this repo, or clone your own fork
git clone git@github.com:methodgrab/heroku-multipack-php-node.git
cd heroku-multipack-php-node

# Create a new Heroku app
heroku create

# Add the buildpacks
heroku buildpacks:add heroku/nodejs
heroku buildpacks:add heroku/php

# Deploy
git push heroku master
heroku open
```

Alternatively, you can deploy your own copy of the app using the web-based flow:

[![Deploy to Heroku](https://www.herokucdn.com/deploy/button.png)](https://heroku.com/deploy)


## What's Happening
1. The [Node.js buildpack](https://github.com/heroku/heroku-buildpack-nodejs) runs, installing the dependencies from `package.json`.
1. The [PHP buildpack](https://github.com/heroku/heroku-buildpack-php) runs, installing the dependencies from `composer.json`.
1. As part of the Composer install, it also runs the custom [`compile` script](https://devcenter.heroku.com/articles/php-support#custom-compile-step) from `composer.json`.  
The Node.js binaries are still available at this point so we can then run the Node.js build while having access to any composer dependencies that might need to be re-organised as part of the build step.
