# Octopress Image Popup Plugin

This repository contains a plugin for generating a modal popup window for images with a resized thumbnail for the [Octopress][] blogging engine. It is adapted from the image popup plugin at https://github.com/bmc/octopress-plugins, but will generate a smaller thumbnail rather than relying on the browser to resize the image.

See [A Simple Octopress Image Popup Plugin][blog-image-popup] for more discussion of the original plugin. This one operates almost identically, with minor differences noted below.

## Installation

Add these lines to your blog's `Gemfile`:

    gem 'erubis'
    gem 'mini_magick'

`mini_magick`, in turn, requires that the Image Magick *mogrify*(1) command
be installed and in your path.

The gem also relies on both jQuery and jQuery UI. Add these lines to your
blog's `sources/_includes/custom/head.html` file:

    <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.7.1/jquery.min.js" type="text/javascript"></script>
    <script src="https://ajax.googleapis.com/ajax/libs/jqueryui/1.8.16/jquery-ui.min.js" type="text/javascript"></script>

Finally, copy `img_popup.rb` and `img_popup.html.erb` to your blog's
`plugins` directory.

## Usage

The plugin implements a [Liquid][] template tag. The tag syntax is
straighforward:

    {% imgpopup /path/to/image percent% [title] %}

The image path is relative to the source directory. The percent argument is the
amount to scale the image down for the clickable preview. The optional title is
put in the title bar of the modal popup. Here’s a real example:

    {% imgpopup /images/bigimage.png 50% My Big Image %}

To use the image resizing functionality, set image_resize_size in in _config.yml to the minimum size, in KB, a file has to be before it will be resized. You may also set a maximum resize percentage with image_resize_percent_limit, so that (for example) if image_resize_percent_limit were set to 80, specifying 90% would leave the image alone. You must set a minimum file resizing size however if you want the images resized, even if that file size is 0. The example below would set image_resize_size to 50KB, and image_resize_percent_limit to 80%:

image_resize_size: 50
image_resize_percent_limit: 80

## License

This plugin is licensed under a [3 clause BSD license][bsd-license]

[blog-image-popup]: http://brizzled.clapper.org/blog/2012/02/05/a-simple-octopress-image-popup-plugin/
[Octopress]: http://octopress.org/
[Liquid]: https://github.com/Shopify/liquid
[bsd-license]: http://opensource.org/licenses/BSD-3-Clause
