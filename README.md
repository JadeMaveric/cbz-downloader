# CBZ Comic Downloader

Download comics from the web and save them as CBZ files for reading. Ideal for loading up a tablet and offline reading.

CBZ Downloader is a lightly extensible comic downloader, that can assemble comic pages by chapter into CBZ files for use in comic readers, available for [desktop](https://lifehacker.com/5858906/five-best-desktop-comic-book-readers) and [mobile](https://thedroidguy.com/2018/01/5-best-comic-book-reader-apps-android-device-2018-1069923).

## Features

* Extensible base to operate on many web comic hosting sites
	* base object's API provides a number of convenience functions for parsing HTML source
* Creates standardized ZIP/deflate-based CBZ files for individual chapters
* Suport for installation and use on [Termux](https://termux.com/) GNU/Linux environment for Android

### Supported sites

This is the list of sites cbzdl knows how to download from.

* Mangakakalot (including manganelo.com)
* MangaFox (fanfox.net)
* MangaHere (mangahere.cc)

## Installing

You will need [Python 3](https://www.python.org/) and `pip3`

Then, on Linux, run

	./install.sh

and the `cbzdl` command will be available to you.

## Using

Simply provide a URL to download from - e.g.

	cbzdl http://mangakakalot.com/manga/acaria

To you can specify a start chapter, and end chapter (both optional, as numbers)

	cbzdl URL -s START -e END [-d DELAY] [-v]

By default, `cbzdl` will wait 1 second between fetching two images (some sites throttle heavy downloaders). You can affect the delay by providing a `-d DELAY` argument.

If the `-v` option is specified, debug output is printed

## Extending

The core CBZ Downloader in `cbzdl/` takes care of managing chapter downloads and CBZ assembling ; support for individual sites must be added by modules.

To add a new module, copy the `modules/example_module.py` file into a new file in the `modules/` folder, add it to the `modules/moduleslist.py` main list, and implement for the site you want.

The `WebResource` class in `cbzdl/web.py` provides some utilities for fetching pages and data, so all you need to do is take care of extracting the relevant portions of the site you are scraping. See the existing modules for examples.

You can deploy new modules from the local `modules/` folder by running

	./update_modules.sh
