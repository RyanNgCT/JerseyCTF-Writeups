## alternate-reality

_400 points, 31 solves_

**Challenged by SpecterOps**

It turns out that there are not one, but two disks in the PC. Finding the flag in the previous disk left you confused. Seems like you will have to find the flag in this forensic disk image too!

[File](https://github.com/RyanNgCT/JerseyCTF-Writeups/blob/main/Forensics%20-%20alternate-reality/NJCTF_Image2.7z)

### Requirements
* Autopsy 4.17.0 (Windows)
* Any other tools that can view Windows NTFS Alternate Data Stream (ADS) 

### Approach

As the title suggests, we suspected that there is a hidden file located in an Alternate Data Stream (ADS). Files hidden in another file's ADS typically cannot be viewed by conventional methods such as through the file explorer or command prompt. 

Firstly, we opened the E01 image via Autopsy to see if we can find any interesting hidden or deleted files within the image. Upon navigating to the `/img_NJCTF_Image2.E01/vol_vol2` directory within the given disk image, we were lucky to found a suspicious entry titled `flag.txt:hidden`. The colon behind the `flag.txt` entry tells us that there is actually a hidden `hidden` file located in its ADS. Autopsy was able to show us the content of this `hidden` file, which gives us the flag `jctf{FLA92 1N 73h S7r34M}`.

![img](https://github.com/RyanNgCT/JerseyCTF-Writeups/blob/main/Forensics%20-%20alternate-reality/autopsy-ans.png)
