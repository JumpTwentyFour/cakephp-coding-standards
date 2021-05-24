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

use Symfony\Component\DependencyInjection\Loader\Configurator\ContainerConfigurator;
use Symplify\EasyCodingStandard\ValueObject\Option;

return static function (ContainerConfigurator $containerConfigurator): void {
    $containerConfigurator->import(__DIR__ . '/vendor/jumptwentyfour/php-coding-standards/ecs.php');

    $parameters = $containerConfigurator->parameters();
    
    $parameters->set(Option::PATHS, [
        __DIR__ . '/app',
        __DIR__ . '/tests',
    ]);
};
```
