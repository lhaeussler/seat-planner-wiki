## How to Generate Entities from an Existing Database

When starting work on a brand new project that uses a database, two different situations comes naturally. In most cases, the database model is designed and built from scratch. Sometimes, however, you’ll start with an existing and probably unchangeable database model. Fortunately, Doctrine comes with a bunch of tools to help generate model classes from your existing database.

The first step towards building entity classes from an existing database is to ask Doctrine to introspect the database and generate the corresponding metadata files. Metadata files describe the entity class to generate based on table fields.

```bash
> php bin/console doctrine:mapping:import "App\Entity" annotation --path=src/Entity
```

### Generating the Getters & Setters or PHP Classes
The generated PHP classes now have properties and annotation metadata, but they do not have any getter or setter methods. If you generated XML or YAML metadata, you don’t even have the PHP classes!

To generate the missing getter/setter methods (or to create the classes if necessary), run:
```bash
// generates getter/setter methods for all Entities
> php bin/console make:entity --regenerate App

// generates getter/setter methods for one specific Entity
> php bin/console make:entity --regenerate App\\Entity\\Example
```
### Create Doctrine Controller
```bash
> php bin/console make:controller ExampleControllerName
```
You can now find the new ontroller in your src/controller directory. Please consider creating a new folder `/graphqlcontroller` or `/graphql/controller` an moving your newly created Controller there to prevent issues. Once everthing is moved properly you can start putting in your Queries and Mutations.

### Doctrine Queries
To get started we can write our first Query

>In GraphQLite, GraphQL queries are created by writing methods in controller classes.
Queries are basically used to print or write out values. They cannot change any Objects ins your database.
Those classes must be in the controllers namespaces which has been defined when you configured GraphQLite. For instance, in Symfony, the controllers namespace is App\Controller by default.

```php
namespace App\Controller;

use TheCodingMachine\GraphQLite\Annotations\Query;

class MyController
{
    /**
     * @Query
     */
    public function hello(string $name): string
    {
        return 'Hello ' . $name;
    }
}
```
Make sure that your class naem is always the same as your Filename!

The easiest way to test a GraphQL endpoint is to use GraphiQL or Altair clients (they are available as Chrome or Firefox plugins)
>If you are using the Symfony bundle, GraphiQL is also directly embedded.
Simply head to http://localhost:8000/graphiql
> Your Port may vary!

![](uploads/f9918a21c1125f31d935452c1a14ce90/query1-5a22bbe2398efcc725ea571a07ff2c9b.png)

### Mutations

Bla Bla Blaaa bla Blaaaa





Additional Inforamtion and Source here:
- https://graphqlite.thecodingmachine.io/docs/queries
- https://www.doctrine-project.org/projects/doctrine-orm/en/2.9/tutorials/getting-started.html#entity-repositories