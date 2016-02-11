# What is JSON?

JSON stands for **Javascript Object Notation** and is a convenient and human-readable way to represent data.

There are two basic types of data that can be represented in JSON, which are **strings** and **numbers**.

Additionally, you can combine data using **arrays** and **objects**.

**Arrays** are lists of other data, wrapped in brackets.
```json
[ "this is an array", "with strings", "and numbers", 2]
```

**Objects** are key-value stores of other data, wrapped in braces.
```json
{
  "this_is_a_key": "this is a value"
}
```

Both arrays and objects can also store arrays and objects. This means that you can represent data of arbitrary size in JSON.

One of the awesome things about JSON is how easy it is to transform a string formatted in JSON into a fully-functional object in Javascript. For example:

```javascript
var json_string = '{ "name": "marie", "user_id": 54871 }';
var user = JSON.parse(json_string);
console.log(user.name, user.user_id);  // output: marie, 54871
```

What if a key has a name with spaces in it?

```javascript
var json_string = '{ "this is a silly name for a key": "but it works" }';
var example = JSON.parse(json_string);
console.log(example["this is a silly name for a key"]);  // output: but it works
```

JSON should always have an outermost object, in which other data is nested.

```json
{
  "this_is_a_key": "this is a value",
  "values_can_be_numbers": 2,
  "keys_can_point_to_other_objects": {
    "which_can_be_nested": {
      "infinitely": "if you want"
    }
  },
  "keys_can_also_point_to_arrays": [
    "which_can_contain_strings",
    10,
    {
      "other": "objects"
    },
    [
      "or even",
      "other arrays"
    ]
  ]
}
```