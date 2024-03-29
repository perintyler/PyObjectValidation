# PyObjectValidation

This Python package makes use of [Type Hints](https://docs.python.org/3/library/typing.html) to define object schemas that can be encoded and decoded.

## Installation 

```console
pip install ./PyObjectValidation
```

## Schemas

Schemas can be defined to build objects from raw JSON data. Properties defined in the schema can be instances of `Schema`, allowing for nested objects.

```python
>>> from object_validation import Schema
>>>
>>> class User(Schema):
>>>   name: str = 'required'
>>>   age:  int
>>>
>>> class Group(Schema):
>>>   title:   str
>>>   creator: User
>>>   msg_set: List[str]
```

### Encoding

If invalid types are provided to the `encode` function, an `EncodingException` will be raised.

```python
>>> from object_validation import encode 
>>>
>>> group = encode({
>>>   'title': 'Revolution?',
>>>   'creator': {'name': 'George Washington', 'age': 23},
>>>   'messages': ['When we stealing that tea?', '@theRealKingGeorge 1v1 me irl']
>>> })
>>>
>>> group.title
'Revolution?'
>>> group.creator
<User name='George Washington' age=23>
```

## Decoding

```python
>>> from object_validation import decode
>>> decode(User('George Washington', 23))
{'name': 'George Washington', 'age': 23}
```
