Observe Closely
=====
#### Solver: ap3xsh0t

## Category: Forensics

> "A simple image with a couple of twists..."

## Methodology
For this challenge we were given an image. My usual approach is to file and strings it to see if anything is out of the ordinary. Strings returned something interesting. Apparently the image contains a "hidden_binary".



## Binwalk and flag retrieval
Using binwalk, we can extract the binary out of the image.

>binwalk -e Griffith_Observatory.png

Now that we've extracted the binary, we can run it and retrieve our flag!

> utflag{2fbe9adc2ad89c71da48cabe90a121c0}
