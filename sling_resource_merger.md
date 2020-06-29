# Sling Resource Merger in AEM

- the content of the customized definition has a higher priority than tge original
- where necessary properties defined in the customization, indicate how content merged from th eoriginal is to be used.

Goals:

- ensure customziation changes are not made in `/libs`
- reduce duplicated customziation code

Note: **Overrides** are not dependent on the search path, they use the property `sling:resourceSuperType` to make connection

## Properties
- `sling:hideProperties`:
	- Specifies the property, or list of properties, to hide.

- `sling:hideResource`:
	- Indicates whether the resources should be completely hidden, **including its children**.

- `sling:hideChildren`: 
	- Contains the child node, or list of child nodes, to hide. The properties of the node will be maintained.

- `sling:orderBefore`:
	- Contains the name of the sibling node that the current node should be positioned in front of

## Creating the Structure
- only need to recreate the skeleton structure, all intermediary nodes can be of type `nt:unstructured`

## Use Cases
- Add a property

- Redefine a property (not auto-created properties)
	- create the corresponding node
	- create the matching property and change its value


- Redefine an auto-create property
	- not supported by default
	- has to create the node first, hide the original property and then redefine it.

- Redefine a node and its children
	- hide children of a node
	- redefine the property/properties

- Hide a property
	- use `sling:hideProperties`

- Hide a node and its children
	- `sling:hideResource: true`

- Hide children of a node (keeping propertues of the node)
	- use `sling:hideChildren`

- Reorder nodes
	- use `sling:orderBefore` to specify the node that current node should be positioned before

## Invoking the Sling Resource Merger from code
- Overlay
	- mount point + relative path
	- `getResource('/mnt/overlay' + '<relative-path-to-resource>');`

- Override
	- mount point + absolute path
	- `getResource('/mnt/override' + '<absolute-path-to-resource>');`

