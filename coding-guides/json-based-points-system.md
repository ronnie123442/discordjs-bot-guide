---
description: THIS PAGE IS ARCHIVED AND FOR INFORMATIONAL PURPOSES ONLY
---

# JSON-Based Points System

## This page has been archived.

{% hint style="danger" %}
JSON files should not be used for storing data that changes constantly. Please use [SQLite](sqlite-based-points-system.md) or [Enmap ](enmap-based-points-system.md)for your points system or any other storage needs. If you want to know why, read below.
{% endhint %}

## Storing Data in a JSON file

### Why is JSON prone to corruption?

The answer is: it's not _inherently_ a problem. JSON is fine for storing data that you access often. JSON is fine as a transfer system between services and apps.

The issue isn't with JSON. The issue is with `fs`. So really, this applies not just to JSON but also to TXT files or any other plain text file you're attempting to write to.

See here's the thing: If you're attempting to simultaneously **read** a file and **write** to it at the same time, or if you're **writing** to a file from **more than one location**, the file risks being corrupted. And the more this happens, the higher the chances. It might work for small bots, but as it grows you are going to lose that data.

### Does this mean JSON is very bad?

Not for all purposes. As we cover in [Adding a Config File](../first-bot/adding-a-config-file.md), you can store _static_ data that generally is modified manually and applied on bot reboot. That data can be as big as you want - it can be just 4 keys, it can be 1000 entries in a random text thing... the fact is it's being loaded once and then not written to.

### So what do I do now, how do I store data?

You have **so many** good alternatives to using JSON. And some are covered right here.

#### If your bot is not sharded?

If you want a simple `key/value` pair storage, like ID + Object, you can use `enmap`, which is covered in [Introducing Enhanced Maps](json-based-points-system.md).

If you need a little more umph, like multiple tables, multiple keys, etc, you can use `sqlite`. The [SQLite-Based Points System](sqlite-based-points-system.md) page shows you how to do a points system but of course, SQLite can be used for much more than this.

#### If your bot is sharded or the database is shared

For more stable, multi-process access, think of getting a bigger database system. While those systems will require the installation of a database server, they will offer much more capabilities, power, and reliability.

A few options are [rethinkdbdash](https://www.npmjs.com/package/rethinkdbdash), [mysql](https://www.npmjs.com/package/mysql), [redis](https://www.npmjs.com/package/redis). You could also use an ORM if you're into this sort of thing, [sequelize](https://www.npmjs.com/package/sequelize) is a highly recommended package!

