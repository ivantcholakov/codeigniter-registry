
Registry library for CodeIgniter
================================

You may use this library for storing and accessing application-level global data.

Installation
------------

Put the file Registry.php within application/libraries/ folder of your project.

Usage Example
-------------

```php
//---------------------------------------------------------------------------
// Context #1:

$ci = get_instance(); // Use $this instead of $ci inside a controller's method.
$ci->load->library('registry'); // You may autoload this library at will.

$title = 'Page Title';
$subtitle = 'Page Subtitle';
$metatitle = 'Page Title (Meta)';
$metadescription = 'Page Description (Meta)';
$metakeywords = 'page, keywords, meta';

$ci->registry
    // Method chaining is possible.
    // Set values individually:
    ->set('page_title', $title)
    ->set('page_subtitle', $subtitle)
    // Set multiple values.
    ->set(compact('metatitle', 'metadescription', 'metakeywords'))
;

unset($title, $subtitle, $metatitle, $metadescription, $metakeywords);

//---------------------------------------------------------------------------
// Context #2:

$ci = get_instance();
$ci->load->library('registry');

// Get values individually.
$title = $ci->registry->get('page_title');
$subtitle = $ci->registry->get('page_subtitle');

// Get multiple values.
extract($ci->registry->get(array('metatitle', 'metadescription', 'metakeywords')));

// Test:
var_dump(compact('title', 'subtitle', 'metatitle', 'metadescription', 'metakeywords'));

//---------------------------------------------------------------------------
// Also:

// Check whether a particular value is present.
$test = $ci->registry->has('test_key');
var_dump($test);

// Gets everything from the registry (for debugging purpose).
$registry = $ci->registry->get_all();
var_dump($registry);

// Unset values.
$ci->registry
    ->delete('page_title')
    ->delete('page_subtitle')
    ->delete(array('metatitle', 'metadescription', 'metakeywords'))
;
var_dump($ci->registry->get_all());

// Use destroy method only for testing purposes
$ci->registry->destroy();
var_dump($ci->registry->get_all());

//---------------------------------------------------------------------------
```

License Information
-------------------

Author: Ivan Tcholakov ivantcholakov@gmail.com, 2014.  
License: The MIT License (MIT), http://opensource.org/licenses/MIT
