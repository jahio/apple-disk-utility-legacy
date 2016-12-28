# Apple Disk Utility (Legacy)

> Version 13 (OS X Yosemite, 2014)

## BUG FOUND!

See Issues for more information, but basically this _might_ crash on launch
because it's missing one (or more?) `dylib` resources. Until I have bandwidth
to figure that out or hack around it, or get community feedback, this short
doc I wrote months ago will have to suffice.

[DIY Boot Disks](https://gist.github.com/jaustinhughey/d717d6c73e20307afaadb1eaee7710c0)

+ Uses `dd` to zero a given disk on MacOS based on the _raw_ disk device (`/dev/rdiskN`)
+ Then does the same thing to copy an ISO to the disk directly.
+ Other notes that might be useful.
+ Definitely not a replacement, but might help you scratch 'yer itch.
+ _Possibly NSFW if you work with hyper-PC-profanity nazis... (contains rants by yours truly)_

## Problem

Latest versions of MacOS (OS X) have a severely neutered version of the
venerable Disk Utility application. Most of those features have been absolutely
stripped out in the latest version of `/Applications/Utilities/Disk Utility.app`,
making it essentially useless. Futhermore, I've personally (anecdotal evidence
only so take it with a grain of salt) seen METRIC CRAPTONS of bugs with the
"new and improved" disk utility on OS X Sierra+.

New Disk Utility:

+ Doesn't Work
+ Hella Pretty

Old Disk Utility:

+ "Swiss Army Knife" of Disk Partitioning, Formatting, etc.
+ Works quite well
+ Best UX of any/all disk utility apps on any platform I've ever seen.
+ Not as pretty as the new version but IT'S ACTUALLY USEFUL.

## Solution

Use the old Disk Utility.app from before they neutered it.

## MD5 Checksums  
#### Proving as best I can that I haven't tampered with it!

Since the application itself isn't a flat file, but a whole *directory*, I
can't just `md5sum` that whole directory all together. The next best thing is
the `md5sum` of the compressed `ZIP` archive itself:

| File | MD5 |
| ---- | --- |
| `Disk Utility.zip` | `2c29483f90bf41e7e022e92dd144459c` |

However, just in case it's somehow useful, I also recursively discovered the
`md5sum` of each file under that directory and shoved all that into the file,
included herein, referred to as [Disk-Utility.app-Original-MD5-Checksums.txt](Disk-Utility.app-Original-MD5-Checksums.txt)

Should you desire to generate a list of your version of Disk Utility and compare
it to my supplied version in the future, try this:

```sh
cd /Applications/Utilities
find ./Disk\ Utility.app -type f -print0 | xargs -0 md5 > ~/Desktop/diskutility-mine.txt
```

Next, you'll want to see which files differ. I suggest a nice GUI tool here that
has color coding and such, just to make things more convenient, but you can
easily do the job with `diff` on the terminal command line:

```sh
diff $PWD/Disk-Utility.app-Original-MD5-Checksums.txt ~/Desktop/diskutility-mine.txt
```

If anything differs, the problem is **your** version, not the data in the original md5sum
text file. I suggest blowing away that old/corrupted mess and attempting to re-acquire.

Also, bear in mind that you *might* see differences in some cases that aren't
really a problem since the files in question are still the same; it's possible
that the _order_ in which files were calculated/passed into the text file you
generated is going to be different from the order in which my text file was
generated. Each file's md5sum should be verified as a match if this happens.

## How do I use this thing?

1. Download or `git clone`;
1. Decompress the archive - usually a double-click on most platforms;
1. Double-click the decompressed application `Disk Utility.app`

## Support

LOL, no.

## Credit + Copyright

Disk Utility.app is the intellectual property of Apple Computer, Inc.
Any claims of unlawful distribution of this application are invalid as they
fall under the doctrine of "fair use". I am not seeking to profit by making
this tool available, nor am I seeking to disparage or cause harm to Apple,
its employees, anyone else associated therewith, or any other human being.

Basically, if you have a mac, you already paid for this and can get it on
your own by installing an *older, downgraded* version of MacOS (OS X). I'm
just making it convenient; separate release means you don't have to suffer
through that nonsense.
