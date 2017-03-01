# Composer template for Islandora 7.x

This is a remix of the https://github.com/drupal-composer/drupal-project Drupal template.
It is a proof-of concept for Composer-based installation of Islandora 7.x.  Composer-based installs are
gaining traction, especially for Drupal 8, as an off-the-island replacement for Drush Makefiles and the like.

This calls on a proof-of-concept Satis site (GH Pages) at https://shorock.github.io/islandora_satis

If you're curious how that Satis server was generated, check out https://github.com/shorock/islandora_satis

## TL;DR

This installs Islandora from composer.json (or composer.lock) into "web/".  Relevant modules get put in
web/sites/all/modules/contrib and web/sites/all/libraries

## Installing Islandora via Composer

* Step 0 *(optional but highly recommended if you're using any modern PHP with the curl library)* - `composer global require hirak/prestissimo`.  You only need to do this once
  per system/user, but
  it [dramatically speeds up Composer/Packagist loading](https://medium.com/@petehouston/improve-composer-performance-with-prestissimo-8f3f55a20b8e#.e5vfz0fpz)
   (parallel curl calls)

* 1 - Clone this repo.

* 2 - `composer install` from inside it

* 3 - set your webroot to the generated "web/" directory, symlink it somewhere into your webroot... your call

* 4 - going forward, consider doing your modules installs with `composer require drupal/panels` rather than `drush dl panels`.  If you do so, those end up in composer.json and composer.lock, you can VCS them, and goodness shall follow.

## Included

The composer.json in this package will give you:

* Drupal (current 7.x)
* Drupal views, views_ui, bootstrap theme (just to show off using Drupal installs)
* Islandora
  * Islandora brings in Tuque as a dependency
* Islandora Collection, PDF and Basic Image packs
  * bringing in the Drupal Imagemagick module
* Islandora Pathauto
  * pulls in Pathauto

**Note: this only installs the modules, you still have to enable them with drush or /admin/modules.**


## Composer commands

*(all at the level with composer.json)*

`composer require islandora/islandora_solution_pack_audio`

`composer require islandora/islandora:1.x-dev` (git clones HEAD for you... you could set everything to 1.x-dev for bleeding-edge, or perhaps a CI script)

`composer require drupal/panels` or other drupal mods

## For the community to consider

If other users have interest in using Composer installs, we have a few options.  It would not be hard to use Satis to make an official Islandora-hosted endpoint (like the personal one I have above).  This is low traffic... all the ZIPs come from GitHub.

If there were community interest, adding an appropriate composer.json to each of the Islandora projects would make things a bit easier.  Individual projects could manage their own dependency mapping that way.  It would be possible, if the modules got composer.json files for the next release, to add the modules to Packagist.org.  There are very good reasons that the general Drupal community doesn't do that, though.

Also, worth noting: it would be fairly easy to build "drupal-library" pseudo-modules using this technique that could automagically bring in (and version-lock) dependencies like PDF.js or Video.js.. as licenses permit.
