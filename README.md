# mongoengine-dataclasses
Convert MongoEngine documents to and from Data Classes
The library provides API for syncing MongoEngine document classes and Data Classes.
This can be useful if you are using Data Class instances in your application and want to isolate MongoEngine classes to the data access layer only.

## Simple Example

```python
from mongoengine_dataclasses import mongo_from_dataclass
from mongoengine import Document, DictField


@dataclass
class SimpleDataClass:
    foo: str
    bar: int = 0


@mongo_from_dataclass(SimpleDataClass)
class SimpleDocument(Document):
    __meta__ = {'collection': 'simple'}


simple = SimpleDataClass(foo='Foo', bar=10)

simple_doc = SimpleDocument.from_dataclass(simple)

simple_2 = SimpleDocument.objects.first().to_dataclass()
```
or 

```python
from mongoengine_dataclasses import DataClassDocument
from mongoengine import DictField


@dataclass
class SimpleDataClass:
    foo: str
    bar: int = 0


class SimpleDocument(SimpleDataClass, DataClassDocument):
    __meta__ = {'collection': 'simple'}


simple = SimpleDataClass(foo='Foo', bar=10)

simple_doc = SimpleDocument.from_dataclass(simple)

simple_2 = SimpleDocument.objects.first().to_dataclass()
```
