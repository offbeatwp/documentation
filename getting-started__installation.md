# Installation

## Requirements

The use OffbeatWP the following services / packages are required:

- <a href="https://getcomposer.org/" target="_blank">Composer</a>
- Git
- NPM / Yarn
- Node
- <a href="https://wp-cli.org/" target="_blank">WP-CLI</a>
- Webserver (Nginx / Apache)
- Database (Mysql / MariaDB)
- PHP (7.2+ recommended)

How to install it depends on the operation system you are using. For Mac users: <a href="https://brew.sh/" target="_blank">Homebrew</a> is your friend.

### Optional, but recommended

- <a href="https://www.advancedcustomfields.com/pro/" target="_blank">Advanced Custom Fields Pro</a> ($25,- for single website / $100 for developer licence (unlimited sites))

To be honest, we're in love with this plugin. It delivers awesome functionality and joined with OffbeatWP, magic is happening. OffbeatWP integrates ACF in three different areas:
1. Adding fields on post types and terms and make them available in the models automatically. [Learn more](https://github.com/offbeatwp/acf)
2. Site settings. Creating different sections of global settings for your website. [Learn more](https://github.com/offbeatwp/acf-sitesettings)
3. **Pagebuilder with OffbeatWP Components**. [Learn more about ACF Layout with OffbeatWP](https://github.com/offbeatwp/acf-layout)

## Install OffbeatWP WP-CLI package
To make it easier to install and scaffold OffbeatWP themes and elements we introduced the WP-CLI package. You can easily install it with the following command:

```bash
wp package install https://github.com/offbeatwp/wp-cli-offbeatwp.git
```

## Install Wordpress, Theme, and Framework

### 1. Install Wordpress

We can easily install Wordpress through WP-CLI:

```bash
mkdir {folder_name}
cd {folder_name}
wp core download
wp core config --dbname="{dbname}" --dbuser="{dbuser}" --dbpass="{dbpassword}" --dbhost="{dbhost}" --dbprefix="{prefix}"
wp core install --url="{url}" --title="{title}" --admin_user="{username}" --admin_email="{email}"
```

### 2. Install the theme

```bash
wp offbeatwp init-theme {theme-slug}
```
The latest bootstrap theme should be automatically been downloaded from git and activated within WordPress.

### 3. Enjoy working with OffbeatWP

When you access the website you should see a link to the default "Hello world" post. _(Will replace this later with some Default OffbeatWP Introduction page)_
