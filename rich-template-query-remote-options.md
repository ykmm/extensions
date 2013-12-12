# DRAFT
# Rich Template and Query objects
#### how to deal with remote c+j data for remote list of options

I think there are two alternatives:

#### 1
we force in the spec that the returned c+j must have in its data array two
elements (named in a really meta way 'prompt' and 'value' =) as in the
following example:

```json
// sample data array
{
  "items" :
  [
    {
      "href" : URI,
      "data" :
        [
          {"name" : "value", "value" : id_for_the_option},
          {"name" : "prompt", "value" : prompt_for_the_option},
        ]
      "links" : [ARRAY]
    },
}
```

#### 2
we must state which are the the c+j data elements
to use for 'prompt' and 'value' in the query or template data elements:

####  [Version 1](rich-template-query-alt1.md) example:

<code>urloptions</code> used to retrieve the elements
two new properties added:

* <code>optprompt</code> specifies the data element name of the returned C+J that contains the label for the options (if the client needs to show it)
* <code>optvalue</code> specifies the calue element name of the returned C+J that contains the value for the options (that the client needs to send back to the server)

```json
{
  "template" :
  {
    "data" : [
      {
        "name": "friend_id",
        "value": "",
        "prompt": "Search for a friend",
        "urloptions": "http://..../friend_autocomplete/",
        "optprompt": "firstname",
        "optvalue": "firstname",
      },
    ]
  }
}
```

#### [Version 2](rich-template-query-alt2.md) example:

<code>remote</code> used to retrieve the elements

* <code>prompt</code> specifies the data element name of the returned C+J that contains the label for the options (if the client needs to show it)
* <code>value</code> specifies the calue element name of the returned C+J that contains the value for the options (that the client needs to send back to the server)

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
          "remote": {
            "href":"http://..../contact_type_autocomplete/",
            "prompt": "firstname",
            "value": "user_id"
          }
        }
      },
    ]
  }
}
```