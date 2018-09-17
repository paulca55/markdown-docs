# WordPress Snippets

<!-- TOC depthFrom:2 depthTo:2 orderedList:false updateOnSave:true withLinks:true -->

- [Disable WP Search Functionality](#disable-wp-search-functionality)
- [Disable WordPress Emoticons](#disable-wordpress-emoticons)

<!-- /TOC -->

## Disable WP Search Functionality

```php
// Disable WP Search Functionality
function disable_search( $query, $error = true ) {
  if ( is_search() ) {
    $query->is_search = false;
    $query->query_vars[s] = false;
    $query->query[s] = false;
    // to error
    if ( $error == true )
    $query->is_404 = true;
  }
}
add_action( 'parse_query', 'disable_search' );
add_filter( 'get_search_form', create_function( '$a', "return null;" ) );
```

## Disable WordPress Emoticons

```php
// Disable WordPress Emoticons
remove_action('wp_head', 'print_emoji_detection_script', 7);
remove_action('wp_print_styles', 'print_emoji_styles');
```
