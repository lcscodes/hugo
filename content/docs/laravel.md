---
title: "Laravel"
weight: 1
# bookFlatSection: false
# bookToc: true
# bookHidden: false
# bookCollapseSection: false
# bookComments: false
# bookSearchExclude: false
---

# Laravel

## On Windows

1.  install composer
2.  buat project

        composer create-project laravel/laravel example-app

    Develop server

        cd example-app

        artisan serve

# Laravel Modular

## Installation On Windows

1.  install composer
2.  buat project

        composer create-project laravel/laravel example-app

    Develop server

        cd example-app

        php artisan serve

3.  install nwidart modules

        composer require nwidart/laravel-modules

    Publish the package's configuration file

        php artisan vendor:publish --provider="Nwidart\Modules\LaravelModulesServiceProvider"

    By default the module classes are not loaded automatically. autoload your modules. edit file composer.json at root directory. add script autoload modules

        {
            "autoload": {
                "psr-4": {
                "App\\": "app/",
                "Modules\\": "Modules/"
                }
            }
        }

    run autoload

        composer dump-autoload

## Basic Usage

1.  Creating a module

    Huruf awal kapital

        php artisan module:make <module-name>

    Beberapa modul sekaligus

        php artisan module:make <module-name> <module-name> <module-name>
