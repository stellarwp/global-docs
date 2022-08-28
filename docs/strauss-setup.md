# Setting up Strauss in your project

[Strauss](https://github.com/BrianHenryIE/strauss) is a library for creating namespaced classes and constants on other libraries included within a WordPress project. This way, if your WordPress project is run alongside another WordPress project that has overlapping dependencies, they won't actually conflict!

Adding Strauss to your `composer.json` is only slightly more complicated than adding a typical dependency.

## Including Strauss as a dev dependency via composer

Firstly, you'll need to require Strauss via composer:

```
composer require --dev brianhenryie/strauss
```

## Adding your configuration

There are a number of configuration settings that might be useful for your project, however, the following is the suggested configuration for this library at a minimum. Add the following to your `composer.json` file:

```
"extra": {
	"strauss": {
		"target_directory": "vendor/strauss",
		"classmap_prefix": "Boom_Shakalaka_",
		"constant_prefix": "BOOM_SHAKALAKA_",
		"packages": [
			"stellarwp/REPO_NAME"
		]
	}
},
```

When Strauss is run, this configuration will cause it to execute for the `stellarwp/REPO_NAME` package and all of its dependencies, placing them inside of the `vendor/strauss` directory in your project. _Note: you'll want to commit that directory into your project._

## Ensuring auto-running of Strauss

Adding the following to your `composer.json` file will ensure that Strauss is run automatically when composer install or update is excecuted:

```
"scripts": {
	"strauss": [
			"vendor/bin/strauss"
	],
	"post-install-cmd": [
			"@strauss"
	],
	"post-update-cmd": [
			"@strauss"
	]
}
```

Additionally, you can run this manually via `composer run strauss`.

## Add the Strauss autoloader

You'll need to add the Strauss autoloader to your project so that all of the relevant classes are available. If you were to put it in a WordPress plugin's bootstrap file (the main file in the base directory of your plugin), you'd add a line like so:

```php
require_once __DIR__ . '/vendor/strauss/autoload.php';
```

## Tell PHPStan about your `vendor/strauss` directory

PHPStan doesn't know about your `vendor/strauss` directory by default. Luckily, you can add a `scanDirectories` to `parameters` in your `phpstan.neon.dist` file and you'll be good to go!

Here's an example:

```
parameters:
	scanDirectories:
		- vendor/strauss
```
