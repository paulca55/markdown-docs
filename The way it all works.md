# The way it all works

- [Image sizes in WordPress](#image-sizes-in-wordpress)
- [Imagify Plugin](#imagify-plugin)
  - [Custom Header](#custom-header)
  - [Bulk Optimisation](#bulk-optimisation)
- [FontAwesome 5](#fontawesome-5)
  - [Basic Use](#basic-use)
  - [CSS Pseudo-elements](#css-pseudo-elements)

## Image sizes in WordPress

- In the Media Settings, image sizes allows you to change the maximum dimensions of images that are displayed on posts and pages. When setting a thumbnail size, the image will be cropped and resized to the setting. Medium and large images will keep the dimension proportions, taking the maximum width and height into account.

- When additional image sizes are registered they can be set to **Hard Crop** and **Soft Crop**.

  Hard Crop - This will crop the image to the exact size that we have defined. This can help make sure everything is proportionate and the design is not breaking. This function will automatically crop the image either from the sides or from the top and bottom depending on the size.

  Soft Crop - This will resizes the image proportionally without distorting it. So you might not get the dimensions that you wanted. Usually it matches the width dimension and the heights are different based on each image’s proportion.

- If the image sizes are changed at some point you must run the **Regenerate Thumbnails** plugin to create the new image sizes for any image that has previously been uploaded (be aware that the old image sizes in the uploads folder will still exist).

- If an image is deleted from the media library then the original image and all image sizes associated with it are deleted from the uploads folder. However, please consider the following scenarios where an image has already been uploaded:

  - **SCENARIO 1:** The image sizes are changed, the Regenerate Thumbnails plugin is run and then the image is deleted from the Media Library.
  - **OUTCOME 1:** The **original image** and the **NEW image sizes** will be deleted and the old image size/s will be left in the uploads folder.

  - **SCENARIO 2:** The image sizes are changed, but the Regenerate Thumbnails plugin is **NOT** run and then the image is deleted from the Media Library.
  - **OUTCOME 2:** The **original image** and the **OLD image sizes** will still be deleted, but the new ones obviously won’t because they have not been created yet.

  - **OVERVIEW:** When an image is added to the Media Library each specified image size is created in the uploads folder and WordPress must remember which image sizes it created for that particular image. So if the image is deleted then all the images that were created originally are deleted too, even if the image sizes have been changed before deleting it. The only exception to this is when the Regenerate Thumbnails is run as this creates the new/changed image sizes and basically any image sizes that aren’t set in either the **Media Settings** or `functions.php` are forgotten about so they will still exist in the uploads folder.

## Imagify Plugin

- Make sure you check the Imagify plugin \*_max width_ settings are correct for your website's design. Basically you want this size to be set to accommodate the size of your largest used image (i.e. the header/slider image), otherwise the default image sizes that are set larger than this (i.e. the header image) will not be created at the right size when adding to the Media Library, and although it can be chosen as a featured image for that particular page header it won’t show because it is not at the right dimensions.

### Custom Header

- If you use the Custom Header menu to add the default header image you can either upload an image or choose one from the media library. The below is assuming the Imagify plugin is configured to make images _smaller_ than what the header image specified to be.

  - **Upload an image:** The image you are uploading will not be the correct size for the header as it will be made smaller by Imagify. However, the image will be scaled in the browser up to the correct size for the header, which will degrade image quality.

  - **Choose an image from the Media Library:** If the image you choose has already been resized by Imagify the image will be scaled up in the browser to the correct size for the header, which will degrade image quality. However, if you choose an image that was uploaded before Imagify was installed then it will have been resized correctly to fit the header, but be cautious if you decide to run the **Bulk Optimisation** (see below).

### Bulk Optimisation

- If you run the **Bulk Optimisation** feature from within Imagify and you had the max image width set to 800px then this will resize anything that is larger than this, which will generally affect the following:

  - **Header Images:** These will be resized by Imagify so the image will be scaled up in the browser to the correct size for the header, which will degrade image quality.

  - **Featured Images for Page Headers:** If a featured image has already been set as a page header before Imagify has resized it, then the image will behave the same as above.

**NOTE:** This only applies to images that will be used through the Media Library, images in the theme folder don’t get resized.

**NOTE:** The Bulk Optimisation process only optimizes images that haven't already been optimized with Imagify. So if you change the **Max Width** you will need to restore all images back to their original state (assuming **Backup original images** is enabled) and then re-run the bulk optimisation.

**NOTE:** When **Backup original images** is enabled, only images that have been processed by Imagify will appear in the backup folder. So if Imagify reports that no further compression is needed then the image is untouched so does not need a backup.

## FontAwesome 5

> Note: If you need to add icons using pseudo-elements you must use **Web Fonts with CSS**. Pseudo-elements are not supported when using **SVG with JavaScript**.

### Basic Use

```html
<i class="fas fa-camera-retro"></i>
```

| Style   | Style Prefix | Version    | @font-face weight | Code                              |
| :------ | :----------- | :--------- | :---------------- | :-------------------------------- |
| Solid   | `fas`        | Free       | 900               | `<i class="fas fa-camera-retro">` |
| Regular | `far`        | Free & Pro | 400               | `<i class="far fa-camera-retro">` |
| Light   | `fal`        | Free       | 300               | `<i class="fal fa-camera-retro">` |
| Brands  | `fab`        | Free       | 400               | `<i class="fab fa-font-awesome">` |

### CSS Pseudo-elements

1.  Set the pseudo-element to either `::before` or `::after`
2.  Set the `font-family` to `Font Awesome 5 Free`, `Font Awesome Brands` or `Font Awesome 5 Pro` (depending on which one you are using)
3.  Set the `font-weight`: 900 (Solid), 400 (Regular or Brands), 300 (Light)
4.  Set the `content` to the unicode value of the icon you want to use.

```css
.login::before {
  font-family: 'Font Awesome 5 Free';
  font-weight: 900;
  content: '\f007';
}
```
