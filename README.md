Yii2 SoftDelete
===============


Soft delete extension for Yii2 framework.

This extension ensures that soft-deleted has delete native consistent behavior and is IDE-friendly. 

Installation
------------

The preferred way to install this extension is through [composer](http://getcomposer.org/download/).

Either run

```
php composer.phar require --prefer-dist rahulabs/yii2-softdelete "*"
```

or add

```
"rahulabs/yii2-softdelete": "*"
```

to the require section of your `composer.json` file.


Usage
-----

Once the extension is installed, simply use it in your code by  :

Edit model class:
```php
use rahulabs\softdelete\behaviors\SoftDeleteBehavior;
use rahulabs\softdelete\SoftDelete;

class Model extends \yii\db\ActiveRecord
{
    use SoftDelete;

    public function behaviors()
    {
        return [
            'class' => SoftDeleteBehavior::className(),
        ];
    }
}
```

Change database table structures, add `deleted_at (int 11)` field and attached to UNIQUE index. 

API
---

### ActiveRecord class (SoftDelete Trait):

The find series method will return `rahulabs\softdelete\ActiveQuery` Object.

+ softDelete() Deleting data using soft delete mode
+ forceDelete() Use physical deletion mode to force delete data
+ restore() Recover soft deleted model data
+ isTrashed() Whether it is soft deleted

The following commands are `find()` / `findOne()` / `findAll()` Corresponding versions in different modes ：

All models (including soft deleted ones)：

+ findWithTrashed()
+ findOneWithTrashed($condition)
+ findAllWithTrashed($condition)

Find only soft deleted models ：

+ findOnlyTrashed()
+ findOneOnlyTrashed($condition)
+ findAllOnlyTrashed($condition)

The following commands have been rewritten as soft delete versions ：

+ find() 
+ findOne()
+ findAll()
+ delete()

### rahulabs\softdelete\ActiveQuery

increased `withTrashed()`, `withoutTrashed()` and `onlyTrashed()` Three methods，
Set the corresponding search mode。