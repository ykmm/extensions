# DRAFT
# Rich Template and Query objects
# embedded or remote list of options

### Alternative 1 Rationale:
the remote or local list of options is represented as properties of the <code>data</code> object

### Specification:
Support for the following features in <code>data</code> objects of <code>template</code> and <code>query</code>: [1]

3. Add an optional property to the <code>data</code> object: <code>multival</code> (boolean)
4. Add an optional property to the <code>data</code> object: <code>options</code> (array)
5. Add an optional property to the <code>data</code> object: <code>urloptions</code> (href)

boolean properties have value of false if not present.

<code>multival</code> means that the element supports multiple values or only
one, if true <code>options</code> or <code>urloptions</code> should be set.

<code>options</code> is an array of embedded options that must be used as
values for this field , each option must have a <code>value</code> and
<code>prompt</code> element, <code>value</code> is sent to the server for the
request, <code>prompt</code> can be used for rendering.

<code>urloptions</code> a list of options that can be retrieved with an url
(with or withouth query parametres), the data object should have at least for
every element a <code>value</code> and a <code>prompt</code>.

### Examples

<code>options</code>, <code>multival</code>, <code>required</code>

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
        "multival": true,
        "options": [
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
          }
        ]
      },
    ]
  }
}
```

#### <code>urloptions</code> for autocomplete

```json
{
  "template" :
  {
    "data" : [
      {
        "name": "friend_id",
        "value": "",
        "prompt": "Search for a friend",
        "urloptions": "http://..../friend_autocomplete/"
      },
    ]
  }
}
```

### Open discussion points:
* [How to deal with remote list of options](rich-template-query-remote-options.md)
* [Using url templates or not](rich-template-query-uritempl-ornot.md)