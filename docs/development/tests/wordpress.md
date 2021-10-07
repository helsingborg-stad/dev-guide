---
title: "Wordpress unit tests"
date: 2021-09-23
draft: false
layout: default
parent: Tests
grand_parent: Development
---

# Wordpress unit tests
Wordpress in it self is unit tested rigorously by the wordpress developers.
Wordpress unit tests on plugins and themes should be done in isolation and not need a Wordpress install to run.

We use [Brain Monkey](https://giuseppe-mazzapica.gitbook.io/brain-monkey/) and [Mockery](https://github.com/mockery/mockery) to mock wordpress functions and classes.

## Test setup
Intall phpunit and brain-monkey.  
Mockery is installed as a dependency when installing brain-monkey.  
phpunit-result-printer for prettier output.  
```
composer require --dev brain/monkey codedungeon/phpunit-result-printer phpunit/phpunit ^9.5
```

### Folder structure and file name convention
Example folder structure for test and test subjects.
File names for test should be ClassnameTest.php and follow the source folder structure.  
ex.
```
project
│   phpunit.xml   
│
└───test
│   │
│   └───php
│       │   EditorTest.php
│       │   ModuleTest.php
│       │   ...
│       │
│       └───includes
│           │   bootstrap.php
│           │   PluginTestCase.php
│           │   ...
│
└───source
    │
    └───php
        │   Editor.php
        │   Module.php
        │   ...
```




#### phpunit.xml
Coverage directory element should point towards your php source directory.  
Testsuites directory element should point towards your php tests directory.  
``` xml
<?xml version="1.0" encoding="UTF-8"?>
<phpunit xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:noNamespaceSchemaLocation="https://schema.phpunit.de/9.3/phpunit.xsd"
         bootstrap="test/php/includes/bootstrap.php"
         backupGlobals="true"
         colors="true"
         convertErrorsToExceptions="true"
         convertNoticesToExceptions="true"
         convertWarningsToExceptions="true"
         verbose="true"
         printerClass="Codedungeon\PHPUnitPrettyResultPrinter\Printer">

  <coverage processUncoveredFiles="false">
    <include>
      <directory suffix=".php">./source/php</directory>
    </include>
    <report>
      <text outputFile="php://stdout" showUncoveredFiles="true"/>
    </report>
  </coverage>

  <testsuites>
    <testsuite name="Plugin Test Suit">
      <directory suffix="Test.php">./test/php</directory>
    </testsuite>
  </testsuites>
</phpunit>

```
#### bootstrap.php
```php
<?php

// Get around direct access blockers.
if (!defined('ABSPATH')) {
    define('ABSPATH', sys_get_temp_dir());
}

if (!defined('PLUGIN_ABSPATH')) {
    define('PLUGIN_ABSPATH', sys_get_temp_dir() . '/wp-content/plugins/my-plugin/');
}

require_once __DIR__ . '/../../../vendor/autoload.php';

require_once __DIR__ . '/PluginTestCase.php';

```

#### PluginTestCase.php
```php
<?php

namespace PluginTestCase;

use PHPUnit\Framework\TestCase;
use Mockery\Adapter\Phpunit\MockeryPHPUnitIntegration;
use Brain\Monkey;

class PluginTestCase extends \PHPUnit\Framework\TestCase
{
    use MockeryPHPUnitIntegration;

    /**
     * Setup which calls \WP_Mock setup
     *
     * @return void
     */
    public function setUp(): void
    {
        parent::setUp();
        Monkey\setUp();
        // A few common passthrough
        // 1. WordPress i18n functions
        Monkey\Functions\when('__')
            ->returnArg(1);
        Monkey\Functions\when('_e')
            ->returnArg(1);
        Monkey\Functions\when('_n')
            ->returnArg(1);
    }

    /**
     * Teardown which calls \WP_Mock tearDown
     *
     * @return void
     */
    public function tearDown(): void
    {
        Monkey\tearDown();
        parent::tearDown();
    }
}

```

## Test example
An example with some example asserts and mocks.

### Test
``` php

```

### Source
``` php
<?php

namespace JobListings\Entity;

/**
 * Class Taxonomy
 * @package JobListings\Entity
 */
class Taxonomy
{
    public $namePlural;
    public $nameSingular;
    public $slug;
    public $args;
    public $postTypes;

    /**
     * Taxonomy constructor.
     * @param $namePlural
     * @param $nameSingular
     * @param $slug
     * @param $postTypes
     * @param $args
     */
    public function __construct($namePlural, $nameSingular, $slug, $postTypes, $args)
    {
        $this->namePlural = $namePlural;
        $this->nameSingular = $nameSingular;
        $this->slug = $slug;
        $this->args = $args;
        $this->postTypes = $postTypes;

        add_action('init', array($this, 'registerTaxonomy'), 10, 0);
    }

    /**
     * @return string
     */
    public function registerTaxonomy()
    {
        $labels = array(
            'name'              => $this->namePlural,
            'singular_name'     => $this->nameSingular,
            'search_items'      => sprintf(__('Search %s', 'todo'), $this->namePlural),
            'all_items'         => sprintf(__('All %s', 'todo'), $this->namePlural),
            'parent_item'       => sprintf(__('Parent %s:', 'todo'), $this->nameSingular),
            'parent_item_colon' => sprintf(__('Parent %s:', 'todo'), $this->nameSingular) . ':',
            'edit_item'         => sprintf(__('Edit %s', 'todo'), $this->nameSingular),
            'update_item'       => sprintf(__('Update %s', 'todo'), $this->nameSingular),
            'add_new_item'      => sprintf(__('Add New %s', 'todo'), $this->nameSingular),
            'new_item_name'     => sprintf(__('New %s Name', 'todo'), $this->nameSingular),
            'menu_name'         => $this->nameSingular,
        );

        $this->args['labels'] = $labels;

        register_taxonomy($this->slug, $this->postTypes, $this->args);
        return $this->slug;
    }
}
```

## Pull Request testing
To indicate test have failed on a Github Pull Request.  

![GitHub Unit Test check](images/github-check-unit-test.png "github-check-unit-test.png")  

Add a Github Action to run the test command on Pull Requests tergeting dev branch.  
`.github/workflow/pre-merge-tests.yaml`
```yaml 
name: pull-request
on:
  pull_request:
    branches: [ dev ]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Check out code
      - uses: actions/checkout@v2

      - name: Setup PHP with composer v2
        uses: shivammathur/setup-php@v2
        with:
          php-version: '7.4'
          tools: composer:v2

      - name: Install dependencies
        run: composer install

      - name: Run tests 
        run: XDEBUG_MODE=coverage ./vendor/bin/phpunit --coverage-text
```

## Test coverage
Requires xdebug installed as php extension.

To check your test coverage
```
XDEBUG_MODE=coverage ./vendor/bin/phpunit --coverage-text
```