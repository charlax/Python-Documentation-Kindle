Read the Python documentation on your Kindle!
=============================================

This project lets you download a **Kindle-optimized version of the Python documentation**. You can also create your own ebook for any project using Sphinx to generate its documentation.

**Download** the Kindle ebook here:  [Python.mobi](http://min.us/mpw85Fw3E)

You can also clone this repository (unfortunately, the file is too big to be downloaded directly from GitHub, you'll get the following error: `Error: blob is too big`).

This file is for Python v3.2.2. Last update: 25 September 2011.

![Kindle Python Documentation book](https://github.com/charlax/Python-Documentation-Kindle/raw/master/img/Kindle-Python-Documentation.png)

Generate your own ebook
=======================

You can also generate a Kindle-optimized file for any other version of Python.

Requirements
------------

The project must use [Sphinx](http://sphinx.pocoo.org/) to generate its documentation (this is the case for Python).

You need to install Amazon's [KindleGen](http://www.amazon.com/gp/feature.html?ie=UTF8&docId=1000234621) tool and have it in your path:

	$ ln -s ~/bin/kindlegen/kindlegen /usr/local/bin/

Step-by-step tutorial
---------------------

I tweaked Sphinx a little bit (see modifications below) to make this possible.

	$ cd ~/Downloads
	$ hg clone https://bitbucket.org/charlax/sphinx
	$ wget http://www.python.org/ftp/python/3.2.2/Python-3.2.2.tar.bz2
	$ tar xjf Python-3.2.2.tar.bz2
	$ cd Python-3.2.2/Doc
	$ echo "\n# to have the correct first page on Kindle\nepub_pre_files = [('index.html', 'Overview'),]" >> conf.py
	$ python ~/Downloads/sphinx/sphinx-build.py -a -b mobi . build/mobi

The MOBI ebook is `~/Downloads/Python-3.2.2/Doc/build/mobi/Python.mobi`

Modified version of Sphinx
--------------------------

A little bit of background: the Kindle uses a proprietary format `.azw`. This format is based MOBI, another format designed by Mobipocket. This French company was bought by Amazon.com in 2005.

I added a MOBI builder to Sphinx, based on the ePub one. There are scarce documentation about the MOBI format which seems rather closed: this is the reason why I use KindleGen (a free tool maintained by Amazon.com) to convert the ePub to a MOBI ebook.

Here's what I changed to Sphinx:

* Added guide section to `content.opf` (required by Amazon to set the first content shown and the TOC file)
* Removed `@font-face` in the CSS (not supported by the MOBI format)
* Used `kindlegen` to convert the ePub to MOBI.