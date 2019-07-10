# Troubleshooting and Known Issues

- [WordPress Cron Jobs not working/queuing up](#wordpress-cron-jobs-not-workingqueuing-up)
- [WordPress redirects](#wordpress-redirects)
  - [URL not redirecting automatically from non-www to www version of the website.](#url-not-redirecting-automatically-from-non-www-to-www-version-of-the-website)
- [WP Rocket](#wp-rocket)
  - [Issue:](#issue)
  - [Solution:](#solution)
- [Justified Image Grid](#justified-image-grid)
  - [Error displayed:](#error-displayed)
  - [Solution 1:](#solution-1)
  - [Solution 2:](#solution-2)
- [The plugin batch options have disappeared](#the-plugin-batch-options-have-disappeared)
- [Error establishing a database connection](#error-establishing-a-database-connection)
  - [Solution 1:](#solution-1-1)
  - [Solution 2:](#solution-2-1)
- [Can’t connect a WordPress plugin to Google](#cant-connect-a-wordpress-plugin-to-google)
  - [Error displayed:](#error-displayed-1)
  - [Step 1:](#step-1)
  - [Step 2:](#step-2)
  - [Step 3:](#step-3)
  - [Step 4:](#step-4)
- [WordPress editor styles not displaying fonts properly](#wordpress-editor-styles-not-displaying-fonts-properly)
  - [Solution 1:](#solution-1-2)
- [Node Version Manager (NVM)](#node-version-manager-nvm)
  - [Error displayed (in the terminal)](#error-displayed-in-the-terminal)
  - [Solution](#solution)

## WordPress Cron Jobs not working/queuing up

#### Possible Solution

This can be caused by the `wp-content/object-cache.php` file (if present). Try deleting this file **if it is not needed** but take a copy first just in case.

Maybe also try deleting/renaming other _cache_ folders and files to see if they are causing the issue.

_Note: You will probably have to run all the Cron jobs manually via WP-CLI to clear the queue with the `wp cron event run --all` command first, and then check to see if scheduled jobs are working as they should._

_Note: The `object-cache.php` file can be created by plugins such as SiteGround's SG Optimizer when you enable memcached on the server and in the plugin settings._

## WordPress redirects

### URL not redirecting automatically from non-www to www version of the website.

#### Solution 1

Try deleting the **wp-content/cache** folder. Also empty the cache from any other caching solutions (i.e. SiteGround SuperCacher, Cloudflare, etc).

#### Solution 2

If solution 1 doesn't work you can add the following to your `.htaccess` file as a quick fix.

```apache
# Redirect non-www to www
<IfModule mod_rewrite.c>
RewriteEngine On
RewriteCond %{HTTP_HOST} ^example.co.uk [NC]
RewriteRule ^(.*)$ https://www.example.co.uk/$1 [L,R=301]
</IfModule>
```

## WP Rocket

### Issue:

File URLs that have been added to the **Rejected files** list under the CDN settings aren't being rejected and are still being served by the CDN.

### Solution:

If you are adding a URL to a file/image with a specific pixel size like below, for example.

`/wp-content/uploads/cropped-favicon-180x180.png`

This may not work and the image will still be served by the CDN. In this situation you can try rejecting the original image from which the other image sizes are being generated (i.e. what it's called in the Media Library).

`/wp-content/uploads/cropped-favicon.png`

## Justified Image Grid

### Error displayed:

> All of the images have failed to load.

### Solution 1:

**Disable HHVM** via the cPanel and try again as on SiteGround there seems to be an issue with TimThumb and HHVM.

### Solution 2:

Although this is not recommended, as a last resort you can **disable TimThumb** from the Justified Image Plugin settings.

## The plugin batch options have disappeared

This error occurs when HHVM is activated and is known to SiteGround as a problem. If you wish to use the bulk options feature you need to deactivate HHVM and then it will appear when you refresh the page. Once finished you can enable HHVM again.

## Error establishing a database connection

### Solution 1:

Check the **wpconfig.php** and make sure the database name, username and password are correct.

### Solution 2:

Check the firewall settings and make sure Apache, MySQL, etc. are allowed.

## Can’t connect a WordPress plugin to Google

### Error displayed:

> The page you have requested cannot be displayed. Another site was requesting access to your Google Account, but sent a malformed request. Please contact the site that you were trying to use when you received this message to inform them of the error. A detailed error message follows:
>
> The site “http://yoursite.co.uk” has not been registered.

### Step 1:

Go to **https://accounts.google.com/ManageDomains** and register the domain (i.e. **http://www.yoursite.co.uk**)

### Step 2:

If you are asked to verify you own the domain then choose **Google Analytics** as the method. You can be logged in as **webmaster@cassify.co.uk** or you can be logged in as the client.

### Step 3:

Agree to the terms or service and when asked for a **Target URL path prefix** enter **http://www.yoursite.co.uk/wp-admin** and click **Save**.

### Step 4:

Now try to connect the plugin again and it hopefully should work.

## WordPress editor styles not displaying fonts properly

### Solution 1:

If you are using the `add_editor_style` function and are adding more than one font you need to add them **separately**. You can't use the pipe character (`|`) to add multiple fonts as it doesn't seem to work correctly.

#### Not Correct

```php
add_editor_style( array( get_template_directory_uri() . '/editor-style.css', 'https://fonts.googleapis.com/css?family=Open+Sans:600,700,600italic,700italic|Josefin+Sans:400,400italic,700,700italic' ) );
```

#### Correct

```php
add_editor_style( array( get_template_directory_uri() . '/editor-style.css', 'https://fonts.googleapis.com/css?family=Open+Sans:600,700,600italic,700italic', 'https://fonts.googleapis.com/css?family=Josefin+Sans:400,400italic,700,700italic' ) );
```

_**Note on local fonts**: Even if you haven't linked the fonts to the editor styles they will show up in the editor if you have them installed locally. Either test on another computer or disable the local fonts so you know they are being added properly._

## Node Version Manager (NVM)

### Error displayed (in the terminal)

```
nvm is not compatible with the npm config "prefix" option: currently set to "/usr/local"
Run `npm config delete prefix` or `nvm use --delete-prefix v8.9.4 --silent` to unset it.
```

### Solution

This is most likely due to `Node` being installed elsewhere on your system. Possibly using `Homebrew` to install `Node` either purposely by you or as part of a formula you have installed.

1.  Uninstall `Node` if installed via `Homebrew`.
2.  Delete the following file/directories.

```
/usr/local/lib/node_modules

/usr/local/bin/npm
```

You don't need these because `Node` and all `node_modules` are stored within `NVM` here:

```
/Users/paul/.nvm/versions/node

/Users/paul/.nvm/versions/node/<node_version>/lib/node_modules)
```

[desktopservererror1]: http://docs.serverpress.com/article/206-unable-to-update-wordpress 'Unable to Update WordPress'
