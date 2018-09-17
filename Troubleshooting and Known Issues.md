<img src="https://raw.githubusercontent.com/paulca55/markdown-docs/master/images/cassify-header-logo.png" alt="Cassify logo" width="300">

# Troubleshooting and Known Issues

<!-- TOC depthFrom:2 depthTo:2 orderedList:false updateOnSave:true withLinks:true -->

- [DesktopServer](#desktopserver)
- [WP Rocket](#wp-rocket)
- [Justified Image Grid](#justified-image-grid)
- [SuperCacher says website is not being cached](#supercacher-says-website-is-not-being-cached)
- [The plugin batch options have disappeared](#the-plugin-batch-options-have-disappeared)
- [Error establishing a database connection](#error-establishing-a-database-connection)
- [Can’t connect a WordPress plugin to Google](#cant-connect-a-wordpress-plugin-to-google)
- [WordPress editor styles not displaying fonts properly](#wordpress-editor-styles-not-displaying-fonts-properly)

<!-- /TOC -->

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

## SuperCacher says website is not being cached

This error occurs because WP Rocket is already caching the website so it throws up an error. According to SiteGround you can ignore the error and be assured that the website is being cached properly even if you check the **Dynamic Cache Status** and it returns **NOT CACHED**.

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
