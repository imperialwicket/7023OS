# playing with marvel

## install marvel

	bin/plugin -i elasticsearch/marvel/latest

## test marvel with the browser
	
	http://localhost:9200/_plugin/marvel/sense/


# add/index a document

	curl -XPUT "http://localhost:9200/blog/post/1" -d'
	{
	"author" : "darth_vader",
	"title" : "Reflexions about the dark side of the Force",
	"body" : "The dark side of the Force is a pathway to many abilities some consider to be... unnatural",
	"created" : "2014-05-10"
	}'

# retrieving a single document

	curl -XGET "http://localhost:9200/blog/post/1"


# insert a new document with generated id

	curl -XPOST "http://localhost:9200/book/post" -d'
	{
		"title" : "There is no why.",
		"author" : "yoda",
		"body" : "Nothing more will I teach you today.",
		"created" : "2014-05-11",
		"ip" : "192.168.1.11"
	}'

# retrieving all documents

	curl -XGET "http://localhost:9200/blog/post/_search?q=*:*"

# looking at the generated mapping

	curl -XGET "http://localhost:9200/blog/post/_mapping"

# modifying the mapping

## delete a mapping

	curl -XDELETE "http://localhost:9200/blog/post/_mapping" 

## update the new mapping

	curl -XPUT "http://localhost:9200/blog/post/_mapping" -d'
	{
	 "post": {
		"properties": {
			"properties": {
				"author": { "type": "string" },
				"body": { "type": "string" },
				"title": { "type": "string" },
				"created": { "type": "date", "format": "dateOptionalTime" },
				"ip": { "type": "ip" }  // HIGHLIGHT
			}
		}
	  }
	}'

# a simple 'match' query

## the actual query

	curl -XGET "http://localhost:9200/blog/post/_search" -d '
	    {
	      "query": {
		"match" : {
		    "title" : "May the Force",
		    "operator" : "and"
		}
	      }
	    }'

## a similar query (a suggested decomposition)

	curl -XGET "http://localhost:9200/blog/post/_search" -d '
	{
	  "query": {
		"bool": {
			"must": [
				{ "term" : { "title" : "may" } },
				{ "term" : { "title" : "force" } }
			]
		}
	  }
	}'


# a range query

	curl -XGET "http://localhost:9200/blog/post/_search" -d'
	{
	  "query": {
		"range" : {
			"ip" : { "gte" : "192.0.0.0", "lt" : "200.0.0.0" }
		}
	  }
	}'

# deleting a document

	curl -XDELETE "http:///localhost:9200/blog/post/4"

# updating a document

## full update example

	curl -XPUT "http://localhost:9200/blog/post/2" -d'
	    {
		"author" : "darth_vader",
		"title" : "Reflexions about...",
		"body" : "The dark side of the Force...",
		"created" : "2014-05-10",
		tags : ["evil", "force"]
	    }'

## partial update example

	curl -XPOST "http://localhost:9200/blog/post/2/_update" -d '
	    {
		"doc" : { tags : ["evil", "force"] }
	    }'
	
## example with script

	curl -XPOST "http://localhost:9200/blog/post/2/_update" -d '
	    {
		"script" : "ctx._source.visitors += count",
		"params" : { "count" : 1 }
	    }'










