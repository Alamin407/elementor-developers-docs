# Add New Action

To add a new action to the context menu we need to define a new action object and insert the object to the relevant context menu group.

## Add New Widget Action

As an example we will add to the "general" group a new "alert" action which activates a callback function that alerts the widget name.

```js {1}
elementor.hooks.addFilter( 'elements/widget/contextMenuGroups', ( groups, view ) => {

	const newAction = {
		name: 'alert',
		icon: 'eicon-alert',
		title: 'Widget Type',
		isEnabled: () => true,
		callback: () => alert( view.model.get( 'widgetType' ) ),
	};

	groups.forEach( ( group ) => {
		if ( 'general' === group.name ) {
			group.actions.push( newAction );
		}
	} );

	return groups;

} );
```

## Add New Column Action

Now let's add to the "tools" group a new action that will console log some text.

```js {1}
elementor.hooks.addFilter( 'elements/column/contextMenuGroups', ( groups, view ) => {

	const newAction = {
		name: 'log',
		icon: 'eicon-code',
		title: 'Some Console Log',
		isEnabled: () => true,
		callback: () => console.log( 'some text...' ),
	};

	groups.forEach( ( group ) => {
		if ( 'tools' === group.name ) {
			group.actions.push( newAction );
		}
	} );

	return groups;

} );
```

## Add New Section Action

Now let's add to the "tools" group a new action that will open the page settings panel.

```js {1}
elementor.hooks.addFilter( 'elements/section/contextMenuGroups', ( groups, view ) => {

	const newAction = {
		name: 'page-settings',
		icon: 'eicon-cog',
		title: 'Page Settings',
		isEnabled: () => true,
		callback: () => $e.run( 'panel/page-settings/settings' ),
	};

	groups.forEach( ( group ) => {
		if ( 'tools' === group.name ) {
			group.actions.push( newAction );
		}
	} );

	return groups;

} );
```
