# Page Diff
## Operation Details
When comparing different versions, AEM recreate the node in `/tmp/versionhistory`

# Tag Libraries
## CQ Tag Library
>`/libs/foundation/global.jsp`

# Style System
Allows a template author to define style classes in the content policy of a component so authors can choose different styles of a component.

- Select a component in a template
- Edit the policy of the selected component and choose the styles tab
- add the corresponding class names for each style

## Setup
- Style tab in design dialog (include on the component):
	- `path = "/mnt/overlay/cq/gui/components/authoring/dialog/style/tab_design/styletab"`
	- `sling:resourceType = "granite/ui/components/coral/foundation/include"`

- Style tab in edit dialog (include on the dialog tab):
	- `path = "/mnt/overlay/cq/gui/components/authoring/dialog/style/tab_design/styletab"`
	- `sling:resourceType = "granite/ui/components/coral/foundation/include"`