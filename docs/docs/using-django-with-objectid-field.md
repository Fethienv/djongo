---
title: Other fields
permalink: /using-django-with-objectid-field/
---

## The ObjectId Field

For every document inserted into a collection MongoDB internally creates an [ObjectID](https://docs.mongodb.com/manual/reference/method/ObjectId/) field with the name `_id`. Reference this field from within the Model:

```python
class Entry(models.Model):
    _id = models.ObjectIdField()
    blog = models.EmbeddedField(
        model_container=Blog,
    )
```

By default the `ObjectIdField` internally sets `primary_key` as `True`. This means the implicitly created `id` AUTOINCREMENT field will not be created. The Field inherits from the `AutoField`. An ObjectID will be automatically generated by MongoDB for every document inserted. 

Consider using the `ObjectIdField` in your models if you want to avoid calling Django migrations every time you create a new model.

## ObjectIdField

```python
class ObjectIdField(Field):
    def __init__(self, *args, **kwargs):
```

### Arguments

Same as the `Field` Base class

## The List field

> Note: To be depreciated soon and replaced with a `JSONField`

`ArrayField` and `ArrayReferenceField` require all Models in the list to be of the same type. MongoDB allows the saving of arbitrary data inside it is embedded array. The `ListField` is useful in such cases. The list field cannot be represented in Django Admin though and can only be used in the python script.

### ListField

```python
class ListField(Field):
    def __init__(self, *args, **kwargs):
```

### Arguments

Same as the `Field` Base class