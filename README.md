# Setup Onlishop

This GitHub action helps you set up Onlishop, PHP, MySQL, Node.js, and other requirements in your GitHub Actions workflows for unit testing, end-to-end testing, and custom CI/CD workflows.

## Features

- **Easy setup**: Install Onlishop from any repository and version.
- **PHP & Composer**: Set up PHP (with optional extensions) and Composer.
- **Database**: Automatically configures MySQL.
- **Custom install**: Optionally install Onlishop with locale and currency.
- **Asset building**: Optionally build Administration and Storefront assets.
- **Test-ready**: Supports PHPUnit and E2E test environments.


## Inputs

| Name                   | Description                                                        | Default             | Required |
|------------------------|--------------------------------------------------------------------|---------------------|----------|
| `env`                  | Environment type: `test` for PHPUnit, `e2e` for end-to-end.        | `test`              | false    |
| `onlishop-version`     | Onlishop version to install (e.g. `v6.5.3.2`).                     |                     | true     |
| `onlishop-repository`  | GitHub repository to clone Onlishop from.                          | `onlishop/onlishop` | true |
| `php-version`          | PHP version (compatible with [shivammathur/setup-php]).            | `8.2`               | false    |
| `php-extensions`       | Comma-separated list of PHP extensions.                            |                     | false    |
| `composer-root-version`| Set the COMPOSER_ROOT_VERSION. `.auto` to discover from composer.json | `.auto`             | false    |
| `install`              | Whether to run the Onlishop installer.                             | `false`             | true     |
| `install-locale`       | Locale for Onlishop installation.                                  | `en-US`             | true     |
| `install-currency`     | Currency for Onlishop installation.                                | `CNY`               | true     |
| `install-admin`        | Build the Administration.                                          |                     | false    |
| `install-storefront`   | Build the Storefront.                                              |                     | false    |
| `keep-composer-tools`  | Keep Composer tools (PHPStan, ECS, BC-Checker) after install.      | `false`             | true     |
| `mysql-version`        | MySQL image to use, or `builtin` for GitHub-hosted MySQL.          | `builtin`           | false    |
| `node-version`         | Node.js version (e.g. `20.x`).                                    | `20.x`              | false    |
| `path`                 | Directory in `$GITHUB_WORKSPACE` to clone Onlishop into.           |                     | true     |

## Example pipeline to run PHPUnit tests

```yaml
jobs:
    phpunit:
        runs-on: ubuntu-latest
        steps:
            - name: Setup Onlishop
              uses: onlishop/setup-onlishop@v1
              with:
                env: test
                onlishop-version: v6.5.3.2
                onlishop-repository: onlishop/onlishop
                php-version: 8.1
                install: true

