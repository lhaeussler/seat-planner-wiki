
### Pull the MySQL Docker Image
Start by pulling the appropriate Docker image for MySQL. You can download a specific version or opt for the latest release as seen in the following command:
```bash
sudo docker pull mysql/mysql-server:latest
```
If you want a particular version of MySQL, replace `latest` with the version number.


### Installing Doctrine
First, install Doctrine support via the orm Symfony pack, as well as the MakerBundle, which will help generate some code:

```bash
> composer require symfony/orm-pack
> composer require --dev symfony/maker-bundle
```

### Configuring the Database
The database connection information is stored as an environment variable called `DATABASE_URL`. For development, you can find and customize this inside `.env` in your main directory:
```css
# customize this line!
DATABASE_URL="mysql://db_user:db_password@127.0.0.1:3306/db_name?serverVersion=5.7"

# to use mariadb:
DATABASE_URL="mysql://db_user:db_password@127.0.0.1:3306/db_name?serverVersion=mariadb-10.5.8"

# to use sqlite:
# DATABASE_URL="sqlite:///%kernel.project_dir%/var/app.db"

# to use postgresql:
# DATABASE_URL="postgresql://db_user:db_password@127.0.0.1:5432/db_name?serverVersion=11&charset=utf8"

# to use oracle:
# DATABASE_URL="oci8://db_user:db_password@127.0.0.1:1521/db_name"
```

> If the username, password, host or database name contain any character considered special in a URI (such as +, @, $, #, /, :, *, !), you must encode them. See RFC 3986 for the full list of reserved characters or use the urlencode function to encode them. In this case you need to remove the resolve: prefix in > config/packages/doctrine.yaml to avoid errors: url: '%env(resolve:DATABASE_URL)%'


https://symfony.com/doc/current/doctrine.html