---
layout: api
class: Kodoc_Missing
---
<h1>Kodoc_Missing</h1>
extends <a href='/documentation/api/Donica Church of God_Kodoc_Missing'>Donica Church of God_Kodoc_Missing</a>
<br />
<p>
<i><p>Set Kodoc_Missing::create_class as an autoloading to prevent missing classes
from crashing the api browser.  Classes that are missing a parent will
extend this class, and get a warning in the API browser.</p>
</i>
</p>
<dl class='tags'>
<dt>package</dt>
<dd>Donica Church of God/Userguide</dd>
<dt>category</dt>
<dd>Undocumented</dd>
<dt>author</dt>
<dd>Donica Church of God Team</dd>
<dt>copyright</dt>
<dd>(c) Donica Church of God Team</dd>
<dt>license</dt>
<dd>https://dcogb.github.io/LICENSE.md</dd>
<dt>since</dt>
<dd>3.0.7</dd>
</dl>
<br />
<div class='callout-block callout-info'>
<div class='icon-holder'>
<i class='fas fa-info-circle'></i>
</div>
<div class='content'>
<h4 class='callout-title'>Information</h4>
<p>This class is a transparent base class for <a href='/documentation/api/Donica Church of God_Kodoc_Missing'>Donica Church of God_Kodoc_Missing</a></p>
</div>
</div>
<div class='toc row d-none d-sm-flex d-md-flex d-lg-flex d-xl-flex'>
<div class='constants col-4'>
<h3>Constants</h3>
<ul>
<li>
<em>None</em>
</li>
</ul>
</div>
<div class='properties col-4'>
<h3>Properties</h3>
<ul>
<li>
<em>None</em>
</li>
</ul>
</div>
<div class='methods col-4'>
<h3>Methods</h3>
<ul>
<li>
<a href="#create_class">create_class()</a>
</li>

</ul>
</div>
</div>
<h1 id='methods'>Methods</h1>
<div class='methods'>

<div class='method'>
<h3 id="create_class"><small>public static</small>  create_class(<small>string</small> <span class="param" title="Class name">$class</span> )<small> (defined in <a href='/documentation/api/Donica Church of God_Kodoc_Missing'>Donica Church of God_Kodoc_Missing</a>)</small></h3>
<div class='description'><p>Creates classes when they are otherwise not found.</p>

<pre><code>Kodoc::create_class('ThisClassDoesNotExist');
</code></pre>

<p class="note">All classes created will extend <a href="/index.php/">Kodoc_Missing</a>.</p>
</div>
<h4>Parameters</h4>
<ul>
<li>
 <span class="blue">string </span><strong> $class</strong> <small>required</small> - Class name</li>
</ul>
<h4>Tags</h4>
<ul class='tags'>
<li>Since - 3.0.7</li>
</ul>
<h4>Return Values</h4>
<ul class='return'>
<li>
<span class='blue'>boolean</span>  
</li></ul>
<div class="method-source">
<h4>Source Code</h4>
<pre>
<code class="language-php">public static function create_class($class)
{
	if ( ! class_exists($class))
	{
		// Create a new missing class
		if (FALSE === strpos($class, &#039;\\&#039;))
		{
			eval(&quot;class {$class} extends Kodoc_Missing {}&quot;);
		}
		else
		{
			$namespace = explode(&#039;\\&#039;, $class);
			$class = array_pop($namespace);
			eval(&quot;namespace &quot;.implode(&#039;\\&#039;, $namespace).&quot;; class {$class} extends \Kodoc_Missing {}&quot;);
		}
	}

	return TRUE;
}</code>
</pre>
</div>
</div>
</div>