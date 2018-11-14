# WordPress Snippets

<!-- TOC depthFrom:2 depthTo:2 orderedList:false updateOnSave:true withLinks:true -->

- [Disable WP Search Functionality](#disable-wp-search-functionality)
- [Disable WordPress Emoticons](#disable-wordpress-emoticons)
- [Using JSON data from a WordPress post](#using-json-data-from-a-wordpress-post)

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

## Using JSON data from a WordPress post

_Note: This snippet is using jQuery._

```js
$(function() {
  $.getJSON('http://www.littlecomets.com/wp-json/wp/v2/posts/', function(json) {
    $('.json01').html('Title: ' + json[0].title.rendered);
    $('.json02').html('Date: ' + json[0].date_gmt);
    $('.json03').html('URL: ' + json[0].link);
    $('.json04').html(json[0].excerpt.rendered);

    $('.json05').html('Title: ' + json[1].title.rendered);
    $('.json06').html('Date: ' + json[1].date_gmt);
    $('.json07').html('URL: ' + json[1].link);
    $('.json08').html(json[1].excerpt.rendered);
  });
});
```
