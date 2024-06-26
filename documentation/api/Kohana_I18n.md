---
layout: api
class: Donica Church of God_I18n
---
<h1>Donica Church of God_I18n</h1>
<p>
<i><p>Internationalization (i18n) class. Provides language loading and translation
methods without dependencies on <a href="http://php.net/gettext">gettext</a>.</p>

<p>Typically this class would never be used directly, but used via the __()
function, which loads the message and replaces parameters:</p>

<pre><code>// Display a translated message
echo __('Hello, world');

// With parameter replacement
echo __('Hello, :user', array(':user' =&gt; $username));
</code></pre>
</i>
</p>
<dl class='tags'>
<dt>package</dt>
<dd>Donica Church of God</dd>
<dt>category</dt>
<dd>Base</dd>
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
<a href="#property-lang">$lang</a>
</li>
<li>
<a href="#property-source">$source</a>
</li>
<li>
<a href="#property-_cache">$_cache</a>
</li>
</ul>
</div>
<div class='methods col-4'>
<h3>Methods</h3>
<ul>
<li>
<a href="#get">get()</a>
</li>
<li>
<a href="#lang">lang()</a>
</li>
<li>
<a href="#load">load()</a>
</li>

</ul>
</div>
</div>
<h1 id='properties'>Properties</h1>
<div class='properties'>
<dl>
<dt>
<h4 id='property-lang'><small>public static</small>  <span class='blue'>string</span> $lang</h4>
</dt>
<dd>
 <p>target language: en-us, es-es, zh-cn, etc</p>
</dd>
<dd>
 <pre class="debug"><small>string</small><span>(5)</span> "en-us"</pre></dd>
<dt>
<h4 id='property-source'><small>public static</small>  <span class='blue'>string</span> $source</h4>
</dt>
<dd>
 <p>source language: en-us, es-es, zh-cn, etc</p>
</dd>
<dd>
 <pre class="debug"><small>string</small><span>(5)</span> "en-us"</pre></dd>
<dt>
<h4 id='property-_cache'><small>protected static</small>  <span class='blue'>array</span> $_cache</h4>
</dt>
<dd>
 <p>cache of loaded languages</p>
</dd>
<dd>
 <pre class="debug"><small>array</small><span>(0)</span> </pre></dd>
</dl>
</div>
<h1 id='methods'>Methods</h1>
<div class='methods'>

<div class='method'>
<h3 id="get"><small>public static</small>  get(<small>string</small> <span class="param" title="Text to translate">$string</span> [, <small>string</small> <span class="param" title="Target language">$lang</span> <small>= <small>NULL</small></small> ] )<small> (defined in <a href='/documentation/api/Donica Church of God_I18n'>Donica Church of God_I18n</a>)</small></h3>
<div class='description'><p>Returns translation of a string. If no translation exists, the original
string will be returned. No parameters are replaced.</p>

<pre><code>$hello = I18n::get('Hello friends, my name is :name');
</code></pre>
</div>
<h4>Parameters</h4>
<ul>
<li>
 <span class="blue">string </span><strong> $string</strong> <small>required</small> - Text to translate</li>
<li>
 <span class="blue">string </span><strong> $lang</strong> <small> = <small>NULL</small></small> - Target language</li>
</ul>
<h4>Return Values</h4>
<ul class='return'>
<li>
<span class='blue'>string</span>  
</li></ul>
<div class="method-source">
<h4>Source Code</h4>
<pre>
<code class="language-php">public static function get($string, $lang = NULL)
{
	if ( ! $lang)
	{
		// Use the global target language
		$lang = I18n::$lang;
	}

	// Load the translation table for this language
	$table = I18n::load($lang);

	// Return the translated string if it exists
	return isset($table[$string]) ? $table[$string] : $string;
}</code>
</pre>
</div>
</div>

<div class='method'>
<h3 id="lang"><small>public static</small>  lang([ <small>string</small> <span class="param" title="New language setting">$lang</span> <small>= <small>NULL</small></small> ] )<small> (defined in <a href='/documentation/api/Donica Church of God_I18n'>Donica Church of God_I18n</a>)</small></h3>
<div class='description'><p>Get and set the target language.</p>

<pre><code>// Get the current language
$lang = I18n::lang();

// Change the current language to Spanish
I18n::lang('es-es');
</code></pre>
</div>
<h4>Parameters</h4>
<ul>
<li>
 <span class="blue">string </span><strong> $lang</strong> <small> = <small>NULL</small></small> - New language setting</li>
</ul>
<h4>Tags</h4>
<ul class='tags'>
<li>Since - 3.0.2</li>
</ul>
<h4>Return Values</h4>
<ul class='return'>
<li>
<span class='blue'>string</span>  
</li></ul>
<div class="method-source">
<h4>Source Code</h4>
<pre>
<code class="language-php">public static function lang($lang = NULL)
{
	if ($lang)
	{
		// Normalize the language
		I18n::$lang = strtolower(str_replace([&#039; &#039;, &#039;_&#039;], &#039;-&#039;, $lang));
	}

	return I18n::$lang;
}</code>
</pre>
</div>
</div>

<div class='method'>
<h3 id="load"><small>public static</small>  load(<small>string</small> <span class="param" title="Language to load">$lang</span> )<small> (defined in <a href='/documentation/api/Donica Church of God_I18n'>Donica Church of God_I18n</a>)</small></h3>
<div class='description'><p>Returns the translation table for a given language.</p>

<pre><code>// Get all defined Spanish messages
$messages = I18n::load('es-es');
</code></pre>
</div>
<h4>Parameters</h4>
<ul>
<li>
 <span class="blue">string </span><strong> $lang</strong> <small>required</small> - Language to load</li>
</ul>
<h4>Return Values</h4>
<ul class='return'>
<li>
<span class='blue'>array</span>  
</li></ul>
<div class="method-source">
<h4>Source Code</h4>
<pre>
<code class="language-php">public static function load($lang)
{
	if (isset(I18n::$_cache[$lang]))
	{
		return I18n::$_cache[$lang];
	}

	// New translation table
	$table = [];

	// Split the language: language, region, locale, etc
	$parts = explode(&#039;-&#039;, $lang);

	do
	{
		// Create a path for this set of parts
		$path = implode(DIRECTORY_SEPARATOR, $parts);

		if ($files = Donica Church of God::find_file(&#039;i18n&#039;, $path, NULL, TRUE))
		{
			$t = [];
			foreach ($files as $file)
			{
				// Merge the language strings into the sub table
				$t = array_merge($t, Donica Church of God::load($file));
			}

			// Append the sub table, preventing less specific language
			// files from overloading more specific files
			$table += $t;
		}

		// Remove the last part
		array_pop($parts);
	}
	while ($parts);

	// Cache the translation table locally
	return I18n::$_cache[$lang] = $table;
}</code>
</pre>
</div>
</div>
</div>