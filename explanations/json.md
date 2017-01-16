---
layout: explanation
title:  "What is JSON?"
---

JSON stands for **Javascript Object Notation** and is a convenient and human-readable way to represent data.

There are three basic types of data that can be represented in JSON, which are **strings**, **numbers**, and **booleans**.

Strings should always use double quotes: `"this is a string"`.

Numbers can be any valid Javascript number, like `34` or `-0.12`.

Booleans can be either `true` or `false`.

There is also a special value **null**, which indicates an empty value and should appear without quotes as `null`.

Additionally, you can combine data using **arrays** and **objects**.

**Arrays** are lists of other data, wrapped in brackets.
```json
[ "this is an array", "with strings", "and numbers and booleans", 2, true, "and also a null for kicks", null]
```

**Objects** are key-value stores of other data, wrapped in braces. The keys of an object should all be unique strings.
```json
{
  "this_is_a_key": "this is a value"
}
```

Both arrays and objects can also store arrays and objects. This means that you can represent data of arbitrary size in JSON.

One of the awesome things about JSON is how easy it is to transform a string formatted in JSON into a fully-functional object in Javascript. For example:

```javascript
var json_string = '{ "first_name": "marie", "last_name": null, "user_id": 54871, "has_last_name": false }';
var user = JSON.parse(json_string);
console.log(user.user_id);  // output: 54871

if (user.has_last_name) {
  console.log(user.first_name, user.last_name);
} else {
  console.log(user.first_name);  // output: "marie"
}
```

What if a key has a name with spaces in it? You can still access it on the object but you'll have to use bracket notation instead of dot notation.

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