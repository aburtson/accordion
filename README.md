# Accordion

This plugin includes an accordion-style dropdown list.

This is used when you want to present the viewer with an overview of related subjects (by title), but want to hide most of the subjects so the viewer can focus on one at a time.

## Initial setup

1. _Dependencies:_ verify that the jQuery is included in your project.
2. Include **accordion.js** in your JS directory.
3. Include **_accordion.scss** or **accordion.css** in your stylesheets.
4. Include the HTML inside **accordion.html** somewhere on your site.
5. Run gulp, and your accordion will be up and running.

## Working with HTML

### Adding new items

If you want to add another item to your accordion, copy an existing `<li>` and its contents and paste next to any existing `li` inside `ul.accordion`. Then, delete the HTML inside your `.accordion__title` and `.accordion__content`.

Or, you can simply copy/paste the below html inside your `ul.accordion`:

```html
<li>
	<h3 class="accordion__title"></h3>
	<div class="accordion__content__wrapper">
	  	<div class="accordion__content">
		   <p></p>
		</div>
	</div>
</li>
```

Enter your new content inside `.accordion__title` and `.accordion__content`.

Of course, feel free to remove/replace existing items. The HTML includes three accordion items by default, but two works fine as well.

## Working with JS

### The accordion function

At the bottom of the __accordion.js__ file, you will find this function:

```javascript
$('.accordion').accordion();
```

This function creates your accordion.

If you want to customize the settings of your accordion, include any of the below options, like so:

```javascript
$('.accordion').accordion({
    speed: 200,
    fade: false,
    sectionsOpen: 2
});
```

#### speed

Sets the slide transition time (in milliseconds). Default is `300`.

#### fade

If `true`, the slide animation will also fade the item content in/out when toggling open/closed. If `false`, there will be no fade animation when sliding open/closed. Default is `true`.

#### sectionsOpen

This determines if any items will be open by default. 

* `1`, `2`, `3`, etc: number corresponds to which item will be open (ie, `2` is second item). This will only work if you a corresponding item exists in your accordion. In other words, nothing will happen if you set `sectionsOpen` to `4` when there isn't a fourth item in your accordion.
* `true`, `'first'`, `1`: first item will be open
* `false`, `'none'`, all items will be closed
* `'last'`: last item will be open
* `all`: all items will be open

You can also make an array, using numbers, and/or `'first'` and `'last'`, like so:

```javascript
sectionsOpen: [ 2, 'last' ]
```

If this `sectionsOpen` is undeclared, all items will be closed.


### Creating multiple versions

The accordion only works on the provided HTML base structure, which has the class `.accordion`. If you want to target all accordions on your site with the same settings, keep the function like so:

```javascript
$('.accordion').accordion();
```
 
Otherwise, you can add classes or ids to different instances of the HTML, and run another function, like so:
 
```javascript
$('.your-class').accordion();
$('.your-other-class').accordion();
```
 
You can keep these functions inside the __accordion.js__ file, or add it to another JS file, as long as it is included on your site after __accordion.js__.

####Unique settings for each version

You can even add different settings in each function for further customization, like so:

```javascript
$('.your-class').accordion({
    speed: 300,
    fade: false
});

$('.your-other-class').accordion({
    speed: 180,
    sectionsOpen: [ 'first', 3 ]
});
```

__Note:__ If you do create different versions of the accordion, make sure to avoid including the default `$('.accordion').accordion();` on the same HTML page as your other accordion versions. 

## Working with CSS

### Page elements

Below is a basic highlight of the HTML structure.

```html
<ul class="accordion">
  <li>
      <h3 class="accordion__title">...</h3>
      <div class="accordion__content__wrapper">
          <div class="accordion__content">...</div>
      </div>
  </li>
  <li>...</li>
  <li>...</li>
</ul>
```

Inside each `li` exists the following elements:

* `.accordion__title`: click target for toggle the content open/closed
* `.accordion__content__wrapper`: wrapper for the item content. This is needed to set the height of the content when hiding/showing the item content.
* `.accordion__content`: exists inside `.accordion__content__wrapper`. If `fade` is `true`, this will animate opacity values to fade in/out the item content.