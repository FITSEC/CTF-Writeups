The Legend of Hackerman Pt. 2
=====
#### Solver: ap3xsh0t

## Category: Forensics

> "Ok, I've received another file from Hackerman, but it's just a Word Document? He said that he attached a picture of the flag, but I can't find it..."

## Methodology
We are provided a .docx file that contains the flag somewhere. My first thought was to strings it and see what may be hidden in the file. Sure enough, it contained lots of png images. The next thing I did was try to unzip it to extact the images. This dumped all of the contents into my working directory and I was able to navigate to word/media and view all of the images. After sifting through all of the images I finally found the flag.

![flag](img/flag.png)

> utflag{unz1p_3v3ryth1ng}
