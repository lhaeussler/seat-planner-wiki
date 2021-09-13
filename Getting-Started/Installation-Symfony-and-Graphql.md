Install Symfony
=========================
### Technical Requirements
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

### Creating Symfony Applications

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

### Setting up an Existing Symfony Project

In addition to creating new Symfony projects, you will also work on projects already created by other developers. In that case, you only need to get the project code and install the dependencies with Composer. Assuming your team uses Git, setup your project with the following commands:
```css
> cd /my_project_name
> composer install
> composer update
```
### Running Symfony Applications

In production, you should install a webserver like Nginx or Apache and configure it to run Symfony. This method can also be used if you’re not using the Symfony local web server for development.

However for local development, the most convenient way of running Symfony is by using the local web server provided by the symfony binary. This local server provides among other things support for HTTP/2, concurrent requests, TLS/SSL and automatic generation of security certificates.

Open your console terminal, move into your new project directory and start the local web server as follows:
```css
symfony server:start
```

For additional information visit [https://symfony.com/doc/current/setup.html#start-coding](https://symfony.com/doc/current/setup.html#start-coding)

Adding Doctrine and Graphql
=========================
### Doctrine Installation and Configuration

Doctrine can be installed with Composer.
Define the following requirement in your `composer.json` file:
```css
{
    "require-dev": {
        "symfony/web-server-bundle": "^4.4",
        "doctrine/orm": "*"
        
    }
}
```
Then call composer install from your command line. If you don't know how Composer works, check out their Getting Started to set up.

### Adding Graphql to Symfony

Open a terminal in your current project directory and run:
```
> composer require thecodingmachine/graphqlite-bundle
```
Enable the library by adding it to the list of registered bundles in the app/AppKernel.php file:
```css
#app/AppKernel.php
<?php
class AppKernel extends Kernel{    public function registerBundles()    {        $bundles = array(            // other bundles...            new TheCodingMachine\GraphQLite\Bundle\GraphQLiteBundle,        );    }}
```
Now, enable the "graphql/" route by editing the config/routes.yaml file:
```css
config/routes.yaml
# Add these 2 lines to config/routes.yamlgraphqlite_bundle:  resource: '@GraphqliteBundle/Resources/config/routes.xml'
```
Last but not least, create the configuration file at config/packages/graphqlite.yaml:
```
config/packages/graphqlite.yaml
graphqlite:  namespace:    # The namespace(s) that will store your GraphQLite controllers.    # It accept either a string or a list of strings.    controllers: App\GraphqlController\    # The namespace(s) that will store your GraphQL types and factories.    # It accept either a string or a list of strings.    types:    - App\Types\    - App\Entity\
```
## Advanced configuration
### Customizing error handling
You can add a "debug" section in the graphqlite.yaml file to customize the way errors are handled. By default, GraphQLite configures the underlying Webonyx GraphQL library this way:
-All exceptions that implement the ClientAware interface are caught by GraphQLite
-All other exceptions will bubble up and by caught by Symfony error handling mechanism
We found out those settings to be quite convenient but you can override those to your preference.
```css
config/packages/graphqlite.yaml
graphqlite:  # ...  debug:    # Include exception messages in output when an error arises.    INCLUDE_DEBUG_MESSAGE: false    # Include stacktrace in output when an error arises.    INCLUDE_TRACE: false    # Exceptions are not caught by the engine and propagated to Symfony.    RETHROW_INTERNAL_EXCEPTIONS: false    # Exceptions that do not implement ClientAware interface are    # not caught by the engine and propagated to Symfony.    RETHROW_UNSAFE_EXCEPTIONS: true
```
The debug parameters are detailed in the documentation of the Webonyx GraphQL library which is used internally by GraphQLite.
**Do not put your GraphQL controllers in the** `App\Controller` namespace Symfony applies a particular compiler pass to classes in the `App\Controller` namespace. This compiler pass will prevent you from using input types. Put your controllers in another namespace. We advise using `App\GraphqlController.`
The Symfony bundle come with a set of advanced features that are not described in this install documentation (like providing a login/logout mutation out of the box). Jump to the "Symfony specific features" documentation of GraphQLite if you want to learn more.



Original can be found her:
[https://graphqlite.thecodingmachine.io/docs/symfony-bundle](https://graphqlite.thecodingmachine.io/docs/symfony-bundle)