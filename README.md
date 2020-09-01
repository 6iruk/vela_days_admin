# Vela-Days-Admin

## Prerequisites
Before you get started make sure Apache, PHP and MySQL are correctly installed and configured. To effectively run some of the commands listed below, you'd need to add PHP to your PATH Environment Variable. [Composer](https://getcomposer.org/download/) is required to download dependencies and hence is a neccessity.
To check if PHP is correctly installed, run
```sh
php -version
```
if you also want to check if Composer is installed successfully, run
```sh
composer
```

## Installation
You can install all dependencies by running the following command from the root directory of the project
```sh
composer install
```

## .env
The .env file is not commited so you must create a .env file in the root directory. The easiest way to do so would be to copy the .env.example file and change the following values.
```
APP_KEY=base64:KqhSRIzzD1KfuxVOvLaMhW2xmpmmRu6PTYR9YcIvfD8=

DB_DATABASE=[DATABASE_NAME]
DB_USERNAME=[DATABASE_USERNAME]
DB_PASSWORD=[DATABASE_PASSWORD]
```
[DATABASE_NAME] must be an empty database and [DATABASE_USERNAME] must be a valid user on your MySQL instance. [DATABASE_PASSWORD] can be left empty if there's no password associated with that particular user.   

## Database Migrations & Seeding
Laravel allows you to create all tables in a database using this one single command
```sh
php artisan migrate
```
**If you're using PHP 7.4, you might encounter a "PHP Error : Unparenthesized `a ? b : c ? d : e` is deprecated. Use either `(a ? b : c) ? d : e` or `a ? b : (c ? d : e)`" error. To solve this you must make changes to /vendor/themsaid/laravel-langman/src/Commands/FindCommand.php file. To be exact, replace the following foreach statement on line 111 with following statement**
```php
foreach ($allLanguages as $languageKey) {
    $original[$languageKey] =
        $values[$languageKey] ??
            $values[$languageKey]
            ?? isset($filesContent[$fileName][$languageKey][$key]) ? $filesContent[$fileName][$languageKey][$key] : '';
}
```
To seed the database, run the following command
```sh
php artisan db:seed
```
