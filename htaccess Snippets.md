# .htaccess Snippets

<!-- TOC depthFrom:2 depthTo:2 orderedList:false updateOnSave:true withLinks:true -->

- [Enable Gzip](#enable-gzip)
- [Image Hotlinking](#image-hotlinking)

<!-- /TOC -->

```
# Compress HTML, CSS, JavaScript, Text, XML and fonts (Gzip)
<IfModule mod_deflate.c>
AddOutputFilterByType DEFLATE application/javascript
AddOutputFilterByType DEFLATE application/rss+xml
AddOutputFilterByType DEFLATE application/vnd.ms-fontobject
AddOutputFilterByType DEFLATE application/x-font
AddOutputFilterByType DEFLATE application/x-font-opentype
AddOutputFilterByType DEFLATE application/x-font-otf
AddOutputFilterByType DEFLATE application/x-font-truetype
AddOutputFilterByType DEFLATE application/x-font-ttf
AddOutputFilterByType DEFLATE application/x-javascript
AddOutputFilterByType DEFLATE application/xhtml+xml
AddOutputFilterByType DEFLATE application/xml
AddOutputFilterByType DEFLATE font/opentype
AddOutputFilterByType DEFLATE font/otf
AddOutputFilterByType DEFLATE font/ttf
AddOutputFilterByType DEFLATE image/svg+xml
AddOutputFilterByType DEFLATE image/x-icon
AddOutputFilterByType DEFLATE text/css
AddOutputFilterByType DEFLATE text/html
AddOutputFilterByType DEFLATE text/javascript
AddOutputFilterByType DEFLATE text/plain
AddOutputFilterByType DEFLATE text/xml
</IfModule>
```

## Image Hotlinking

If you want to stop being hotlinking your images you need to put the following code into your `.htaccess` file.

```
# Disable Hotlinking
RewriteEngine On
RewriteCond %{HTTP_REFERER} !^$
RewriteCond %{HTTP_REFERER} !^http(s)?://(www\.)?yourdomain.co.uk [NC]
RewriteCond %{HTTP_REFERER} !^http(s)?://(www\.)?staging[0-9]|[1-9][0-9].yourdomain.co.uk [NC]
RewriteCond %{HTTP_REFERER} !^http(s)?://cdn.yourdomain.co.uk [NC]
RewriteCond %{HTTP_REFERER} !^http(s)?://yourdomain-5733.kxcdn.com [NC]
RewriteRule \.(jpe?g|png|gif|svg)$ – [NC,F]
```

- The first line, `RewriteEngine On`, begins the rewrite.
- The second line means allow empty referrals.
- The third to fourth lines are allowing the domains specified access to the images, any other domains will be blocked. The `http(s)?` and `(www\.)?` means that multiple variations of the domains will be allowed, for example:
  - `http://www.yourdomain.co.uk`
  - `http://yourdomain.co.uk`
  - `https://www.yourdomain.co.uk`
  - `https://yourdomain.co.uk`
- The last line matches any files ending with the specified extensions (i.e. `jpg`, `png`, `gif`, etc.).
- Note: `NC` code means "No Case", meaning match the URL regardless of being in upper or lower case letters.
- Note: `F` code means display a `403 Forbidden` error code instead of an image.
