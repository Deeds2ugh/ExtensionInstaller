# MediaWiki Extension Installer

This is a MediaWiki extension that allows installing other extensions via
the [Composer](http://getcomposer.org/) dependency manager. You can specify
the extensions you want to have installed, and their versions, in a simple list.
When this is done, you run the install command, and the extensions get download,
and loaded. Dependencies of extensions get downloaded automatically and do not
have to be specified. If there are any conflicts between versions of the various
software, you will be notified of these conflicts, and thus also do not need to
bother wth this manually.

## Steps to take

### Install this extension

Place the "ExtensionInstaller" directory in the "extensions" directory of your
MediaWiki installation and add the following line to the end of your LocalSettings file:

    require_once( "$IP/extensions/SubPageList/SubPageList.php" );

### Install Composer

[Download Composer](http://getcomposer.org/download/). See the instructions on that
download page for all options. Important to note is that one can simply get the
composer.phar file and run composer via this file.

    wget http://getcomposer.org/composer.phar
    php composer.phar someCommand

This is equivalent to doing an actually installation of Composer and the running

    composer someCommand

### Specify the extensions to be installed

Copy the example.json file to a new file named composer.json.

In this file, add
the extensions you want to install in the "require" section. See
"[declaring dependencies](http://getcomposer.org/doc/00-intro.md#declaring-dependencies)" and
"[package setup](http://getcomposer.org/doc/01-basic-usage.md#composer-json-project-setup)".
Or have a look at the examples below.

The default contents of the json file specifies nothing should be installed, and looks as follows:

	{
		"require": {
			"php": ">=5.3.2"
		}
	}

Adding version 1.0 or later of the SubPageList extension requires adding a single line:

	{
		"require": {
			"php": ">=5.3.2",
			"mediawiki/sub-page-list": ">=1.0"
		}
	}

The following example also adds the latest matching version of Semantic MediaWiki:

	{
		"require": {
			"php": ">=5.3.2",
			"mediawiki/sub-page-list": ">=1.0",
			"mediawiki/semantic-mediawiki": "*"
		}
	}

Each line, except the last one, should have a comma at the end.

#### Supported extensions

Extensions need to support installation via Composer before they can be installed
via ExtensionInstaller. At present this list is not that big. Most of these extensions,
and the package names that should be used in the json file, can be found
[on Packagist](https://packagist.org/search/?q=mediawiki), the main Composer package repository.

### Installing the extensions

Execute "composer install" in the ExtensionInstaller directory, and see the magic happen.
In case you got the composer.phar file, the command is "php composer.phar install".

That's it! Hit Special:Version and you should see the extensions installed.

Note that some extensions might require further setup and configuration before they are usable.

#### Updating extensions

Once extensions have been installed, you might want to add additional ones, change the version
of existing ones, or perhaps remove a few. Just update the list in the json file and run
"composer update".