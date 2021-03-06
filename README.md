Bootstrap Image Modal for Octopress
========================
For the [Octopress][] blogging engine.

Uses Twitter Bootstrap Modal windows for displaying larger images in a popup dialog. Allows for scaled down clickable thumbnails with the use of Mini Magick to calculate the appropriate size based on a given percentage.
 
This plugin is useful when you want to display an image as a thumbnail, with the option to display it in its full size with a popup or when you simply have an image that's just too wide for the blog.

## About
This project originated from the [bmc\octopress-plugins][] project, which is a good jQuery UI example. This project remains very similar and almost identical to that. You can view Brian's [A Simple Octopress Image Popup Plugin][blog-image-popup] blog post on the original plugin.

This plugins is merely a Bootstrap implementation versus the jQuery UI version and also includes the ability to float\align your thumbnail image.

**Potential Future Enhancements:**

1. Ability to generate actual separate and smaller thumbnails images versus letting the browser size down the original via width and height attributes.
2. Generate modals for more than images (text, videos, AJAX requests, etc.).

## Prerequisites
1. The "mini_magick" and "erubis" gems
2. [ImageMagick][] toolkit, you will need the mogrify function in your PATH variable, if not already

	For more information on the Image Magick toolkit you may visit http://www.imagemagick.org/.
	
	For installing on OS X I recommend using [MacPorts][] just as ImageMagick recommends, for more information on MacPorts, http://www.macports.org/.

3. [jQuery][] plugin

	I recommend a hosted version by someone like Google, https://developers.google.com/speed/libraries/devguide#jquery.

4. [Twitter Bootstrap][]

	This example uses Bootstrap 3.0
	
	I'm using the http://www.bootstrapcdn.com/ for hosting just the JS, I'm hosting a CSS file locally that is customized/stripped down just for this plugin/project.

**Note:** I myself also needed to update my Perl version as implementing this plugin broke my Octopress builds. I went from version 5.10 to 5.16. See http://learn.perl.org/installing/ for upgrading your Perl version.

## Installation
1. Gemfile

  Update your `Gemfile` by adding these lines:

        gem 'mini_magick'
        gem 'erubis'

	Don't forget to run a `bundle install` afterwards to install the gems

2. JavaScript

	Add the following lines to your `source/_includes/custom/head.html` file:

        <!--Twitter Bootstrap-->
        <script src="//netdna.bootstrapcdn.com/bootstrap/3.0.0/js/bootstrap.min.js"></script>
        
	**Note:** The jQuery libary should already be included your `source/_includes/head.html` file. If not include it by adding the following in-between the head tags:

        <script src="//ajax.googleapis.com/ajax/libs/jquery/2.0.3/jquery.min.js"></script>
        
3. CSS
	
	Copy the `_botstrap.scss` file to your `sass/custom` directory. This is a stripped down version of the non-minimized Boostrap 3.0 CSS file that only includes the .btn, .btn-primary, .close and .modal classes needed for this plugin to prevent any additional changes or conflicts with your sites layout/theme that may come from other Bootstrap styles.

	**Note** If you are using a Boostrap theme for Octopress I wouldn't include this file and thus would skip updating your `screen.scss` file in the next step as well.
	
	Next, update your `sass/screen.scss` file by adding the following line:
	
        @import "custom/bootstrap";
	
  	Lastly, add the following CSS to your `sass/custom/_styles.scss` file:

        a.imgModal {
          text-decoration: none;
          white-space: normal;
        }

        a.imgModal > img {
          margin: 0;
        }

        a.imgModal.floatLeft {
          float: left;
        }

        a.imgModal.floatLeft > img {
          margin: 0 15px 15px 0;
        }

        a.imgModal.floatRight {
          float: right;
        }

        a.imgModal.floatRight > img {
          margin: 0 0 15px 15px;
        }

3. Copy the plugin

  Finally, copy `img_popup.rb` and `img_popup.html.erb` to your `plugins` directory.

## Usage and Examples
The plugin implements a [Liquid][] template tag, which can be used in blog posts as shown:
   
    {% imgpopup /path/to/image percent% [float alignment (left|right)] [title] %}

  1. The image path is relative to the source directory.
  2. The percent argument is the amount to scale the image down for the clickable thumbnail preview.
  3. The optional float\alignment will align your image and wrap text around it (see [w3schools][]).
  4. The optional title will be the title\tooltip text when hovering over the image and will also be put in the title bar of the modal popup.

**Examples:**

    {% imgpopup /images/bigimage.png 50% right My Big Image %} <!--Loaded and fully dressed-->
    {% imgpopup /images/bigimage.png 50% My Big Image %} <!--No alignment, with a title-->
    {% imgpopup /images/bigimage.png 50% right %} <!--Alignment with no title-->
    {% imgpopup /images/bigimage.png 50% %} <!--Bare, no alignment or title-->
    
For a live example visit http://www.rayfaddis.com/blog/2013/05/27/jquery-validation-with-twitter-bootstrap/

## License
This plugin is licensed under the [BSD 3-Clause License][bsd-license]

[Octopress]: http://octopress.org/
[bmc\octopress-plugins]: https://github.com/bmc/octopress-plugins
[blog-image-popup]: http://brizzled.clapper.org/blog/2012/02/05/a-simple-octopress-image-popup-plugin/
[ImageMagick]: http://www.imagemagick.org/
[MacPorts]: http://www.macports.org/
[jQuery]: http://jquery.com/
[Twitter Bootstrap]: http://getbootstrap.com
[Liquid]: https://github.com/Shopify/liquid
[w3schools]: http://www.w3schools.com/cssref/pr_class_float.asp
[bsd-license]: http://opensource.org/licenses/BSD-3-Clause
