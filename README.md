# How to setup a simple docker container for laravel.

## Setup: 

1. Clone latest Laravel release from their repo: [https://github.com/laravel/laravel.git](https://github.com/laravel/laravel.git)

2. Install Composer via Docker 
	`docker run --rm -v $(pwd):/app composer/composer:php7 install`

3. Clone/Copy all files from the docker-laravel repo to the directory of your choosing.

4. In your laravel root Remember to rename .env-example to .env

5. Delete the composer.lock file, it makes things die :'(

6. Run Docker with the command:
	* `docker-compose up --build `
	* `docker-compose up --build -d` (for kitematic users)

7. Setting Laravel's Application key and Optimization, to run these commands we type
	* `docker-compose exec app php artisan key:generate`
	* `docker-compose exec app php artisan optimize`

8. To access it in your browser go to http://localhost:8080 

9. Start building in laravel :)


## Notes:

### Artisan: 

So to access Laravel's Artisan via Docker is pretty long winded you have to type:

`docker-compose exec app php artisan ....`

I recommend adding an alias in your terminal's .bash_profile or ohmyzsh's .zshrc like so:

`alias docker-laravel="docker-compose exec app php artisan"`

This saves you a few key strokes here and there. Therefore to run an artisan command would be like so: 

`docker-laravel make:controller MyController`

### Composer Commands: 

Obviously you may want to install packages via composer at some point back in the globally installed days we just did `composer require` but with the docker approach its a bit longer... To install a package,say Laravel Collective's Illuminate/html we would run the following command in our docker container. 

`docker run --rm -v $(pwd):/app composer/composer:php7 require "laravelcollective/html":"^5.2.0"`

### Seeding the DB:

Sometimes you may get the error: `[ReflectionException] Class ...TableSeeder does not exist` when trying to seed the DB using the `db:seed` command if this happens and you're sure its not code related run this command `docker run --rm -v $(pwd):/app composer/composer:php7 dumpautoload` to regenerate the composer packages, then you can run the `db:seed` again, happy seeding!

### SQL Access:
For DB access via Sequal Pro or similar remember to use port 33061 when you connect!

##### References
https://medium.com/@shakyShane/laravel-docker-part-1-setup-for-development-e3daaefaf3c


