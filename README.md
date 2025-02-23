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

## Pro Tip 1

Keep your fork of this repo clean when developing your packages by creating a new branch for every single one of them. This way, your Laravel copy will always be clean from other package changes and will make your life easier by isolating any problems that might occur during your development phase.

### Create a New Branch for Each Package

Each package should be developed in its own branch to keep your fork clean:

```sh
git checkout -b feature/my-new-package
```

### Develop and Commit Your Changes

Work on your package and commit changes as needed:

```sh
git add .
git commit -m "Add my new package"
```

### Push the Package Branch to Your Fork

```sh
git push origin feature/my-new-package
```

### Create a Pull Request (If Needed)

If you want to merge your package into another branch, create a pull request on GitHub.

### Switch Back to a Clean State for New Development

Once your package is complete, return to the main branch and remove old package branches if necessary:

```sh
git checkout main
git pull origin main
```

### Optional

```sh
git branch -D feature/my-new-package  # Delete local branch
git push origin --delete feature/my-new-package  # Delete remote branch
```

By following this workflow, your Laravel fork will remain clean, and you’ll avoid conflicts when working on multiple packages. 🚀

## Pro Tip 2

Add [Laravel Package Tools](https://github.com/spatie/laravel-package-tools) to your package, it package contains a PackageServiceProvider that you can use in your packages to easily register config files, migrations, and more.

```sh
# Navigate to Your Package Directory
cd packages/vendor-name/package-name
# Install dependency
php composer require spatie/laravel-package-tools
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
