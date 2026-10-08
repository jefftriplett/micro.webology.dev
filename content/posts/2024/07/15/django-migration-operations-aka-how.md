---
title: "🐘 Django Migration Operations aka how to rename Models"
date: "2024-07-15T12:20:41-05:00"
url: "/2024/07/15/django-migration-operations-aka-how/"
type: "post"
feed_id: "http://webology.micro.blog/2024/07/15/django-migration-operations-aka-how/"
categories: ["Django", "Python"]
---

Renaming a table in Django seems more complex than it is. Last week, a client asked me how much pain it might be to rename a Django model from Party to Customer. We already used the model's `verbose_name`, so it has been referencing the new name for months. 

Renaming the model should be as easy as renaming the model while updating any foreign key and many-to-many field references in other models and then running Django's `make migrations` sub-command to see where we are at.

The main issue with this approach is that Django will attempt to create a new table first, update model references, and then drop the old table. 

Unfortunately, Django will either fail mid-way through this migration and roll the changes back or even worse, it may complete the migration only for you to discover that your new table is empty. 

Deleting data is not what we want to happen. 

As it turns out, Django supports a [`RenameModel`](https://docs.djangoproject.com/en/5.0/ref/migration-operations/#renamemodel) migration option, but it did not prompt me to ask if we wanted to rename Party to Customer. 

I am also more example-driven, and the Django docs don't have an example of how to use `RenameModel`. Thankfully, this migration operation is about as straightforward as one can imagine: `class RenameModel(old_model_name, new_model_name)`

I re-used the existing migration file that Django created for me. I dropped the `CreateModel` and `DeleteModel` operations, added a `RenameField` operation, and kept the `RenameField` operations which resulted in the following migration: 

```python
from django.db import migrations


class Migration(migrations.Migration):

    dependencies = [
        ('resources', '0002_alter_party_in_the_usa'),
    ]

    operations = [
        migrations.RenameModel('Party', 'Customer'),
        migrations.RenameField('Customer', 'party_number', 'customer_number'),
        migrations.RenameField('AnotherModel', 'party', 'customer'),
    ]
```

The story's moral is that you should *always check and verify* that your Django migrations will perform as you expect before running them in production. Thankfully, we did, even though glossing over them is easy. 

I also encourage you to dive deep into the areas of the Django docs where there aren't examples. Many areas of the docs may need examples or even more expanded docs, and they are easy to gloss over or get intimidated by. 

You don't have to be afraid to create and update your migrations by hand. After all, Django migrations are Python code designed to give you a jumpstart. You can and should modify the code to meet your needs. [Migration Operations](https://docs.djangoproject.com/en/5.0/ref/migration-operations/) have a clean API once you dig below the surface and understand what options you have to work with.
