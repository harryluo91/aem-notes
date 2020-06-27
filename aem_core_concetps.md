# AEM Core Concepts

## Sling Request Processing
A Web application framework based on REST principles that provides easy development of content-oriented applications.

Example:

HTTP Request:
```
GET /wiki/Sling.edit.html/richtext?simple=true HTTP/1.1
```
>Path: `/wiki/Sling`

>Selector: `edit`

>Extension: `html`

>Suffix: `richtext`

>Query Param: `simple=true`

- Content Resolution: `/wiki/Sling`
  - node properties: `sling:resourceType: wiki/page`

- Get resource type:
  - first use: `sling:resourceType=wiki/page`
  - fallback: `sling:resourceuperType=<null></null>`
  - last resource: `jcr:primaryType=nt:file`

- Script locations:
  - `apps/wiki/page`
  - `libs/wiki/page`

- Script names:
  - Best match: `edit.html.esp`
  - Selector match: `edit.esp`
  - Extenstion match: `html.esp`
  - Worst match: `GET.esp`

### Sling is content centric:
- the first target is the resource (JCR node) holding the content
- the script is located from the resource properties in combination with certain oarts o fthe request (selectors/extensions)

### URL Decomposition
```
https://myhost/tools/spy.printable.a4.html/a/b?x=12
```

> **content path**: path sepcfying the content to be rendered, used in combination with the extension

> **selectors**: used for alternative methods of rendering the cntent

> **extension**: ccontent format, also specifies the script to be used for rendering

> **suffix**: can be used to specify additional information

### From URL to Content and Scripts
- uses the content path to locate the resource
- uses the resource type to of the slign resource to locate the script sued for rendering the content

### Locating the script
- When the appropriate resource is located (content node), he sling resource type is extracted.
- all Sling scripts are stored in subfolders of either `/apps` or `/libs`
- various script engines are supported
	- esp
	- jsp
	- java
	- jst
- the list of script engines supported for an instance can be found here - `http://<host>:<port>/system/console/slingscripting`

Example: `../content/corporate/jobs/developer.html`, and `sling:resourceType` is `hr/jobs`

-  GET/HEAD requests, URLs ending in .html, the script will be `apps/hr/jobs/jobs.esp`, the last section of the resource type forms the file name

- POST requests: `apps/hr/jobs/jobs.POST.esp`

- URLs in other formats, not ending with .html, for example `../content/corporate/jobs/developer.pdf`, the script will be `/apps/hr/jobs/jobs.pdf.esp`

- URLs with selectors, for example `../content/corporate/jobs/developer.print.html`, the script will be `/apps/hr/jobs/jobs.print.esp`, the selector is added to the script name.

- If no `sling:resourceType` has been defined then:
	- the cotent path will be used to search for the script, for example, `/apps/content/corporate/jobs/`

- If no sciprt is found the the defauly script will be used: .txt, .html, .json

- For error handlin (403, 404), the script will be either
	- `/apps/sling/servlet/errorhandler`
	- or `/libs/sling/servlet/errorhandler/403.esp`

### If multiple scripts are matched
- The best matched is selected
- The more selectors matched the better, regardless of any request extension or method name match
- For example: `/content/corporate/jobs/developer.print.a4.html` with a sling:resourceType of `hr/jobs`, assuming the following list of scripts are in the correct location:
	1. GET.esp
	2. jobs.esp
	3. html.esp
	4. print.esp
	5. print.html.esp
	6. print/a4.esp
	7. print/a4/html.esp
	8. print/a4.html.esp

Then the order of preference will be **8, 7, 6, 5, 4, 3, 2, 1**

### sling:resourceSuperType
- the `sling:resourceSuperType` of the resource
- the `sling:resourceSuperType` property of the node which `sling:resourceType` points

For example:
- a
- b
	- sling:resourceSuperType = a
- c
	- sling:resourceSuperType = b
- x
	- sling:resourceType = c
- y
	- sling:resourceType = c
	- sling:resourceSuperType = a

Then the hierarchy of:
- /x
	- [ c, b, a, default]
- /y
	- [ c, a, default]
	- the `resourceSuperType` is taken from the node itself instead of the node that `resourceType` points to

### Sling scripts cannot be called directly

### Referencing existing elements using sling:include
- sling:include("/path/resource")
	- `%><sling:include resourceType="geometrixx/components/image/img"/><%`

### OSGI

Defines an architecture for developing and deploying modular applications and libraries.