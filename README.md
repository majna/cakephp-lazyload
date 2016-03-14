[![Build Status](https://secure.travis-ci.org/jeremyharris/cakephp-lazyload.png?branch=master)](http://travis-ci.org/jeremyharris/cakephp-lazyload)

# CakePHP LazyLoad Plugin

A lazy loader for CakePHP entities.

## Installation

Requirements

- CakePHP >= 3.1.x, < 4.0.0
- sloth

`$ composer require jeremyharris/cakephp-lazyload`

Load it up in your bootstrap:

`CakePlugin::load('JeremyHarris\LazyLoad');`

## Usage

Add the trait to the entity you wish to lazily load association data for. Or,
attach it to your base entity if you have one to affect all entities:

**src/Model/Entity/User.php**
```php
<?php
namespace App\Model\Entity;

use Cake\ORM\Entity;
use JeremyHarris\LazyLoad\ORM\LazyLoadEntityTrait;

class User extends Entity
{
    use LazyLoadEntityTrait;
}
```

Associations to the Users table can now be lazily loaded from the entity!

### Example

Assuming your Users table belongsTo Groups, you can lazily load Groups instead
of using `contain()`.

```php
<?php
// get an entity, don't worry about contain
$user = $this->Users->get(1);
// group is lazily loaded when you call it here
$groupName = $user->group->name;
```

## Notes

This is not a replacement for contain, which can write complex queries to dictate
what data to contain. The lazy loader obeys the association's conditions that
you set when defining the association on the table, but apart from that it grabs
all associated data.

*The lazy loader requires that your result set is hydrated in order to
provide lazy loading functionality.*

> Special thanks to @lorenzo for reviewing the plugin!
