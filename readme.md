![Logo](docs/logo.svg)

# Jekyll Picture Tag

![Tests & Formatting](https://github.com/rbuchberger/jekyll_picture_tag/workflows/Tests%20&%20Formatting/badge.svg)

**Responsive Images done correctly.**

It's simple to throw a photo on a page and call it a day, but doing justice to users on all
different browsers and devices is tedious and tricky. Tedious, tricky things should be automated.

Jekyll Picture Tag automatically builds cropped, resized, and reformatted images, builds several
kinds of markup, offers extensive configuration while requiring none, and solves both the art
direction and resolution switching problems with a little YAML configuration and a simple template
tag.

## Why use Responsive Images?

**Performance:** The fastest sites are static sites, but if you plonk a 2mb picture of your dog at
the top of a blog post you throw it all away. Responsive images allow you to keep your site fast,
without compromising image quality.

**Design:** Your desktop image may not work well on mobile, regardless of its resolution. We often
want to do more than just resize images for different screen sizes, we want to crop them or use a
different image entirely.

## Why use Jekyll Picture Tag?

**Developer Sanity:** If you want to serve multiple images in multiple formats and resolutions, you
have a litany of markup to write and a big pile of images to generate and organize. Jekyll Picture
Tag is your responsive images minion - give it simple instructions and it'll handle the rest.

## Features

* Generate piles of cropped, resized, and converted image files.
* Generate corresponding markup in several different formats.
* Configure it easily, or not at all.
* Make Lighthouse happy.

## Documentation:

https://rbuchberger.github.io/jekyll_picture_tag/

## Changelog:

https://rbuchberger.github.io/jekyll_picture_tag/devs/releases

Recent releases:

* 2.0.1 March 31, 2021
  * Select imagemagick deliberately when appropriate, rather than simply rescuing all vips errors
    and trying again. This will stop JPT from suppressing useful vips errors.
* **2.0** March 25, 2021 - [Migration guide](https://rbuchberger.github.io/jekyll_picture_tag/users/notes/migration_2)
  * Switch from ImageMagick to libvips.
    * 🚀🔥🔥**MUCH MORE FASTER**🔥🔥🚀
    * Will still attempt to use imagemagick if libvips cannot handle a
      particular image format.
    * Eliminate the ImageMagick v7 on Ubuntu pain we've been dealing with for so
      long.
  * Require Ruby >= 2.6, support Ruby 3.0
  * Require Jekyll >= 4.0
  * Cropping is changing.
      * We now use the libvips
        [smartcrop function](https://www.rubydoc.info/gems/ruby-vips/Vips/Image#smartcrop-instance_method),
        which does some magic to keep the most useful part of the image.
      * Geometry is renamed to 'crop', and reduced to simple aspect ratios only. (`width:height`)
      * Gravity is gone, replaced by 'keep' which is translated to a libvips
        [interestingness](https://www.rubydoc.info/gems/ruby-vips/Vips/Interesting) setting.
  * Add stock presets and media queries, under the `jpt-` prefix.
  * Add `format_quality` default settings for webp, avif, and jp2.
  * Add image-format-specific write options.
  * Overhaul user input handling; we can now validate inputs and give error
    messages which are less useless. Stronger validation and nicer errors will be added in future
    releases.
  * Drop support for `markup_presets` and `media_presets`. They are now
    officially and only `presets` and `media_queries`.
  * Improve docs with an introductory tutorial and 'how-to' flow.

* 1.14.0 January 10, 2021
  * Gracefully handle empty tag arguments.
  * Re-add metadata stripping. I removed it inadvertently when refactoring; now
    there's a test and a setting to turn it off.
  * Respect Jekyll's `--disable-disk-cache` argument.
  * Add baseurl configuration, allowing increased plugin support (such as I18n via `jekyll-multiple-languages-plugin`)
  * Tooling & test suite maintenance and improvements.

## Help Wanted

Writing code is only part of the job; often the harder part is knowing what needs to be changed. Any
and all feedback is greatly appreciated, especially in regards to documentation. What are your pain
points? See the [contributing
guidelines](https://rbuchberger.github.io/jekyll_picture_tag/devs/contributing), or the
[issues](https://github.com/rbuchberger/jekyll_picture_tag/issues) page for more.
