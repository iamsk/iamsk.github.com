---
layout: single
title: Docopt - Command-line interface description language
tags: [command, argparse, optparse, getopt, click]
date: 2014-05-13 14:02
---
When we want a user-friendly command-line interface

What we want are:

* useful help and usage messages
* easy to parse the arguments

### Docopt helps you:

* define interface for your command-line app
* automatically generate parser for it

Seems other libs in python can handle this also, like: argparse, optparse, getopt, click.

But after I used all of those libs, I find docopt is the easiest way to handle this, and what your see is what your get.

### Demo(naval_fate.py)

	"""Naval Fate.
	
	Usage:
	  naval_fate.py ship new <name>...
	  naval_fate.py ship <name> move <x> <y> [--speed=<kn>]
	  naval_fate.py ship shoot <x> <y>
	  naval_fate.py mine (set|remove) <x> <y> [--moored|--drifting]
	  naval_fate.py -h | --help
	  naval_fate.py --version
	
	Options:
	  -h --help     Show this screen.
	  --version     Show version.
	  --speed=<kn>  Speed in knots [default: 10].
	  --moored      Moored (anchored) mine.
	  --drifting    Drifting mine.
	
	"""
	from docopt import docopt
	
	
	if __name__ == '__main__':
	    arguments = docopt(__doc__, version='Naval Fate 2.0')
	    print(arguments)

When you want to get help and usage messages

python naval_fate.py --help

	Naval Fate.
		
	Usage:
	  naval_fate.py ship new <name>...
	  naval_fate.py ship <name> move <x> <y> [--speed=<kn>]
	  naval_fate.py ship shoot <x> <y>
	  naval_fate.py mine (set|remove) <x> <y> [--moored|--drifting]
	  naval_fate.py -h | --help
	  naval_fate.py --version
	
	Options:
	  -h --help     Show this screen.
	  --version     Show version.
	  --speed=<kn>  Speed in knots [default: 10].
	  --moored      Moored (anchored) mine.
	  --drifting    Drifting mine.

And when we type: python naval_fate.py ship new 'Going Merry'

The parsed arguments are:

	{'--drifting': False,
	 '--help': False,
	 '--moored': False,
	 '--speed': '10',
	 '--version': False,
	 '<name>': ['Going Merry'],
	 '<x>': None,
	 '<y>': None,
	 'mine': False,
	 'move': False,
	 'new': True,
	 'remove': False,
	 'set': False,
	 'ship': True,
	 'shoot': False}

Write less code than others, and get all what we want, this is `Docopt`

Visit [Homepage](http://docopt.org/) to get all the documents.

Read [Github](https://github.com/docopt/docopt) to know the amazing code.

Try [Demo Source Code](https://github.com/docopt/docopt/blob/master/examples/naval_fate.py) in your terminal.
