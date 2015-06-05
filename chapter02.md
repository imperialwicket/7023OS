## CHP02
## mooc cooking example [DRAFT]

GET /_cluster/state

GET /mooc/course/_search

PUT /mooc/

DELETE /mooc/

DELETE /mooc/_mapping/course

PUT /mooc/_mapping/course
{
   "course":{
      "properties" : {
        "course" : {"type" : "string", "store" : true},
        "title" : {"type" : "string", "store" : true},
        "text" : {"type" : "string", "store" : true},
        "lesson": {"type" : "integer", "store" : true}
      },
    "_routing":{
         "required":true,
         "path":"course"
    }
   }
}

POST /mooc/course?routing=cooking
{
  "course" : "cooking",
  "title" : "cooking broccoli",
  "text" : "learn how to cook broccoli... ",
  "lesson": 1,
  "routing" : "cooking"
}


GET http://localhost:9200/mooc/course/_search

# EXAMPLE 2: modelling a simple mooc index, with type course
# we have two courses: cooking and bakerying

DELETE /mooc/
PUT /mooc/

GET /mooc/course/_search?routing=other

GET /mooc/course/_search?routing=cooking

GET /mooc/course/_search?routing=bakerying


POST /mooc/course?routing=cooking
{
  "title" : "cooking",
  "lesson-title" : "cooking broccoli",
  "text" : "learn how to cook broccoli :-)",
  "lesson": 2
}

POST /mooc/_bulk?routing=cooking
{"index":{ "_index" : "course", "_id":"CK01", "_type": "course", "_routing": "cooking"}}
{"title":"introduction to cooking","text": "this will be the introduction...", "lesson" : 1}
{"index":{ "_index" : "cooking", "_id":"CK02", "_type": "course", "_routing": "cooking"}}
{"title":"first recipe", "text": "let's start cooking something simple", "lesson" : 2}

POST /mooc/_bulk?routing=bakerying
{"index":{ "_index" : "course", "_id":"CK01", "_type": "course", "_routing": "bakerying"}}
{"title":"where to start from?", "text": "let's prepare something good!", "lesson":1}




###########################################
# EXAMPLE 1
# BULK INSERTING

DELETE /blog
GET /blog/_search?routing=mary

POST /_bulk?routing=mary
{ "index" : { "_index" : "articles", "_type" : "article", "_id" : "1", "_routing" : "John"} }
{ "title" : "value1" }
{ "create" : { "_index" : "articles", "_type" : "article", "_id" : "3", "_routing" : "john" } }
{ "title" : "value3" }
{ "delete" : { "_index" : "articles", "_type" : "article", "_id" : "3", "_routing" : "john" } }
{ "update" : {"_id" : "1", "_type" : "article", "_index" : "articles", "_routing" : "mary"} }
{ "doc" : {"field2" : "value2"} }

###########################################
