---
title: Drupal 8 Configuration Management with Drush
date: 2017-03-02
redirect_from: /drupal-8-configuration-management-with-drush/
---
You can easily control your Drupal 8 configurations with Drush. First I’d recommend that you set your configurations files out of files folder:

Add this to your settings.php (or default.settings.php if you’d like it to be default):

```
$config_directories['sync'] = 'config/sync';
```

Now you configurations should be more available and also visible for Git.

To export your current configurations use this:

```
drush config-export sync
```

and to import:

```
drush config-import sync
```

Notice that if you are a team or you are developing on multiple systems then **it is necessary to have the same UUID** for the site you are developing.

You can find out the site UUID with this:

```
drush config-get "system.site" uuid
```

and set it with this:

```
drush config-set "system.site" uuid "INSERT-UUID-HERE"
```