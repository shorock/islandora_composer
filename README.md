# Composer template for Islandora 7.x

This is a remix of the https://github.com/drupal-composer/drupal-project Drupal template
serving as a proof-of concept for a Composer-based installation of Islandora 7.x.  Composer-based installs are
gaining traction, especially in Drupal 8, as an off-the-island replacement for Drush Makefiles and the like.

This calls a proof-of-concept Satis server at https://islandorapkg.shorock.com

If you're curious how that was generated, check out https://github.com/shorock/islandora_satis

## TL;DR

This installs Islandora from composer.json (or composer.lock) into "web/".  Relevant modules get put in
web/sites/all/modules/contrib and web/sites/all/libraries

## Included

This composer.json will give you:

* Drupal (current 7.x)
* Drupal views, views_ui, bootstrap theme (just to show off using Drupal installs)
* Islandora
  * Islandora brings in Tuque as a dependency
* Islandora Collection, PDF and Basic Image packs
* Islandora Pathauto (to show off pulling in Drupal's pathauto as a dependency)

**Note: this only installs the modules, you still have to enable them with drush or /admin/modules.**

## Installing by composer

* Step 0 (optional but highly recommended) - `composer global require hirak/prestissimo`.  You only need to do this once
  per system/user, but
  it [dramatically speeds up Composer/Packagist loading](https://medium.com/@petehouston/improve-composer-performance-with-prestissimo-8f3f55a20b8e#.e5vfz0fpz)
   (parallel curl calls)

* 1 - Clone this repo.

* 2 - `composer install` from inside it

* 3 - set your webroot to the generated "web/" directory, symlink it somewhere into your webroot... your call

## Composer commands

*(all at the level with composer.json)*

`composer require islandora/islandora_solution_pack_audio`

`composer require islandora/islandora:1.x-dev` (git clones HEAD for you... you could set everything to 1.x-dev for bleeding-edge, or maybe a CI script)

`composer require drupal/panels`

## To consider

It would be fairly easy to build pseudo-modules that would automatically bring in JS libraries.