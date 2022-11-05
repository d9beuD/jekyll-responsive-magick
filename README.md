# Responsive Images for Jekyll Sites

`jekyll-responsive-magick` is a Jekyll plugin Jekyll plugin for responsive images. It adds filters for setting the `srcset`, `width` and `height` attributes of `img` elements, while automatically generating image variants of configured sizes using the ImageMagick command-line tools. Resized images are cached to minimize build times, regenerated only when the original source image changes.

The plugin has no dependencies besides the ImageMagick command line tools. This is by design, to make it easy to deploy on services such as Cloudflare Pages. For an example of its use, see [indii.org](https://indii.org). For a walkthrough of the implementation, see [Responsive Images with Jekyll and ImageMagick](https://indii.org/blog/responsive-images-with-jekyll-and-imagemagick/).

## License

`jekyll-responsive-magick` is open source software. It is licensed under the Apache License, Version 2.0 (the "License"); you may not use it except in compliance with the License. You may obtain a copy of the License at
<http://www.apache.org/licenses/LICENSE-2.0>.

## Getting started

The plugin requires ImageMagick. It is standard in Linux distributions and available through Homebrew on macOS. If you happen to be hosting with [CloudFlare Pages](https://pages.cloudflare.com/), it is already installed.

1. **Install the plugin** If you are using a `Gemfile`, add the following:
  ```ruby
  group :jekyll_plugins do
    gem 'jekyll-responsive-magick', '~> 1.0'
  ```
  Alternatively, copy the `lib/jekyll-responsive-magick.rb` file into your site's `_plugins` directory.

2. **Enable the plugin** Add the following to your site's `_config.yml` file:
  ```yaml
  plugins: 
  - jekyll-responsive-magick
  ```

## Usage

The plugin provides three filters: `srcset`, `width` and `height`. Each consumes an absolute path to an image (as it would appear in `src`) and generates a value for the corresponding attribute. The intended usage is:
```html
<img
    src="{{ src }}"
    srcset="{{ src | srcset }}"
    width="{{ src | width }}"
    height="{{ src | height }}"
>
```
`src` **must be** an absolute path, i.e. beginning with `/`, such as `/assets/example.jpg`. This is necessary for the plugin to find the right file in your project.

With the plugin installed and one or more uses of the `srcset`, `width` or `height` filters, you can build your site as normal, now with responsive images.

## Configuration

You can configure the size variants and quality of resized images by adding configuration options such as the following to your `_config.yml`:

```yaml
responsive:
  widths: [400,500,700,900]
  quality: 30
```

The choice of `widths` should cover the typical sizes of images as they appear on your site. The choice of quality (between 0 and 100) is a trade-off between file size (lower at lower quality) and clarity (higher at higher quality). It could be tuned by eye. Low quality can be satisfactory with the prevalence of high definition displays.