<!-- DO NOT EDIT THIS FILE! -->
<!-- Instead edit recipe/magento2.php -->
<!-- Then run bin/docgen -->

# How to Deploy a Magento 2 Project

```php
require 'recipe/magento2.php';
```

[Source](/recipe/magento2.php)

Deployer is a free and open source deployment tool written in PHP. 
It helps you to deploy your Magento 2 application to a server. 
It is very easy to use and has a lot of features. 

Three main features of Deployer are:
- **Provisioning** - provision your server for you.
- **Zero downtime deployment** - deploy your application without a downtime.
- **Rollbacks** - rollback your application to a previous version, if something goes wrong.

Additionally, Deployer has a lot of other features, like:
- **Easy to use** - Deployer is very easy to use. It has a simple and intuitive syntax.
- **Fast** - Deployer is very fast. It uses parallel connections to deploy your application.
- **Secure** - Deployer uses SSH to connect to your server.
- **Supports all major PHP frameworks** - Deployer supports all major PHP frameworks.

You can read more about Deployer in [Getting Started](/docs/getting-started.md).

The [deploy](#deploy) task of **Magento 2** consists of:
* [deploy:prepare](/docs/recipe/common.md#deployprepare) – Prepares a new release
  * [deploy:info](/docs/recipe/deploy/info.md#deployinfo) – Displays info about deployment
  * [deploy:setup](/docs/recipe/deploy/setup.md#deploysetup) – Prepares host for deploy
  * [deploy:lock](/docs/recipe/deploy/lock.md#deploylock) – Locks deploy
  * [deploy:release](/docs/recipe/deploy/release.md#deployrelease) – Prepares release
  * [deploy:update_code](/docs/recipe/deploy/update_code.md#deployupdate_code) – Updates code
  * [deploy:shared](/docs/recipe/deploy/shared.md#deployshared) – Creates symlinks for shared files and dirs
  * [deploy:writable](/docs/recipe/deploy/writable.md#deploywritable) – Makes writable dirs
* [deploy:vendors](/docs/recipe/deploy/vendors.md#deployvendors) – Installs vendors
* [deploy:clear_paths](/docs/recipe/deploy/clear_paths.md#deployclear_paths) – Cleanup files and/or directories
* [deploy:magento](/docs/recipe/magento2.md#deploymagento) – Magento2 deployment operations
  * [magento:build](/docs/recipe/magento2.md#magentobuild) – Magento2 build operations
    * [magento:compile](/docs/recipe/magento2.md#magentocompile) – Compiles magento di
    * [magento:deploy:assets](/docs/recipe/magento2.md#magentodeployassets) – Deploys assets
  * [magento:maintenance:enable-if-needed](/docs/recipe/magento2.md#magentomaintenanceenable-if-needed) – Set maintenance mode if needed
  * [magento:config:import](/docs/recipe/magento2.md#magentoconfigimport) – Config Import
  * [magento:upgrade:db](/docs/recipe/magento2.md#magentoupgradedb) – Upgrades magento database
  * [magento:maintenance:disable](/docs/recipe/magento2.md#magentomaintenancedisable) – Disables maintenance mode
  * [magento:cache:flush](/docs/recipe/magento2.md#magentocacheflush) – Flushes Magento Cache
* [deploy:publish](/docs/recipe/common.md#deploypublish) – Publishes the release
  * [deploy:symlink](/docs/recipe/deploy/symlink.md#deploysymlink) – Creates symlink to release
  * [deploy:unlock](/docs/recipe/deploy/lock.md#deployunlock) – Unlocks deploy
  * [deploy:cleanup](/docs/recipe/deploy/cleanup.md#deploycleanup) – Cleanup old releases
  * [deploy:success](/docs/recipe/common.md#deploysuccess) – 


In addition the **Magento 2** recipe contains an artifact deployment.
This is a two step process where you first execute

```php
bin/dep artifact:build [options] [localhost]
```

to build an artifact, which then is deployed on a server with

```php
bin/dep artifact:deploy [host]
```

The `localhost` to build the artifact on has to be declared local, so either add
```php
localhost()
    ->set('local', true);
```
to your deploy.php or
```yaml
hosts:
    localhost:
        local: true
```
to your deploy yaml.

The [artifact:build](#artifact:build) command of **Magento 2** consists of: * [build:prepare](/docs/recipe/magento2.md#buildprepare) – Prepare local artifact build
* [build:remove-generated](/docs/recipe/magento2.md#buildremove-generated) – Clears generated files prior to building.
* [deploy:vendors](/docs/recipe/deploy/vendors.md#deployvendors) – Installs vendors
* [magento:compile](/docs/recipe/magento2.md#magentocompile) – Compiles magento di
* [magento:deploy:assets](/docs/recipe/magento2.md#magentodeployassets) – Deploys assets
* [artifact:package](/docs/recipe/magento2.md#artifactpackage) – Packages all relevant files in an artifact.


 The [artifact:deploy](#artifact:deploy) command of **Magento 2** consists of:
* [artifact:prepare](/docs/recipe/magento2.md#artifactprepare) – Prepares an artifact on the target server
  * [deploy:info](/docs/recipe/deploy/info.md#deployinfo) – Displays info about deployment
  * [deploy:setup](/docs/recipe/deploy/setup.md#deploysetup) – Prepares host for deploy
  * [deploy:lock](/docs/recipe/deploy/lock.md#deploylock) – Locks deploy
  * [deploy:release](/docs/recipe/deploy/release.md#deployrelease) – Prepares release
  * [artifact:upload](/docs/recipe/magento2.md#artifactupload) – Uploads artifact in release folder for extraction.
  * [artifact:extract](/docs/recipe/magento2.md#artifactextract) – Extracts artifact in release path.
  * [deploy:additional-shared](/docs/recipe/magento2.md#deployadditional-shared) – Adds additional files and dirs to the list of shared files and dirs
  * [deploy:shared](/docs/recipe/deploy/shared.md#deployshared) – Creates symlinks for shared files and dirs
  * [deploy:writable](/docs/recipe/deploy/writable.md#deploywritable) – Makes writable dirs
* [magento:maintenance:enable-if-needed](/docs/recipe/magento2.md#magentomaintenanceenable-if-needed) – Set maintenance mode if needed
* [magento:config:import](/docs/recipe/magento2.md#magentoconfigimport) – Config Import
* [magento:upgrade:db](/docs/recipe/magento2.md#magentoupgradedb) – Upgrades magento database
* [magento:maintenance:disable](/docs/recipe/magento2.md#magentomaintenancedisable) – Disables maintenance mode
* [deploy:symlink](/docs/recipe/deploy/symlink.md#deploysymlink) – Creates symlink to release
* [artifact:finish](/docs/recipe/magento2.md#artifactfinish) – Executes the tasks after artifact is released
  * [magento:cache:flush](/docs/recipe/magento2.md#magentocacheflush) – Flushes Magento Cache
  * [cachetool:clear:opcache](/docs/contrib/cachetool.md#cachetoolclearopcache) – Clears OPcode cache
  * [deploy:cleanup](/docs/recipe/deploy/cleanup.md#deploycleanup) – Cleanup old releases
  * [deploy:unlock](/docs/recipe/deploy/lock.md#deployunlock) – Unlocks deploy


The magento2 recipe is based on the [common](/docs/recipe/common.md) recipe.

## Configuration
### static_content_locales
[Source](https://github.com/deployphp/deployer/blob/master/recipe/magento2.php#L23)

By default setup:static-content:deploy uses `en_US`.
To change that, simply put `set('static_content_locales', 'en_US de_DE');`
in you deployer script.

```php title="Default value"
'en_US'
```


### magento_themes
[Source](https://github.com/deployphp/deployer/blob/master/recipe/magento2.php#L40)

You can also set the themes to run against. By default it'll deploy
all themes - `add('magento_themes', ['Magento/luma', 'Magento/backend']);`
If the themes are set as a simple list of strings, then all languages defined in [static_content_locales](/docs/recipe/magento2.md#static_content_locales) are
compiled for the given themes.
Alternatively The themes can be defined as an associative array, where the key represents the theme name and
the key contains the languages for the compilation (for this specific theme)
Example:
set('magento_themes', ['Magento/luma']); - Will compile this theme with every language from [static_content_locales](/docs/recipe/magento2.md#static_content_locales)
set('magento_themes', [
    'Magento/luma'   => null,                              - Will compile all languages from [static_content_locales](/docs/recipe/magento2.md#static_content_locales) for Magento/luma
    'Custom/theme'   => 'en_US fr_FR'                      - Will compile only en_US and fr_FR for Custom/theme
    'Custom/another' => '[static_content_locales](/docs/recipe/magento2.md#static_content_locales) it_IT' - Will compile all languages from [static_content_locales](/docs/recipe/magento2.md#static_content_locales) + it_IT for Custom/another
]); - Will compile this theme with every language

```php title="Default value"
[

]
```


### static_deploy_options
[Source](https://github.com/deployphp/deployer/blob/master/recipe/magento2.php#L45)

Static content deployment options, e.g. '--no-parent'



### split_static_deployment
[Source](https://github.com/deployphp/deployer/blob/master/recipe/magento2.php#L48)

Deploy frontend and adminhtml together as default

```php title="Default value"
false
```


### static_content_locales_backend
[Source](https://github.com/deployphp/deployer/blob/master/recipe/magento2.php#L51)

Use the default languages for the backend as default

```php title="Default value"
'{{static_content_locales}}'
```


### magento_themes_backend
[Source](https://github.com/deployphp/deployer/blob/master/recipe/magento2.php#L55)

backend themes to deploy. Only used if split_static_deployment=true
This setting supports the same options/structure as [magento_themes](/docs/recipe/magento2.md#magento_themes)

```php title="Default value"
['Magento/backend' => null]
```


### static_content_jobs
[Source](https://github.com/deployphp/deployer/blob/master/recipe/magento2.php#L61)

Also set the number of conccurent jobs to run. The default is 1
Update using: `set('static_content_jobs', '1');`

```php title="Default value"
'1'
```


### content_version
[Source](https://github.com/deployphp/deployer/blob/master/recipe/magento2.php#L63)



```php title="Default value"
return time();
```


### magento_dir
[Source](https://github.com/deployphp/deployer/blob/master/recipe/magento2.php#L68)

Magento directory relative to repository root. Use "." (default) if it is not located in a subdirectory

```php title="Default value"
'.'
```


### shared_files
[Source](https://github.com/deployphp/deployer/blob/master/recipe/magento2.php#L71)

Overrides [shared_files](/docs/recipe/deploy/shared.md#shared_files) from `recipe/deploy/shared.php`.



```php title="Default value"
[
    '{{magento_dir}}/app/etc/env.php',
    '{{magento_dir}}/var/.maintenance.ip',
]
```


### shared_dirs
[Source](https://github.com/deployphp/deployer/blob/master/recipe/magento2.php#L75)

Overrides [shared_dirs](/docs/recipe/deploy/shared.md#shared_dirs) from `recipe/deploy/shared.php`.



```php title="Default value"
[
    '{{magento_dir}}/var/composer_home',
    '{{magento_dir}}/var/log',
    '{{magento_dir}}/var/export',
    '{{magento_dir}}/var/report',
    '{{magento_dir}}/var/import',
    '{{magento_dir}}/var/import_history',
    '{{magento_dir}}/var/session',
    '{{magento_dir}}/var/importexport',
    '{{magento_dir}}/var/backups',
    '{{magento_dir}}/var/tmp',
    '{{magento_dir}}/pub/sitemap',
    '{{magento_dir}}/pub/media',
    '{{magento_dir}}/pub/static/_cache'
]
```


### writable_dirs
[Source](https://github.com/deployphp/deployer/blob/master/recipe/magento2.php#L90)

Overrides [writable_dirs](/docs/recipe/deploy/writable.md#writable_dirs) from `recipe/deploy/writable.php`.



```php title="Default value"
[
    '{{magento_dir}}/var',
    '{{magento_dir}}/pub/static',
    '{{magento_dir}}/pub/media',
    '{{magento_dir}}/generated',
    '{{magento_dir}}/var/page_cache'
]
```


### clear_paths
[Source](https://github.com/deployphp/deployer/blob/master/recipe/magento2.php#L97)

Overrides [clear_paths](/docs/recipe/deploy/clear_paths.md#clear_paths) from `recipe/deploy/clear_paths.php`.



```php title="Default value"
[
    '{{magento_dir}}/generated/*',
    '{{magento_dir}}/pub/static/_cache/*',
    '{{magento_dir}}/var/generation/*',
    '{{magento_dir}}/var/cache/*',
    '{{magento_dir}}/var/page_cache/*',
    '{{magento_dir}}/var/view_preprocessed/*'
]
```


### bin/magento
[Source](https://github.com/deployphp/deployer/blob/master/recipe/magento2.php#L106)



```php title="Default value"
'{{release_or_current_path}}/{{magento_dir}}/bin/magento'
```


### magento_version
[Source](https://github.com/deployphp/deployer/blob/master/recipe/magento2.php#L108)



```php title="Default value"
// detect version
$versionOutput = run('{{bin/php}} {{bin/magento}} --version');
preg_match('/(\d+\.?)+(-p\d+)?$/', $versionOutput, $matches);
return $matches[0] ?? '2.0';
```


### config_import_needed
[Source](https://github.com/deployphp/deployer/blob/master/recipe/magento2.php#L115)


:::info Autogenerated
The value of this configuration is autogenerated on access.
:::




### database_upgrade_needed
[Source](https://github.com/deployphp/deployer/blob/master/recipe/magento2.php#L129)


:::info Autogenerated
The value of this configuration is autogenerated on access.
:::




### enable_zerodowntime
[Source](https://github.com/deployphp/deployer/blob/master/recipe/magento2.php#L144)

Deploy without setting maintenance mode if possible

```php title="Default value"
true
```


### artifact_file
[Source](https://github.com/deployphp/deployer/blob/master/recipe/magento2.php#L328)

The file the artifact is saved to

```php title="Default value"
'artifact.tar.gz'
```


### artifact_dir
[Source](https://github.com/deployphp/deployer/blob/master/recipe/magento2.php#L331)

The directory the artifact is saved in

```php title="Default value"
'artifacts'
```


### artifact_excludes_file
[Source](https://github.com/deployphp/deployer/blob/master/recipe/magento2.php#L335)

Points to a file with a list of files to exclude from packaging.
The format is as with the `tar --exclude-from=[file]` option

```php title="Default value"
'artifacts/excludes'
```


### build_from_repo
[Source](https://github.com/deployphp/deployer/blob/master/recipe/magento2.php#L338)

If set to true, the artifact is built from a clean copy of the project repository instead of the current working directory

```php title="Default value"
false
```


### repository
[Source](https://github.com/deployphp/deployer/blob/master/recipe/magento2.php#L341)

Overrides [repository](/docs/recipe/common.md#repository) from `recipe/common.php`.

Set this value if "build_from_repo" is set to true. The target to deploy must also be set with "--branch", "--tag" or "--revision"

```php title="Default value"
null
```


### artifact_path
[Source](https://github.com/deployphp/deployer/blob/master/recipe/magento2.php#L344)

The relative path to the artifact file. If the directory does not exist, it will be created

```php title="Default value"
if (!testLocally('[ -d {{artifact_dir}} ]')) {
runLocally('mkdir -p {{artifact_dir}}');
}
return get('artifact_dir') . '/' . get('artifact_file');
```


### bin/tar
[Source](https://github.com/deployphp/deployer/blob/master/recipe/magento2.php#L352)

The location of the tar command. On MacOS you should have installed gtar, as it supports the required settings
:::info Autogenerated
The value of this configuration is autogenerated on access.
:::




### additional_shared_files
[Source](https://github.com/deployphp/deployer/blob/master/recipe/magento2.php#L424)

Array of shared files that will be added to the default shared_files without overriding



### additional_shared_dirs
[Source](https://github.com/deployphp/deployer/blob/master/recipe/magento2.php#L426)

Array of shared directories that will be added to the default shared_dirs without overriding




## Tasks

### magento:compile
[Source](https://github.com/deployphp/deployer/blob/master/recipe/magento2.php#L154)

Compiles magento di.

To work correctly with artifact deployment, it is necessary to set the MAGE_MODE correctly in `app/etc/config.php`
e.g.
```php
'MAGE_MODE' => 'production'
```


### magento:deploy:assets
[Source](https://github.com/deployphp/deployer/blob/master/recipe/magento2.php#L180)

Deploys assets.

To work correctly with artifact deployment it is necessary to set `system/dev/js` , `system/dev/css` and `system/dev/template`
in `app/etc/config.php`, e.g.:
```php
'system' => [
    'default' => [
        'dev' => [
            'js' => [
                'merge_files' => '1',
                'minify_files' => '1'
            ],
            'css' => [
                'merge_files' => '1',
                'minify_files' => '1'
            ],
            'template' => [
                'minify_html' => '1'
            ]
        ]
    ]
```


### magento:deploy:assets:adminhtml
[Source](https://github.com/deployphp/deployer/blob/master/recipe/magento2.php#L194)

Deploys assets for backend only.




### magento:deploy:assets:frontend
[Source](https://github.com/deployphp/deployer/blob/master/recipe/magento2.php#L199)

Deploys assets for frontend only.




### magento:sync:content_version
[Source](https://github.com/deployphp/deployer/blob/master/recipe/magento2.php#L247)

Syncs content version.




### magento:maintenance:enable
[Source](https://github.com/deployphp/deployer/blob/master/recipe/magento2.php#L257)

Enables maintenance mode.




### magento:maintenance:disable
[Source](https://github.com/deployphp/deployer/blob/master/recipe/magento2.php#L263)

Disables maintenance mode.




### magento:maintenance:enable-if-needed
[Source](https://github.com/deployphp/deployer/blob/master/recipe/magento2.php#L269)

Set maintenance mode if needed.




### magento:config:import
[Source](https://github.com/deployphp/deployer/blob/master/recipe/magento2.php#L276)

Config Import.




### magento:upgrade:db
[Source](https://github.com/deployphp/deployer/blob/master/recipe/magento2.php#L285)

Upgrades magento database.




### magento:cache:flush
[Source](https://github.com/deployphp/deployer/blob/master/recipe/magento2.php#L294)

Flushes Magento Cache.




### deploy:magento
[Source](https://github.com/deployphp/deployer/blob/master/recipe/magento2.php#L299)

Magento2 deployment operations.




This task is group task which contains next tasks:
* [magento:build](/docs/recipe/magento2.md#magentobuild)
* [magento:maintenance:enable-if-needed](/docs/recipe/magento2.md#magentomaintenanceenable-if-needed)
* [magento:config:import](/docs/recipe/magento2.md#magentoconfigimport)
* [magento:upgrade:db](/docs/recipe/magento2.md#magentoupgradedb)
* [magento:maintenance:disable](/docs/recipe/magento2.md#magentomaintenancedisable)
* [magento:cache:flush](/docs/recipe/magento2.md#magentocacheflush)


### magento:build
[Source](https://github.com/deployphp/deployer/blob/master/recipe/magento2.php#L309)

Magento2 build operations.




This task is group task which contains next tasks:
* [magento:compile](/docs/recipe/magento2.md#magentocompile)
* [magento:deploy:assets](/docs/recipe/magento2.md#magentodeployassets)


### deploy
[Source](https://github.com/deployphp/deployer/blob/master/recipe/magento2.php#L315)

Deploys your project.




This task is group task which contains next tasks:
* [deploy:prepare](/docs/recipe/common.md#deployprepare)
* [deploy:vendors](/docs/recipe/deploy/vendors.md#deployvendors)
* [deploy:clear_paths](/docs/recipe/deploy/clear_paths.md#deployclear_paths)
* [deploy:magento](/docs/recipe/magento2.md#deploymagento)
* [deploy:publish](/docs/recipe/common.md#deploypublish)


### artifact:package
[Source](https://github.com/deployphp/deployer/blob/master/recipe/magento2.php#L363)

Packages all relevant files in an artifact.




### artifact:upload
[Source](https://github.com/deployphp/deployer/blob/master/recipe/magento2.php#L373)

Uploads artifact in release folder for extraction.




### artifact:extract
[Source](https://github.com/deployphp/deployer/blob/master/recipe/magento2.php#L378)

Extracts artifact in release path.




### build:remove-generated
[Source](https://github.com/deployphp/deployer/blob/master/recipe/magento2.php#L384)

Clears generated files prior to building.




### build:prepare
[Source](https://github.com/deployphp/deployer/blob/master/recipe/magento2.php#L389)

Prepare local artifact build.




### artifact:build
[Source](https://github.com/deployphp/deployer/blob/master/recipe/magento2.php#L414)

Builds an artifact.




This task is group task which contains next tasks:
* [build:prepare](/docs/recipe/magento2.md#buildprepare)
* [build:remove-generated](/docs/recipe/magento2.md#buildremove-generated)
* [deploy:vendors](/docs/recipe/deploy/vendors.md#deployvendors)
* [magento:compile](/docs/recipe/magento2.md#magentocompile)
* [magento:deploy:assets](/docs/recipe/magento2.md#magentodeployassets)
* [artifact:package](/docs/recipe/magento2.md#artifactpackage)


### deploy:additional-shared
[Source](https://github.com/deployphp/deployer/blob/master/recipe/magento2.php#L430)

Adds additional files and dirs to the list of shared files and dirs.




### artifact:prepare
[Source](https://github.com/deployphp/deployer/blob/master/recipe/magento2.php#L437)

Prepares an artifact on the target server.




This task is group task which contains next tasks:
* [deploy:info](/docs/recipe/deploy/info.md#deployinfo)
* [deploy:setup](/docs/recipe/deploy/setup.md#deploysetup)
* [deploy:lock](/docs/recipe/deploy/lock.md#deploylock)
* [deploy:release](/docs/recipe/deploy/release.md#deployrelease)
* [artifact:upload](/docs/recipe/magento2.md#artifactupload)
* [artifact:extract](/docs/recipe/magento2.md#artifactextract)
* [deploy:additional-shared](/docs/recipe/magento2.md#deployadditional-shared)
* [deploy:shared](/docs/recipe/deploy/shared.md#deployshared)
* [deploy:writable](/docs/recipe/deploy/writable.md#deploywritable)


### artifact:finish
[Source](https://github.com/deployphp/deployer/blob/master/recipe/magento2.php#L450)

Executes the tasks after artifact is released.




This task is group task which contains next tasks:
* [magento:cache:flush](/docs/recipe/magento2.md#magentocacheflush)
* [cachetool:clear:opcache](/docs/contrib/cachetool.md#cachetoolclearopcache)
* [deploy:cleanup](/docs/recipe/deploy/cleanup.md#deploycleanup)
* [deploy:unlock](/docs/recipe/deploy/lock.md#deployunlock)


### artifact:deploy
[Source](https://github.com/deployphp/deployer/blob/master/recipe/magento2.php#L458)

Actually releases the artifact deployment.




This task is group task which contains next tasks:
* [artifact:prepare](/docs/recipe/magento2.md#artifactprepare)
* [magento:maintenance:enable-if-needed](/docs/recipe/magento2.md#magentomaintenanceenable-if-needed)
* [magento:config:import](/docs/recipe/magento2.md#magentoconfigimport)
* [magento:upgrade:db](/docs/recipe/magento2.md#magentoupgradedb)
* [magento:maintenance:disable](/docs/recipe/magento2.md#magentomaintenancedisable)
* [deploy:symlink](/docs/recipe/deploy/symlink.md#deploysymlink)
* [artifact:finish](/docs/recipe/magento2.md#artifactfinish)


