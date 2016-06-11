# Cryptographic Hash Function

## Overview

A cryptographic hash is fundamental to encryption and security. A practical use of the hash function is to make sure that a credit card number that is keyed into a point of sale device is correct. In this assignment you use SHA256 to verify that a downloaded file is not corrupt..

## Terms You Should Know

md5sum
: Compute and check MD5 message digest.

sha256sum
: Compute and check SHA256 message digest.

Cryptographic Hash
: A cryptographic hash function is a mathematical algorithm that maps data of arbitrary size to a bit string of a fixed size... Wikipedia

ISO image
: Software distributed on bootable discs is often available for download in ISO image format. And like any other ISO image, it may be written to an optical disc such as CD or DVD. Wikipedia

## Preparation

1. Download the smallest ISO file from [one of the CentOS mirrors](http://isoredirect.centos.org/centos/7/isos/x86_64/).
2. Download the *sha256sum.txt* from the same mirror. Don't open the file but save it to the same directory as the ISO file.
2. Open a terminal from the Dash. The Dash is the Ubuntu icon at the top of the Lauchbar.

![Opening the terminal from the Dash.](https://dkibbe.github.io/images/cis126dl_open_terminal_from_dash.png)

## Use SHA to Verify a Download

1. Open a terminal from the Dash. Use the `cd` command to change to the *Downloads* directory.
2. Use `sha256sum -c sha256sum.txt` to verify that the download is not corrupt.

<!--## Use SHA to Compare Two Photographs

1. Download an image from the Net or use the super hero image you created.
2. Open a terminal and navigate to the Download  directory
3. sha2556sum -->

<!--## One Your Own

This assignment is a good opportunity to demonstrate the power of combining commands. Redirecting *stderr* and filtering the `sha256sum` command through `grep` to remove unwanted output.-->

## What to Submit

Submit a screenshot of the output of the `sha256sum` command  you ran above showing that the ISO you downloaded is not corrupt.

## Resources

- [Secure Hash Algorithm](https://en.wikipedia.org/wiki/Secure_Hash_Algorithm)
- [What is a Hash Code? part 1](https://www.youtube.com/watch?v=DSTpMWv0IlA)
- [What is a Hash Code? part 2](https://www.youtube.com/watch?v=MHdrZfL1_oc)
- [sha256sum - Linux man page](http://linux.die.net/man/1/sha256sum)
- [Dictionary Attack](https://en.wikipedia.org/wiki/Dictionary_attack)
- [SHA-256 hash calculator](http://www.xorbin.com/tools/sha256-hash-calculator)
- [Latest version of this assignment](http:/dkibbe.github.io)

## License

  <a rel="license" href="http://creativecommons.org/licenses/by-sa/4.0/">
  <img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-sa/4.0/88x31.png" /></a><br />
  This work is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by-sa/4.0/">Creative Commons Attribution-ShareAlike 4.0 International License</a>.
