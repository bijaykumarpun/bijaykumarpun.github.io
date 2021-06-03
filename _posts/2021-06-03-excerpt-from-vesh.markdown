## MySQL 8 & Laravel migration error

Something changed in MySQL8 - the default authentication plugin - causing `php artisan migrate` to not work as intended.

> This is an exceprt from a GitHub issue created on [Vesh Grg's repository](https://github.com/VeshGrg/laravel_email_notify) - the link could be private!

More below:

This error occurs during database migration with `php artisan migrate`.
Possible issue could be due to wrongly configured *.env* file.

Full stacktrace:

```
   Illuminate\Database\QueryException 

  SQLSTATE[HY000] [2054] The server requested authentication method unknown to the client (SQL: select * from information_schema.tables where table_schema = laravel and table_name = migrations and table_type = 'BASE TABLE')

  at vendor/laravel/framework/src/Illuminate/Database/Connection.php:678
    674▕         // If an exception occurs when attempting to run a query, we'll format the error
    675▕         // message to include the bindings with SQL, which will make this exception a
    676▕         // lot more helpful to the developer instead of just the database's errors.
    677▕         catch (Exception $e) {
  ➜ 678▕             throw new QueryException(
    679▕                 $query, $this->prepareBindings($bindings), $e
    680▕             );
    681▕         }
    682▕ 

      +33 vendor frames 
  34  artisan:37
      Illuminate\Foundation\Console\Kernel::handle(Object(Symfony\Component\Console\Input\ArgvInput), Object(Symfony\Component\Console\Output\ConsoleOutput))
```

Also, a snippet of the locally configured *.env* file:

```
APP_NAME=Laravel
APP_ENV=local
*APP_KEY=base64:/qgmHvbwlINiFb47G8QBjaKwmPqG4oW0hrSaAe8fDk8= *
APP_DEBUG=true
APP_URL=http://localhost

LOG_CHANNEL=stack
LOG_LEVEL=debug

DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=laravel
DB_USERNAME=root
DB_PASSWORD=

BROADCAST_DRIVER=log
CACHE_DRIVER=file
QUEUE_CONNECTION=sync
SESSION_DRIVER=file
SESSION_LIFETIME=120

MEMCACHED_HOST=127.0.0.1 
```
Steps performed :

- Making sure MySQL server is running properly
> Running `> mysql.server start` returns a *Success* message

- Making sure MySQL database credentials are correct
> Running `> mysql -u root` puts user inside MySQL interface

- Making sure MySQL server address/port is correct
> Running `>netstat -an | grep "LISTEN"` returns all IP address with open port; Contains the default MySQL server port address *3306*. This port can also be checked with `SHOW GLOBAL VARIABLES LIKE 'PORT'` inside MySQL interface


---

Database configured inside *.env* file apparently didn't exist.
Running `>SHOW DATABASES;` inside MySQL interface showed all databases except the `laravel` database configured by default in *.env* file.
> Apparently ~~Laravel~~ Migrations can only work on *Database* level - meaning it can do everything that is possible within a database - such as create tables - but not actually create database itself.

This however didn't solve the issue.

---

Adding `DB_SOCKET` variable with path of *mysql.sock* as value inside *.env* seems to have solved some* cases.

Path of *mysql.sock* file can be found with `> find \ mysql.sock` - very time consuming-
Or just via MySQL interface with `SHOW GLOBAL VARIABLES LIKE socket;`

In this case - the file was in `\tmp\mysql.sock` - locked even with *sudo* access.

The final change in *.env* file looked:
`DB_SOCKET=\tmp\mysql.sock`

This however didn't solve the issue.

> Need confirmation: `mysql.sock` is a socket file created after MySQL server starts - and destroyed after MySQL server stops.

---

[This](https://stackoverflow.com/questions/50547724/how-to-resolve-the-error-sql-authentication-method-unknown-in-laravel-mysql) Stackoverflow solution that talks about setting legacy style password for PHP7+ and MySQL 8 solved the issue.

- >  Run `ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'root'; ` command inside MySQL interface to set native password for current user
- > Set the password inside *.env* file as well
- > Finally run `php artisan migrate`

> Apparently, the default authentication plugin changed in MySQL 8 to `caching_sha2_password` - thus causing the *authentication method* issue during migration
Above code explicitly sets authentication plugin to *mysql_native_password* for the current user

---
