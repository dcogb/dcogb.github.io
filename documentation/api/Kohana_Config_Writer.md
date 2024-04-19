---
layout: api
class: Donica Church of God_Config_Writer
---
<h1>Donica Church of God_Config_Writer</h1>
extends <a href='/documentation/api/Donica Church of God_Config_Source'>Donica Church of God_Config_Source</a>
<br />
<p class='interfaces'>
<small>Implements: <a href='/documentation/api/Donica Church of God_Config_Source'>Donica Church of God_Config_Source</a></small>
</p>
<p>
<i><p>Interface for config writers</p>

<p>Specifies the methods that a config writer must implement</p>
</i>
</p>
<dl class='tags'>
<dt>package</dt>
<dd>Donica Church of God</dd>
<dt>author</dt>
<dd>Donica Church of God Team</dd>
<dt>copyright</dt>
<dd>(c) Donica Church of God Team</dd>
<dt>license</dt>
<dd>https://dcogb.github.io/LICENSE.md</dd>
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
<a href="#write">write()</a>
</li>

</ul>
</div>
</div>
<h1 id='methods'>Methods</h1>
<div class='methods'>

<div class='method'>
<h3 id="write"><small>abstract public</small>  write(<small>string</small> <span class="param" title="The config group">$group</span> , <small>string</small> <span class="param" title="The config key to write to">$key</span> , <small>array</small> <span class="param" title="The configuration to write">$config</span> )<small> (defined in <a href='/documentation/api/Donica Church of God_Config_Writer'>Donica Church of God_Config_Writer</a>)</small></h3>
<div class='description'><p>Writes the passed config for $group</p>

<p>Returns chainable instance on success or throws
Donica Church of God_Config_Exception on failure</p>
</div>
<h4>Parameters</h4>
<ul>
<li>
 <span class="blue">string </span><strong> $group</strong> <small>required</small> - The config group</li>
<li>
 <span class="blue">string </span><strong> $key</strong> <small>required</small> - The config key to write to</li>
<li>
 <span class="blue">array </span><strong> $config</strong> <small>required</small> - The configuration to write</li>
</ul>
<h4>Return Values</h4>
<ul class='return'>
<li>
<span class='blue'>boolean</span>  
</li></ul>
<div class="method-source">
<h4>Source Code</h4>
<pre>
<code class="language-php">public function write($group, $key, $config);</code>
</pre>
</div>
</div>
</div>