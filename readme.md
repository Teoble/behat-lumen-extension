## This project is a update of arisro/behat-lumen-extension to work in Lumen v5.2 or higher

The purpose of the project is to make available the [behat-lumen-extension](https://github.com/arisro/behat-lumen-extension
) for Lumen higher versions than v5.1, since that in the original project it works on in v5.2.

Thanks for [Aris Buzachis](https://github.com/arisro) for developing suching an helping tool as behat-lumen-extension 

# 1. Install Dependencies

As always, we need to pull in some dependencies through Composer.

    composer require behat/behat behat/mink behat/mink-extension teoble/behat-lumen-extension --dev

This will give us access to Behat, Mink, and, of course, the Lumen extension.

If you want to use a custom .env file for the Behat tests you will need to modify `bootstrap/app.php` like this:

```php
try {
    (new Dotenv\Dotenv(__DIR__.'/../', isset($dotEnvFile) ?: '.env'))->load();
} catch (Dotenv\Exception\InvalidPathException $e) {
    //
}
```

# 2. Create the behat.yml configuration file

Next, within your project root, create a `behat.yml` file, and add:

```yml
default:
  autoload: [ %paths.base%/tests/functional/contexts ]
  extensions:
    Arisro\Behat\ServiceContainer\LumenExtension:
      # env_file: .env.behat
    Behat\MinkExtension:
      default_session: lumen
      lumen: ~
  suites:
    default:
      paths: [ %paths.base%/tests/functional/features ]
      filters:
      contexts:
        - FeatureContext
```

Optinally, you can specify a different .env file for your functional tests (with a test DB for example).

# 3. Write Some Features

You have a very small example here https://github.com/arisro/behat-lumen-example.

Note: if you want to leverage some of the Mink helpers in your `FeatureContext` file, then be sure to extend `Behat\MinkExtension\Context\MinkContext`.
