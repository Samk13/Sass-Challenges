# Sass-Challenges
Sass Challenges


SASS

Store Data with Sass Variables

Sass, or "Syntactically Awesome StyleSheets", is a language extension of CSS. It adds features that aren't available using basic CSS syntax. Sass makes it easier for developers to simplify and maintain the style sheets for their projects.

Sass: Store Data with Sass Variables
One feature of Sass that's different than CSS is it uses variables. They are declared and set to store data, similar to JavaScript.
In JavaScript, variables are defined using the letand constkeywords. In Sass, variables start with a $followed by the variable name.
Here are a couple examples:
$main-fonts: Arial, sans-serif;
$headings-color: green;

//To use variables:
h1 {
  font-family: $main-fonts;
  color: $headings-color;
}



Nest CSS with Sass
Sass allows nestingof CSS rules, which is a useful way of organizing a style sheet.
Normally, each element is targeted on a different line to style it, like so:
nav {
  background-color: red;
}

nav ul {
  list-style: none;
}

nav ul li {
  display: inline-block;
}
For a large project, the CSS file will have many lines and rules. This is where nestingcan help organize your code by placing child style rules within the respective parent elements:
nav {
  background-color: red;

  ul {
    list-style: none;

    li {
      display: inline-block;
    }
  }
}


Create Reusable CSS with Mixins
In Sass, a mixinis a group of CSS declarations that can be reused throughout the style sheet.
Newer CSS features take time before they are fully adopted and ready to use in all browsers. As features are added to browsers, CSS rules using them may need vendor prefixes. Consider "box-shadow":
div {
  -webkit-box-shadow: 0px 0px 4px #fff;
  -moz-box-shadow: 0px 0px 4px #fff;
  -ms-box-shadow: 0px 0px 4px #fff;
  box-shadow: 0px 0px 4px #fff;
}
It's a lot of typing to re-write this rule for all the elements that have a box-shadow, or to change each value to test different effects.
Mixinsare like functions for CSS. Here is how to write one:
@mixin box-shadow($x, $y, $blur, $c){ 
  -webkit-box-shadow: $x, $y, $blur, $c;
  -moz-box-shadow: $x, $y, $blur, $c;
  -ms-box-shadow: $x, $y, $blur, $c;
  box-shadow: $x, $y, $blur, $c;
}
The definition starts with @mixinfollowed by a custom name. The parameters (the $x, $y, $blur, and $cin the example above) are optional.
Now any time a box-shadowrule is needed, only a single line calling the mixinreplaces having to type all the vendor prefixes. A mixinis called with the @includedirective:
div {
  @include box-shadow(0px, 0px, 4px, #fff);
}

Here is my exemple : 
<style type='text/sass'>
@mixin border-radius($radius){
-webkit-border-radius: $radius;
-moz-border-radius: $radius;
-ms-border-radius: $radius;
border-radius: $radius;
}
 
  #awesome {
   width: 150px;
   height: 150px;
   background-color: green;
   @include border-radius(15px);  
 }
</style>
<div id="awesome"></div>
 
Use @if and @else to Add Logic To Your Styles


The @ifdirective in Sass is useful to test for a specific case - it works just like the ifstatement in JavaScript.
@mixin make-bold($bool) {
  @if $bool == true {
    font-weight: bold;
  }
}
And just like in JavaScript, @else ifand @elsetest for more conditions:
@mixin text-effect($val) {
  @if $val == danger {
    color: red;
  }
  @else if $val == alert {
    color: yellow;
  }
  @else if $val == success {
    color: green;
  }
  @else {
    color: black;
  }
}


<style type='text/sass'>
 @mixin border-stroke($val){
 @if $val == light {
   border: 1px solid black;
 }
 @else if $val == medium {
   border: 3px solid black;
 }
 @else if $val == heavy {
   border: 6px solid black;
 }
 @else {
   border: none;
 }
 }
 
 #box {
   width: 150px;
   height: 150px;
   background-color: red;
   @include border-stroke(medium);
 } 
</style>

<div id="box"></div>


Use @for to Create a Sass Loop


The @fordirective adds styles in a loop, very similar to a forloop in JavaScript.
@foris used in two ways: "start through end" or "start to end". The main difference is that "start to end" excludes the end number, and "start through end" includes the end number.
Here's a start through end example:
@for $i from 1 through 12 {
  .col-#{$i} { width: 100%/12 * $i; }
}
The #{$i}part is the syntax to combine a variable (i) with text to make a string. When the Sass file is converted to CSS, it looks like this:
.col-1 {
  width: 8.33333%;
}

.col-2 {
  width: 16.66667%;
}

...

.col-12 {
  width: 100%;
}
This is a powerful way to create a grid layout. Now you have twelve options for column widths available as CSS classes.

Write a @fordirective that takes a variable $jthat goes from 1 to 6.
It should create 5 classes called .text-1to .text-5where each has a font-sizeset to 10px multiplied by the index.

<style type='text/sass'>
@for $j from 1 to 6 {
.text-#{$j} {font-size: 10px * $j;}
}
 
 </style>

<p class="text-1">Hello</p>
<p class="text-2">Hello</p>
<p class="text-3">Hello</p>
<p class="text-4">Hello</p>
<p class="text-5">Hello</p>

 Use @each to Map Over Items in a List
The last challenge showed how the @fordirective uses a starting and ending value to loop a certain number of times. Sass also offers the @eachdirective which loops over each item in a list or map.
On each iteration, the variable gets assigned to the current value from the list or map.
@each $color in blue, red, green {
  .#{$color}-text {color: $color;}
}
A map has slightly different syntax. Here's an example:
$colors: (color1: blue, color2: red, color3: green);

@each $key, $color in $colors {
  .#{$color}-text {color: $color;}
}
Note that the $keyvariable is needed to reference the keys in the map. Otherwise, the compiled CSS would have color1, color2... in it.
Both of the above code examples are converted into the following CSS:
.blue-text {
  color: blue;
}

.red-text {
  color: red;
}

.green-text {
  color: green;
}

Write an @eachdirective that goes through a list: blue, black, redand assigns each variable to a .color-bgclass, where the "color" part changes for each item.
Each class should set the background-colorthe respective color.
<style type='text/sass'>
$colors :(blue, black, red);
@each $color in $colors {
.#{$color}-bg {background-color: $color;}
}
 
  div {
   height: 200px;
   width: 200px;
 }
</style>

<div class="blue-bg"></div>
<div class="black-bg"></div>
<div class="red-bg"></div>

	



Sass: Apply a Style Until a Condition is Met with @while
The @whiledirective is an option with similar functionality to the JavaScript whileloop. It creates CSS rules until a condition is met.
The @forchallenge gave an example to create a simple grid system. This can also work with @while.
$x: 1;
@while $x < 13 {
  .col-#{$x} { width: 100%/12 * $x;}
  $x: $x + 1;
}
First, define a variable $xand set it to 1. Next, use the @whiledirective to create the grid system while $xis less than 13.
After setting the CSS rule for width, $xis incremented by 1 to avoid an infinite loop.

Use @whileto create a series of classes with different font-sizes.
There should be 10 different classes from text-1to text-10. Then set font-sizeto 5px multiplied by the current index number. Make sure to avoid an infinite loop!

<style type='text/sass'>
$x: 1;
@while $x < 11 {
 .text-#{$x} { font-size: 5 * $x;}
 $x: $x + 1;
}
</style>

<p class="text-1">Hello</p>
<p class="text-2">Hello</p>
<p class="text-3">Hello</p>
<p class="text-4">Hello</p>
<p class="text-5">Hello</p>
<p class="text-6">Hello</p>
<p class="text-7">Hello</p>
<p class="text-8">Hello</p>
<p class="text-9">Hello</p>
<p class="text-10">Hello</p>


Split Your Styles into Smaller Chunks with Partials

	Partialsin Sass are separate files that hold segments of CSS code. These are imported and used in other Sass files. This is a great way to group similar code into a module to keep it organized.
Names for partialsstart with the underscore (_) character, which tells Sass it is a small segment of CSS and not to convert it into a CSS file. Also, Sass files end with the .scssfile extension. To bring the code in the partialinto another Sass file, use the @importdirective.
For example, if all your mixinsare saved in a partialnamed "_mixins.scss", and they are needed in the "main.scss" file, this is how to use them in the main file:
// In the main.scss file

@import 'mixins'
Note that the underscore is not needed in the importstatement - Sass understands it is a partial. Once a partialis imported into a file, all variables, mixins, and other code are available to use.

Write an @importstatement to import a partialnamed _variables.scssinto the main.scss file.


// The main.scss file
@import 'variables'


Extend One Set of CSS Styles to Another Element



Sass has a feature called extendthat makes it easy to borrow the CSS rules from one element and build upon them in another.
For example, the below block of CSS rules style a .panelclass. It has a background-color, heightand border.
.panel{
  background-color: red;
  height: 70px;
  border: 2px solid green;
}
Now you want another panel called .big-panel. It has the same base properties as .panel, but also needs a widthand font-size.
It's possible to copy and paste the initial CSS rules from .panel, but the code becomes repetitive as you add more types of panels.
The extenddirective is a simple way to reuse the rules written for one element, then add more for another:
.big-panel{
  @extend .panel;
  width: 150px;
  font-size: 2em;
}
The .big-panelwill have the same properties as .panelin addition to the new styles.


