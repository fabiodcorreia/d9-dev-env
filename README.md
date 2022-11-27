# Drupal 9 Development Environment

This is a lando env with a naked installation of Drupal 9

## First Run

Download and install all the required docker images and create the containers

`lando start`

Download and install all the composer packages set on **composer.json**

`lando composer install`

It will also replace the file **web/sites/development.services.yml** with the default settings, we need to revert back to
the development mode settings

`git restore web/sites/development.services.yml`

After this all the vendor and Drupal core packages should be installed and the server running

### Setup Drupal

Configures Drupal to connect to the database with the default credentials and creates the admin user

`lando drush site:install --db-url=mysql://drupal9:drupal9@database/drupal9 -y > site-install.txt`

Save the admin password inside the .env file

### Stop Tracking Settings.php changes

`git update-index --skip-worktree web/sites/default/settings.php`

To track again

`git update-index --no-skip-worktree web/sites/default/settings.php`


## Start and Stop

Boots the development environment

`lando start`

Stops just the app containers keeping the lando containers running

`lando stop`

Stops the app and lando containers

`lando poweroff`

## Add Modules and Themes

Just clone the repo to `web/themes/custom/` or `web/modules/custom` depending if it's a theme or modules

## Purge all the containers, volumes, images and clean lando's cache

`lando poweroff && docker system prune -a --volumes && rm -rf ~/.lando/cache`

