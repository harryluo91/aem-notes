# Query Builder
- **group**
	- allows to build nested conditions
	- example:
		- ```
			group.p.or=true
			group.1_property=jcr:title
			group.1_property.value=My Page
			group.2_property=navTitle
			group.2_property.value=My Page
			```
		- this is basically `(1_property OR 2_property)`

- **path**
	- searches within a given path
	- properties:
		- paths
		- exact
		- falt: searches only direct children
		- self: searches the subtree but includes the base node

- **properties**
	- property - relative path to property
	- value
	- N_value - check for multiple values (default is OR)
	- and
	- operation - `equals`, `unequals`, `like`(jcr:like xpath function), `not`, `exists`
	- depth - nu,ber of levels that the property can exist, for example, `property=size depth=2` will check `node/size`, `node/*/size` and `node/*/*/size`

- **root**
	- root predicate group, supports all features of a group and allows to set global query params
	- p.offset
	- p.limit
	- p.excerpt
	- p.hits

p.limit = -1 will return all results


## Debugging
- http://localhost:4502/libs/cq/search/content/querydebug.html
- http://localhost:4502/bin/querybuilder.json?path=/tmp

- create new logger at `com.day.cq.search.impl.builder.QueryImpl`
- copy the XPath generated into Explain Query