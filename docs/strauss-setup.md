# Setting up Strauss in your project

[Strauss](https://github.com/BrianHenryIE/strauss) is a library for creating namespaced classes and constants on other libraries included within a WordPress project. This way, if your WordPress project is run alongside another WordPress project that has overlapping dependencies, they won't actually conflict!

Adding Strauss to your `composer.json` is only slightly more complicated than adding a typical dependency.

* [Including Strauss](#including-strauss)
  * [As a `.phar` file](#as-a-phar-file)
  * [As a dev dependency via composer (not recommended)](#as-a-dev-dependency-via-composer-not-recommended)
* [Adding your configuration](#adding-your-configuration)
* [Ensuring auto-running of Strauss](#ensuring-auto-running-of-strauss)
* [Add the Strauss autoloader](#add-the-strauss-autoloader)
* [Tell PHPStan about your `vendor/vendor-prefixed` directory](#tell-phpstan-about-your-vendorvendor-prefixed-directory)

## Including Strauss

### As a `.phar` file

To reduce the potentials for conflicts while using Strauss in your project, it is recommended that Straus is added to your project as a `.phar` file during the build process. There are a couple of small steps to make this possible.

#### Create a `bin/.gitkeep` file

This ensures that there is a `bin/` directory in the root of your project. This is where the `.phar` file will go.

```bash
mkdir bin
touch bin/.gitkeep
```

#### `.gitignore` the `.phar` file

Add the following to your `.gitignore`:

```bash
bin/strauss.phar
```

#### Create a `composer.json` `scripts` entry for Strauss

In your `composer.json`, add `strauss` to the `scripts` section:

```json
"scripts": {
	"strauss": [
		"test -f ./bin/strauss.phar || curl -o bin/strauss.phar -L -C - https://github.com/BrianHenryIE/strauss/releases/download/0.13.0/strauss.phar",
		"@php bin/strauss.phar"
	]
}
```

### As a dev dependency via composer (not recommended)

If you prefer to include Strauss as a dev dependency, you can still do so. You mileage may vary when you include it this way.

```
composer require --dev brianhenryie/strauss
```

#### Create a `composer.json` `scripts` entry for Strauss

In your `composer.json`, add `strauss` to the `scripts` section:

```json
"scripts": {
	"strauss": [
		"vendor/bin/strauss"
	]
}
```

## Adding your configuration

There are a number of configuration settings that might be useful for your project, however, the following is the suggested configuration for this library at a minimum. Add the following to your `composer.json` file:

```
"extra": {
	"strauss": {
		"target_directory": "vendor/vendor-prefixed",
		"namespace_prefix": "Boom\\Shakalaka\\",
		"classmap_prefix": "Boom_Shakalaka_",
		"constant_prefix": "BOOM_SHAKALAKA_",
		"delete_vendor_files": true,
		"packages": [
			"stellarwp/REPO_NAME"
		]
	}
},
```

When Strauss is run, this configuration will cause it to execute for the `stellarwp/REPO_NAME` package and all of its dependencies, placing them inside of the `vendor/vendor-prefixed` directory in your project.

## Ensuring auto-running of Strauss

Adding the following to your `composer.json` file will ensure that Strauss is run automatically when composer install or update is excecuted:

```
"scripts": {
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
require_once __DIR__ . '/vendor/vendor-prefixed/autoload.php';
```

## Tell PHPStan about your `vendor/vendor-prefixed` directory

PHPStan doesn't know about your `vendor/vendor-prefixed` directory by default. Luckily, you can add a `scanDirectories` to `parameters` in your `phpstan.neon.dist` file and you'll be good to go!

Here's an example:

```
parameters:
	scanDirectories:
		- vendor/vendor-prefixed
```
