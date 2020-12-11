# Response Type Scheme "iqb-simple-player" 1.0.0
The response-type is a standard-JSON object.

* Because the testcenter in current version does *not* support 
  data-chunks other that `all`, on top-level of the object there is an all object.
* The next level contains at least an `answers` field. Other fields might be 
  used by extensions.
* The `answers`-field contains all values of all form/contenteditable elements
  of the unit. They are strings or arrays of strings and resemble the 
  `iqb-key-value`-format.
  
## JSON-Schema

```
{
   "title":"iqb-simple-player@1.0.0",
   "$schema":"https://json-schema.org/draft/2019-09/schema",
   "type":"object",
   "required":[
      "all"
   ],
   "properties":{
      "all":{
         "$id":"#/properties/all",
         "type":"object",
         "description":"Chunk-Container",
         "default":{
            
         },
         "examples":[
            {
               "answers":{
                  
               }
            }
         ],
         "required":[
            "answers"
         ],
         "properties":{
            "answers":{
               "$id":"#/properties/all/properties/answers",
               "type":"object",
               "description":"Containing all fields-values - primaray answer data of the unit",
               "examples":[
                  {
                     "text-field":[
                        "x",
                        "y"
                     ],
                     "number-field":"3",
                     "date-field":"",
                     "email-field":"a@c.de",
                     "range-field":"6",
                     "radio-group":"c",
                     "check-box":"on",
                     "select-box":"a",
                     "list-field":"miau",
                     "text-area":"some text",
                     "multi-select":[
                        "red",
                        "blue",
                        "yellow"
                     ],
                     "":[
                        "a",
                        "b",
                        "c",
                        "d"
                     ]
                  }
               ],
               "required":[
                  
               ],
               "additionalProperties":{
                  "type":[
                     "string",
                     "array"
                  ],
                  "items":{
                     "type":"string"
                  }
               }
            }
         },
         "additionalProperties":true
      }
   },
   "additionalProperties":true
}
```
