# DRAFT
# Rich Template and Query objects

### Rationale:
The purpose of this extension is to add just enough information to query and
template objects so that the client can interact with them in a richer(proper?)
way.

These additions are meant to assist an automated client to create queries or
templates with the correct values in cases where those values:

- can be retrieved with an autocomplete mechanism
- can be selected from an embedded static list
- can be selected from a remote list
- can be set as a list of elements (ie: tag1,tag2,tag3)
- should be validated before sending

### Specification:
Support for the following features in <code>data</code> objects of <code>template</code> and <code>query</code>: [1]

1. Add an optional property to the <code>data</code> object: <code>required</code> (boolean)
2. Add an optional property to the <code>data</code> object: <code>regexp</code> (string)
3. Add support for embedded or remote list of options [Version 1](rich-template-query-alt1.md) [Version 2](rich-template-query-alt2.md)

boolean properties have value of false if not present.

<code>required</code> means that the element is required and the query or
template cannot be sent to the server without a value.

<code>regexp</code> a regular expression checked by the client to verify the
content of the field before sending it to the server.

### Examples:

<code>required</code>

```json
{
  "template" :
  {
    "data" : [
      {
        "name": "contact_type",
        "value": "",
        "prompt": "Invite to appointment",
        "required": true,
      },
    ]
  }
}
```

<code>regexp</code>

```json
{
  "template" :
  {
    "data" : [
      {
        "name": "zipcode",
        "value": "",
        "prompt": "Search for a friend",
        "regexp": "[0-9]{5}"
      },
    ]
  }
}
```

### Open discussion points:

<code>regexp</code>:

* There are different regexp [flavours](http://www.regular-expressions.info/refflavors.html)
* Do we stick to one? Which one? Maybe [Posix](http://pubs.opengroup.org/onlinepubs/009695399/basedefs/xbd_chap09.html)?
* Do we want a way to specify which one should be used? How do we specify a regular expression flavour? There is no naming convention for them.



### References
1. https://groups.google.com/forum/#!topic/collectionjson/Vi77wpjH2x0

### Inspired by:
1. Template validation: https://github.com/collection-json/extensions/blob/master/template-validation.md
2. Value Types (Array values): https://github.com/collection-json/extensions/blob/master/value-types.md
3. Autocomplete: https://groups.google.com/forum/#!searchin/collectionjson/autocomplete/collectionjson/-l7IbsiMfh0/mktNpa2xLqcJ
