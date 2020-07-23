# coding-standard

[![Build Status](https://travis-ci.com/DmitryBezik/ground-coding-standard.svg?branch=master)](https://travis-ci.com/DmitryBezik/ground-coding-standard)


The coding standard ruleset

This specification extends and expands [PSR-12](https://github.com/php-fig/fig-standards/blob/master/proposed/extended-coding-style-guide.md), 
the extended coding style guide and requires adherence to [PSR-1](https://www.php-fig.org/psr/psr-1), 
the basic coding standard. 

## Installation

1. Install the module via composer by running:

   ```bash
   $ composer require --dev ground/coding-standard
   ```

2. Add composer scripts into your `composer.json`:

   ```json
   "scripts": {
     "cs-check": "phpcs",
     "cs-fix": "phpcbf"
   }
   ```

3. Create `phpcs.xml` file on base path of your repository:

   ```xml
   <?xml version="1.0"?>
   <ruleset xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
            xsi:noNamespaceSchemaLocation="vendor/squizlabs/php_codesniffer/phpcs.xsd">
   
       <arg name="basepath" value="."/>
       <arg name="cache" value=".phpcs-cache"/>
       <arg name="colors"/>
       <arg name="extensions" value="php"/>
       <arg name="parallel" value="80"/>
       
       <!-- Show progress -->
       <arg value="p"/>
   
       <!-- Paths to check -->
       <file>config</file>
       <file>src</file>
       <file>test</file>
   
       <!-- Include all rules from the Laminas Coding Standard -->
       <rule ref="LaminasCodingStandard"/>
   </ruleset>
   ```

You can add or exclude some locations in that file.
For a reference please see: https://github.com/squizlabs/PHP_CodeSniffer/wiki/Annotated-Ruleset

## Usage

* To run checks only:

  ```bash
  $ composer cs-check
  ```

* To automatically fix many CS issues:

  ```bash
  $ composer cs-fix
  ```

## Ignoring parts of a File

Disable parts of a file:
```php
$xmlPackage = new XMLPackage;
// phpcs:disable
$xmlPackage['error_code'] = get_default_error_code_value();
$xmlPackage->send();
// phpcs:enable
```

Disable a specific rule:
```php
// phpcs:disable Generic.Commenting.Todo.Found
$xmlPackage = new XMLPackage;
$xmlPackage['error_code'] = get_default_error_code_value();
// TODO: Add an error message here.
$xmlPackage->send();
// phpcs:enable
```

Ignore a specific violation:
```php
$xmlPackage = new XMLPackage;
$xmlPackage['error_code'] = get_default_error_code_value();
// phpcs:ignore Generic.Commenting.Todo.Found
// TODO: Add an error message here.
$xmlPackage->send();
```

## Reference

Rules can be added, excluded or tweaked locally, depending on your preferences. 
More information on how to do this can be found here:

- [Coding Standard Tutorial](https://github.com/squizlabs/PHP_CodeSniffer/wiki/Coding-Standard-Tutorial)
- [Configuration Options](https://github.com/squizlabs/PHP_CodeSniffer/wiki/Configuration-Options)
- [Selectively Applying Rules](https://github.com/squizlabs/PHP_CodeSniffer/wiki/Annotated-Ruleset#selectively-applying-rules)
- [Customisable Sniff Properties](https://github.com/squizlabs/PHP_CodeSniffer/wiki/Customisable-Sniff-Properties)