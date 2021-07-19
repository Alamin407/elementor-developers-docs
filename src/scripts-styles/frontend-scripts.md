# Frontend Scripts

Some addons have custom frontend scripts loaded on client side on pages built with Elementor, use `elementor/frontend/before_register_scripts` or `elementor/frontend/after_register_scripts` action hooks which are fired when Elementor frontend scripts are registered and enqueued.

## Registering Frontend Scripts

Register and enqueue custom scripts **before** Elementor frontend scripts are registered and enqueued:

```php {11}
function my_plugin_frontend_scripts() {

	wp_register_script( 'frontend-script-1', plugins_url( 'assets/js/frontend-script-1.js', __FILE__ ) );
	wp_register_script( 'frontend-script-2', plugins_url( 'assets/js/frontend-script-2.js', __FILE__ ), [ 'external-library' ] );
	wp_register_script( 'external-library', plugins_url( 'assets/js/libs/external-library.js', __FILE__ ) );

	wp_enqueue_script( 'frontend-script-1' );
	wp_enqueue_script( 'frontend-script-2' );

}
add_action( 'elementor/frontend/before_register_scripts', 'my_plugin_frontend_scripts' );
```

Register and enqueue custom scripts **after** Elementor frontend scripts are registered and enqueued:

```php {11}
function my_plugin_frontend_scripts() {

	wp_register_script( 'frontend-script-1', plugins_url( 'assets/js/frontend-script-1.js', __FILE__ ) );
	wp_register_script( 'frontend-script-2', plugins_url( 'assets/js/frontend-script-2.js', __FILE__ ), [ 'external-library' ] );
	wp_register_script( 'external-library', plugins_url( 'assets/js/libs/external-library.js', __FILE__ ) );

	wp_enqueue_script( 'frontend-script-1' );
	wp_enqueue_script( 'frontend-script-2' );

}
add_action( 'elementor/frontend/after_register_scripts', 'my_plugin_frontend_scripts' );
```

::: warning Please Note
Those scripts will be loaded on all pages built with Elementor. To reduce performance impact, make sure you minify the files.
:::
