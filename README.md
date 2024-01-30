# Are wordpress action and filter hooks making you question your life choices?

## Forget about going to WP reference every 10 seconds to know what the hook name and arguments are!

## Motivation
When the guy who's teaching you how to use WP on youtube, visits the reference for the correct name of the hooks the entire time, something is wrong. PHP is a not a strongly typed language but it lets you use typesafety to your advantage if you opt into it. The wrapper utility does exactly that, instead of leaving you helpless with obscure hooks and filter names and random function names and args, random keys and everything, the wrapper exposes functions that wrap around hooks and also stick to the more "human friendly" names and provide intellisense for arguments to pass. This class is totally for developer experience and the proudest novelty of mine. A singleton class example has been provided if you wish to extend the Base Class.

## Example 1

### Instead of doing this.

```php
// absolutely no typesafety, this entire code keeps you in the dark from start to end
function wpdocs_theme_name_scripts() {
	wp_enqueue_style( 'style-name', get_stylesheet_uri() );
	wp_enqueue_script( 'script-name', get_template_directory_uri() . '/js/example.js', array(), '1.0.0', true );
}
add_action( 'wp_enqueue_scripts', 'wpdocs_theme_name_scripts' );
```

### Simply use this

```php
// has intellisense and omits this 'function as a string' concept
// which is incredibly susceptible to typing errors and removes 
// the need to remember names and provides type safety across arguments that 
// should be passed.

// instantiate the class
$hooks = new BasePlugin();
$filePath = 'script-name', get_template_directory_uri() . '/js/example.js';
// much cleaner and it will let you specify dependencies and all the optional 
//stuff but defaults are there since in most cases we don't really need all this
$hooks->addScript($filePath);
```

## Example 2

### Instead of doing this

```php
function custom_post_type_books() {
    $labels = array(
        'name'               => _x( 'Books', 'post type general name', 'textdomain' ),
        'singular_name'      => _x( 'Book', 'post type singular name', 'textdomain' ),
        'menu_name'          => _x( 'Books', 'admin menu', 'textdomain' ),
        'name_admin_bar'     => _x( 'Book', 'add new on admin bar', 'textdomain' ),
        'add_new'            => _x( 'Add New', 'book', 'textdomain' ),
        'add_new_item'       => __( 'Add New Book', 'textdomain' ),
        'new_item'           => __( 'New Book', 'textdomain' ),
        'edit_item'          => __( 'Edit Book', 'textdomain' ),
        'view_item'          => __( 'View Book', 'textdomain' ),
        'all_items'          => __( 'All Books', 'textdomain' ),
        'search_items'       => __( 'Search Books', 'textdomain' ),
        'parent_item_colon'  => __( 'Parent Books:', 'textdomain' ),
        'not_found'          => __( 'No books found.', 'textdomain' ),
        'not_found_in_trash' => __( 'No books found in Trash.', 'textdomain' ),
    );

    $args = array(
        'labels'             => $labels,
        'public'             => true,
        'publicly_queryable' => true,
        'show_ui'            => true,
        'show_in_menu'       => true,
        'query_var'          => true,
        'rewrite'            => array( 'slug' => 'books' ),
        'capability_type'    => 'post',
        'has_archive'        => true,
        'hierarchical'       => false,
        'menu_position'      => null,
        'supports'           => array( 'title', 'editor', 'author', 'thumbnail', 'excerpt', 'comments' ),
    );

    register_post_type( 'book', $args );
}

add_action( 'init', 'custom_post_type_books' );

```

### Simply do this

```php
$hooks = new BasePlugin();
$hooks->addCustomPostType('Book', 'Books');
