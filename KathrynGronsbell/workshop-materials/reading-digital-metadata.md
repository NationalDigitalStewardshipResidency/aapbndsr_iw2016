
# Reading key digital metadata

The following information is related to the _NDSR 2016 Immersion Week - Automating Procedures for Digital Asset Management_ presentation also found in this GitHub repository. 

## Overview

This page focuses on understanding the construction and permissions related to files we access. 

We can use checksum validation to confirm that data has NOT changed in any way (down to the bit level) compared to specific reference point. Checksums can be generated for individual files, batches of files, or chunks within files. The core concepts below lay the foundation for more extensive or complex data validation procedures. For archivisits and preservationists, you will likely see MD5 and SHA-256 most commonly in your work. These are not used for encryption or encoding (as they both have significant vulnerabilities) but are appropriate for use in verifying data integrity and supporting data management. 


## Getting started

1. Open Terminal (Applications > Utilities > Terminal). 

2. Change your working directory to the CLI samples folder from the (previous exercise)[cli-basics.md] called [cli-basics-samples] that should be on your Desktop.

### Viewing read and write access

1. We can use the list or `ls` command to get a summary of permissions in a given directory. If you're in _cli-basics-samples_, use the `-l` option for long listing formatted output:

            `ls -l`

What you see on the Terminal probably looks something like this:

`total 1280`
`-rw-r--r--@ 1 kathryngronsbell  staff   63148 Jul 25 20:26 Shar_pei_casa.JPG`
`-rw-r--r--@ 1 kathryngronsbell  staff  582947 Jul 25 18:23 celebrate.gif`
`-rw-r--r--  1 kathryngronsbell  staff      17 Jul 25 18:25 hello.txt`
`drwxr-xr-x  3 kathryngronsbell  staff     102 Jul 25 20:58 this-is-a-subdir`

The output can be interpreted (c/o [this stackexchange answer](http://unix.stackexchange.com/a/103118)) as:

"file permissions,
number of links,
owner name,
owner group,
file size,
time of last modification, and
file/directory name
File permissions is displayed as following;

first character is - or d, d indicates a directory, a line represents a file
three sets of characters, three times, indicating permissions for owner, group and other:
r = readable
w = writable
x = executable"

2. Having quick access to the permissions and last modified timestamp can be helpful when troubleshooting or assessing risk factors for a given directory's content. Try using the same command on a different directory (one of your own, probably a more complex one!)


### Checksum creation

The following instructions lay out the basics of generating a checksum. 

1. Make sure your working directory is _cli-basics-samples_, which should be on your Desktop (HINT: use `pwd`).

2. Generating a hash value can be done using downloaded or already-installed programs and utilties. Most UNIX operating systems already have tools like `md5` and `shasum` installed by default so we will start with these to create our source checksum hash value for a given file. Type:

            `md5 hello.txt`

The information printed to the Terminal from that command should look like this, containing the alogrithm desination, the file in parantheses, and the 32 character hash value for the file following the equals sign:

            `MD5 (hello.txt) = 9522afb8dc1fa2e1f7a5a771a94765a6`

3. Great job! You have created a checksum using md5. Let's try to create a SHA-356 checksum for the same file. Type:

            `shasum -a 256 hello.txt`

The `-a` option allows you to designate the algorithm used to generate a hash value (in this case, 256). Look at the output from this command. Does it look like the output below (with the 64 character hash value followed by the file name)?

            `8488307e4acd57561c432dea45da696b3d29935478fdde7de544522016851606  hello.txt`


4. Nice! Okay, so printing hash values to the Terminal might be a blast...but there are more powerful and efficient ways to create hashes so that they are more primed to be validated. The next section shows us how we can validate checksums on a small scale. 



### Checksum valiation


1. Copy _hello.txt_ to your Desktop (outside of the _cli-basics-samples_ folder). You can copy & paste or use `cp hello.txt ~/Desktop/hello.txt`

2. Generate a md5 checksum for the *hello.txt file on your Desktop*. Does it match the hash value of the hello.txt in your _cli-basics-samples_ folder? (It should! You haven't done anything to it...) So let's say you're downloading or moving a single file and need to see if it's transferred without corruption or modification. Visually comparing two hash values is fine...but you do not want to do this programmatically. 


3. Let's try a command that creates a specially-formatted text files containing the hash information for validation in your working directory. If you are not already on the Desktop, `cd` into your Desktop so you are pointing at the correct file (_)/Desktop/hello.txt_):

            `shasum -a 256 hello.txt > hello.txt.sha256sum`

4. Now let's see what ended up in that .sha256sum file. Use `cat` to print the text to the Terminal and review it (should look familiar!):

            `cat hello.txt.sha256sum`

5. We can use shasum to "check" or validate previously generated checksums. When we do this first validation it should work since there has been no intentional modification of our target file (and hopefully no unintentional corruption!). Use the command below to validate your SHA-256 checksum for _hello.txt_ on the Desktop:

            `shasum -c hello.txt.sha256sum`

The output should have printed the filename followed by a colon and the text "OK", as seen here:

            `hello.txt: OK`

Congrats - you used shasum to automatically validate a checksum! Now let's rustle some bit-level feathers.

6. Use a text editing program (or vim!) to modify the text of the _hello.txt_ file and save it.

7. Re-run validation using shasum (Step #5 above). Did the output say:

            `hello.txt: FAILED`
            `shasum: WARNING: 1 computed checksum did NOT match`

That makes sense, right? You modified the file. The checksum should NOT match because of that modification. If you didn't get this result, check the file and make sure you actually saved/wrote the changes to your file.

8. Now go back into your _cli-basics-samples_ folder. Mess around with the provided files (modify the contents, filename, size, anything!). Use manual and automated validation procedures to see what causes the checksum to change.

- For example, change the name of one of the provided files. You can do this by just changing the filename of the file's icon or using the `mv` command we explored in the [CLI Basics](cli-basics.md) section. What happens to the checksum after the file name is changed? [Will changing a file name affect the MD5 Hash of a file?](http://stackoverflow.com/a/14360831)


## Recommended resources


[md5 man page](https://www.freebsd.org/cgi/man.cgi?query=md5&sektion=1)

[shasum man page](http://ss64.com/osx/shasum.html)

[Documentation and official code releases of the FITS and the FITS Web Service projects](http://projects.iq.harvard.edu/fits/home) by Harvard University (last update: July 20, 2016)

[Comparison of file verification software](https://en.wikipedia.org/wiki/Comparison_of_file_verification_software) on Wikipedia (last update: May 30, 2016)


