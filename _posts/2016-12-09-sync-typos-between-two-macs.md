---
layout: single
title: Sync typos between two Macs
tags: [mac, typo, pycharm, dictionaries, LocalDictionary, sync]
---
I think every programer or writer may face this scenario, when we write some text in mac, the OS may detect typo for us.
So we need train the OS to learn those new words which OS treat them as typo.

![Learn-spelling][image-1]

## some typo dictionaries for programer
* Mac
	\~/Library/Spelling/LocalDictionary
* PyCharm
	.idea/dictionaries/{username}.xml

## build unique LocalDictionary
> The words in the dictionary file are arranged alphabetically. When your Mac scans to see if the dictionary contains a word, it stops once it reaches the point where it should be. In other words, if you put the word colour at the end of the dictionary, it will not be detected because spell check will only look up to theCs.
> Similarly, if you put the word Zebedee at the start of your list, spell check would stop instantly. When you are adding words to the dictionary you must be careful to keep them in alphabetical order.
> — [PhilETaylor][1]

Fixed with Mac level should be more generic, so read article [Quick Tip: Bulk Add Words to Your Mac's Spell Check Dictionary][2] to build your unique `LocalDictionary`.

## Use a soft link to dropbox will be fine.
**Link the directory `Spelling` instead of the file `LocalDictionary`** as when you learn a new word, the symbol file will change to an ordinary file, the link will broken.

```
cp -r ~/Library/Spelling ~/Dropbox
cd ~/Library
rm -rf Spelling
ln -s ~/Dropbox/Spelling
```

## refs
* [How to improve the Mac OS X Dictionary][3]
* [MacSpelling shell][4]
* [https://gist.github.com/PhilETaylor/9e7fd5ba5ffc52fa8dec][5]

[1]:	https://github.com/PhilETaylor
[2]:	https://computers.tutsplus.com/tutorials/quick-tip-bulk-add-words-to-your-macs-spell-check-dictionary--mac-60820
[3]:	http://www.techradar.com/how-to/software/applications/how-to-improve-the-os-x-dictionary-1297396
[4]:	https://github.com/bchroneos/system-tweaks
[5]:	https://gist.github.com/PhilETaylor/9e7fd5ba5ffc52fa8dec

[image-1]:	/photos/learn-middle.png