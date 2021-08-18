# Registering Finder Categories

When you create new [Finder Categories](/finder/) you need to register them to let the **Finder Categories Manager** know them. The registration process is done by hooking to the `elementor/finder/categories/init` action hook.

## Registering New Finder Categories

To register new finder categories use the following code:

```php
/**
 * Register new Elementor finder categories.
 *
 * @param \Elementor\Core\Common\Modules\Finder\Categories_Manager $finder_categories_manager Elementor finder categories manager.
 *
 * @return void
 */
function register_new_finder_categories( $finder_categories_manager ) {

	require_once( __DIR__ . '/finder/finder-1.php' );
	require_once( __DIR__ . '/finder/finder-2.php' );

	$finder_categories_manager->add_category( 'finder-category-1', new \Elementor_Finder_Category_1() );
	$finder_categories_manager->add_category( 'finder-category-2', new \Elementor_Finder_Category_2() );

}
add_action( 'elementor/finder/categories/init', 'register_new_finder_categories' );
```

We hook to the `elementor/finder/categories/init` action hook that holds `$categories_manager` parameter and pass a callback function that imports the new finder files and then registers them with the finder categories manager.

## New Registration Method

As of Elementor 3.5, developers should use the new way to register finder categories:

```php
/**
 * Register new Elementor finder categories.
 *
 * @param \Elementor\Core\Common\Modules\Finder\Categories_Manager $finder_categories_manager Elementor finder categories manager.
 *
 * @return void
 */
function register_new_finder_categories( $finder_categories_manager ) {

	require_once( __DIR__ . '/finder/finder-1.php' );
	require_once( __DIR__ . '/finder/finder-2.php' );

	$finder_categories_manager->register( new \Elementor_Finder_Category_1() );
	$finder_categories_manager->register( new \Elementor_Finder_Category_2() );

}
add_action( 'elementor/finder/categories/register', 'register_new_finder_categories' );
```

We hook to the new `elementor/finder/categories/register` action hook which holds the finder categories manager. Then we use the manager to register new finder categories by passing the finder category instance.
