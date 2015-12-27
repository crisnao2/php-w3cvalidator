# php-w3cvalidator

[![Build Status](https://travis-ci.org/emmanuelroecker/php-w3cvalidator.svg?branch=master)](https://travis-ci.org/emmanuelroecker/php-w3cvalidator)
[![Coverage Status](https://coveralls.io/repos/emmanuelroecker/php-w3cvalidator/badge.svg?branch=master&service=github)](https://coveralls.io/github/emmanuelroecker/php-w3cvalidator?branch=master)

Validate html and css files using [w3c markup validation](http://validator.w3.org/) and [w3c css validation](http://jigsaw.w3.org/css-validator/).

## Installation

This library can be found on [Packagist](https://packagist.org/packages/glicer/w3c-validator).

The recommended way to install is through [composer](http://getcomposer.org).

Edit your `composer.json` and add:

```json
{
    "require": {
      "glicer/w3c-validator": "dev-master"
    }
}
```

And install dependencies:

```bash
php composer.phar install
```

## Example

```php
     <?php
     // Must point to composer's autoload file.
     require 'vendor/autoload.php';

    use Symfony\Component\Finder\SplFileInfo;
    use Symfony\Component\Finder\Finder;
    use GlValidator\GlW3CValidator;

    //create validator with directory destination of reports
    $validator = new GlW3CValidator(__DIR__ . "/result");

    //list of files to validate, it can be a Finder Symfony Object
    $finder = new Finder();

    //all files in entry directory
    $files  = $finder->files()->in(__DIR__ . "/entry/");

     //add glicer.css and glicer.html
    $files  = [$files, __DIR__ . "/glicer.css", __DIR__ . "/glicer.html"];

    //return array of reports path in html format
    $results = $validator->validate(
                                    $files,
                                    ['html', 'css'],  //validate html and css files
                                    function (SplFileInfo $file) { //callback function
                                            echo $file->getRealpath();
                                    }
                                    );

```

In this example, you can view reports result/w3c_css_glicer.html, result/w3c_html_glicer.html, result/... in your browser.

## Running Tests

Launch from command line :

```console
vendor\bin\phpunit
```

## Contact

Authors : Emmanuel ROECKER & Rym BOUCHAGOUR

[Web Development Blog - http://dev.glicer.com](http://dev.glicer.com/)

