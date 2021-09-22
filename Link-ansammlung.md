- https://www.doctrine-project.org/projects/doctrine-orm/en/2.9/tutorials/getting-started.html#entity-repositories
- https://symfony.com/doc/current/doctrine/reverse_engineering.html
- https://symfony.com/doc/current/doctrine.html#configuring-the-database
- https://docs.docker.com/engine/reference/commandline/run/#publish-or-expose-port--p---expose
- https://graphqlite.thecodingmachine.io/docs/queries

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
