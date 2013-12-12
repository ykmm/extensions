# DRAFT
# Rich Template and Query objects
# embedded or remote list of options

### Alternative 2 Rationale:
the remote or local list of options is represented as an object part of the <code>data</code> object

### Specification:
Support for the following features in <code>data</code> objects of <code>template</code> and <code>query</code>: [1]

1. Add an optional object to the <code>data</code> object:
<code>options</code> this object has two optional properties
<code>multival</code>, <code>remote</code> and an <code>local</code> object.

boolean properties have value of false if not present.

<code>options</code> contains an optional <code>multival</code> property an
<code>options</code> array or an <code>remote</code> property

- <code>multival</code> means that the element supports multiple values or only
one, if true <code>options</code> or <code>urloptions</code> should be set.

- <code>local</code> is an array of embedded options that must be used as
values for this field , each option must have a <code>value</code> and
<code>prompt</code> element, <code>value</code> is sent to the server for the
request, <code>prompt</code> can be used for rendering.

- <code>remote</code> is the url where the list of options can be retrieved
with an http request ()with or withouth query parametres), the data object
should have at least for every element a <code>value</code> and a
<code>prompt</code>.

### Examples

we use an <code>options</code> object which embeds the optional
<code>multival</code> property and one between an <code>local</code> array or
a <code>remote</code> property.

#### with embedded <code>local</code>

```json
{
  "template" :
  {
    "data" : [
      {
        "name": "attendees",
        "value": "",
        "prompt": "Invite to appointment",
        "required": true,
        "options": {
          "multival": true,
          "local": [
            {
              "value": "1",
              "prompt": "Luke Skywalker"
            },
            {
              "value": "2",
              "prompt": "James Bond"
            },
            {
              "value": "3",
              "prompt": "Hulk"
            },
            {
              "value": "4",
              "prompt": ""
            }
          ]
        }
      },
    ]
  }
}
```

#### with <code>remote</code> used to retrieve the elements

```json
{
  "template" :
  {
    "data" : [
      {
        "name": "attendees",
        "value": "",
        "prompt": "Invite to appointment",
        "required": true,
        "options": {
          "multival": true,
          "remote": "http://..../contact_type_autocomplete/"
        }
      },
    ]
  }
}
```

### Open discussion points:
* [How to deal with remote list of options](rich-template-query-remote-options.md)
* [Using url templates or not](rich-template-query-uritempl-ornot.md)