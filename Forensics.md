# tunn3l vision
**Flag:**  `picoCTF{qu1t3_a_v13w_202}`

How you approached the challenge:

- We are given a file with no details about it's types , i tried to find the type of file using `cyberchef` and `file command` , but was unsuccessful.
- Then I opened the file in a hex editor and tried to search it's beginning bytes to common magic numbers of files using `Gary Kessler's File Signatures Table`.
- The first 2 bytes were `42 4D` which were the magic numbers of a bitmap file, so i tried to rename the file by appending `.bmp` extension after the file but it was not readable indicating that it was corrupted.
![Renaming to .bmp](https://github.com/loded-diper/cryptonite_tp_2/blob/main/Images/Renaming_to_bmp.png)
- Then i checked the rest of the 14 byte header of bmp file but found nothing, so i moved on to check DIB header.
 - The size of a DIB header (for windows NT 5.0 , 98 or later) should be `124` bytes, but it showed `BA D0 00 00` as the size of the DIB header which in decimal is `53434` bytes , much larger. So i changed it to `7C 00 00 00` (124 in decimal).
 - The file did open but only a fake flag was visible , which was `notaflag{sorry}`.
![fake flag](https://github.com/loded-diper/cryptonite_tp_2/blob/main/Images/not_a_flag.png)
 - So i tried to tweak it's width (which completely distorted the image) , then i tried to change it's height from `32 01` to `32 03` which finally gave me the full picture and the flag.
![true flag](https://github.com/loded-diper/cryptonite_tp_2/blob/main/Images/full_flag.png)
What you learned through solving this challenge:
1. A unique magic number is associated to every file type.

2. Reading the file structure of a specific type of file and editing it's hex values.

Other incorrect methods you tried
- I tried to convert bmp image to other formats

- I tried to use steganography on the image

References
- https://www.garykessler.net/library/file_sigs.html

- https://en.wikipedia.org/wiki/BMP_file_format
- etc.

# Challenge name

  

**Flag:**  `picoCTF{beep_boop_im_in_space}`

  

How you approached the challenge:
- We have `wav` file with the hint "how did pictures from the moon landing get sent back to earth" , on researching I found out that `sstv image transmission` was used to do this.
-  To decode it, i used a decoder from a github repository, which had the following modes-   
-- Martin 1, 2
--   Scottie 1, 2, DX
--   Robot 36, 72
From the 2nd hint we know that the model we need to use is Scottie, but the decoder automatically chose it while decoding.
- To install the decoder is used the following commands
```bash
$ git clone https://github.com/colaclanth/sstv.git
$ cd sstv
$ sudo python3 setup.py install
```
This cloned and installed the decoder on my system. To decode it i used the following command
```bash
vishad@VISHAD:~$ sstv -d message.wav -o result.png
[sstv] Searching for calibration header... Found!
[sstv] Detected SSTV mode Scottie 1
[sstv] Decoding image...   [###################################################################################################] 100%
[sstv] Drawing image data...
[sstv] ...Done!
``` 
This gave an image which contained the flag
![result](https://github.com/loded-diper/cryptonite_tp_2/blob/main/Images/result.png)

What you learned through solving this challenge:
1. Using SSTV transmission to transmit and receive static pictures via radio.

2. How to decode a an SSTV audio file 

3. etc.

Other incorrect methods you tried:
-  Morse Code Adaptive Audio Decoder

- Spectrogram

References
- https://en.wikipedia.org/wiki/Slow-scan_television

- https://github.com/colaclanth/sstv

- etc.
