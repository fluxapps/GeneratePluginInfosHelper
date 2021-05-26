<!-- Autogenerated from composer.json - All changes will be overridden if generated again! -->

# srag/generateplugininfoshelper Library

Automatic generate plugin infos such README.md, plugin.php, plugin.xml, ... from composer.json

This project is licensed under the GPL-3.0-only license

## Usage

### Composer

First add the following to your `composer.json` file:

```json
"require": {
  "srag/generateplugininfoshelper": ">=1.0.0"
},
```

And run a `composer install`.

If you deliver your plugin, the plugin has it's own copy of this library and the user doesn't need to install the library.

Tip: Because of multiple autoloaders of plugins, it could be, that different versions of this library exists and suddenly your plugin use an older or a newer version of an other plugin!

So I recommand to use [srag/librariesnamespacechanger](https://packagist.org/packages/srag/librariesnamespacechanger) in your plugin.

### GeneratePluginPhpAndXml

Generate `plugin.php` and `plugin.xml` and `LuceneObjectDefinition.xml` for ILIAS plugins from `composer.json`

Complete your `composer.json` with

```json
  ...
  "version": "x.y.z",
  ...
  "extra": {
    "ilias_plugin": {
      "id": "x",
      "name" => "X",
      "ilias_min_version": "x.y.z",
      "ilias_max_version": "x.y.z",
      "learning_progress": true | false,
      "lucene_search": true | false,
      "supports_export": true | false,
      "supports_cli_setup": true | false,
      "slot": "x/y/z"
      "events": [
        {
          "id": "X/Y",
          "type": "listen|raise"
        }
      ]
    }
  },
  ...
  "authors": [
    {
      "name": "...",
      "email": "...",
      "homepage": "...",
      "role": "Developer"
    }
  ],
  ...
```

#### Composer script

##### Automatic

```json
  ...
  "pre-autoload-dump": [
    ...,
      "srag\\GeneratePluginInfosHelper\\x\\GeneratePluginPhpAndXml::generatePluginPhpAndXml"
    ]
  ...
```

```bash
composer du
```

##### Manual

```json
  ...
  "generate-plugin-php-and-xml": [
    ...,
     "srag\\GeneratePluginInfosHelper\\x\\GeneratePluginPhpAndXml::generatePluginPhpAndXml"
    ]
  ...
```

```bash
composer generate-plugin-php-and-xml
```

#### In code

```php
...
use srag\GeneratePluginInfosHelper\x\GeneratePluginPhpAndXml; 
...
GeneratePluginPhpAndXml::getInstance()->doGeneratePluginPhpAndXml(string $project_root, ?string $version = null, ?array $extra_ilias_plugin = null, bool $autogenerated_comment = false, bool $log = false);
...
```

### GeneratePluginReadme

Auto generate `README.md`

Complete your `composer.json` with

```json
  ...
  "extra": {
    ...
    "generate_plugin_readme_template": "...",
    "long_description_template": "..."
    ...
  }
  ...
```

#### Composer script

##### Automatic

```json
  ...
  "pre-autoload-dump": [
    ...,
     "srag\\GeneratePluginInfosHelper\\x\\GeneratePluginReadme::generatePluginReadme"
    ]
  ...
```

```bash
composer du
```

##### Manual

```json
  ...
  "generate-plugin-readme": [
    ...,
     "srag\\GeneratePluginInfosHelper\\x\\GeneratePluginReadme::generatePluginReadme"
    ]
  ...
```

```bash
composer generate-plugin-readme
```

#### In code

```php
...
use srag\GeneratePluginInfosHelper\x\GeneratePluginReadme; 
...
GeneratePluginReadme::getInstance()->doGeneratePluginReadme(string $project_root, ?string $template = null, ?string $long_description_template = null, ?string $version = null, ?array $extra_ilias_plugin = null, bool $autogenerated_comment = false, bool $log = false);
...
```

### UpdateVersion

Auto update version in `composer.json` and `CHANGELOG.md`

- If the latest version in `CHANGELOG.md` is newer than the version in `composer.json`
  - It just sets the version in `CHANGELOG.md` to the version in `composer.json` and skip updating version
- If the version in `composer.json` is missing
  - It just sets the version to `1.0.0` and skip updating version
- If available a `x` version in `CHANGELOG.md`, it will be replaced with the new version
  - Otherwise a new version is added to `CHANGELOG.md` (With `TODO`)

#### Composer script

```json
  ...
  "update-version": [
    ...,
     "srag\\GeneratePluginInfosHelper\\x\\UpdateVersion::updateVersion"
    ]
  ...
```

```bash
composer update-version [update_type] [todo_changelog]
```

#### In code

```php
...
use srag\GeneratePluginInfosHelper\x\UpdateVersion; 
...
UpdateVersion::getInstance()->doGeneratePluginReadme(string $project_root, int $update_type = UpdateVersion::UPDATE_TYPE_PATCH|UpdateVersion::UPDATE_TYPE_MINOR|UpdateVersion::UPDATE_TYPE_MAJOR, ?string $todo_changelog = null, bool $log = false);
...
```

## Requirements

* PHP >=7.0
