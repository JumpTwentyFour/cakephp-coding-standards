# cakephp-coding-standards
Our coding standards for CakePHP applications.

## Setup

`composer require jumptwentyfour/cakephp-coding-standards --dev`

You will also need to add the following to your local phpstan.neon file includes:

`- ./vendor/jumptwentyfour/cakephp-coding-standards/phpstan.neon`

## Running PHP Easy Coding Standard
`vendor/bin/ecs check`

## Extending the Base ecs.php file
Create a new `ecs.php` file like the following example:-
```
<?php

declare(strict_types=1);

use JumpTwentyFour\PhpCodingStandards\Support\ConfigHelper;
use Symplify\EasyCodingStandard\Config\ECSConfig;
use Symplify\EasyCodingStandard\ValueObject\Option;

return static function (ECSConfig $ecsConfig): void {
    $ecsConfig->import(__DIR__ . '/vendor/jumptwentyfour/php-coding-standards/ecs.php');

    $parameters = $ecsConfig->parameters();
    
    $parameters->set(Option::PATHS, [
        __DIR__ . '/app',
        __DIR__ . '/tests',
    ]);
    
    $ecsConfig->skip(array_merge(ConfigHelper::make()->getParameter(Option::SKIP), [
        UnusedParameterSniff::class => [
            __DIR__ . '/app/Console/Kernel.php',
            __DIR__ . '/app/Exceptions/Handler.php',
        ],
        'Unused parameter $attributes.' => [
            __DIR__ . '/database/*.php',
        ],
        CamelCapsFunctionNameSniff::class => [
            '/tests/**',
        ],
    ]));
};
```
