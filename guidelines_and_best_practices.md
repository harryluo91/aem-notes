# AEM Development - Guidelines and Best Practices

## Using templates and components
General recommended approach:
- Keep the number of templates low - as low as the number of fundamentally different page structures on the web sites.
- Provide necessary flexibility and configuration capabilities to your custom components.
- Maximize use of the power and flexibility of AEM paragraph system - the parsys & iparsys components.

## Customizing components and other elements
Should always use existing components if possible (Overlaying). For example:
- Customizing a component
	- copy from `/libs/foundation/components/text`
	- to `/apps/myProject/components/text`

- Customizing pages shown by the error handler
	- copy `/libs/sling/servlet/errorhandler/`
	- to `/apps/sling/servlet/errorhandler/`

> You should not change anything in the `/libs` path because it will be overwritten next time the instance is upgraded. Instead do:
> 1. copy the items in `/libs` to `/apps`
> 2. make any changes within `/apps`

## When to use JCR Queries and when not to use them
Use:
- real end user requests, e.g. fulltext searches on content
- when structured content needs to be found across the entire repository
	- make sure it's only run when absolutely required, e.g. on component activation or cache invalidation (as opposed to workflow steps, event handlers, filters, etc.)

Do not use:
- rendering navigation
- creating a top X items overview
- showing counts of content items
- for rendering content, use navigational access to the content tree instead of performing a JCR Query

## Security Considerations
### JCR (Repository) Sessions
- Use the user session, not the administrative session
	- `slingRequest.getResourceResolver().adaptTo(Session.class);`

### Preventing XXS
- AEM applies the principle of filtering all user-supplied content upon output

