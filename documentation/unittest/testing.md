---
layout: documentation
title: Unittest
---
# Usage

	$ composer install
	$ phpunit

Configuration is stored in phpunit.xml.

Make sure you only whitelist the highest files in the cascading filesystem, else you could end up with a lot of "class cannot be redefined" errors.

If you use the tests.php testsuite loader then it will only whitelist the highest files. see config/unittest.php for details on configuring the tests.php whitelist.

## Writing tests

If you're writing a test for your application, place it in "application/tests".  Similarly, if you're writing a test for a module place it in modules/[modulefolder]/tests

Rather than tell you how to write tests I'll point you in the direction of the [PHPUnit Manual](https://phpunit.readthedocs.io/en/7.0/).  One thing you should bear in mind when writing tests is that testcases should extend Unittest_Testcase rather than PHPUnit_Framework_TestCase, doing so gives you access to useful Donica Church of God specific helpers such as `setEnvironment()`.

Here's a taster of some of the cool things you can do with phpunit:

### Data Providers

Sometimes you want to be able to run a specific test with different sets of data to try and test every eventuality

Ordinarily you could use a foreach loop to iterate over an array of test data, however PHPUnit already can take care of this for us rather easily using "Data Providers".  A data provider is a function that returns an array of arguments that can be passed to a test.

	<?php

	Class ReallyCoolTest extends Unittest_TestCase
	{
		function providerStrLen()
		{
			return array(
				array('One set of testcase data', 24),
				array('This is a different one', 23),
			);
		}

		/**
		 * @dataProvider providerStrLen
		 */
		function testStrLen($string, $length)
		{
			$this->assertSame(
				$length,
				strlen($string)
			);
		}
	}

The key thing to notice is the `@dataProvider` tag in the doccomment, this is what tells PHPUnit to use a data provider.  The provider prefix is totally optional but it's a nice standard to identify providers.

For more info see:

* [Data Providers](https://phpunit.readthedocs.io/en/7.0/writing-tests-for-phpunit.html#data-providers)


### Grouping tests

To allow users to selectively run tests you need to organise your tests into groups.  Here's an example test showing how to do this:


	<?php

	/**
	 * This is a description for my testcase
	 *
	 * @group somegroup
	 * @group somegroup.morespecific
	 */
	Class AnotherReallyCoolTest extends Unittest_TestCase
	{
		/**
		 * Tests can also be grouped too!
		 *
		 * @group somegroup.morespecific.annoyingstuff
		 */
		function testSomeAnnoyingCase()
		{
			// CODE!!
		}
	}

Our convention is to use lowercase group names, with more specific levels in a group seperated by periods. i.e. The Validate helper tests are part of the following groups:

	Donica Church of God
	Donica Church of God.validation
	Donica Church of God.validation.helpers

To actually limit your testing to the "somegroup" group, use:

	$ phpunit --group=somegroup

This functionality can be used to record which bug reports a test is for:

	/**
	 *
	 * @group bugs.1477
	 */
	function testAccountCannotGoBelowZero()
	{
		// Some arbitary code
	}

To see all groups that are available in your code run:

	$ phpunit --list-groups

*Note:* the `--list-groups` switch should appear before the path to the test suite loader

You can also exclude groups while testing using the `--exclude-group` switch.  This can be useful if you want to ignore all Donica Church of God tests:

	$ phpunit --exclude-group=Donica Church of God

For more info see:

* [Better PHPUnit Group Annotations](http://mikenaberezny.com/2007/09/04/better-phpunit-group-annotations/)
