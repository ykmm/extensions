# DRAFT
# Rich Template and Query objects
# use uri templates or not

### Note:

This is explained using the format described in [Version
1](rich-template-query-alt1.md) , but is valid also for [Version
2](rich-template-query-alt2.md)

### Rationale:
While writing this specification I thought of two ways to specify a url to allow also query information to be retrieved:

1. uri templates (http://tools.ietf.org/html/rfc6570)
2. query object in a C+J representation

### Working scenario:

We have a C+J representation that has also a template for adding new items to the collection.

One of the fields for this template is a list of options to be retrieved remotely with some kind of filtering.

example of <code>urloptions</code> with a uri template

```json
{
  "template" :
  {
    "data" : [
      {
        "name": "friend_id",
        "value": "",
        "prompt": "Search for a friend",
        "urloptions": "http://..../friend_autocomplete/{part_of_friend_name}"
      },
    ]
  }
}
```

* The advantage is that the client already knows that the linked resource can
be queried.
* The downside is that the client must also understand uri templates.

example of <code>urloptions</code> with a plain url

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

In this case the clients only knows that he can get a list of options from
querying the url. Only by GETting the url it will know if it also query-able
if the collections contains also a query object. (We assume that the
autocomplete resource is represented as C+J).

* The advantage is that we use what is already part of the base C+J
specification.

* The downside is that the client needs to fire a GET request for all the
template data objects that have a urloptions to learn if they can be queried.
