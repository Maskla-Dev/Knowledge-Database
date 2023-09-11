# Configuration
Laravel config files can be reached in `/config` path from the root project. Environment configuration has environment variables of the server where the application is running. Any variable at server or system level will override environment config from Laravel project. Environment variables are loaded in PHP super global.

Access to config values follows:
```php
<?php
	$time = config("app.timezone"); //Read
	config(['app.timezon'] => "America/Chicago"); //Write
?>
```
# Directory structure
- `/app` contains core application code. Default namespace is App. Nested directories may be generated after ``artisan make`` command.
	- `/app/Console` serves as API for artisan commands, redirects to console processing.
	- `/app/Http` Controllers in MVC.
	- `/app/models` Models in MVC
	- 
- `/bootsrap`  contains code to run the framework (**don't modify**)
- `/config` config framework variables
- `/database` for database migration or SQLite container
- `/public` entry point of the host and assets storage
- `/resources` stores view (V in MVC) and assets.
- `/routes`  `web.php` handles routes, state sessions and some protections. `api.php` handles routes via tokens. `console.php` entry point to console commands. `channels.php` web sockets entry points.
- `/storage` serves as app and framework generated files and log files.
- `/tests` testing files with PHPUnit.
- `/vendor` Composer dependencies.
