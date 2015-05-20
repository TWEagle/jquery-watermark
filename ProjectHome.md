# Watermark plugin for jQuery #

## Version 3.2.0 ##

**_Compatible with jQuery 1.2.3+_**

**_Dual-licensed under the MIT or GPL2 licenses._**

## Contents ##

[Introduction](#Introduction.md)

[Using the Plugin](#Using_the_plugin.md)
> [Important Usage Notes](#Important_usage_notes.md)<br>
<blockquote><a href='#Static_properties_and_methods.md'>Static Properties and Methods</a></blockquote>

<a href='#Troubleshooting.md'>Troubleshooting</a>
<blockquote><a href='#Watermark_does_not_ever_appear.md'>Watermark does not ever appear</a><br>
<a href='#Watermark_only_appears_in_gray_text.md'>Watermark only appears in gray text</a><br>
<a href='#Watermark_appears_in_regular-styled_text_(not_light_gray_text).md'>Watermark appears in regular-styled text (not light gray text)</a><br>
<a href="#Can't_enter_the_same_text_as_the_watermark.md">Can't enter the same text as the watermark</a><br>
<a href='#Using_the_Watermark_and_Validate_plugins_on_the_same_elements.md'>Using the Watermark and Validate plugins on the same elements</a></blockquote>

<a href='#About_the_author.md'>About the Author</a>

<font size='4'><img src='http://jquery-watermark.googlecode.com/svn/trunk/jquery-watermark/wiki/icon-download-green-32.png' align='center' border='0' width='32' height='32' /> <b><a href='http://jquery-watermark.googlecode.com/svn/trunk/jquery-watermark/jquery.watermark-3.2.0.zip'>Download the latest version (3.2.0)</a></b></font>

<font size='4'><img src='http://jquery-watermark.googlecode.com/svn/trunk/jquery-watermark/wiki/icon-new-32.png' align='center' border='0' width='32' height='32' /> <b><a href='http://jquery-watermark.googlecode.com/svn/trunk/jquery-watermark/wiki/changelog.txt'>See latest change log</a></b></font>

<b>Note:</b> Because Google has disabled the ability to create new downloads on the Download page, the Download page only contains versions prior to release 3.2.0, and will not be updated. All versions will continue to be archived and available for download in the Source tab.<br>
<br>
<h1>Introduction</h1>

This simple-to-use jQuery plugin adds watermark capability to HTML input and textarea elements.<br>
<br>
A watermark typically appears as light gray text within an input or textarea element whenever the element is empty and does not have focus.  This provides a hint to the user as to what the input or textarea element is used for, or the type of input that is required.<br>
<br>
For example, a search input space sometimes appears at the top of the page, giving the user quick access to the search functionality.  Oftentimes you will see the word "Search" in light gray text in that space, and when the user clicks into the entry space, the word disappears.  That is an example of a watermark.<br>
<br>
<img src='http://jquery-watermark.googlecode.com/svn/trunk/jquery-watermark/wiki/sample-watermark.png' />

This plugin lets you specify the text that will be used for the watermark, and optionally you can supply your own CSS class name that will be applied to the input or textarea element every time the watermark is shown.<br>
<br>
If you do not supply your own class name, the class name "watermark" is used.<br>
<br>
Other important features include:<br>
<br>
<ul><li>Allows you to change the watermark text and/or class name any time after the watermark is initialized.  One of the examples included with the plugin demonstrates this capability by showing a watermark that doubles as a countdown timer.</li></ul>

<ul><li>Capable of displaying a watermark in password input elements, showing the watermark in plain text, but then switching to password-protected (obscured) mode when focused.  (Because of the complexity of making password watermarks operate, it is recommended that programmatic changes to password input elements be avoided.)</li></ul>

<ul><li>The plugin can also handle input elements of type="search" (WebKit browsers).</li></ul>

<ul><li>Supports HTML5 "placeholder" capabilities natively (in browsers that support it), or native support can be disabled so that the plugin controls all watermarks. (Watermarks are referred to as "placeholders" in HTML5.)</li></ul>

<ul><li>Supports drag-and-drop to watermarked elements.  Drag-and-drop support is significant, because it is currently supported by few (if any) jQuery plugins.  Combined with the Watermark plugin's ability to support native browser watermark features, this may be the most feature-complete watermark plugin available.</li></ul>

<ul><li>Enhances the native jQuery <code>.val()</code> function so you can use <code>.val()</code> directly to get and/or set an element's value.</li></ul>

<ul><li><b>New for version 3.2</b>, the plugin can set watermarks based on attribute values, so you can use <code>placeholder</code> attributes on input elements, using the plugin to add support for older browsers.</li></ul>

<h1>Using the plugin</h1>

To set a watermark of "Required information" on an input element, you would use a line of code such as:<br>
<br>
<pre><code>   $( '#inputId' ).watermark( 'Required information' );<br>
</code></pre>

If you want to use a different class name to define the appearance of the watermark, simply add the class name to the options specified in the second argument:<br>
<br>
<pre><code>   $( '#inputId' ).watermark( 'Required information', { className: 'myClassName' } );<br>
</code></pre>

If you want to avoid using native browser support (for example, for Search elements that have buggy drag-and-drop support in WebKit), add the useNative option to the options specified in the second argument, as follows:<br>
<br>
<pre><code>   $( '#inputId' ).watermark( 'Search', { useNative: false } );<br>
</code></pre>


<b>New for version 3.2</b>, you can set watermarks using the content of an attribute. For example, to use the <code>placeholder</code> attribute for native support in modern browsers, with the plugin providing support for older browsers, you can use one line of code such as the following. (When using the <code>textAttr</code> option the watermark string argument is optional.)<br>
<br>
<pre><code>   $( ':text' ).watermark( { textAttr: 'placeholder' } );<br>
</code></pre>

The <code>textAttr</code> option can be set to the name of any attribute, so (for example) you could use the <code>title</code> attribute by using <code>textAttr: 'title'</code>. When using <code>textAttr</code> to set watermarks, if the specified attribute does not exist on an element, no watermark is set on that element.<br>
<br>
<h2>Important usage notes</h2>

<ul><li><b>Multiple input elements</b> - You can set multiple input elements to the same watermark at once by including them all in the jQuery matched set.  For example, you can let the user know which input is optional by setting a watermark based on class name:<br>
<pre><code>   $( 'input.optional' ).watermark( 'Optional' );<br>
</code></pre></li></ul>

<ul><li><b>Non-relevant elements ignored</b> - The plugin ignores any elements in the matched set that are not input elements of <code>type="text/password/search"</code> and not <code>textarea</code> elements, so you do not have to filter your matched set to remove extra elements.</li></ul>

<ul><li><b>Return value</b> - When <code>watermark(...)</code> is called on a matched set, it returns the same matched set, allowing you to chain the plugin.</li></ul>

<ul><li><b>No longer necessary as of version 3.1!</b> Now you can use <code>.val()</code> to get and/or set an element's value, and all the plumbing is handled automatically for you. <del><b>Programmatic changes</b> - JavaScript events do not generally respond to programmatic changes in an input element's value, so you will need to manually refresh the watermark after you change the value through code.  When calling the plugin for the purpose of a refresh, do not include any arguments.  An example of changing the value, followed by a watermark refresh, would be:</del>
<blockquote><del>{{{<br>
$( '#myInput' ).val( 'newValue' ).watermark();<br>
}}}</del></blockquote></li></ul>

<ul><li><b>Avoid programmatic changes to passwords</b> - Because of the complexity of making password watermarks operate, it is recommended that programmatic changes to password input elements (changes made after the page finishes loading) be avoided.</li></ul>

<ul><li><b>Mutli-line textarea watermarks</b> - In textarea elements, you can create multi-line watermarks by specifying a line-break character ( <code>\n</code> ) where each new line should start.</li></ul>

<ul><li><b>Form submission</b> - <b>New functionality in version 3.2</b> - Prior to version 3.2 the plugin would automatically clean up all watermarks on the page prior to form submission. As of version 3.2 the plugin will only clean up watermarks within the form being submitted, so if you have additional forms on the page the watermarks in those other forms will not disappear when submitting the page. If you set the option <code>clearAllFormsOnSubmit</code> to <code>true</code>, the old behavior of cleaning up all watermarks on the page prior to submission will be performed.</li></ul>

<ul><li><b>Dynamic changes to watermark text and/or class</b> - After a watermark is initialized, you can continue to make changes to it, changing the text, the class name (style), or both.  The plugin demo page included in the download package demonstrates a watermark that doubles as a countdown timer.  As the timer nears zero, the style changes to red text.</li></ul>

<h2>Static properties and methods</h2>

The plugin includes static properties and methods that are called in a "stand-alone" manner (not on a matched set).  Many developers will never need to use any of these properties or methods, but they exist in case you need them.<br>
<br>
Any time <i>< selector ></i> is indicated, you can pass <b>any valid jQuery selector</b>, such as a DOM element, selector string, jQuery matched set, an array of elements, etc.<br>
<br>
<h3>$.watermark.options</h3>

<blockquote><h4>Examples</h4>
<pre><code>   $.watermark.options.className = 'myClass';<br>
   <br>
   $.watermark.options.useNative = false;<br>
   <br>
   $.watermark.options.useNative = myFunction;<br>
   <br>
   $.watermark.options.hideBeforeUnload = false;<br>
   <br>
   $.watermark.options = {<br>
      className: 'myClass',<br>
      useNative: false,<br>
      hideBeforeUnload: false<br>
   };<br>
</code></pre></blockquote>

<blockquote><h4>Description</h4>
You can control the default class name to use for watermarks, as well as if native browser support for watermarks should be used.  Both values can be overidden for individual watermarks.</blockquote>

<blockquote>The <code>hideBeforeUnload</code> option can be set to <code>false</code> to disable the automatic hiding of watermarks during the <code>beforeunload</code> event.  It is a global option that determines the behavior of all watermarks on the current page.  The option is not evaluated until the <code>beforeunload</code> event takes place, so the option can be set at any point before that.  The default value for this option is <code>true</code>.</blockquote>

<blockquote>If you try to set <code>hideBeforeUnload</code> by passing the option to the <code>.watermark()</code> function, it will have no effect, because it is a global option.  You must define the option by setting it as follows:<br>
<pre><code>   $.watermark.options.hideBeforeUnload = (true | false);<br>
</code></pre></blockquote>

<h3>$.watermark.show( < selector > )</h3>

<blockquote><h4>Example</h4>
<pre><code>   $.watermark.show( 'input.optional' );<br>
</code></pre></blockquote>

<blockquote><h4>Description</h4>
The equivalent of calling <code>.watermark()</code> (with no arguments) on a matched set, this method "refreshes" all matched elements.</blockquote>

<h3>$.watermark.hide( < selector > )</h3>

<blockquote><h4>Example</h4>
<pre><code>   $.watermark.hide( '#myInput' );<br>
</code></pre></blockquote>

<blockquote><h4>Description</h4>
Removes the watermark from all matched elements.  This does not completely destroy the watermark definition, so if after calling this method the user enters and leaves the element, the watermark will re-activate.</blockquote>

<h3>$.watermark.showAll()</h3>

<blockquote><h4>Example</h4>
<pre><code>   $.watermark.showAll();<br>
</code></pre></blockquote>

<blockquote><h4>Description</h4>
This method "refreshes" all watermarks on the page.  Maybe use useful after several programmatic changes were made to input values.</blockquote>

<h3>$.watermark.hideAll()</h3>

<blockquote><h4>Example</h4>
<pre><code>   $.watermark.hideAll();<br>
</code></pre></blockquote>

<blockquote><h4>Description</h4>
Removes all watermarks from the page.  This method is called automatically just before form submission to "clean up" all watermarks, and ensure that watermark text is not submitted to the Web server.  After calling this method, a watermark will re-appear if the user enters and then leaves an input element that previously contained a watermark.</blockquote>

<h1>Troubleshooting</h1>

<h3>Watermark does not ever appear</h3>

Check the following:<br>
<br>
<ul><li>Verify you are using the right syntax:<br>
<pre><code>   $( &lt; selector &gt; ).watermark( &lt; text &gt; [ , &lt; options &gt; ] )<br>
</code></pre></li></ul>

<ul><li>Be sure the first argument includes a valid string, and that the string is not empty.</li></ul>

<ul><li>Are you certain that your jQuery selector matched one or more input elements?  You can quickly test if your selector is matching elements by temporarily inserting an <code>alert()</code> call into your code.  If a zero (<code>0</code>) is displayed in the alert box, you know that it did not match any elements.<br>
<pre><code>   alert( $( &lt; selector &gt; ).length );<br>
</code></pre></li></ul>

<ul><li>The plugin only places watermarks on input elements with <code>type="text/password/search"</code> and on <code>textarea</code> elements.  Are you sure that you are matching the correct input element(s) and/or textarea(s)?  For example, you cannot use a watermark on an input element with <code>type="checkbox"</code>.</li></ul>

<h3>Watermark only appears in gray text</h3>

This plugin uses native browser watermark abilities if they are available.  For example, in Safari and Google Chrome, text input tags have built-in watermark abilities using the <code>placeholder</code> property.  Currently the use of <code>placeholder</code> always renders gray text.<br>
<br>
To override the use of native browser support for watermarks (placeholders), use the <code>$.watermark.options.useNative = false</code> option described above.<br>
<br>
<b>EXPERIMENTAL:</b> All modern Web browsers contain non-standard ways of styling placeholders (native watermarks).  Until there is an official W3C standard for styling placeholders, you'll need to keep an eye on this and adjust your code as browsers refine their placeholder styling features.<br>
<br>
<ul><li>WebKit and Blink (Safari, Google Chrome, Opera 15+):<br>
<pre><code>   input::-webkit-input-placeholder {<br>
      color: #f00;<br>
   }<br>
</code></pre></li></ul>

<ul><li>Firefox (version 4 to 18):<br>
<pre><code>   input:-moz-placeholder {<br>
      color: #f00;<br>
      opacity: 1;  /* FF sets opacity to 0.54 by default */<br>
   }<br>
</code></pre></li></ul>

<ul><li>Firefox (version 19+):<br>
<pre><code>   input::-moz-placeholder {<br>
      color: #f00;<br>
      opacity: 1;  /* FF sets opacity to 0.54 by default */<br>
   }<br>
</code></pre></li></ul>

<ul><li>Internet Explorer (version 10+):<br>
<pre><code>   input:-ms-input-placeholder {<br>
      color: #f00;<br>
   }<br>
</code></pre></li></ul>

<b>Note:</b> In the style definition for Firefox above we have set the opacity to 1 because Firefox (unlike other browsers) automatically sets the opacity of placeholders to 0.54 by default.<br>
<br>
User agents are required to ignore a rule with an unknown selector, so you need to separate the rules for each browser in your CSS. Otherwise the whole group would be ignored by all browsers, and you would see a regular gray watermark.<br>
<br>
So until a W3C standard is implemented, you <b>cannot</b> include a definition like the following.<br>
<pre><code>input::-webkit-input-placeholder,<br>
input:-moz-placeholder,<br>
input:-ms-input-placeholder {<br>
   color: #f00;<br>
}<br>
</code></pre>
Instead, you need three separate CSS definition blocks, one for each browser -- even though they will in all likelihood be made up of the same styles.<br>
<br>
<h3>Reading the element's <code>value</code> property gets the watermark, not the value</h3>

To get or set the value of a watermarked element (the value that the user enters), use the jQuery <code>.val()</code> function, not the <code>value</code> property of the element directly.  For example:<br>
<br>
<pre><code>// Set the value<br>
$( '#myElement' ).val( 'John Doe' );<br>
<br>
// Get the value<br>
alert( $( '#myElement' ).val() );<br>
</code></pre>

<h3>Watermark appears in regular-styled text (not light gray text)</h3>

Don't forget that you need to define the CSS style for the watermark, either in an external style sheet, or within the page itself (in <code>style</code> tags).<br>
<br>
If you are using the default class name (not specifying a className property in the second argument), you will need to define the watermark style using the class name <code>watermark</code>.  For example:<br>
<br>
<pre><code>&lt;style type="text/css"&gt;<br>
.watermark {<br>
   color: #999;<br>
}<br>
&lt;/style&gt;<br>
</code></pre>

If you specified the className property in the second argument, be sure that you have defined the watermark styles using that class name.<br>
<br>
Another common cause is a CSS cascade problem, where your style definition is overridden by another definition with a higher level of specificity.<br>
<br>
In the following example, the watermark style would appear as black text, even though the gray color is defined <b>after</b> the black definition:<br>
<br>
<pre><code>&lt;style type="text/css"&gt;<br>
input[type=text] {<br>
   color: #000;<br>
}<br>
.watermark {<br>
   color: #999;<br>
}<br>
&lt;/style&gt;<br>
</code></pre>

Even though the definition containing the gray color (<code>#999</code>) appears after the definition with the black color (<code>#000</code>), the watermark text will still be black.  That's because the first definition has a higher level of specificity, according to CSS rules, than the second definition.<br>
<br>
A sure-fire way to be sure this doesn't happen is to use <code>!important</code> on your watermark definitions, like so:<br>
<br>
<pre><code>&lt;style type="text/css"&gt;<br>
.watermark {<br>
   color: #999 !important;<br>
}<br>
&lt;/style&gt;<br>
</code></pre>

<h3>Can't enter the same text as the watermark</h3>

What if you want the user to be able to enter the exact same text as a watermark?  For example, your search box has the watermark "Search", and the user wants to search for the term "Search".<br>
<br>
Normally, once the user enters "Search", the plugin recognizes the text as a watermark, and applies the watermark style.<br>
<br>
One easy way around this is to use a watermark that contains spaces after the text.  So in the case of the search box, you could use<br><code>"Search      "</code> instead of <code>"Search"</code>.<br>
<br>
The user can't see the spaces, but internally they distinguish the watermark in a way that the user is unlikely to stumble across.<br>
<br>
<h3>Using the Watermark and Validate plugins on the same elements</h3>

If you find that your form validation is failing because the watermarks are not being cleared before validation occurs, then you need to adjust the order in which you set up the watermarks and validation.<br>
<br>
The proper order is to always set up watermarks before anything else -- especially before validation.  That's because jQuery carefully controls the order of events during form submission, and calls them in the order they were set up.  If you set up validation first, then the form will be validated before the watermarks are cleared.<br>
<br>
Setting up watermarks and validation in the proper order is as simple as placing the lines of code in the correct order, like in the following example:<br>
<br>
<pre><code>$( '#myElement' ).watermark( 'Required' );<br>
$( '#myForm' ).validate();<br>
</code></pre>

Also, it is recommended that you specify a <code>$.watermark.showAll()</code> call to be triggered every time form validation fails.  By doing so, you will ensure the watermarks re-appear when validation fails.<br>
<br>
For example, using the jQuery Validation plugin (available at <a href='http://bassistance.de/jquery-plugins/jquery-plugin-validation/'>http://bassistance.de/jquery-plugins/jquery-plugin-validation/</a>), you would change the above example as follows:<br>
<br>
<pre><code>$( '#myElement' ).watermark( 'Required' );<br>
$( '#myForm' ).validate( { invalidHandler: $.watermark.showAll } );<br>
</code></pre>

<h1>About the author</h1>

Todd Northrop is the owner and developer of Lottery Post (<a href='http://www.lotterypost.com/'>www.lotterypost.com</a>), the world's largest community of lottery players and home to the #1 lottery results service worldwide.<br>
<br>
He founded his technology company, Speednet Group (<a href='http://www.speednet.biz/'>www.speednet.biz</a>), in 2000.<br>
<br>
Todd was featured in Microsoft's (<a href='http://www.asp.net/ajax/showcase/interview/default.aspx?as=28'>ASP.NET AJAX Showcase</a>).