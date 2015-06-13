img-fixheight element
==========================

[![Build Status](https://travis-ci.org/didrocks/img-fixheight.svg?branch=master)](https://travis-ci.org/didrocks/img-fixheight)

See the [component page](https://didrocks.github.io/img-fixheight) for more information.

## Getting Started

The img-fixheight is an element implementing responsive support for fixed height images. You can provide breakpoints, scale factors and optional limit the maximum width for this image.

## Install

via [Bower](http://twitter.github.com/bower/)

	bower install img-fixheight

or [Yeoman](http://yeoman.io/)

	yeoman install img-fixheight

## API and tools

The whole component API is documented on the [component](index.html) page.

This element ships with a python tool, `tools/prepare-images` which would cut multiple images to the right sizes to be
compatible with the `<img-fixheight>` element.

Example:
```sh
  tools/prepare-images <fixed height at 1x in pixels> <dest pattern> <path to image[:scale]> [<path to image[:scale]> ...] --breakpoint <width 1>  [ --breakpoint <width 2> ...]
```

Where:
 * `<fixed height at 1x in pixels>` is the desired height with a scale factor of 1x in device pixels.
index.html* `<dest pattern>` is the output pattern for cut images. `::::` will be replaced by the image size.
 * various images at maximum width size, with an optional scale factor suffix. If no scale factor is defined, 1x would
	be used. Only one image per scaled factor is accepted.
 * one or more --breakpoint `<width>` options defining multiple breakpoints in css pixels that would be used to delimit
	different image sizes that would be used. -b is equivalent to --breakpoints. At least one breakpoint is required.

  Note that we currently require that the height of the images corresponds to fixed_height * scale factor.

  Example:
```sh
  tools/prepare-images 560 /tmp/banner_::::.jpg img.jpg img_hdpi.jpg:2 img_hhdpi.jpg:3 -b 480 -b 960  -b 1260 -b 1920
```

Let's imagine img.jpg is 2500x560, and img_hdpi.jpg 4000x1120 and img_hhdpi.jpg 4000x1680 widths. All heights correspond
to 560 * `<scale factor for this image>`. An error will be raised otherwise.

This would generate:
 * all images for `1x`: `/tmp/banner_480x560.jpg` (breakpoint 480), `/tmp/banner_960x560.jpg` (breakpoint 960),
`/tmp/banner_1260x560.jpg` (breakpoint 1260), `/tmp/banner_1920x560.jpg` (breakpoint 1920), `/tmp/banner_2500x560.jpg` (for any width > 1920)
 * all images for `2x`: `/tmp/banner_960x1120.jpg` (breakpoint 480), `/tmp/banner_1920x1120.jpg` (breakpoint 960),
`/tmp/banner_2520x1120.jpg` (breakpoint 1260), `/tmp/banner_3840x1120.jpg` (breakpoint 1920), `/tmp/banner_4000x1120.jpg` (for any width > 1920)
 * all images for `3x`: `/tmp/banner_1440x1680.jpg` (breakpoint 480), `/tmp/banner_2880x1680.jpg` (breakpoint 960),
`/tmp/banner_3780x1680.jpg` (breakpoint 1260), `/tmp/banner_4000x1680.jpg` (for any width > 1260, as 4000 < 2500*3)

## Play with this element

This element has some unit tests, to get them running, one easy method is to run the
[Polyserve](https://github.com/PolymerLabs/polyserve) web server, you can install it via:

    npm install -g polyserve

And you can run it via:

    polyserve

Once running, you can preview this element at
`http://localhost:8080/components/img-fixheight/`, where `img-fixheight` is the name of the directory containing it.



## Testing Your Element

Simply navigate to the `/test` directory of your element to run its tests. If
you are using Polyserve: `http://localhost:8080/components/img-fixheight/test/`

### web-component-tester

The tests are also compatible with [web-component-tester](https://github.com/Polymer/web-component-tester).
Install it via:

    npm install -g web-component-tester

Then, you can run your tests on _all_ of your local browsers via:

    wct

## WCT Tips

		`wct -l chrome` will only run tests in chrome.

		`wct -p` will keep the browsers alive after test runs (refresh to re-run).

		`wct test/some-file.html` will test only the files you specify.

## License

Licensed under MIT.
