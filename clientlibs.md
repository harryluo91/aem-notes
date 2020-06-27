# Using Client-Side Libraries
**cq:ClientLibraryFolder**
```
[cq:ClientLibraryFolder] > sling:Folder
  - dependencies (string) multiple
  - categories (string) multiple
  - embed (string) multiple
  - channels (string) multiple
```
- **categories**: Identifies the categories of the JS and/or CSS files, a multivalued property, allows a library folder to be part of mroe than one category
- **dependencies**: a list of other client lib catrgories that this lib folder depends
- **embed**: used to embed code from other libs
- **allowProxy**: if a client lib is under `/apps`, this prop allows access to it via proxy servlet.

## Referencing Client-Side Libraries
use `data-sly-use` and `data-sly-call` to load client libs
- css
- js
- all

Each helper template expects a `categories` option referencing the categories of the client lib, it can be a string or array


## Creating Client Library Folders
a node with type `cq:ClientLibraryFolder`
- the JS and CSS files to be merged
- Resources that supports CSS styles
- One js.txt and css.txt file that defines the source files to merge

Web client must have permissions to access the  `cq:ClientLibraryFolder` node

## Overriding Libraries in /lib
Client libs under `/apps` take precedence over same-named folders located under `/libs`

## Locating a Client Library Folder and Using the Proxy Client Libraries Servlet
A proxy servlet is used in order to access client libs located under `/apps`

The ACLs are still enforced on the client libs folder but the servelt allows for the content to be read via `etc.clientlibs/` if the allowProxy property is set to true

A static resource can only be accessed via the proxy if it resides below a resource below the client lib folder

For example:

- `/apps/myproject/clientlibs/foo`
- `/apps/myprojects/clientlibs/foo/resources/icon.png`

Then you can access it from:
- `/etc.clientlibs/myprojects/clientlibs/foo.js`
- `/etc.clientlibs/myprojects/clientlibs/foo/resources/icon.png`

## Debugging Tools
> Append `debugClientLibs=true` to the URL of your web page to view the embedded files

> The `/libs/cq/granite/components/dumplibs/dumplibs` component generates a page of information about all client library folders on the system.