#jQuery Formelements
#### jQuery plugin to easily customize radio buttons, checkboxes and select elements

Formelements makes it easier gives a reliable way to customize the appearence and functionality of radio buttons, checkboxes and select elements.

Refer to the demo folder for examples.

###Note
-----
This used to be a privately used project but has by request been shared publicly, which means that a major cleanup will be needed, especially in the documentation and demo section.

###Setup
-----

Just include [jquery.formelements.js] after jQuery and add the formelements_base.css

####Standard
``` html
<script src='jquery.js'></script>
<script src='jquery.formelements.js'></script>
<link href="formelements_base.css" rel="stylesheet" type="text/css" />
```

``` js
<script src='jquery.js'></script>
<script src='jquery.formelements.js'></script>
<link href="formelements_base.css" rel="stylesheet" type="text/css" />
```
####NPM
$ npm install --save jquery.formelements

[npm]: http://npmjs.org/package/jquery.formelements
[jquery.formelements.js]: https://github.com/erikohmy/jquery.formelements/tree/master

``` js
var $ = jQuery = require('jquery');
require('jquery.formelements');
```

###Usage
-----

Code needs to be run after the elements are created ( and updated if changed )

``` js
$(function(){
	$('input[type="checkbox"], input[type="radio"], select').formelements();
});
```

###Available Options
-----

``` js
$('element').formelements({
	'classlist': "formelements_item my_custom_class"
});
```

``` js
{
	// For all elements
	'classlist': "formelements_item",
	
	// For select only
	'sel_multiselect_control': false,
	'sel_tinyscroll': false,
	'sel_searchbar': false,
	'sel_searchbar_focus': true,
	'text_search_placeholder': "Search...",
	'sel_delegate_click': false,
	'sel_label': function( $li, $input, index ) {},
	'sel_open': function( e, dd ) {
		dd.optwrap.not( ".open" ).fadeIn( 200, function() {
			if( dd.settings.sel_searchbar_focus ) {
				$( this ).find( 'input' ).focus();
			}
		});
		dd.optwrap.addClass( "open" );
		dd.wrap.addClass( "open" );
	},
	'sel_close': function( e, dd ) {
		dd.optwrap.fadeOut( 200, function() {
			dd.optwrap.removeClass( "open" );
			dd.wrap.removeClass( "open" );
		});
	},
	'search_function': function( search, $el ) {
		var text = $el.text();
	
		// hide the item if it is a placeholder, or if the searchvalue is not in its text
		if( $el.hasClass( 'placeholder' ) || text.toLowerCase().indexOf( search.toLowerCase() ) === -1 ) {
			return 0;
		}
		return 1;
	},
	'render_display': function() {
		var $select = $(this);
		var $display = $select.closest('.formelements_select').find('.formelements_select_display');
		var $opts = $select.formelements('selected');
	
		var labels = [];
		$opts.each(function(){
			labels.push( $(this).text() );
		});
	
		$display.html(labels.join(', '));
	}
}
```