# Drupal stack changelog

This is the changelog for Drupal stack deployed via Wodby, for docker4drupal changes see [GitHub releases page](https://github.com/wodby/docker4drupal/releases).

!!! caution "Changes between your version and the latest"
    Changes and upgrade instructions are relative to a preceding version, e.g. if you're upgrading from version 5.2.0 to 5.2.2 you should also look up version 5.2.1 changes.

!!! caution "MariaDB updates"
    - We strongly recommend to backup your database before upgrading your application stack if the new version contains MariaDB updates 
    - During MariaDB upgrade we run `mysql-check` and `mysql-upgrade`. This operation may take a few minutes for big databases

!!! caution "MariaDB 10.1"
    If your app has MariaDB 10.1 service and the app was created (or its stack was upgraded) after June 2018, you're actually running MariaDB 10.2 (see https://twitter.com/wodbycloud/status/1206943424861102081 for more details).

## 5.4.14

- Vanilla Drupal 8.8.0, 7.68
- PHP:
  - Added PHP 7.4 (with the [exception](https://github.com/wodby/drupal-php/issues/71) for vanilla Drupal 7)
  - Updated extension: ast 1.0.5, xdebug 2.8.0, mcrypt 1.0.3, oauth 2.0.4
  - Added Kerberos and SSL support for IMAP extension https://github.com/wodby/drupal-php/issues/70
- MariaDB 10.4.11, 10.3.21, 10.2.30
- Solr 8.3.1
- Nginx:
  - `/.well-known` URIs excluded from denied hidden files location instead of explicitly allowed
  - Locations `wodby.yml` and `Makefile` are now forbidden
- Apache hidden files, directories, `wodby.yml`, `Makefile` and certain extension are now forbidden 
- XHProf viewer updated to 2.1.3 (updated PECL extension) https://github.com/wodby/xhprof/issues/1
- Bugfix: broken webgrind image tag
- Adminer, webgrind and xhprof rebuilt against updated PHP image    
           
## 5.4.13

- Vanilla Drupal 8.7.10
- Drupal launcher 1.9.4
- PHP 7.3.12, 7.2.25
- Nginx:
    - Updated to 1.17.6
    - Brotli compression level set to 1 https://github.com/wodby/nginx/issues/40
- MariaDB 10.4.10, 10.3.20, 10.2.29, 10.1.43
- Added liveness checks for Varnish, Nginx and Apache
- Improved performance for Apache and Nginx readiness checks
- Solr 8.3.0
- Memcached 1.5.20
- Adminer 4.7.5
- Redis 5.0.7
- Adminer, xhprof, webgrind rebased to PHP 7.2

## 5.4.12

- PHP:
  - ❗️Security updates: 7.1.33, 7.2.24, 7.3.11
  - Updated PECL extensions: mongodb 1.6.0, grpc 1.23.1, apcu 5.1.18, memcached 3.1.4
  - Bugfix: `$DRUPAL8_REVERSE_PROXY_ADDRESSES` had no effect https://github.com/wodby/drupal-php/issues/69
  - `$DRUPAL8_REVERSE_PROXY_ADDRESSES` renamed to `$DRUPAL_REVERSE_PROXY_ADDRESSES`
  - Reverse proxy setting support added to Drupal 7
- Nginx:
  - Updated to 1.17.5
  - Added brotli compression extension (enabled by default in addition to gzip) https://github.com/wodby/nginx/issues/37
- Varnish:
  - Varnish updated to 6.0.5
  - Varnish modules now installed from branch 6.0 https://github.com/varnish/varnish-modules/issues/144
  - Bugfix: private files access restricted with enabled static files cache https://github.com/wodby/varnish/issues/24
- Adminer 4.7.4
- Alpine Linux updated to 3.10.3 for most images
- XHProf viewer, adminer, webgrind rebuilt against latest PHP image

## 5.4.11

- Vanilla Drupal 8.7.8
- PHP:
  - Updated to 7.3.10, 7.2.23
  - Drupal console launcher 1.9.3
- Nginx 1.17.4
- MariaDB 10.4.8, 10.3.18, 10.2.27
- Memcached 1.5.19
- Redis 3.1.3
- Alpine updated to 3.10.2 for Solr images
- Webgrind, adminer and xhprof viewer rebuilt against latest PHP image

## 5.4.10

- Vanilla Drupal updated to 8.7.7
- PHP:
    - Security updates: 7.3.9, 7.2.22, 7.1.32
    - New Relic extension log level set to `warning` by default
    - Drupal console launcher updated to 1.9.2
- Varnish security update 6.0.4
- Nginx 1.17.3, 1.16.1
- Apache 2.4.41
- Memcached 1.5.17
- Adminer 4.7.3

## 5.4.9

- Vanilla Drupal updated to 8.7.6
- PHP:
    - ❗️Security updates: 7.3.8, 7.2.21, 7.1.31
    - Updated PECL extensions: rdkafka 3.1.2, mongo 1.5.5
    - NewRelic extension: 
        - Added additional options https://github.com/wodby/php/issues/85
        - Default logging destination changed to `stderr`
        - The extension no longer loaded unless `$PHP_NEWRELIC_ENABLED` specified 
    - Drupal console launcher updated to 1.9.1
    - Bugfix: crond service missed preloaded iconv library
- MariaDB:
    - ❗️Security updates: 10.4.7, 10.3.17, 10.2.26, 10.1.41
    - Version 10.4 temporary has no PAM https://github.com/wodby/mariadb/issues/20
    - `open_files_limit` is now configurable https://github.com/wodby/mariadb/issues/18
- Nginx:
    - Updated to 1.17.2
    - Added default location `humans.txt` https://github.com/wodby/nginx/pull/35
- Solr:
    - Updated to 8.2.0
    - We now run upgrade action that removes `default` core if it has a broken config set (so it can be automatically recreated). NOT applicable to EOL versions (6.4, 7.1, 7.2, 7.3, 7.4)
- Adminer, Webgrind, Xhprof viewer rebuilt against the updated base image
- Alpine Linux updated to 3.10 for Varnish, OpenSMTPD and MariaDB (except 10.1)

## 5.4.8

- Vanilla Drupal updated to 8.7.5
- PHP:
    - Bugfix updates to 7.3.7, 7.2.20
    - Event extension updated to 2.5.3
    - Drupal console launcher updated to 1.9.0
- MariaDB:
    - Updated to 10.3.16, 10.2.25
    - Added new major version 10.4
    - You can now add plugins via `$MARIADB_PLUGIN_LOAD` https://github.com/wodby/mariadb/issues/15
    - Added linux-pam library for PAM auth 
    - Added `$MYSQL_CONNECT_TIMEOUT` https://github.com/wodby/mariadb/issues/17
- Varnish:
    - `webp` added to the list of default static file extensions
    - PageSpeed downstream caching:
        - PS-CapabilityList now set to "fully general optimizations only" only if static files cache enabled
        - Bugfix: caching for `text/html` was disabled
- Solr:
    - Solr updated to 7.7.2
    - Added new Solr 8.1 variant with search_api_solr 8.x-3.x configset https://github.com/wodby/solr/issues/8 
    - Bugfix: `$SOLR_HEAP` did not have any effect
    - Images rebased to wodby/base-solr (see README at https://github.com/wodby/base-solr)        
- Drupal-node service had a `$NODE_PORT` environment variable with a wrong value that could break its startup
- Nginx updated to 1.17.1
- Webgrind updated to 1.6.1
- Adminer updated to 4.7.2
- Adminer, Webgrind, Xhprof viewer rebuilt against the updated base image
- Alpine Linux (base OS) updated to 3.10.1 for most of the images

## 5.4.7

- Vanilla Drupal updated to 8.7.2
- PHP:
    - ❗️Security updates: 7.3.6, 7.2.19, 7.1.30
    - Updated extensions: 
        - ast 1.0.1
        - ds 1.2.9
        - event 2.5.1
        - grpc 1.20.0
        - igbinary 3.0.1
        - redis 4.3.0
        - tideways xhprof 5.0-beta3
- Nginx: added new version 1.17
- MariaDB:
  - Updated to 10.3.15
  - `log_warnings` now configurable, set to `2` by default for all versions
- Varnish now supports modpagespeed downstream caching https://github.com/wodby/varnish
- Memcached updated to 1.5.16
- Redis updated to 5.0.5
- Adminer, Webgrind, Xhprof viewer rebuilt against updated base image

## 5.4.6

- Vanilla Drupal updated to 8.7.1, 7.67
- PHP:
    - ❗️Security updates: 7.3.5, 7.2.18, 7.1.29
    - Packages updates: imagemagick 7.0.8.44 (PHP 7.x only), libpng 1.6.37, libxslt 1.1.33
    - Extensions update: event 2.5.0, xdebug 2.7.2, imagick 3.4.4, rdkafka 3.1.0
- Nginx:
    - Added new latest version 1.16
    - Updated to 1.15.12
    - Pagespeed version no longer shown in headers https://github.com/wodby/nginx/issues/32
- MariaDB updates: 10.2.24, 10.1.40
- Solr updated to 6.6.6
- Memcached updated to 1.5.14
- Alpine Linux updated to 3.9.4 (only for images based on 3.9)

## 5.4.5

Bugfix: composer install/update executed from post-deployment scripts may sometimes stuck.

## 5.4.4

- Vanilla Drupal updates: 8.6.14
- PHP:
  - ❗️Security updates: 7.3.4, 7.2.17, 7.1.28
  - Xdebug extension updated to 2.7.1
- Nginx:
  - Updated to 1.15.11
  - Default static files expiration increased to 1 year https://github.com/wodby/nginx/pull/30
- MariaDB updated to 10.3.14
- ❗️Apache security update: 2.4.39
- Alpine Linux updated to 3.9.3 for PHP (except 5.x), Varnish, MariaDB (except 10.1), Redis, Memcached, Solr, OpenSMTPD
- Webgrind, Xhprof viewer and admirer rebuilt against updated PHP image

## 5.4.3

- Vanilla Drupal updates: 8.6.13, 7.65
- PHP:
    - ❗️Security updates: 7.3.3, 7.2.16, 7.1.27
    - Xdebug updated to 2.7.0 (now PHP 7.3 supported)
    - Global composer package `hirak/prestissimo` removed https://github.com/wodby/docker4drupal/issues/365
- Nginx:
    - Updated to 1.15.10
    - Make extra config be able to work without defaults https://github.com/wodby/nginx/pull/27
- Solr: 
    - Versions 5.4, 6.4, 7.1-7.4 no longer supported (marked as EOL)
    - Versions 7.6, 7.7 added (and 5.5 for Drupal 7)
    - Added new search_api_solr config sets (Drupal 8 default config set updated to `8.x-2.7`)    
    - Bugfix: attachments indexation did not work in Drupal 7 https://github.com/wodby/solr/issues/5
- MariaDB updated to 10.2.23
- Redis updates: 5.0.4, 4.0.14
- Varnish bugfix: GeoIP did not work (now uses `X-Real-IP` header instead of `X-Forwarded-For`) https://github.com/wodby/varnish/pull/18
- XHProf, Webgrind, Adminer rebuilt against the latest PHP image
- Apache base image changed from `wodby/httpd` to `httpd`
- Alpine upgraded to 3.9.2 for all alpine-based updated images

## 5.4.2

- Vanilla Drupal updates: 8.6.10, 7.64
- PHP:
  - Rebased to Alpine 3.9: runtime packages updated, switched from LibreSSL to OpenSSL 1.1
  - PHP updates: 7.3.2, 7.2.15
  - Introduced additional env vars for NewRelic runtime configuration: `$PHP_NEWRELIC_BROWSER_MONITORING_AUTO_INSTRUMENT`, `$PHP_NEWRELIC_GUZZLE_ENABLED`
  - WebP support added to gd (PHP 7.x only) https://github.com/wodby/php/issues/68
  - MariaDB client updated to 10.3.13/10.2.22
  - Extensions update: igbinary 3.0.0,  apcu 5.1.17
  - Bugfix: `$PATH` was missing in SSH environment variables
  - `$SSHD_PERMIT_USER_ENV` default values changed to `yes`
- Nginx:
  - Patch update: 1.15.9
  - `.map` added to the list of default static files extensions (`$NGINX_STATIC_EXT_REGEX`)
  - Bugfix: `$NGINX_LOG_FORMAT_OVERRIDE` had no effect
- Varnish:
  - Patch updates: 4.1.11, 6.0.3
  - Bugfix: cookie always stripped for static files requests
- MariaDB:
  - Patch updates: 10.3.13, 10.2.22, 10.1.38
  - MariaDB 10.2, 10.3 rebased to Alpine 3.9 and OpenSSL 1.1
  - `innodb_force_recovery` and `innodb_purge_threads` are now configurable via env vars
  - Added `mysql-check` orchestration action and now run with every MariaDB deployment to detect potential issues
- `mod_include` added to Apache https://github.com/wodby/apache/issues/6
- Adminer updated to 4.7.1
- Redis updated to 4.0.13
- XHProf, Webgrind, Adminer rebuilt against the latest PHP image

## 5.4.1

- Alpine Linux for the services listed below updated to 3.8.2
- ❕Vanilla Drupal security updates: 8.6.7, 7.63
- PHP:
    - ❕️Security updates: 7.3.1, 7.2.14, 7.1.26, 5.6.40
    - GeoIP extension removed https://github.com/wodby/php/issues/59
    - Updated libraries: ImageMagic (7.0.7.39), libjpeg-turbo, MariaDB client (10.2.19)
    - Updated php extensions: AMQP 1.9.4, APCu 5.1.16, Memcached 3.1.3, GRPC 1.17.0, event 2.4.3 
    - The following extensions now added to PHP 7.3: NewRelic, Blackfire, AMQP, Memcached
    - `/var/www/html/bin` added to `$PATH` https://github.com/wodby/php/issues/60
    - Bugfix: event extension could be not be disabled
- Apache:
    - ❕Security update 2.4.38
    - SSL module temporary disabled due to build failures https://github.com/wodby/apache/issues/5    
- Nginx:
    - Patch update: 1.15.8
    - GeoIP module deleted https://github.com/wodby/php/issues/59
    - PageSpeed module now respects `X-Forwarded-Proto` by default
    - Bugfix: dynamic modules image filter and xslt could not be enabled
    - Bugfix: `.well-known/*.txt` were not accessible https://github.com/wodby/nginx/issues/17
- Varnish:
    - We no longer set `X-Real-IP` header in Varnish
    - Bugfix: unrestricted cache purge from internal network did not work https://github.com/wodby/varnish/issues/14
- MariaDB updates: 10.2.21, 10.3.12, ~~10.1.37~~ https://github.com/wodby/mariadb/issues/10
- Webgrind, XHProf, Adminer rebuilt against the latest PHP image    

## 5.4.0

### Changes since 5.3.4

* Vanilla Drupal updated to 8.6.4
* PHP:
    * ⭐️Added PHP 7.3 ([some extensions not yet supported](https://github.com/wodby/php/issues?q=is%3Aissue+is%3Aopen+label%3A%22PHP+7.3%22))
    * Patch updates: 7.2.13, 7.1.25, 5.6.39
    * Update extensions: yaml 2.0.4, redis 4.2.0, apcu 5.1.14
    * ImageMagick library now comes with disabled openmp
    * Bugfix: `/home/www-data` owned by wodby https://github.com/wodby/drupal-php/issues/62
* Varnish:
    * ⭐️ Varnish 6.0 added
    * We now compile varnish from sources, Alpine Linux updated to 3.8
    * Patch updates: 4.1.10
    * GeoIP module added and imported by default
    * Added [9 additional modules](https://github.com/wodby/varnish#installed-modules), not imported by default
    * ⭐️ We now [detect country code](https://github.com/wodby/varnish#geoip) and [currency (USD, EUR)](https://github.com/wodby/varnish#currency) and pass it to backend in headers, you can optionally uniquify cache per country or currency
    * ⭐️ You can now personify cache additionally by setting cookies starting with [`VCKEY-`](https://github.com/wodby/varnish#cache-personification)
    * `fbclid` added to stripped query params
    * Adjusted order of included files https://github.com/wodby/varnish/pull/7
    * Bugfix: duplications in `X-Forwarded-For`
    * Bugfix: Bugfix: Drupal private files auth did not work https://github.com/wodby/varnish/pull/7
    * Deprecated environment variables (listed in [5.2.0](#520)) no longer supported
* Nginx:
    * Patch updates: 1.15.7, 1.14.2
    * ⭐️  Added [ModSecurity with OWASP CRS](https://github.com/wodby/nginx#modsecurity) (disabled by default) https://github.com/wodby/nginx/pull/13, https://github.com/wodby/nginx/pull/14
    * PageSpeed is now dynamic module, [disabled by default](https://github.com/wodby/nginx#pagespeed)
    * `$NGINX_FASTCGI_INDEX` added to separate from index file https://github.com/wodby/nginx/pull/11
    * `index.html` added to index file for PHP-based presets https://github.com/wodby/nginx/pull/11
    * Bugfix: broken links for Drupal private files containing ampersand https://github.com/wodby/nginx/pull/15
* Solr:
    * Added version 7.5
    * Drupal 7 now supports Solr 6/7 
    * search_api_solr version used for config sets now shown in titles and have been updated:
        * Drupal 7: 7.x-1.14 
        * Drupal 8: 8.x-1.2 for Solr 5, 8.x-2.1 for others
* MariaDB:    
    * Patch updates: 10.3.11, 10.2.19
    * We now run `mysql_upgrade` automatically on stack upgrades      
    * Import action now allows `*.mysql` files      
* Patch updates: 
    * Redis: 5.0.3, 4.0.12
    * Memcached: 1.5.12
    * Node: 10.14.2, 8.14.0, 6.15.1
    * Elasticsearch/Kibana: 5.6.14
* Adminer updated to 4.7.0  
* Webgrind, adminer and xhprof rebuilt against the latest PHP image
* ~~Apache patch update: 2.4.37~~ https://github.com/wodby/apache/issues/5
* ~~MariaDB patch update: 10.1.37~~ https://github.com/wodby/mariadb/issues/10

### Update instructions

* If you used [deprecated environment variables](#520) in Varnish updated them to the new version 
* If you used Nginx pagespeed module, add `$NGINX_PAGESPEED_ENABLED=1`, if you had `$NGINX_PAGESPEED=on` you can delete it since it's `on` by default
* If you use Solr you might need to update search_api_solr module since we fetch schema from the update version of the module   

## 5.3.4

* Bugfix: Nginx did not convert deprecated environment variables to new

## 5.3.3

* Added new profiler service [xhprof viewer](https://wodby.com/docs/stacks/drupal/containers/#xhprof-viewer) for analysis and graphical review of [xhprof traces](https://wodby.com/docs/stacks/drupal/containers/#xhprof)
* Added Redis 5
* Vanilla Drupal patch updates: 8.6.3, 7.61
* PHP:
    * Patch updates: 7.2.12, 7.1.24
    * Added [event](https://pecl.php.net/package/event) extension
    * You can now disable extensions via `$PHP_EXTENSIONS_DISABLE` (separated by comma)
    * Extensions updates: igbinary 2.0.8, ast 1.0.0, grpc 1.16.0
    * ImageMagick downgraded to 7.0.7.32 with enabled openmp 
    * Bugfix: tideways xhprof extension could not be enabled
* Nginx:
    * Patch updates: 1.15.6, 1.14.1
    * Nginx now uses real IP set from Edge
    * Default security headers duplicated https://github.com/wodby/docker4drupal/issues/336
    * Added `$NGINX_STATIC_404_TRY_INDEX`, when set Nginx redirects 404 static files request to index file (required for stage_file_proxy module) https://github.com/wodby/docker4drupal/issues/270
* Memcached patch update 1.5.12    
* MariaDB 10.0 `innodb_default_row_format` now set to `dynamic` by default
* Webgrind and Adminer rebuilt against the latest PHP image
* ~~Apache patch update~~ https://github.com/wodby/apache/issues/5
* ~~MariaDB 10.0 patch update~~ https://github.com/wodby/mariadb/issues/10

## 5.3.2

* ❗️Vanilla Drupal core security update: 8.6.2, 7.60
* Memcached patch update: 1.5.11    
    
## 5.3.1

* PHP:
    * Patch updates: 7.1.23, 7.2.11
    * uuid pecl extension added https://github.com/wodby/php/issues/43
    * oauth extension patch update: 2.0.3
    * PHP env vars moved from FPM config to the general PHP config
    * Bugfix: invalid Drupal 8 sync directory permissions
* Nginx:
    * Patch update 1.15.5
    * real_ip params are now configurable https://github.com/wodby/nginx/issues/9
* Node:
    * Minor updates: 10.12, 8.12
    * Directory `/usr/src/app/node_modules/.bin` added to `$PATH`
* MariaDB patch update 10.3.10
* Adminer:
    * Bugfix: some `$PHP_` env vars were ignored
    * Default memory limit set to 512M
* Adminer and Webgrind rebuilt against the latest PHP image

## 5.3.0

### Changes 

* PHP:
    * Rebased to Alpine 3.8 with updated runtime libraries
    * ❗️PHP 7.0 will no longer be maintained ([see why?](https://github.com/wodby/php/issues/40))
    * Argon2 password hash supported added to PHP 7.2
    * MongoDB extension updated to 1.5.3
    * Bugfix: segfault in PHP's `mail` function when sent to multiple recipients ([busybox bug](http://lists.busybox.net/pipermail/busybox/2017-August/085798.html))
    * Bugfix: xhprof tideways extension enabled twice
* MariaDB:
    * Patch update: 10.2.18
    * Improved performance for backup orchestration action
* Apache:
    * Patch update: 2.4.35
    * Option `Indexes` now disabled by default, can be enabled via `$APACHE_INDEXES_ENABLED`
* Adminer:
    * Added the default list of plugins, enabled via `$ADMINER_PLUGINS`
    * You can now change Adminer design via `$ADMINER_DESIGN` z   
    * Updated to the latest stable PHP image
* Varnish:
    * Bugfix: batch pages did not work with Varnish
    * `has_js` cookie no longer stripped
    * Default response headers max length doubled to `16k`
* Nginx patch update: 1.15.4
* Webgrind image updated to the latest stable PHP image

### Upgrade instructions 

* Switch your application's PHP service implementation from 7.0 to 7.1

## 5.2.5

* PHP:
    * Libraries update: ImageMagick 7.0.8.11, FreeType 2.9.1
    * OpenMP disabled in ImageMagick due to stability issues
    * Bugfix: xhprof (tideways) extension could not be enabled  

## 5.2.4

* PHP 
    * ❗️Security updates: 7.2.10, 7.1.22, 7.0.32, 5.6.38
    * Added `$PHP_PHAR_` env vars for Phar runtime configuration
    * Updated PHP extensions:
        * patch: apcu 5.1.12, ds 1.2.6, igbinary 2.0.7, xdebug 2.6.0
        * minor: mongodb 1.5.2, grpc 1.15.0
        * major: redis 4.1.1

## 5.2.3

* Nginx:
    * New 50x error page, use `$NGINX_ERROR_MESSAGE_50x` to add a custom message
    * Env vars `$NGINX_ERROR_PAGE_40x` replaced to `$NGINX_ERROR_40x_URI`

## 5.2.2

* Vanilla Drupal updated to 8.6.1
* PHP extension XHProf (tideways) updated to 5.0-beta2
* Nginx:
    * Nginx no longer hides 50x errors by default on non-prod instances
    * Setting `$NGINX_VHOST_PRESET` to empty value now disables usage of any presets
    * New `$NGINX_VHOST_NO_DEFAULTS` to disable default rules for virtual host
    * New default 50x error page, new `$NGINX_ERROR_MESSAGE_50x` to add a message on this page
* MariaDB patch update: 10.1.36
* Solr patch update: 6.6.5
* Varnish bugfix: flush action from dashboard failed
* Adminer and Webgrind rebased to the latest stable php image

## 5.2.1

Do not add trailing slashes for non-directory requests

## 5.2.0

### Changes 

* Vanilla Drupal core updated to 8.5.6
* PHP:
    * Patch updates: 7.2.9, 7.1.21, 7.0.31, 5.6.37
    * `/var/www/html/vendor/bin` added to `$PATH`
    * Added [rdkafka](https://pecl.php.net/package/rdkafka) extension
    * Added `~/.bash_profile` for `wodby` user
    * SSH key and crontab can now be added via bind mounts
    * PostgreSQL lib updated to 10.5
    * Bugfix: Nice shell prompt is missing when connecting via `drush ssh`
    * Bugfix: PHP 5.6 missed GMP library
    * Bugfix: drush could not be found when connection via `drush ssh`  
    * Bugfix: incorrect owner on wodby's `~/.shrc`, `~/.bashrc`
    * Libraries and extensions versions moved out from env vars
* Nginx:
    * Image `wodby/drupal-nginx` has been replaced with [`wodby/nginx`](https://github.com/wodby/nginx) with [`$NGINX_VHOST_PRESET=drupal`](https://github.com/wodby/nginx/#virtual-hosts-presets)
    * Nginx updated to 1.15.3
    * Nginx image rebased to Alpine Linux 3.8
    * Use of `$NGINX_LOG_FORMAT_OVERRIDE` now prevails use of `$NGINX_LOG_FORMAT_SHOW_REAL_IP`
    * Drupal's preset env vars renamed (old names still supported):
        ```
        NGINX_STATIC_CONTENT_* => NGINX_STATIC_*
        NGINX_ALLOW_XML_ENDPOINTS => NGINX_DRUPAL_ALLOW_XML_ENDPOINTS
        NGINX_XMLRPC_SERVER_NAME => NGINX_DRUPAL_XMLRPC_SERVER_NAME
        NGINX_DRUPAL_TRACK_UPLOADS => NGINX_TRACK_UPLOADS
        ```
    * New env vars `$NGINX_ERROR_PAGE_` to customize 403/404 pages location
    * Extended list of static files extensions
    * New env vars `$NGINX_STATIC_` to control settings for handling static content
    * New env var `$NGINX_ALLOW_ACCESS_HIDDEN_FILES` to control access to files starting with a dot
    * Added pseudo-streaming server-side for `.flv`, `.mp4`, `.mov`, `.m4a` files
    * Env vars `$NGINX_STATIC_MP4_` for mp4 streaming configuration
    * Updated default values for `open_file_cache` settings
    * Default expires for static content set to `7d` by default
    * Bugfix: overriding log format via `$NGINX_LOG_FORMAT_OVERRIDE` produced an error
* Apache:
    * Image `wodby/php-apache` has been replaced with [`wodby/apache`](https://github.com/wodby/apache) with `$APACHE_VHOST_PRESET=php`
    * Env var `$APACHE_SERVER_ROOT` renamed to `$APACHE_DOCUMENT_ROOT` (old name still supported)
    * MPM modules are now shared and can be changed (event is still the default)
* MariaDB:
    * MariaDB patch updates: 10.3.9, 10.2.17, 10.1.35
    * Image rebased to Alpine Linux 3.8
    * Backup action performance improvement: no intermediate file created
    * `ionice` no longer used in orchestration actions 
    * Bugfix: triggers duplicated during db dump
    * Bugfix: no privileges before import could cause failure
* Solr:
    * Image `wodby/drupal-solr` now replaced with `wodby/solr` and `$SOLR_DEFAULT_CONFIG_SET`, see [versions matrix](https://github.com/wodby/solr#drupal-search-api-solr) 
    * New Solr versions added: 7.4, 7.3 
    * Dropped versions 6.3, 6.5, 7.0 
    * Config sets and `solr.xml` now symlinked to volume, existing cores won't be affected
    * Core directory get deleted when you delete a core via orchestration actions
    * Bugfix: duplicated `configsets/configsets` directory
* Varnish:
    * Image `wodby/drupal-varnish` now replaced with `wodby/varnish` and `$VARNISH_CONFIG_PRESET=drupal`
    * External purge now always restricted by purge key
    * Unrestricted purge from the internal network can be optionally enabled (enabled by default)
    * Cache for mobile devices can now be separated or disabled entirely
    * Big files (by default >10M) won't be cached by default
    * Static files cache disabled by default for all presets
    * All varnish-related headers now start with `X-VC-`, e.g. `X-Varnish-Cache` is now `X-VC-Cache`
    * Secondary storage can now be defined for all presets
    * List of static files extensions expanded
    * Analytics/marketing cookies and query params stripped, configurable
    * New env vars to optionally preserve all cookies and query params
    * Query params can be ignored to cache URLs as a single object
    * Purge method now can be changed to regex and exact (respects query params)
    * Hashes and trailing ? stripped from URL before passing to a backend
    * All AJAX requests not cached
    * Error pages 404 and >500 not cached with a configurable grace period
    * Env vars changed for presets (old => new), old variant still supported:
      ```
       VARNISH_EXCLUDE_URLS => VARNISH_DRUPAL_EXCLUDE_URLS
       VARNISH_PRESERVED_COOKIES => VARNISH_DRUPAL_PRESERVED_COOKIES
       ```
    * Friendly varnish error message by default
* Memcached:
    * Memcached returned as cache storage service option for Drupal 8/7
    * Memcached patch update: 1.5.10
* OpenSMTPD patch update: 6.0.3

### Upgrade instructions

* Nginx: if you overridden a virtual host config (via `$NGINX_CONF_INCLUDE`) you'll have to update it from the original `/etc/nginx/conf.d/vhost.conf` and re-apply your changes again
* If you used somewhere Varnish's header `X-Varnish-Cache`, update it to `X-VC-Cache`

## 5.1.0

### Changes

* Drupal
    * Vanilla Drupal core updated to 8.5.4
    * We now set `$settings['reverse_proxy_addresses']` and `$settings['reverse_proxy']` in `wodby.settings.php` file. You can also add additional proxy addresses via env var `DRUPAL_REVERSE_PROXY_ADDRESSES`
* PHP
    * ⭐️ Added new PHP 7.2
    * Added php tidy extension
    * Added tideways xhprof extension https://github.com/wodby/drupal-php#49 (disabled by default)
    * `auto_prepend_file` and `auto_append_file` are now configurable
    * Updated PHP extensions: GRPC 1.12.0, igbinary 2.0.6, mongodb 1.4.4
* MariaDB:
    * New version 10.3 added (10.3.7)
    * MariaDB updates: 10.2.15, 10.1.34
    * `optimizer_prune_level` and `optimizer_search_depth` are now configurable https://github.com/wodby/mariadb/issues/4
    * ⭐️ Default `innodb_buffer_pool_size` set to `128M` that should significantly decrease memory usage by MariaDB container. See [MariaDB stack documentation](../mariadb/index.md) to learn how to calculate the optimal size of `innodb_buffer_pool_size` for your application
    * Default `innodb_buffer_pool_instances` set to `1`
* Nginx:
    * Added new Nginx 1.15, dropped legacy Nginx 1.12
    * ⭐️ Added [mog_pagespeed](https://www.modpagespeed.com/) module. Disabled by default, to enable add `NGINX_PAGESPEED=on` to nginx service
    * Added new modules:
    ```
    http_image_filter_module
    http_slice_module
    http_xslt_module
    stream_geoip_module
    stream_realip_module
    stream_ssl_preread_module
    ```
* Varnish
    * Environment variable `VARNISHD_STORAGE_SIZE` has been dropped, we no longer add a predefined secondary storage. You can now add your custom secondary storage via `VARNISHD_SECONDARY_STORAGE` https://github.com/wodby/varnish/pull/4
    * ❗Static files no longer cached unless you set `VARNISH_CACHE_STATIC_FILES` https://github.com/wodby/drupal-varnish/pull/4
    * Added `VARNISH_SECONDARY_STORAGE_CONDITION` to specify the condition when to use secondary storage https://github.com/wodby/drupal-varnish/pull/3
* Webgrind: error reporting now exludes strict and deprecated errors, rebased to latest PHP 7.1 image

### Upgrade instructions

* Make sure the new default size of `innodb_buffer_pool_instances` (128M) is enough for your project, see [MariaDB stack documentation](../mariadb/index.md) to learn how to calculate the optimal size of `innodb_buffer_pool_size` for your application

## 5.0.7

* PHP:
    * **Security update**: 7.2.5, 7.1.17, 7.0.30
    * New php extensions added: [GMP](http://php.net/manual/en/book.gmp.php) and [igbinary](https://github.com/igbinary/igbinary/)
    * APCu extension updated to 5.0.11 for PHP 7.x
    * APCu serialized is now configurable with `$PHP_APCU_SERIALIZER`
    * Shell prompt in PHP containers now shows current user, application name and instance name
    * Added new helper script [`files_chown`](https://github.com/wodby/php#users-and-permissions)
    * Bugfix: iconv implementation missing [wodby/php#25](https://github.com/wodby/php/issues/25)
* Vanilla Drupal:
    * **Security update**: 8.5.3
    * Bugfix: drush cache permission issues [wodby/drupal#261](https://github.com/wodby/docker4drupal/issues/261)
* Drupal node container rebased to [`wodby/node`](https://github.com/wodby/node) with freezed node version
* Added Nginx 1.14, patch update for 1.13
* Nginx's `underscores_in_headers` is now configurable via `$NGINX_UNDERSCORES_IN_HEADERS`

## 5.0.6

* PHP [log errors max length](http://php.net/manual/en/errorfunc.configuration.php#ini.log-errors-max-len) set to unlimited
* Bugfix: PHP errors didn't show up in the container output
* Bugfix: `APACHE_LIMITED_ACCESS` support from 5.0.4 release was missing

## 5.0.5

* PHP:
    * Updated to 7.2.4, 7.1.16, 7.0.35 (**security update**)
    * Added [jpegoptim](https://github.com/tjko/jpegoptim)

## 5.0.4

* Vanilla Drupal updated to 8.5.1 (**security update**)
* Apache:
    * Updated to 2.4.33 (**security update**)
    * New environment variable `APACHE_LIMITED_ACCESS` to remove `Require all granted` when you need to limit access by IP

## 5.0.3

* PHP:
    * PHP extension grpc updated to 1.10.0
    * Added environment variables for PHP session runtime configuration
    * Improved error reporting and progress messages for public files directory init
    * Bugfix: global drush used instead of drush launcher
* Solr:
    * New 7.2 version
    * Patch update: 6.6.3
    * Solr 7.x config sources updated to search_api_solr `8.x-2.0-alpha3`
* Nginx updated to 1.13.10
* You can now override apache config with `APACHE_INCLUDE_CONF`

## 5.0.2

* Cron now runs from `www-data` user instead of `wodby`
* Vanilla Drupal updated to 8.5.0
* Drupal console launcher updated to 1.7.0 and freezed
* [`files_chmod`](https://github.com/wodby/php#users-and-permissions) script now sets permissions with execution allowed only for directories

## 5.0.1

* PHP updated to 7.2.3, 7.1.15, 7.0.28 (security updates)
* Global drush freezed to 8.x

## 5.0.0

### Changes

* All containers now have [resources request](../config.md#resources) as listed [here in Resources column](https://wodby.com/stacks/drupal/docs/containers/), in addition, crond has CPU limit
* PHP:
    * Container default user has been changed to `wodby` (uid/gid 1000), see https://github.com/wodby/php#users-and-permissions for more details
    * PHP updated to 7.1.14, 7.0.27, 5.6.33 (security updates)
    * Rebased to Alpine Linux 3.7
    * Now when your upgrade stack with a new version of vanilla Drupal, your source code will be updated
    * You can [monitor PHP with NewRelic APM](https://wodby.com/stacks/drupal/docs/containers/php/#newrelic-apm-monitoring)
    * `allow_url_fopen` and `default_socket_timeout` is now configurable
    * New php extensions added: newrelic, grpc, ds
    * Global drush updated to 9.x for PHP 7.x
    * Drush launcher updated to 0.5.1
    * Deprecated environment variables dropped (listed in [4.4.0 changes](#440))
    * Added postgresql client bins (pg_dump, pg_restore, ...)
    * Added redis-cli
    * Updated php extensions: amqp 1.9.3, redis 3.1.6, mongodb 1.4.0, apcu 5.1.10
    * Environment variable `WODBY_DIR_FILES` replaced to `FILES_DIR`
    * Vanilla Drupal updated to 8.4.5
* MariaDB:
    * Updated to 10.1.31, 10.2.12
    * Rebased to Alpine Linux 3.7
* Nginx:
    * Updated to 1.13.9
    * Rebased to Alpine Linux 3.7
* Redis:
    * Updated to 4.0.8
    * Bugfix: redis 4 init could not disable THP on some servers
* OpenSMTPD:
    * Improved health check now runs smtp command
    * Messages queue is now persistent
* Varnish:
    * The following environment variables changed names (old version no longer supported), DEPRECATED > NEW:
    ```
    VARNISHD_THREAD_POOLS > VARNISHD_PARAM_THREAD_POOLS
    VARNISHD_THREAD_POOL_ADD_DELAY > VARNISHD_PARAM_THREAD_POOL_ADD_DELAY
    VARNISHD_THREAD_POOL_MIN > VARNISHD_PARAM_THREAD_POOL_MIN
    VARNISHD_THREAD_POOL_MAX > VARNISHD_PARAM_THREAD_POOL_MAX
    ```
    * Changed default values:
    ```
    VARNISHD_PARAM_THREAD_POOL_ADD_DELAY from 2 to 0.000
    VARNISHD_PARAM_THREAD_POOLS from 1 to 2
    VARNISHD_PARAM_THREAD_POOL_MAX from 1000 to 5000
    ```
    * Added additional env vars that control varnishd params (https://github.com/wodby/varnish/issues/1)
* Bugfix: auth issue in Apache (https://github.com/wodby/php-apache/issues/1)

### Upgrade instructions

* Make sure you don't use any of deprecated environment variables in PHP (listed in [4.4.0 changes](#440)) and Varnish (listed above) otherwise update their names
* If you used `WODBY_DIR_FILES` in your code replace it with `FILES_DIR`
* Make sure the default cron container 512M RAM limit is enough for your cron jobs, otherwise increase it manually from service configuration page

## 4.4.1

* Vanilla Drupal updated to 8.4.3
* Fixed missing tags for vanilla with PHP 7.0
* Restored MariaDB 10.1 `innodb_large_prefix` setting (enabled by default) removed in 4.4.0

## 4.4.0

### Changes

* PHP:
    * PHP updated to 7.1.12, 7.0.26
    * PHP extensions updated: memcached 3.0.4, ast 0.1.6
    * Added packages: tig, nano, tmux, less, libjpeg-turbo-utils
    * PHPunit deleted from image to avoid composer conflicts
    * Env vars naming fixes (old names still supported), old > new:
    ```
    PHP_APCU_ENABLE > PHP_APCU_ENABLED
    PHP_FPM_SLOWLOG_TIMEOUT > PHP_FPM_REQUEST_SLOWLOG_TIMEOUT
    PHP_FPM_MAX_CHILDREN > PHP_FPM_PM_MAX_CHILDREN
    PHP_FPM_START_SERVERS > PHP_FPM_PM_START_SERVERS
    PHP_FPM_MIN_SPARE_SERVERS > PHP_FPM_PM_MIN_SPARE_SERVERS
    PHP_FPM_MAX_SPARE_SERVERS > PHP_FPM_PM_MAX_SPARE_SERVERS
    PHP_FPM_MAX_REQUESTS > PHP_FPM_PM_MAX_REQUESTS
    PHP_FPM_STATUS_PATH > PHP_FPM_PM_STATUS_PATH
    ```
    * New `-dev` image tags (replacing `-debug`) for CI/CD (TBA)
    * Env var `WODBY_HOST_PRIMARY` value now contains host (instead of URL) as it should, `WODBY_URL_PRIMARY` has been added for the URL value. See environment variables section
    * Drush launcher added
    * Improved validation and error reporting for drush import
    * Git email and name now can be configured via environment variables
* Nginx:
    * Nginx updated to 1.13.7, 1.12.2
    * Fixed broken health check
    * New env var `NGINX_NO_DEFAULT_HEADERS` to hide default headers
    * We now show request real IP in access logs
    * New env var `NGINX_DRUPAL_FILE_PROXY_URL` to set up static files proxy
* MariaDB:
    * New MariaDB 10.2.11
    * MariaDB updated to 10.1.29
    * Shutdown grace period increased to 5 minutes
    * Deployment strategy no longer can be changed
    * Optimized default config (my.cnf) values
    * New environment variables to configure recovery options
    * Default user/group in a container now `mysql`
    * Backup action now runs with `nice` and `ionice` to prioritize CPU and I/O time for this process
    * Improved error reporting during import
* Solr:
    * New Solr versions 7.0.1 and 7.1.0 have been added
    * Solr versions updated and freezed: 6.6.2, 6.5.1, 6.4.2, 6.3.0, 5.5.5, 5.4.1
    * Config set source search_api_solr updated to 8.x-1.2
    * We now create a default solr core named `default` automatically if no cores found
* Redis:
    * Redis updated to 3.2.11, 4.0.2
    * Fixed init failure when there's no `/sys/kernel/mm/transparent_hugepage/enabled`
* Varnish:
    * Varnish updated to 4.1.9
    * Cache hash id now respects protocol (http/https)
* Global environment variables changes:
    * `$WODBY_APP_NAME` no longer contains instance machine name, only application machine name
    * `$WODBY_ENVIRONMENT_` variables have been deprecated and replaced with `$WODBY_INSTANCE_`
    * New variables `$WODBY_INSTANCE_UUID` and `$WODBY_APP_UUID`
* Apache updated to 2.4.29
* Vanilla Drupal updated to 8.4.2
* Health checks timeout increased to 30 seconds for all services
* OpenSMTPD now supports relay auth without password
* Files backup and mirroring actions now run with `nice` and `ionice` to prioritize CPU and I/O time for this process

### Upgrade instructions

* If you used `$WODBY_APP_NAME` update your code accordingly to the new value (machine name of the app)
* If you used `$WODBY_HOST_PRIMARY` (now contains host instead of URL) before you should replace it to `$WODBY_URL_PRIMARY`
* Upgrade downtime ~5 minutes

## 4.3.0

### Changes

* User `www-data` is now default in php, nginx and apache containers
* PHP:
    * PHP updated to 7.0.24, 7.1.10
    * Default vanilla Drupal updated to 8.4.0
    * Core extension pcntl is now enabled in PHP 7.x
    * Libressl added
    * Extensions update: redis 3.1.4, mongodb 1.3.0
    * New extension geoip
    * Default `post_max_size`, `upload_max_filesize` set to 32m
    * Optimized default opcache settings
    * New env var `PHP_MAX_FILE_UPLOADS` to control `max_file_uploads`
    * Bugfix: apcu (PHP 7.x) could cause segfaults in some cases
    * Bugfix: path to CA certificates specified in ldap config
    * Bugfix: files backup could fail when files changed during the process
    * Bugfix: missing quotes in `wodby.sites.php`
* Nginx:
    * Nginx updated to 1.13.5
    * Nginx config revamped: upstream name changed from `backend` to `php` and moved from `nginx.conf` to `drupal.conf`
    * Default `client_max_body_size` set to 32m
    * Bugfix: broken static files on Drupal's 8 update.php page
* Apache:
    * Apache updated to 2.4.28
    * Image has been replaced to generic [`wodby/php-apache`](https://github.com/wodby/php-apache)
* Varnish
    * Env vars for daemon launch params now have prefix `VARNISHD_` to avoid collisions
    * New env vars `VARNISH_EXCLUDE_URLS` and `VARNISH_STATIC_FILES` for customization
    * Default exclude URLs now consider language prefixes
* OpenSMTPD bugfix: health probes caused warning in logs

### Update instructions

* !!! If you forked `drupal.conf`, you must get the latest version from the source (`/etc/nginx/conf.d/drupal.conf`) and re-apply your changes. If you used `NGINX_SERVER_EXTRA_CONF_FILEPATH`, update usage of `backend` upstream to `php`
* Make sure that the new default value (32m) of php's `post_max_size`, `upload_max_filesize` and nginx's `client_max_body_size` is enough for you
* If you customized varnish launch params, update corresponding env vars prefix to `VARNISHD_`

## 4.2.1

* Improved backward compatibility, the following environment variables are now available from PHP-FPM

## 4.2.0

* PHP updated to 7.1.9, 7.0.23
* PHPUnit updated to 6.3
* New service Blackfire agent for profiling via blackfire.io, see [usage instructions](containers.md#blackfire)
* Environment varibles now cleared in PHP-FPM by default except for `WODBY_APP_NAME`, `WODBY_ENVIRONMENT_TYPE`, `WODBY_ENVIRONMENT_NAME`. You can disable it by adding environment variable `PHP_FPM_CLEAR_ENV` with `no` value to Drupal (PHP) container
* OpenSMTPD now supports relay without auth
* Bugfix: PHP-FPM health probes sometimes could fail

## 4.1.9

* Vanilla Drupal updated to 8.3.7
* MariaDB and its client updated to 10.1.26
* Athenapdf versions freeze to 2.10.0
* Bugfix: PHP-FPM health probes sometimes could fail

## 4.1.8

* Updated service: Redis (1.0.3)
* PHP containers now have health checks and can be upgraded without downtime
* We no longer support `sites/*/files` directories under version control
* Drush modules added: registry rebuild and patchfile
* PHP update: 7.1.8, 7.0.22
* Vanilla Drupal update: 8.3.6
* Nginx update: 1.13.4
* Experimental redis 4.0 added
* You can now enable PHP slowlog via environment variable `PHP_FPM_SLOWLOG_TIMEOUT`
* Improved Varnish health checks, now use varnishadm instead of curl
* Varnish bugfix: duplicated X-Forwarded-For header
* Varnish bugfix: unrestricted purge/ban, now allowed only from internal network

## 4.1.7

* New container [webgrind](https://github.com/jokkedk/webgrind) – Xdebug profiling web frontend
* Additional environment variables for Xdebug extension configuration including tracing and profiling
* PHP extensions update: ast 0.1.5; yaml 2.0.2
* Improvement: better handling of failed deployments
* Bugfix: some environment variable could be unavailble in SSH container

## 4.1.6

* Solr: fixed persistent data paths configuration

## 4.1.5

* New fast health-check endpoints for Nginx and Apache2 hidden from access logs by default
* Updated services: Redis (1.0.2), MariaDB (1.0.3), AthenaPDF (1.0.1)
* PHP extension redis updated to 3.1.3
* Number of default PHP-FPM workers set to 8

## 4.1.4

* PHP updates: [7.1.7](http://php.net/ChangeLog-7.php#7.1.7), [7.0.21](http://php.net/ChangeLog-7.php#7.0.21) with security fixes
* Nginx updates: [1.13.3](http://nginx.org/en/CHANGES), [1.12.1](http://nginx.org/en/CHANGES-1.12) with a fix in the range filter vulnerability (CVE-2017-7529).
* Apache2 updates: [2.4.27](http://www.apache.org/dist/httpd/CHANGES_2.4.27)
* Vanilla Drupal updates: [8.3.5](https://www.drupal.org/project/drupal/releases/8.3.5)
* Solr: new versions 6.6 and 6.5 for Drupal 8
* Solr: search_api_solr version updated from to 8.x-1.0 (default solr configs used from this module)
* Nginx: Content-Type is now set only if not empty https://github.com/wodby/drupal-nginx/issues/27
* Bugfix: some files could be delete during drush import
* Bugfix: vanilla Drupal always re-synced Drupal sources https://github.com/wodby/drupal/issues/2
* Solr versions are now frozen https://github.com/wodby/solr#versions
* Redis version is now frozen https://github.com/wodby/redis#versions

## 4.1.3

* New Apache container
* New Adminer container
* Nginx updated to 1.13.2
* Drupal headers no longer hidden by default, configurable via Nginx/Apache environment variables
* MariaDB now recovers privileges in case of an error during import
* Drupal node container freeze

## 4.1.2

* Updated MariaDB with bug fixes
* PHP extension APCu is now configurable
* All PHP extensions are now frozen
* Runtime Alpine Linux libraries used by PHP extension are now frozen
* Dropped few environment variables
* Updated vanilla Drupal: 8.3.4

## 4.1.1

* Updated PHP: 7.1.5 > 7.1.6, 7.0.19 > 7.0.20
* OpenSMTPD can now relay emails to 3rd party SMTP servers
* OpenSMTPD rebased to Alpine 3.6 with freezed version
* Environment variables for OpenSMTPD configuration
* OpenSMTPD now writes logs to container output
* Increased max_allowed_packet for MariaDB daemon
* PHP expose header now disabled by default
* Nginx images rebased to Alpine 3.6
* Updated vanilla Drupal

## 4.1.0

* Bug fix: git checkout in php container sometimes failed
* Bug fix: varnish cache flush action failed
* Bug fix: some environment variables missed in SSH container
* MariaDB: No longer lock table during backups (--single-transaction)
* MariaDB: Excludes cache tables data from backups. See [backups section](../../apps/backups.md) for more details
* Nginx: New version: 1.13.0 > 1.13.1
* PHP: All images rebased to Alpine Linux 3.6 and now use LibreSSL instead of OpenSSL
* PHP: Fixed segfault caused by imagick extension
* PHP: MongoDB extension downgraded to 1.1.10
* New [AthenaPDF](containers.md#athenapdf) container – drop-in replacement for wkhtmltopdf
* New [Rsyslog](containers.md#rsyslog) container
* New [Node.js](containers.md#nodejs) container

## 4.0.1

* Bug fixes and stabilization improvements
* Images versions freeze
* PHP versions freeze

## 4.0.0

### Changes

* All-new revamped docker container images consistent with docker4drupal
* Improved performance of containers
* Revamped orchestration with better logging and performance
* Optional services now can be enabled/disabled on the working app
* Services configuration via environment variables from the dashboard
* Services' containers now can can be scaled (# of replicas)
* Detailed log output for orchestration tasks
* Redesigned scalability for cluster deployments

There's no backward compatibility with stacks 3.x
