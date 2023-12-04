---
author: os
created: 2020-12-08
title: MySQL with JSON in Laravel
intro: Learn about JSON columns in MySQL and how to use them in Laravel.
lead: Learn about JSON columns in MySQL and how to use them in Laravel.
figure:
  src: mysql-json-laravel.png
tag:
  - webdev
---


## Why JSON columns?

MySQL, like any other relational database, is great at modelling data structures and making connections between them. But what if there is some parts of your data that does not fit into a relational model - data that does not follow a strict schema? You could opt for a NoSQL database like MongoDB, that is optimized for storing JSON-like documents. But the truth is you don't need another database. MySQL has had a built-in JSON column type since 5.7, and a lot of improvements have been introduced with the 8.0 release. This hybrid approach is not new - PostgreSQL has supported JSON since 2013.

## RAW SQL - preparation

To understand what you can do with JSON columns, let's create a table with a `meta` JSON field and also a reference to an imaginary users table. (Feel free to ignore the `user_id` field: it's just there to show that we can mix relational data and JSON objects in a single table.)

```
CREATE TABLE things (
    id INT AUTO_INCREMENT PRIMARY KEY,
    user_id INT NOT NULL,
    meta JSON,
    created_at DATETIME DEFAULT CURRENT_TIMESTAMP
);    
```

We also need some dummy data to play around with. If you take a look at the `INSERT` statements below, you will notice that the values we insert into the `meta` fields look like strings.

```
INSERT INTO things (user_id, meta) VALUES(100, '{"single": "Towel", "many": ["Toilet Paper", "Mirror", "Soap"]}');
INSERT INTO things (user_id, meta) VALUES(200, '{"single": "Gingerbread", "many": ["Clotted cream", "Fruit fool"]}');
INSERT INTO things (user_id, meta) VALUES(300, '{"single": "Table", "many": ["Sideboard", "Bench", "Wardrobe"]}');
```

To validate the inserts, let's query the whole table:

```
SELECT * FROM `things`;
+----+---------+--------------------------------------------------------------------+---------------------+
| id | user_id | meta                                                               | created_at          |
+----+---------+--------------------------------------------------------------------+---------------------+
|  1 |     100 | {"many": ["Toilet Paper", "Mirror", "Soap"], "single": "Towel"}    | 2020-12-01 10:00:41 |
|  2 |     200 | {"many": ["Clotted cream", "Fruit fool"], "single": "Gingerbread"} | 2020-12-01 10:00:42 |
|  3 |     300 | {"many": ["Sideboard", "Bench", "Wardrobe"], "single": "Table"}    | 2020-12-01 10:00:43 |
+----+---------+--------------------------------------------------------------------+---------------------+
```

As you can see, there is nothing special so far. The `meta` fields look like the JSON encoded strings we inserted previously, just like any other column with string data type `TEXT` or `VARCHAR`.

However, under the hood MySQL stores the values in a binary format and validates the documents when inserting or updating them. Which means, if you try to insert invalid or broken JSON, you will get an `Invalid JSON text` error.

## Raw SQL - JSON queries

So far we gained almost nothing from the JSON columns, except a bit of validation. But there is much more!

Let's start with a very basic query and try to select specific data from our `meta` field. The JSON objects in our example have two properties on the root level: "many" and "single". As of MySQL 5.7.13, we can use the `->>` accessor to specify which property we want to access. If this were a PHP object, you would call `$meta->single` to retrieve the values of the `single` property on the `$meta` object. The MySQL syntax is a bit different:

```
SELECT user_id, meta->>"$.single" FROM `things`;
+---------+-------------------+
| user_id | meta->>"$.single" |
+---------+-------------------+
|     100 | Towel             |
|     200 | Gingerbread       |
|     300 | Table             |
+---------+-------------------+
```

If you are still on MySQL 5.7.12 or lower, instead of `->>` you should use `->`. With this accessor, all string values are quoted - for example `Towel` becomes `"Towel"`. If you wrap your expression in a `JSON_UNQUOTE()` function you can get rid of the quotes without using the `->>` operator.

So far we've extracted data from the nested JSON object in our result. Using it in a WHERE condition or with an ORDER BY clause is even more interesting. In the example below, we basically search in the JSON object and limit the result to the matching condition.

```
SELECT user_id, meta FROM `things` WHERE meta->>"$.single" = 'Gingerbread';
+---------+--------------------------------------------------------------------+
| user_id | meta                                                               |
+---------+--------------------------------------------------------------------+
|     200 | {"many": ["Clotted cream", "Fruit fool"], "single": "Gingerbread"} |
+---------+--------------------------------------------------------------------+
```

You can go even further using functions like `JSON_CONTAINS`, `JSON_EXTRACT` or `JSON_KEYS` to perform more advanced search or comparison operations on JSON values. Explaining all the functions would be beyond the scope of this article, but the [official documentation](https://dev.mysql.com/doc/refman/8.0/en/json-search-functions.html) covers plenty of use cases. Here is just a basic example of how to use `JSON_CONTAINS()`:  
  
```
SELECT user_id, meta  FROM `things` WHERE JSON_CONTAINS(`meta`, JSON_QUOTE('Wardrobe'), '$.many');
+---------+-----------------------------------------------------------------+
| user_id | meta                                                            |
+---------+-----------------------------------------------------------------+
|     300 | {"many": ["Sideboard", "Bench", "Wardrobe"], "single": "Table"} |
+---------+-----------------------------------------------------------------+
```

## Laravel built-in support

Let's be honest, who writes raw SQL these days? Most likely you rely on some kind of abstraction layer to access your database. Eloquent has supported JSON columns since Laravel 5.7, which means it translates a human readable syntax to a [grammar specific to MySQL](https://github.com/laravel/framework/blob/8.x/src/Illuminate/Database/Query/Grammars/MySqlGrammar.php) or other database engines. With the `$casts` property on your Model you specify how you want to work with the decoded JSON in PHP.

The migration below describes the table we used before:

```
<?php

use Illuminate\Database\Migrations\Migration;
use Illuminate\Database\Schema\Blueprint;
use Illuminate\Support\Facades\Schema;

class CreateThingsTable extends Migration
{
    public function up(): void
    {
        Schema::create('things', function (Blueprint $table) {
            $table->id();
            $table->foreignIdFor(\App\Models\User::class);
            $table->json('meta')->nullable();
            $table->timestamps();
        });
    }
}
```

In the `App\Models\Thing` class you define a caster for the JSON field. It's up to you if you prefer work with an associative `array` or with an `object` of stdClass:

```
<?php

namespace App\Models;

use Illuminate\Database\Eloquent\Model;

class Thing extends Model
{
    protected $casts = [
        'meta' => 'array',
    ];
}

```

These are the SQL queries we used before translated to Eloquent:

```
// all things
App\Models\Thing::all();

// user_id and the meta.single property
$things = App\Models\Thing::select(['user_id', 'meta->single'])->get();

// all things where the meta.single property matchs 'Gingerbread'
$things = App\Models\Thing::where('meta->single', 'Gingerbread')->get();

// all things where the meta.many array contains Wardrobe
$things = App\Models\Thing::whereJsonContains('meta->many', 'Wardrobe')->first();

```

To prove that the JSON encoded string is cast to an array, we can dump the `$things->meta` attribute of the last query:

```
array:2 [▼
  "many" => array:3 [▼
    0 => "Sideboard",
    1 => "Bench",
    2 => "Wardrobe"
  ]
  "single" => "Table"
]
   
```

As you would expect, type casting also works the other way around. You don't need to worry about serializing or encoding to JSON before saving the data. It happens automatically since you've defined the `$casts` property in your model:  

```
// read
$thing = Thing::find(1);
$meta = $thing->meta;

// manipulate 
$meta['single'] = 'overwrite';
$meta['many'][] = 'or add something';

// write
$thing->meta = $meta;
$thing->save();
```

## Indexing and virtual columns

MySQL doesn't have a way to index JSON documents directly, but there is an alternative: generated columns.

As long as you don't use a `WHERE` condition or an `ORDER BY` clause on the JSON column, you don't need to worry about generated columns and indexing. On a very small dataset it's also not that important, but with larger datasets the right index will improve read performance a lot.

To index a property within your JSON document, you first create a generated column. By default is a `VIRTUAL` column, which means values in these columns are evaluated on-the-fly and do not take up any storage. The `STORED` keyword, on the other hand, indicates that values are evaluated when rows are inserted or updated.

Let's have a look at the syntax:

```
ALTER TABLE things ADD v_single VARCHAR(30) AS (meta->>"$.single") VIRTUAL;
ALTER TABLE things ADD INDEX `idx_single` (v_single);
```

The expression after `AS` tells MySQL how to access the value for the generated column. The second line creates a secondary index with the name `idx_single` on the column with the name `v_single` we've just defined.

The Laravel migration for altering the table with the virtual column and the index is even easier:

```
Schema::table('things', function (Blueprint $table) {
    $table->string('v_single', 30)
        ->virtualAs('meta->>"$.single"')
        ->index('idx_single');
});
```

Let's have a look at the different index usage using `EXPLAIN`.
Before adding the index:

```
EXPLAIN SELECT user_id, meta FROM `things` WHERE meta->>"$.single" = 'Gingerbread';
+----+-------------+--------+------+---------------+------+---------+------+------+----------+-------------+
| id | select_type | table  | type | possible_keys | key  | key_len | ref  | rows | filtered | Extra       |
+----+-------------+--------+------+---------------+------+---------+------+------+----------+-------------+
|  1 | SIMPLE      | things | ALL  | NULL          | NULL | NULL    | NULL |    3 |   100.00 | Using where |
+----+-------------+--------+------+---------------+------+---------+------+------+----------+-------------+
```

And after adding the `idx_single` index on the generated column `v_single`:

```
EXPLAIN SELECT user_id, meta FROM `things` WHERE meta->>"$.single" = 'Gingerbread';
+----+-------------+--------+------+---------------+------------+---------+-------+------+----------+-------+
| id | select_type | table  | type | possible_keys | key        | key_len | ref   | rows | filtered | Extra |
+----+-------------+--------+------+---------------+------------+---------+-------+------+----------+-------+
|  1 | SIMPLE      | things | ref  | idx_single    | idx_single | 123     | const |    1 |   100.00 | NULL  |
+----+-------------+--------+------+---------------+------------+---------+-------+------+----------+-------+
```

Explanation of the `EXPLAIN`: In the first example, "Key `NULL`", "Rows `3`" and "Extra `Using where`" mean we perform a full table scan across the entire table - no index is used because there is none.

For the same query, after adding the index, we see "Key `idx_single`" - the key (index) that MySQL actually decided to use - and "Rows `1`" - the number of rows MySQL thinks it has to examine to execute the query. Fewer rows means less work for the database and faster execution.

## Summary

I learned a few new things in preparing this article and I hope some of you have too. Everything discussed here can be used on fortrabbit. For Apps on the Universal Stack, MySQL 5.7 has been available for a while, and recently we [introduced Mysql 8.0](https://blog.fortrabbit.com/mysql-8-now-available-for-pro-apps) support on the Professional Stack.

In a follow-up article you will learn how to cast JSON fields to custom DTOs.

### Further reading elsewhere

* [Arrays in MySQL 8.0 and multi-valued indexes](https://saveriomiroddi.github.io/Storage-and-indexed-access-of-denormalized-columns-arrays-on-mysql-8.0-via-multi-valued-indexes/)
* [Performance Gains on JSON Column Queries using MySql Virtual Columns](https://medium.com/@michalisantoniou6/massive-performance-gains-on-json-column-queries-using-mysql-virtual-columns-and-indexes-in-laravel-dc7d289a41b3)
