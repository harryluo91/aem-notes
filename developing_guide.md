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
  - 