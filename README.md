[![Latest Stable Version](https://poser.pugx.org/lecturize/laravel-tags/v/stable)](https://packagist.org/packages/lecturize/laravel-tags)
[![Total Downloads](https://poser.pugx.org/lecturize/laravel-tags/downloads)](https://packagist.org/packages/lecturize/laravel-tags)
[![License](https://poser.pugx.org/lecturize/laravel-tags/license)](https://packagist.org/packages/lecturize/laravel-tags)

# Laravel Tags

Simple way to tag Eloquent models in Laravel 5.

## Important Notice

**This package is a work in progress**, please use with care and feel free to report any issues or ideas you may have!

We've transferred this package to a new owner and therefor updated the namespaces to **Lecturize\Tags**. The config file is now `config/lecturize.php`.

## Installation

Require the package from your `composer.json` file

```php
"require": {
    "lecturize/laravel-tags": "dev-master"
}
```

and run `$ composer update` or both in one with `$ composer require lecturize/laravel-tags`.

Next register the service provider and (optional) facade to your `config/app.php` file

```php
'providers' => [
    // ...
    Cviebrock\EloquentSluggable\ServiceProvider::class,
    Lecturize\Tags\TagsServiceProvider::class
];
```

## Configuration & Migration

```bash
$ php artisan vendor:publish --provider="Cviebrock\EloquentSluggable\ServiceProvider"
$ php artisan vendor:publish --provider="Lecturize\Tags\TagsServiceProvider"
```

This will create a `config/sluggable.php`, a `config/lecturize.php` and a migration file, that you'll have to run like so:

```bash
$ php artisan migrate
```

## Usage

First, add our `HasTags` trait to your model.
        
```php
<?php namespace App\Models;

use Lecturize\Tags\Traits\HasTags;

class Post extends Model
{
    use HasTags;

    // ...
}
?>
```

##### Get all tags for a model
```php
$tags = $model->tags();
```

##### Check if model is tagged with a given tag
```php
$tags = $model->hasTag('Check');
```

##### Add one or more tags
```php
$tags = $model->tag('My First Tag');
$tags = $model->tag(['First', 'Second', 'Third']);
```

##### Remove given tags from model
```php
$tags = $model->untag('Remove');
```

##### Replace all existing tags for a model with new ones
```php
$tags = $model->retag('A New Tag');
$tags = $model->retag(['Fourth', 'Fifth', 'Sixth']);
```

##### Remove all existing tags from model
```php
$tags = $model->detag();
```

##### Get a list of all tags
```php
$tags = $model->listTags();
```

This is a convenience method for `$model->tags->pluck('tag')`

##### Scopes

There are two scopes included to fluently query models (e.g. Posts) with given tags.

```php
$posts = Post::withTag('My First Tag')->get();
$posts = Post::withTags(['First', 'Second', 'Third'])->get();
```

## License

Licensed under [MIT license](http://opensource.org/licenses/MIT).

## Author

**Handcrafted with love by [Alexander Manfred Poellmann](https://twitter.com/AMPoellmann) in Vienna &amp; Rome.**