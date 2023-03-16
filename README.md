# Laravel Passport ##

<img width="1440" alt="register" src="https://user-images.githubusercontent.com/55048197/225738529-16ab8ee7-6b4f-40c9-bae3-b058451fbffb.png">

## Installation

``` bash
# clone the repo
$ git clone https://github.com/mudassarali964/laravel-passport-laravel-10.git my-project

# go into app's directory
$ cd my-project

# install app's dependencies
$ composer install

# install app's dependencies
$ npm install

```

### If you choice to use SQLite

``` bash

# create database
$ touch database/database.sqlite
```
Copy file ".env.example", and change its name to ".env".
Then in file ".env" replace this database configuration:
* DB_CONNECTION=mysql
* DB_HOST=127.0.0.1
* DB_PORT=3306
* DB_DATABASE=laravel_passport
* DB_USERNAME=root
* DB_PASSWORD=

To this:

* DB_CONNECTION=sqlite
* DB_DATABASE=/path_to_your_project/database/database.sqlite

### If you choice to use PostgreSQL

1. Install PostgreSQL

2. Create user
``` bash
$ sudo -u postgres createuser --interactive
enter name of role to add: laravel
shall the new role be a superuser (y/n) n
shall the new role be allowed to create database (y/n) n
shall the new role be allowed to create more new roles (y/n) n
```
3. Set user password
``` bash
$ sudo -u postgres psql
postgres= ALTER USER laravel WITH ENCRYPTED PASSWORD 'password';
postgres= \q
```
4. Create database
``` bash
$ sudo -u postgres createdb laravel_passport
```
5. Copy file ".env.example", and change its name to ".env".
   Then in file ".env" replace this database configuration:

* DB_CONNECTION=mysql
* DB_HOST=127.0.0.1
* DB_PORT=3306
* DB_DATABASE=laravel_passport
* DB_USERNAME=root
* DB_PASSWORD=

To this:

* DB_CONNECTION=pgsql
* DB_HOST=127.0.0.1
* DB_PORT=5432
* DB_DATABASE=laravel_passport
* DB_USERNAME=laravel
* DB_PASSWORD=password

### If you choice to use MySQL

Copy file ".env.example", and change its name to ".env".
Then in file ".env" complete this database configuration:
* DB_CONNECTION=mysql
* DB_HOST=127.0.0.1
* DB_PORT=3306
* DB_DATABASE=laravel_passport
* DB_USERNAME=root
* DB_PASSWORD=

### Set APP_URL

> If your project url looks like: example.com/sub-folder
Then go to `my-project/.env`
And modify this line:

* APP_URL =

To make it look like this:

* APP_URL = http://example.com/sub-folder


### Next step

``` bash
# in your app directory
# generate laravel APP_KEY
$ php artisan key:generate

# run database migration and seed
$ php artisan migrate:refresh --seed

# generate mixing
$ npm run build

# and repeat generate mixing
$ npm run dev
```

## Usage

``` bash
# start local server
$ php artisan serve
```

## APIS
1. Register
2. Login
3. List all products
4. Create a product
5. Retrieve a product
6. Update a product
7. Delete a product

## Postman
1. Register API: (POST)
[localhost:8000/api/register](localhost:8000/api/register)

- Body => form-data
* name: someOneName
* email: someOneEmail
* password: password
* confirm_password: repeatPassword

<img width="1440" alt="register" src="https://user-images.githubusercontent.com/55048197/225737071-e0e5c678-6ef3-43ce-8df0-613591ef8e9a.png">

2. Login API: (POST)
[localhost:8000/api/login](localhost:8000/api/login)

- Body => form-data
* email: someOneEmail
* password: password

<img width="1440" alt="login" src="https://user-images.githubusercontent.com/55048197/225737101-092bfb34-d82f-44ed-8031-2c131b9c579a.png">

3. List all products API: (GET)
[localhost:8000/api/products](localhost:8000/api/products)
* Make sure access token (get from login api) in your Headers or Authorization tab

``` bash
‘headers’ => [
    ‘Accept’ => ‘application/json’,
    ‘Authorization’ => ‘Bearer ‘.$accessToken,
]
```

<img width="1440" alt="list all products" src="https://user-images.githubusercontent.com/55048197/225737187-c4237775-b77d-447e-ac89-83a2983ee518.png">

4. Create a product API: (POST)
[localhost:8000/api/products](localhost:8000/api/products)

<img width="1440" alt="create a product" src="https://user-images.githubusercontent.com/55048197/225737659-68576dc1-b970-4bb6-b0c7-13dd2ce2d06e.png">

5. Retrieve a product API: (GET)
[localhost:8000/api/products/1](localhost:8000/api/products/1)

<img width="1440" alt="retrieve a product" src="https://user-images.githubusercontent.com/55048197/225737798-7b60c3c9-dc09-47ed-992f-02e2cca9a337.png">

6. Update a product API: (PUT)
[localhost:8000/api/products/1](localhost:8000/api/products/1)

<img width="1440" alt="update a product" src="https://user-images.githubusercontent.com/55048197/225738194-960d9508-141b-4828-8bc6-dcd0f33e4516.png">

7. Delete a product API: (DELETE)
[localhost:8000/api/products/1](localhost:8000/api/products/1)

<img width="1440" alt="delete a product" src="https://user-images.githubusercontent.com/55048197/225738442-4e4190d5-3d95-4d01-81b4-d0bf8fbca963.png">

## Postman collection path in json file

[localhost:8000/collection/LaravelPassport.postman_collection.json](localhost:8000/collection/LaravelPassport.postman_collection.json)

## About Passport - Following 7 points are most important

1. Install Passport Auth:

``` bash
$composer require laravel/passport
```

2. After successfully install laravel passport, register providers. Open config/app.php . and put the bellow code:

``` bash
# config/app.php
    'providers' =>[
        Laravel\Passport\PassportServiceProvider::class,
    ],
```

3. Now, you need to install laravel to generate passport encryption keys. This command will create the encryption keys needed to generate secure access tokens:

``` bash
$ php artisan passport:install
```

4. Passport Configuration:

``` bash
# In this step, Navigate to App/Models directory and open User.php file. Then update the following code into User.php:\
    
    use Laravel\Passport\HasApiTokens;
    class User extends Authenticatable
    {
       use HasApiTokens;
```
   

5. Next Register passport routes in App/Providers/AuthServiceProvider.php:

``` bash
# Go to App/Providers/AuthServiceProvider.php and update this line => Register Passport::routes(); inside of boot method

    <?php
    namespace App\Providers;
    use Laravel\Passport\Passport;
    use Illuminate\Support\Facades\Gate;
    use Illuminate\Foundation\Support\Providers\AuthServiceProvider as ServiceProvider;
     
     
    class AuthServiceProvider extends ServiceProvider
    {
        /**
         * The policy mappings for the application.
         *
         * @var array
         */
        protected $policies = [
            'App\Model' => 'App\Policies\ModelPolicy',
        ];
     
     
        /**
         * Register any authentication / authorization services.
         *
         * @return void
         */
        public function boot()
        {
            $this->registerPolicies();
        }
    }
```

6. Next, Navigate to config/auth.php and open auth.php file. Then Change the API driver to the session to passport:

``` bash
# Put this code ‘driver’ => ‘passport’, in API

[ 
         'web' => [ 
             'driver' => 'session', 
             'provider' => 'users', 
         ], 
         'api' => [ 
             'driver' => 'passport', 
             'provider' => 'users', 
         ], 
     ],
```

7. Run Migration:

``` bash
$ php artisan migrate
```




