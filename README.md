# laravel-blog


- ./vendor/bin/sail up

- ./vendor/bin/sail bash

- installing filament Php

- cmd: composer require filament/filament:"^2.0"

- next step put it in composer.json file as 

- "post-update-cmd":["@php artisan filament:upgrade"]



- next step migration to create database and models for the dashboard

- php artisan migrate

- To create an user in filament dashboard

- php artisan make:filament-user


- we have to create storage links for images 

- cmd: php artisan storage:link

- Now lets create Models


- php artisan make:model Category -m

- php artisan make:model Post -m

- php artisan make:model CategoryPost -m



- now lets open categories table

- after declaring variables then migrate it 
- php artisan migrate
- next model link class to eloquent relationships

- next step creating filament resources

- through its documentation

- To create a resource for the App\Models\Customer model:

- php artisan make:filament-resource Customer

- use this cmd in our project

- php artisan make:filament-resource Category --simple --generate

- Now you will see a category column in our dashboard

- next install composer require doctrine/dbal --dev


- if you ant dedicated view page you should add this cmd

- php artisan make:filament-resource Post --view --generate



- I have done an mistake in the database column declaration file as nullable without using function bracket as nullable();

- so we have modify the table coulumn so we have  to create a migration file 
- 1.php artisan make:migration modify_thumbnail_column_in_your_table

```
public function up()
{
    Schema::table('your_table_name', function (Blueprint $table) {
        $table->string('thumbnail', 2048)->nullable()->change();
    });
}
```
```
public function down()
{
    Schema::table('your_table_name', function (Blueprint $table) {
        $table->string('thumbnail', 2048)->change();
    });
}
```
- php artisan migrate

- then passing migrate command if you didn't see any changes then try these cmds

- php artisan cache:clear


- composer dump-autoload


- In my case i didn't see any changes so the filament resource is the issue 
they clearly mentioned with thumbnail as required like below

  ```
    Forms\Components\TextInput::make('thumbnail')
                    ->required(),
                    ->maxLength(2048),
```
- Now I removed required now its working completely fine