Coding Standards
================

> *Disclaimer* This is a copy of [Symfony's coding standards](https://github.com/symfony/symfony-docs/blob/2.7/contributing/code/standards.rst) but didn't want to fork the whole docs project.

When contributing code to Vinelab, you must follow its coding standards. To
make a long story short, here is the golden rule: **Imitate the existing
Symfony code**. Most open-source Bundles and libraries used by Symfony also
follow the same guidelines, and you should too.

Remember that the main advantage of standards is that every piece of code
looks and feels familiar, it's not about this or that being more readable.

Vinelab follows the standards defined in the `PSR-0`_, `PSR-1`_, `PSR-2`_ and `PSR-4`_
documents.

Since a picture - or some code - is worth a thousand words, here's a short
example containing most features described below:

```php
    <?php

    /*
     * This file is part of the Symfony package.
     *
     * (c) Fabien Potencier <fabien@symfony.com>
     *
     * For the full copyright and license information, please view the LICENSE
     * file that was distributed with this source code.
     */

    namespace Acme;

    /**
     * Coding standards demonstration.
     */
    class FooBar
    {
        const SOME_CONST = 42;

        private $fooBar;

        /**
         * @param string $dummy Some argument description
         */
        public function __construct($dummy)
        {
            $this->fooBar = $this->transformText($dummy);
        }

        /**
         * @param string $dummy Some argument description
         * @param array  $options
         *
         * @return string|null Transformed input
         *
         * @throws \RuntimeException
         */
        private function transformText($dummy, array $options = array())
        {
            $mergedOptions = array_merge(
                array(
                    'some_default' => 'values',
                    'another_default' => 'more values',
                ),
                $options
            );

            if (true === $dummy) {
                return;
            }

            if ('string' === $dummy) {
                if ('values' === $mergedOptions['some_default']) {
                    return substr($dummy, 0, 5);
                }

                return ucwords($dummy);
            }

            throw new \RuntimeException(sprintf('Unrecognized dummy option "%s"', $dummy));
        }

        private function reverseBoolean($value = null, $theSwitch = false)
        {
            if (!$theSwitch) {
                return;
            }

            return !$value;
        }
    }
```

Structure
---------

* Add a single space after each comma delimiter;

* Add a single space around binary operators (``==``, ``&&``, ...), with
  the exception of the concatenation (``.``) operator;

* Place unary operators (``!``, ``--``, ...) adjacent to the affected variable;

* Always use `identical comparison`_ unless you need type juggling;

* Use `Yoda conditions`_ when checking a variable against an expression to avoid
  an accidental assignment inside the condition statement (this applies to ``==``,
  ``!=``, ``===``, and ``!==``);

* Add a comma after each array item in a multi-line array, even after the
  last one;

* Add a blank line before ``return`` statements, unless the return is alone
  inside a statement-group (like an ``if`` statement);

* Use braces to indicate control structure body regardless of the number of
  statements it contains;

* Define one class per file - this does not apply to private helper classes
  that are not intended to be instantiated from the outside and thus are not
  concerned by the `PSR-0`_ and `PSR-4`_ autoload standards;

* Declare class properties before methods;

* Declare public methods first, then protected ones and finally private ones.
  The exceptions to this rule are the class constructor and the ``setUp`` and
  ``tearDown`` methods of PHPUnit tests, which should always be the first methods
  to increase readability;

* Use parentheses when instantiating classes regardless of the number of
  arguments the constructor has;

* Exception message strings should be concatenated using :phpfunction:`sprintf`.

Naming Conventions
------------------

* Use camelCase, not underscores, for variable, function and method
  names, arguments;

* Use underscores for option names and parameter names;

* Use namespaces for all classes;

* Prefix abstract classes with ``Abstract``. Please note some early Symfony classes
  do not follow this convention and have not been renamed for backward compatibility
  reasons. However all new abstract classes must follow this naming convention;

* Suffix interfaces with ``Interface``;

* Suffix traits with ``Trait``;

* Suffix exceptions with ``Exception``;

* Use alphanumeric characters and underscores for file names;

* For type-hinting in PHPDocs and casting, use ``bool`` (instead of ``boolean``
  or ``Boolean``), ``int`` (instead of ``integer``), ``float`` (instead of
  ``double`` or ``real``);

* Don't forget to look at the more verbose :doc:`conventions` document for
  more subjective naming considerations.

.. _service-naming-conventions:

Service Naming Conventions
~~~~~~~~~~~~~~~~~~~~~~~~~~

* A service name contains groups, separated by dots;

* The DI alias of the bundle is the first group (e.g. ``fos_user``);

* Use lowercase letters for service and parameter names;

* A group name uses the underscore notation.

Documentation
-------------

* Add PHPDoc blocks for all classes, methods, and functions;

* Omit the ``@return`` tag if the method does not return anything;

* The ``@package`` and ``@subpackage`` annotations are not used.

License
-------

* Symfony is released under the MIT license, and the license block has to be
  present at the top of every PHP file, before the namespace.

.. _`PSR-0`: http://www.php-fig.org/psr/psr-0/
.. _`PSR-1`: http://www.php-fig.org/psr/psr-1/
.. _`PSR-2`: http://www.php-fig.org/psr/psr-2/
.. _`PSR-4`: http://www.php-fig.org/psr/psr-4/
.. _`identical comparison`: https://php.net/manual/en/language.operators.comparison.php
.. _`Yoda conditions`: https://en.wikipedia.org/wiki/Yoda_conditions
