Describes an application that uses `pyaudibletags` to do something useful: to arrange audiobooks into one folder per author and one subfolder per book.

# What this Program Does #

This program is the reason I wrote `pyaudibletags` in the first place. I wanted to arrange my audiobooks into one folder per author and one subfolder per book.

I got the idea from iTunes, which does something similar for music, by arranging music files into one folder per performer, with subfolders for album. But iTunes doesn't do it right with audiobooks, because it lumps all books by an author into a single folder called Unknown Album.

This little program does it properly.


# Using the Program #

How you use the program depends on whether you just want the [application to reorganize your audiobook folder](InstallableApplication.md) or if you want the [Python source program](PythonSource.md) so that you can see how it's done and tinker with it to suit your needs better.

# Operation #

You must specify a folder to operate on. The program will examine every `.aa` file in the specified subtree, extract the author and title tags, and construct a fresh subtree, in place, with one folder per author, and within that folder, one subfolder per book. This means that short books that consist of only a single file will have a folder all to themselves with one file in it.

The program tries to be reasonably sensible about creating short, useful folder names.

If there is more than one author, then only the first author appears in the name. If the book title is of the form _title: subtitle_ then the _subtitle_ part will be removed. Obviously, characters that are not permitted in filenames have to be removed: these are `\ / : * ? " < > |`. On platforms that don't allow spaces in filenames, an underscore will be used instead.

The program treats any non-ascii character that it finds in the author and title tags as being encoded using latin-1 (essentially the Windows character set). This may give unexpected results if you are working with a filesystem (such as a portable drive) that encodes characters in the range 128-255 differently.

If in the process of moving files from one folder to another, a folder is left empty, then that folder will be silently removed. The program will _never_ delete files or non-empty folders.

After you have done this, Audible Manager and iTunes will say that they can no longer locate the files. To access them from these programs, you will need to delete the library entries and add them back again. **_Under Audible Manager this is an extremely tedious process._**