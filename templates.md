# Templates

Two basic types of templates for creating pages:

- Editabe Templates
- Static Templates

## Template Availability
Start simple:
- only define `cq:allowedTemplates` property
- only on the site root
- When possible, define the `cq:allowedTemplates` property on sub-sections of the site
- `allowTemplates` can be defined by author whereas the other properties needs to be defined by developer

Example:

The following properties determine whether a template `T` is allowed to be used for a new page to be placed as a child page of `P`.

- `cq:allowedTemplates` of P or an ancestor of P
- `allowedPaths` of T
- `allowedParents` of T
- `allowedChildren` of T of P

The evaluation works as follows:

- `cq:allowedTemplates` found on the page starting from P and and traversing up its hierarchy. If none matches the path of T, then T is rejected.
- If T has `allowedPaths` defined and is value does not match the path of P, then T is rejected.
- If both the above scenario fails then T is rejected unless it belongs to the same application as P. For example, T - `/apps/geometrixx/templates/foo` and P - `/content/geometrixx/`
- If T has `allowedParents` defined and the value does not match P, then T is rejected
- If the template of P has `allowedChildren` defined, and the values do not match the path of T, then T is rejected
- In all other cases, T is allowed.

## Editable Templates
- stored under `/conf/xxx/settings/wcm/templates`
- allows specialized authors to edit and create templates
	- must be members of the `template-authors` group
- provide templates that retain a dynamic connection to any pages created from them. Changes to the templates are reflected on the pages
- make page component more generic

### Creating new template
Template types and policies are inherited across all folders according to the order of precedence:
1. The current folder.
2. Parent(s) of the current folder.
3. /conf/global
4. /apps
5. /libs

### Template Type
- the template type is copied to create the template
- no dynamic connection between template type and created templates
- allows you to define:
	- the resource type
	- the policy of the root node, which defines the components allowed in the template editor
	- recommended to define the breakpoitns for the responsive grid
- ootb template types are under `/libs/settings/wcm/template-types`
- customzied template types should be stored in user-defined folders with folder structure `/settings/wcm/...`:
	- `/conf/<my-folder-01>/<my-folder-02>/settings/wcm/template-types`
	- `/conf/<my-folder>/settings/wcm/template-types`
	- `/conf/global/settings/wcm/template-types`

### Template Type and Mobile Device Groups
> `cq:deviceGroups`: defines which mobile defices are available as emulators in the layout mode, can be set in 2 places:
>- editable template type
>- editable template
>
> must be set as a relative path

Creating Template Type:
- create a template
- copy the template from `templates` to `template-types`
- delete the template from the `templates` node
- delete all `cq:template` and `cq:templateType` `jcr:content` properties.

### Template Definitions
```
<template-name>
[initial](#initial-content)
jcr:content
[structure](#structure)
[policies](#policies)
thumbnail.png
```

**jcr:content**: holds properties of the template
- name, status, etc.

**structure**: Defines the structure of the resultant page
- merged with initial content
- changes made to structure will reflected in the created pages
- the root node (`structure/jcr:content/root`) defiens the list of components that will be available in the resulting page.
- The cq:responsive node holds definitions for the responsive layout.

**initial content**: defines the initial content that a new page will gave upon creation
- contains a jcr:content node that is copied to any new pages
- merged with structure
- existing pages will not be updated if the initial content is changed after creation

**content policies**: define the design properties of a component. For example, the components available
- stored on `/conf/<your-folder>/settings/wcm/policies/wcm/foundation/components`
- `cq:policy` on `/conf/<your-folder>/settings/wcm/templates/<your-template>/policies/jcr:content/root` provides a reference to the actual policy definition

**page policies**: allow you to define the content policy for the page

**Note: pages created with editable templates do not have a design mode**

## Static Templates
### Design Path Resolution
- If there is a design for the full and exact path of the content node
- If there is a design for the content node of the parent, then use that design.
- If there is a design for any node on the path of the content node, then use that design.