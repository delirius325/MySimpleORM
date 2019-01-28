# MySimpleORM
MySimpleORM is a simple PHP/MySQL Object-relational mapping library. It started out as a personal and educational project, but turned into this little project you see here.

## Setting up MySimpleORM (MsORM)

To be able to use the ORM, you need to have a PHP application and a MySQL database. Follow these simple guidelines to setup MsORM on your PHP web application.

### Database-side guidelines

1. The name of your tables are going to be the names of your object classes in PHP. Therefore, a table named "Users" will refer to the class "Users".
2. Make sure that your primary keys all start with "ID". For instance; "IDUsers".

### Application-side setup

1. Make sure to "require" the "BaseClass.php" file in your class file and then extend your class with it.
3. Make sure that your class attributes are all equivalent to your table columns and ensure that they all have the same name.
4. Create your getters/setters.
5. Read the (short) documentation to understand how to select/update/delete/insert objects to your DB.
6. Don't forget to modify the "Database.php" class with your database information.

#### Example of a class

```php
require_once("BaseClass.php");

class MyClass extends BaseClass {
  public $IDMyClass;
  public $Name;

  public __construct() {
    parent::__construct($this);
    $this->IDMyClass = 0;
    $this->Name = "";
  }
  public __destruct() {}

  public getIDMyClass() {
    return $this->IDMyClass;  
  }

  public getName() {
    return $this->Name;  
  }

  public setIDMyClass($id) {
    $this->IDMyClass = $id;  
  }

  public setName($n) {
    $this->Name = $n;  
  }
}
```

#### Example of a table
| _MyClass_ |
|-----------|
| IDMyClass |
| Name      |

## Documentation
*The examples below are all used as if they were part of a function within a controller (MVC).

### Select
#### To select an object by its ID
```php
$Users = new Users();
$Users = $Users->findById(1);
```
You've retrieved the user "1" from the table "Users" and can now use it as an object.

#### To retrieve an array of objects
```php

$Users = new Users();
//replace by whatever condition you desire
$wheres = array(
    "column" => "IDCompanies",
    "condition" => "=",
    "value" => 1 //keep in mind you could use a sub-query here
);
$Users = $Users->getArray($wheres);
```
You've just retrieved all the users that were part of the company "1". You're object ```$Users``` is now an array of ```Users```

#### To retrieve current object, depending on what you've already set
Assuming the database contains a```Users``` with the name "foo".
```php

$Users = new Users();
$Users->setName("foo");
$Users = $Users->getCurrent();

//The mapper returned the object User named "foo"
``` 

### Insert / Update / Delete
Inserting, updating or deleting an object is very simple. All you need to do is call a few functions!
```php
//Insert
$Users = new $Users();
$Users->setName("foo");
$Users->insert();

//Update
$Users->setName("bar");
$Users->update();

//Delete
$Users->delete();
```
