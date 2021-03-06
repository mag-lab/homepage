+++
date = "2018-12-21T00:00:08+02:00"
draft = false
title = "Install strichliste"
[menu]
  [menu.main]
    parent = "Install"
+++

For strichliste to run, **PHP 7.1 or higher is required**. You should have a webserver running which supports **mod_php** or **php-fpm**.

### Installing

1. Go to the Github project to download the [latest release](https://github.com/strichliste/server/releases). It comes already with a bundled front-end.
2. Extract the package content to your target directory (e.g. `tar xvfz strichliste.tar.gz -C /var/www/strichliste.yourdomain.tld`)
3. Move the database in `var/` from `app.db.example` to `app.db` if you want to use the default sqlite setup

If you want to keep sqlite as your database, you're done. Continue configuring your webserver

### Using a different database (optional)

The [ORM](https://www.doctrine-project.org/projects/doctrine-dbal/en/2.9/reference/platforms.html) used in
Strichliste supports multiple database backends such as:

* MySQL / MariaDB
* Oracle
* Microsoft SQL Server
* PostgreSQL
* SQLite

If you want to use another database then sqlite, just adjust the `DATABASE_URL` variable in your `.env` file in your root
directory according to the [Doctrine ORM](https://www.doctrine-project.org/projects/doctrine-dbal/en/2.9/reference/configuration.html#connecting-using-a-url)
recommendations.

For example, to configure **mysql/mariadb**:

```
DATABASE_URL="mysql://strichliste:32YourPassWord42@localhost/strichliste"
```

Create a database and a separate user:

```sql
CREATE USER 'strichliste'@'localhost' IDENTIFIED BY '32YourPassWord42';
GRANT ALL PRIVILEGES ON strichliste.* TO 'strichliste'@'localhost';
FLUSH PRIVILEGES;
```

Afterwards just run the following commands to create the schema:

```bash
php bin/console doctrine:schema:create
```

You're done! Strichliste now works with mysql instead of sqlite.

### Configuring NGINX

Config examples for nginx can be found here:

* https://github.com/strichliste/server/blob/master/examples/nginx_ssl.conf (with SSL)
* https://github.com/strichliste/server/blob/master/examples/nginx.conf (without SSL)

### Configuring Apache

* https://github.com/strichliste/server/blob/master/examples/apache.conf (without SSL)
* TODO: SSL-Config

### Common Pitfalls

* Check your folder owner/group if you're using sqlite as your database! Otherwise strichliste can't write to it.

### Commands

#### Import strichliste 1 database

To import your old strichliste 1 database, copy the `database.sqlite`-file to the strichliste2 directory and run:

`php bin/console app:import database.sqlite`

After import the terminal outputs "Import done!"



 
