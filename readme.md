<p align="center"><img src="https://laravel.com/assets/img/components/logo-laravel.svg"></p>

<p align="center">
<a href="https://travis-ci.org/laravel/framework"><img src="https://travis-ci.org/laravel/framework.svg" alt="Build Status"></a>
<a href="https://packagist.org/packages/laravel/framework"><img src="https://poser.pugx.org/laravel/framework/d/total.svg" alt="Total Downloads"></a>
<a href="https://packagist.org/packages/laravel/framework"><img src="https://poser.pugx.org/laravel/framework/v/stable.svg" alt="Latest Stable Version"></a>
<a href="https://packagist.org/packages/laravel/framework"><img src="https://poser.pugx.org/laravel/framework/license.svg" alt="License"></a>
</p>

## 5.8 Laravel test only


Config folder->database.php
.env file check for database

1)php artisan make:migration create_sample_data_table--create=sample_data

2)database foler->migrations foler

3)php artisan migrate

4)php artisan make: model Crud-m

   go to app folder for->Crud.php
5)php artisan make:controller CrudsController --resource

go to App foler->Http foler->CrudsController.php


        $data=Crud::latest()->paginate(5);
        return view('index',compact('data'))->with('i',(request()->input('page',1)-1)*5);







