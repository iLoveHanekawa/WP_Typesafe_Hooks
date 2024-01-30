# Are wordpress action and filter hooks making you question your life choices?

## Forget about going to WP reference every 10 seconds to know what the hook name and arguments are!

## Motivation
When the guy who's teaching you how to use WP on youtube, visits the reference for the correct name of the hooks the entire time, something is wrong. PHP is a not a strongly typed language but it lets you use typesafety to your advantage if you opt into it. The wrapper utility does exactly that, instead of leaving you helpless with obscure hooks and filter names and random function names and args, random keys and everything, the wrapper exposes functions that wrap around hooks and also stick to the more "human friendly" names and provide intellisense for arguments to pass. This class is totally for developer experiencen and the proudest novelty of mine. A singleton class example has been provided if you wish to extend the Base Class.

## Example

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
// has intellisense and omits this 'function as a string' 
// concept which is incredibly susceptible to typing errors and removes 
// the need to remember names and provides type safety across arguments that 
// should be passed.

// instantiate the class
$hooks = new BasePlugin();
$filePath = 'script-name', get_template_directory_uri() . '/js/example.js';
// much cleaner and it will let you specify dependencies and all the optional 
//stuff but defaults are there since in most cases we don't really need all this
$hooks->addScript($filePath);
```