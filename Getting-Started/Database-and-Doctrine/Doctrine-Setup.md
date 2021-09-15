## Installing Doctrine
First, install Doctrine support via the orm Symfony pack, as well as the MakerBundle, which will help generate some code:

```bash
> composer require symfony/orm-pack
> composer require --dev symfony/maker-bundle
```

### Configuring the Database
The database connection information is stored as an environment variable called `DATABASE_URL`. For development, you can find and customize this inside `.env` in your main directory:

![](uploads/4b0b2aea7469913ed40d97ae7fcd0929/Screenshot_30.png)
> If the username, password, host or database name contain any character considered special in a URI (such as +, @, $, #, /, :, *, !), you must encode them. See RFC 3986 for the full list of reserved characters or use the urlencode function to encode them. In this case you need to remove the resolve: prefix in > config/packages/doctrine.yaml to avoid errors: url: '%env(resolve:DATABASE_URL)%'
```bash 
> php bin/console doctrine:database:create
```
A few helpfull sites this is based on:
- https://symfony.com/doc/current/doctrine.html