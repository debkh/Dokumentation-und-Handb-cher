Yii Database Migration Manual
=============================

Preparing system enviroment
---------------------------

First of all, we need to check our php-cli version and availability. Open the terminal, and enter next command:

``` php.exe -v ```

After that, we need to create migration, enter to project directory and type the next command
``` yii.bat migrate/create {migration_name} ```

For example:

``` yii.bat migrate/create create_category_table ```

or

``` yii.bat migrate/create alter_category_table ```

This command create ``` migrations ``` folder in console directory and migration class with empty data.

``` 
<?php

use yii\db\Schema;
use yii\db\Migration;

class m150101_185401_create_category_table extends Migration
{
    public function up()
    {
    }

    public function down()
    {
        echo "m101129_185401_create_category_table cannot be reverted.\n";
        return false;
    }
} 
```
You can use ActiveRecord methods or SQL queries for creating/changing tables or rows.

For example:

```
use yii\db\Schema;
use yii\db\Migration;

class m150101_185401_create_category_table extends \yii\db\Migration
{
    public function up()
    {
        $this->createTable('category', [
            'id' => Schema::TYPE_PK,
            'title' => Schema::TYPE_STRING . ' NOT NULL',
            'content' => Schema::TYPE_TEXT,
        ]);
    }

    public function down()
    {
        $this->dropTable('category');
    }

}
```


After creating new migrations, or fetching other migrations from git, we need to execute them, via next command:

``` yii.bat migrate ```

This command will migrate all new migrations.

If we need migrate only one migration, we can use next command: 

``` yii.bat migrate 3 ```

And of course we have a method for removing changes from last migration:

``` yii.bat migrate/down ```


Full documentation for migration methods you can find here http://www.yiiframework.com/doc-2.0/yii-db-migration.html
