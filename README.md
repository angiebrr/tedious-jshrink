# JShrink for Laravel 4 (fork)

> [!WARNING]
> Archived and no longer maintained; kept for reference. This is my April 2014 fork of JShrink 0.5 with a Laravel 4 service provider, not the official package. Laravel 4 is long past end-of-life, and the provider uses `$app->share()`, which later Laravel versions removed. The upstream project is [tedious/JShrink](https://github.com/tedious/JShrink); the README below is its README as I adapted it for Laravel.

## Overview

A fork of JShrink, a JavaScript minifier written in PHP, that registers it with Laravel 4 so you can call `JShrink::minify($js)` through a facade alias. My changes, all from April 29, 2014:

- **`src/JShrink/JShrinkServiceProvider.php`**: a Laravel service provider that binds a `Minifier` instance into the container as `JShrink`
- **`composer.json`**: renamed the package to `angelahnicole/jshrink` so it could be installed from this fork as a VCS repository
- **README**: Laravel install steps (Composer repository, service provider, class alias), a short troubleshooting list, and the facade-style usage examples

My commits are the six by angelahnicole; the minifier itself and everything else is upstream.

**Tech:** PHP, Laravel 4, Composer

The minifier is BSD-3-Clause licensed, like upstream; see [LICENSE](LICENSE).

---

## The fork's original README

# JShrink for Laravel 4 [![Build Status](https://travis-ci.org/tedivm/JShrink.svg?branch=master)](https://travis-ci.org/tedivm/JShrink)
[![License](http://img.shields.io/packagist/l/tedivm/JShrink.svg)](https://github.com/tedivm/JShrink/blob/master/LICENSE)
[![Latest Stable Version](http://img.shields.io/github/release/tedivm/JShrink.svg)](https://packagist.org/packages/tedivm/JShrink)
[![Total Downloads](https://poser.pugx.org/tedivm/JShrink/downloads.png)](https://packagist.org/packages/tedivm/JShrink)


JShrink is a php class that minifies javascript so that it can be delivered to the client quicker. This code can be used
by any product looking to minify their javascript on the fly (although caching the results is suggested for performance
reasons). Unlike many other products this is not a port into php but a native application, resulting in better
performance.

**This has been tested on Laravel version 4.0, but it should work on version 4.1.**


## Default Usage

Minifying your code is simple call to a static function-

```php
// Basic (default) usage.
$minifiedCode = JShrink::minify($js);

// Disable YUI style comment preservation.
$minifiedCode = JShrink::minify($js, array('flaggedComments' => false));
```


## Results

* Raw - 586,990
* Gzip - 151,301
* JShrink - 371,982
* JShrink and Gzip - 93,507


## Installing

### Composer

In order for this to work with Laravel, you must install this via Composer. If you wish to install it another way, then I would recommend using [tedivm's repository](https://github.com/tedivm/JShrink).

Until JShrink reaches a stable API with version 1.0 it is recommended that you
review changes before even Minor updates, although bug fixes will always be
backwards compatible.

```yaml
{
    "repositories": [
        {
            ...	
            "type": "vcs",
            "url": "https://github.com/angelahnicole/JShrink"
            ...
        }
    ],
    "require": {
        ...
        "angelahnicole/jshrink": "dev-main"
        ...
    }
}
```

### Laravel

To register JShrink with Laravel you must include it in the Autoloaded Service Providers array along with adding it to the list of Class Aliases. 


```php
// app/config/app.php
...
/*
|--------------------------------------------------------------------------
| Autoloaded Service Providers
|--------------------------------------------------------------------------
|
| The service providers listed here will be automatically loaded on the
| request to your application. Feel free to add your own services to
| this array to grant expanded functionality to your applications.
|
*/
  'providers' => array(
    ...
    'JShrink\JShrinkServiceProvider',
    ...
  )

...

/*
|--------------------------------------------------------------------------
| Class Aliases
|--------------------------------------------------------------------------
|
| This array of class aliases will be registered when this application
| is started. However, feel free to register as many as you wish as
| the aliases are "lazy" loaded so they don't hinder performance.
|
*/
	'aliases' => array( 
	  ...
	  'JShrink'         => 'JShrink\Minifier',
	  ...
	 )
...
```

### Problems?

- Make sure to perform a **composer update** in the command line after including it in your **composer.json** file.
- You may have to perform a **php artisan dump-autoload**
- You may also have to perform a **composer dump-autoload**


### Github

Releases of JShrink (from tedivm) are available on [Github](https://github.com/tedivm/JShrink/releases).


## License

JShrink is licensed under the BSD License. See the LICENSE file for details.

In the spirit of open source, use of this library for evil is discouraged but not prohibited.
