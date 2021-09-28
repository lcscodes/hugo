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

## Installation On Windows

1.  install composer
2.  buat project

        composer create-project laravel/laravel example-app

    Develop server

        cd example-app

        artisan serve

## Basic Usage

### Set Database

    Open file .env di root folder

### Make Model

        php artisan make:model <model-name> -m

    Tambahan -m artinya untuk generate database migration sekaligus

### Set Migration

    Pada folder root/database/migration, lengkapi field untuk databasenya. contoh :

        $table->id();
        $table->string('nama',100);
        $table->string('alamat',100);
        $table->date('tanggalJoin');
        $table->timestamps();

### migrate database

        php artisan migrate

    rollback migrate database

        php artisan migrate:rollback

    Buka model di root/app/Models/<model-name>. isikan data berikut:

        class Customer extends Model
        {
            protected $table = "pegawai";
            protected $primaryKey = "id";
            protected $fillable =['id','nama','alamat','tanggal_lahir'];
        }

## Laravel Modular

### Installation On Windows

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

### Basic Usage Modular

1.  Creating a module

    Huruf awal kapital

        php artisan module:make <module-name>

    Beberapa modul sekaligus

        php artisan module:make <module-name> <module-name> <module-name>
