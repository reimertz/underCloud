☁ underCloud
=

Use iCloud as your backup solution even if you spend much of your time in the terminal.

## Description

If you are familiar with iCloud Drive, you know that there is a folder where you drop files and they get synced automagically to the cloud️™.

This folder is also reachable from the terminal: `cd "/Users/$(whoami)/Library/Mobile Documents/com~apple~CloudDocs/"`.

So what if I as a developer would like use this in terminal-land to store all my files? The main problem is all those git repos and especially the `.git` directory.
If you checkout a new branch, thousands of files can change and that basically kills iCloud Drive from syncing. It just dies.

Luckily, there is one hidden feature we could utilize to solve this issue: the ability to ignore folders by appending `.nosync` to it!

So if you combine all of this, you get underCloud, or `_`.

underCloud is has just a _very_ opinionated folder structure, symlinking `/Users/$(whoami)/Library/Mobile Documents/com~apple~CloudDocs/_` to `~/_`


```
~/
  _/illustrations
  _/movies
  _/music
  _/presentations
    /presentation a
    /presentation b.nosync (git)
  _/repos.nosync
    /project a
    /project b
  _/school
    university a
      /course a
      /course b
  _/secrets.nosync
    /SomeThingIShouldntDownload.2007.720p
  _/work
    /company a
      /documents
      /invoices
      /repos.nosync
        /project a (git)
      /illustrations
```

## Usage ⚠ read before copy-pasting! ⚠

```
# Be sure you don't have a folder at the top hierarchy in your iCloud named _

$ cd "/Users/$(whoami)/Library/Mobile Documents/com~apple~CloudDocs/"
$ git clone --depth=1 https://github.com/reimertz/underCloud _
$ rm _/README.md && rm -rf _/.git
$ ln -s _ ~/_
$ cd ~/_
```

The following lines of code basically
* git clone `reimertz/underCloud` to `"/Users/$(whoami)/Library/Mobile Documents/com~apple~CloudDocs/_`
* removes `.git` and `README.md`
* symlink "/Users/$(whoami)/Library/Mobile Documents/com~apple~CloudDocs/_" to `~/_`
* cd into `~/_`


## The Result
```
& ls -al
lrwxr-xr-x     1 reimertz  staff        62 Jan 24  2017 _ -> /Users/reimertz/Library/Mobile Documents/com~apple~CloudDocs/_

& cd _ && ls -al
total 8
drwxr-xr-x   12 reimertz  staff   384 Sep 28 20:51 .
drwxr-xr-x@ 127 reimertz  staff  4064 Sep 28 20:43 ..
drwxr-xr-x    3 reimertz  staff    64 Sep 28 20:45 illustrations
drwxr-xr-x    2 reimertz  staff    64 Sep 28 20:45 movies
drwxr-xr-x    2 reimertz  staff    64 Sep 28 20:45 music
drwxr-xr-x    3 reimertz  staff    96 Sep 28 20:48 presentations
drwxr-xr-x    2 reimertz  staff    64 Sep 28 20:44 repos.nosync
drwxr-xr-x    2 reimertz  staff    64 Sep 28 20:45 school
drwxr-xr-x    2 reimertz  staff    64 Sep 28 20:45 secrets.nosync
drwxr-xr-x    3 reimertz  staff    96 Sep 28 20:46 work

```
