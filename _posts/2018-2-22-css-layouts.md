---
layout: post
title: Css Layouts
image: /assets/img/2018-2-22-css-layouts/css.jpg
readtime: 14 minutes
---

I found myself doing some front end work, after months of backend and migration work. I felt a bit rusty when it came to layouts, and although using a prebuilt grid system is all good, i wanted to go back over layouts in general, and some more modern parts such as flexbox and grid.

Layouts are important if you more than just one big column of content. Its important to support a variety of devices and sizes nowadays, so just having one column isnt great, because you end up with really long content on wide screens, and on small screens, you tend to have to scroll sideways a lot, which isnt very user friendly.


## display

You can control the layout of content in a webpage using the css property display. most elements have a default of block or inline (also referred to as inline element and block element).

An example of an inline element is 
```html
<span></span> or <a></a>
```
An example of a block element is 
```html
<p></p> or <div></div>
```
An example of a none element is 
```html
<script></script> or <link />
```

You can override these in css to whichever display type you want to use.

## sizing blocking content

If you have a blocking element, and don't want it to stretch to the edge of the container element, you can set the width, and you can centralise the content by using `margin: 0 auto;`. This will cause problems where the width is longer than the screensize, or container div, but you can combat this by using max-width instead, which works better on smaller screens, such as mobile or tablet.

When sizing a blocking element, you can run into issues with padding, because the element will stretch beyond the specified width. e.g.

```html
<style>
   .style1{
    width: 300px;
    margin: 30px auto;
    background-color: #ccc;
  }
  .style2{
    width: 300px;
    margin: 30px auto;
    padding: 30px;
    background-color: #ccc;
    box-sizing: initial;
  }
  .style3{
    width: 300px;
    margin: 30px auto;
    padding: 30px;
    background-color: #ccc;
    box-sizing: border-box;
  }
</style>
<div class="style1">
  Some content with style 1
</div>
<div class="style2">
  Some content with style 2
</div>
<div class="style3">
  Some content with style 3
</div>
```

<style>
  .style1{
    width: 300px;
    margin: 30px auto;
    background-color: #ccc;
  }
  .style2{
    width: 300px;
    margin: 30px auto;
    padding: 30px;
    background-color: #ccc;
    box-sizing: initial;
  }
  .style3{
    width: 300px;
    margin: 30px auto;
    padding: 30px;
    background-color: #ccc;
    box-sizing: border-box;
  }
</style>
<div class="style1">
  Some content with style 1
</div>
<div class="style2">
  Some content with style 2
</div>
<div class="style3">
  Some content with style 3
</div>

The solution used to be to work out the difference and add it to your styles, to combat this, there is a css property called box-sizing, which will take into account the padding size on a blocking element, and makes for much simpler styles for blocking elements.

box-sizing is supported in almost all browsers, but it is still safest to use the prefixes:

```css
  -webkit-box-sizing: border-box;
     -moz-box-sizing: border-box;
          box-sizing: border-box;
```

## media queries

Media queries are probably the most important tool when it comes to responsive design. It allows you to apply styles based on screen size.


```html
<style>
@media screen and (min-width:600px) {
  nav {
    float: left;
    width: 25%;
  }
  section {
    margin-left: 25%;
  }
}
@media screen and (max-width:599px) {
  nav li {
    display: inline;
  }
}
.mediaquery-container{

}
</style>
<div class="mediaquery-container">
<nav>
Home
Directions
Contact
</nav>
<section>
Now when you resize your browser it's even cooler than ever!
</section>
<section>
The quick, brown fox jumps over a lazy dog. DJs flock by when MTV ax quiz prog. Junk MTV quiz graced by fox whelps. Bawds jog, flick quartz, vex nymphs. Waltz, bad nymph, for quick jigs vex! Fox nymphs grab quick-jived waltz. Brick quiz whangs jumpy veldt fox. Bright vixens jump; dozy fowl quack. Quick wafting zephyrs vex bold Jim. Quick zephyrs blow, vexing daft Jim.
</section>
</div>
```

<style>
@media screen and (min-width:600px) {
  nav {
    float: left;
    width: 25%;
  }
  section {
    margin-left: 25%;
  }
}
@media screen and (max-width:599px) {
  nav li {
    display: inline;
  }
}
.mediaquery-container{

}

.mediaquery-container-small{
  width:300px;
}
</style>
<div class="mediaquery-container">
<nav>
Home
Directions
Contact
</nav>
<section>
Now when you resize your browser it's even cooler than ever!
</section>
<section>
The quick, brown fox jumps over a lazy dog. DJs flock by when MTV ax quiz prog. Junk MTV quiz graced by fox whelps. Bawds jog, flick quartz, vex nymphs. Waltz, bad nymph, for quick jigs vex! Fox nymphs grab quick-jived waltz. Brick quiz whangs jumpy veldt fox. Bright vixens jump; dozy fowl quack. Quick wafting zephyrs vex bold Jim. Quick zephyrs blow, vexing daft Jim.
</section>
</div>

<div class="mediaquery-container-small">
<nav>
Home
Directions
Contact
</nav>
<section>
Now when you resize your browser it's even cooler than ever!
</section>
<section>
The quick, brown fox jumps over a lazy dog. DJs flock by when MTV ax quiz prog. Junk MTV quiz graced by fox whelps. Bawds jog, flick quartz, vex nymphs. Waltz, bad nymph, for quick jigs vex! Fox nymphs grab quick-jived waltz. Brick quiz whangs jumpy veldt fox. Bright vixens jump; dozy fowl quack. Quick wafting zephyrs vex bold Jim. Quick zephyrs blow, vexing daft Jim.
</section>
</div>

## column

There is a css property which allows you to present content in columns. It isn't fully supported, but it makes putting content into columns very simple.

<style>
.three-column {
  padding: 1em;
  -moz-column-count: 3;
  -moz-column-gap: 1em;
  -webkit-column-count: 3;
  -webkit-column-gap: 1em;
  column-count: 3;
  column-gap: 1em;
}
</style>
<div class="three-column">
The quick, brown fox jumps over a lazy dog. DJs flock by when MTV ax quiz prog. Junk MTV quiz graced by fox whelps. Bawds jog, flick quartz, vex nymphs. Waltz, bad nymph, for quick jigs vex! Fox nymphs grab quick-jived waltz. Brick quiz whangs jumpy veldt fox. Bright vixens jump; dozy fowl quack. Quick wafting zephyrs vex bold Jim. Quick zephyrs blow, vexing daft Jim.
</div>

## flexbox

Flexbox is great! It has redifined the way layouts are created, making it much simpler. There are a few things though, the specification changed a lot, and it is implemented differently in each browser. You will also find if you look for example online that people will use different properties, which are now obsolete.

examples of these are:
box; or a property that is box-{*}, you are looking at the 2009 version of Flexbox.
flexbox; or the flex() function, you are looking at a transition phase in 2011.
flex; and flex-{*} properties, you are looking at the current (as of this writing) specification.


<div style="display:none">http://weblog.bocoup.com/dive-into-flexbox/</div>

<style>
  .flexcontainer {
    display: -webkit-flex;
    display: flex;
    background-color: #eee;    
  }
  nav {
    width: 100px;    
  }
  .flex-column {
    -webkit-flex: 1;
            flex: 1;
  }
  .flextitle{
    background-color:#bbb;
  }
</style>

<div class="flexcontainer">
<nav>
Home
Directions
Contact
</nav>
<div class="flex-column">
  <section class="flextitle">
  Flexbox is so easy!
  </section>
  <section>
The quick, brown fox jumps over a lazy dog. DJs flock by when MTV ax quiz prog. Junk MTV quiz graced by fox whelps. Bawds jog, flick quartz, vex nymphs. Waltz, bad nymph, for quick jigs vex! Fox nymphs grab quick-jived waltz. Brick quiz whangs jumpy veldt fox. Bright vixens jump; dozy fowl quack. Quick wafting zephyrs vex bold Jim. Quick zephyrs blow, vexing daft Jim.
  </section>
</div>