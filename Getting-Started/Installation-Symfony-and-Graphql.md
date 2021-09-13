Install Symfony
**Technical Requirements**

Before creating your first Symfony application you must:

- Install PHP 7.2.5 or higher.
```css
> sudo apt install php7.4-{sqlite,xml,mbstring}
```
- Install Composer, which is used to install PHP packages.

```css 
> php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
> php -r "if (hash_file('sha384', 'composer-setup.php') === '756890a4488ce9024fc62c56153228907f1545c228516cbf63f885e036d37e9a59d27d63f46af1d4d07ee0f76181c7d3') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
> php composer-setup.php
> php -r "unlink('composer-setup.php');"
```
- Install Symfony

```css
> wget https://get.symfony.com/cli/installer -O - | bash
```

**Creating Symfony Applications**

Open your console terminal and run any of these commands to create a new Symfony application:
```css
# Full application
> symfony new my_project_name --full
# Microservice
> symfony new my_project_name
# Demo Files
> symfony new my_project_name --demo
```
The only difference between these two commands is the number of packages installed by default. The --full option installs all the packages that you usually need to build web applications, so the installation size will be bigger.
The Symfony Demo Application is a fully-functional application that shows the recommended way to develop Symfony applications. It’s a great learning tool for Symfony newcomers and its code contains tons of comments and helpful notes.


If you’re not using the Symfony binary, run these commands to create the new Symfony application using Composer
```css
# Composer for Full Version
> composer create-project symfony/website-skeleton my_project_name
# Composer for Demo And Microservice Build
> composer create-project symfony/skeleton my_project_name
```

**Setting up an Existing Symfony Project**

In addition to creating new Symfony projects, you will also work on projects already created by other developers. In that case, you only need to get the project code and install the dependencies with Composer. Assuming your team uses Git, setup your project with the following commands:
```css
> cd /my_project_name
> composer install
> composer update
```

**Running Symfony Applications**

In production, you should install a webserver like Nginx or Apache and configure it to run Symfony. This method can also be used if you’re not using the Symfony local web server for development.

However for local development, the most convenient way of running Symfony is by using the local web server provided by the symfony binary. This local server provides among other things support for HTTP/2, concurrent requests, TLS/SSL and automatic generation of security certificates.

Open your console terminal, move into your new project directory and start the local web server as follows:
```css
symfony server:start
```

For additional information visit [https://symfony.com/doc/current/setup.html#start-coding](https://symfony.com/doc/current/setup.html#start-coding)

**Adding Graphql**