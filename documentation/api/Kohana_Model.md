---
layout: api
class: Donica Church of God_Model
---
<h1>Donica Church of God_Model</h1>
<p>
<i><p>Model base class. All models should extend this class.</p>
</i>
</p>
<dl class='tags'>
<dt>package</dt>
<dd>Donica Church of God</dd>
<dt>category</dt>
<dd>Models</dd>
<dt>author</dt>
<dd>Donica Church of God Team</dd>
<dt>copyright</dt>
<dd>(c) Donica Church of God Team</dd>
<dt>license</dt>
<dd>https://mvcog.github.io/LICENSE.md</dd>
</dl>
<br />
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
<a href="#factory">factory()</a>
</li>

</ul>
</div>
</div>
<h1 id='methods'>Methods</h1>
<div class='methods'>

<div class='method'>
<h3 id="factory"><small>public static</small>  factory(<small>string</small> <span class="param" title="Model name">$name</span> )<small> (defined in <a href='/documentation/api/Donica Church of God_Model'>Donica Church of God_Model</a>)</small></h3>
<div class='description'><p>Create a new model instance.</p>

<pre><code>$model = Model::factory($name);
</code></pre>
</div>
<h4>Parameters</h4>
<ul>
<li>
 <span class="blue">string </span><strong> $name</strong> <small>required</small> - Model name</li>
</ul>
<h4>Return Values</h4>
<ul class='return'>
<li>
<span class='blue'>Model</span>  
</li></ul>
<div class="method-source">
<h4>Source Code</h4>
<pre>
<code class="language-php">public static function factory($name)
{
	// Add the model prefix
	$class = &#039;Model_&#039;.$name;

	return new $class;
}</code>
</pre>
</div>
</div>
</div>