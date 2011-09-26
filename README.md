This project lets you download a **Kindle-optimized version of the Python documentation**. You can also create your own ebook for any project using Sphinx to generate its documentation.

Download
--------

<p><a href="http://minus.com/dblPImJCjz05oC.mobi"><img src="https://github.com/charlax/Python-Documentation-Kindle/raw/gh-pages/img/KindleBook.png" /></a> <a href="http://minus.com/dblPImJCjz05oC.mobi">Python.mobi</a> (Python 3.2.2, generated: 09/25/2011)</p>

You can also clone the project with [Git](http://git-scm.com) by running:

	$ git clone git://github.com/charlax/Python-Documentation-Kindle

![Kindle Python Documentation book](https://github.com/charlax/Python-Documentation-Kindle/raw/gh-pages/img/Kindle-Python-Documentation.png)

Generate your own ebook
-----------------------

You can also generate a Kindle-optimized file for any other version of Python.

### Requirements

The project must use [Sphinx](http://sphinx.pocoo.org/) (this is the case for Python).

You also need to install Amazon's [KindleGen](http://www.amazon.com/gp/feature.html?ie=UTF8&docId=1000234621) tool and have it in your path:

	$ ln -s ~/bin/kindlegen/kindlegen /usr/local/bin/

### Step-by-step tutorial

I tweaked Sphinx a little bit (see modifications below) to make this possible.

	$ cd ~/Downloads
	$ hg clone https://bitbucket.org/charlax/sphinx
	$ wget http://www.python.org/ftp/python/3.2.2/Python-3.2.2.tar.bz2
	$ tar xjf Python-3.2.2.tar.bz2
	$ cd Python-3.2.2/Doc
	$ echo "\n# to have the correct first page on Kindle\nepub_pre_files = [('index.html', 'Overview'),]" >> conf.py
	$ python ~/Downloads/sphinx/sphinx-build.py -a -b mobi . build/mobi

The MOBI ebook is `~/Downloads/Python-3.2.2/Doc/build/mobi/Python.mobi`

### Modified version of Sphinx

Context: the Kindle uses a proprietary format `.azw`. It is based on MOBI, another format designed by Mobipocket. This French company was acquired by Amazon.com in 2005.

I added a MOBI builder to Sphinx, based on the ePub one. Since there are scarce documentation about the MOBI format, I used KindleGen to convert the generated ePub to a MOBI ebook.

Here's what I changed to [Sphinx](https://bitbucket.org/charlax/sphinx):

* Added guide section to `content.opf` (required by Amazon to set the first content shown and the TOC file)
* Removed `@font-face` in the CSS (not supported by the MOBI format)
* Used `kindlegen` to convert the ePub to MOBI.

Author
------

Charles-Axel Dein – [www.d3in.org](http://www.d3in.org/)