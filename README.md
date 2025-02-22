# Laravel 11 Pagkage Development Project

Clean Laravel 11 with only Laravel Packager installed

## Stack

![Laravel](https://img.shields.io/badge/laravel-%23FF2D20.svg?style=for-the-badge&logo=laravel&logoColor=white)
![Docker](https://img.shields.io/badge/docker-%230db7ed.svg?style=for-the-badge&logo=docker&logoColor=white)

## Features

- [x] 📦 Laravel Packager - A cli tool for creating Laravel packages

## Installation

```sh
composer install
```

## Laravel Packager Commands

### New

**Command:**

```bash
php artisan packager:new my-vendor my-package
```

**Result:**
The command will handle practically everything for you. It will create a packages directory, creates the vendor and package directory in it, pulls in a skeleton package, sets up composer.json and creates a service provider.

**Options:**

```bash
php artisan packager:new my-vendor my-package --i
php artisan packager:new --i
```

The package will be created interactively, allowing to configure everything in the package's `composer.json`, such as the license and package description.

```bash
php artisan packager:new my-vendor/my-package
```

Alternatively you may also define your vendor and name with a forward slash instead of a space.

**Remarks:**
The new package will be based on [this custom skeleton](https://github.com/jeroen-g/packager-skeleton). If you want to use a different package skeleton, you can either:

- (A) publish the configuration file and change the default skeleton that will be used by all `packager:new` calls.
- (B) use the flag `--skeleton="http://github.com/path/to/archive/master.zip"` with your own skeleton to use the given skeleton for this one run instead of the one in the configuration.

### Get & Git

**Command:**

```bash
php artisan packager:get https://github.com/author/repository
php artisan packager:git https://github.com/author/repository
```

**Result:**
This will register the package in the app's `composer.json` file.
If the `packager:git` command is used, the entire Git repository is cloned. If `packager:get` is used, the package will be downloaded, without a repository. This also works with Bitbucket repositories, but you have to provide the flag `--host=bitbucket` for the `packager:get` command.

**Options:**

```bash
php artisan packager:get https://github.com/author/repository --branch=develop
php artisan packager:get https://github.com/author/repository my-vendor my-package
php artisan packager:git https://github.com/author/repository my-vendor my-package
```

It is possible to specify a branch with the `--branch` option. If you specify a vendor and name directly after the url, those will be used instead of the pieces of the url.

### Tests

**Command:**

```bash
php artisan packager:tests
```

**Result:**
Packager will go through all maintaining packages (in `packages/`) and publish their tests to `tests/packages`.
Add the following to phpunit.xml (under the other testsuites) in order to run the tests from the packages:

```xml
<testsuite name="Packages">
    <directory suffix="Test.php">./tests/packages</directory>
</testsuite>
```

**Options:**

```bash
php artisan packager:tests my-vendor my-package
```

**Remarks:**
If a tests folder exists, the files will be copied to a dedicated folder in the Laravel App tests folder. This allows you to use all of Laravel's own testing functions without any hassle.

### List

**Command:**

```bash
php artisan packager:list
```

**Result:**
An overview of all packages in the `/packages` directory.

**Options:**

```bash
php artisan packager:list --git
```

The packages are displayed with information on the git status (branch, commit difference with origin) if it is a git repository.

### Remove

**Command:**

```bash
php artisan packager:remove my-vendor my-package
```

**Result:**
The `my-vendor\my-package` package is deleted, including its references in `composer.json` and `config/app.php`.

### Publish

**Command:**

```bash
php artisan packager:publish my-vendor my-package https://github.com/my-vendor/my-package
```

**Result:**
The `my-vendor\my-package` package will be published to Github using the provided url.

### Check

**Command:**

```bash
php artisan packager:check my-vendor my-package
```

**Result:**
The `my-vendor\my-package` package will be checked for security vulnerabilities using SensioLabs security checker.

**Remarks**
You first need to run

```bash
composer require sensiolabs/security-checker
```

## License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for more information.
