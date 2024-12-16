# freakada 3301
On extracting the strings from the initial image, i got this string
```
ZIT HQZI OL GWLEXKTR, WXZ ZIT ZKXZI SOTL OF ZIT LIQRGVL. LTTA ZIT HQZZTKFL. QDGFU ZIT EIQGL, Q WTQEGF QVQOZL: izzhl://woz.sn/yktqatlztof0. GFSN ZIT VGKZIN VOSS LTT ZIT XFLTTF. ZIT PGXKFTN IQL PXLZ WTUXF
```
this is a substitution cipher which on decoding gives
```
THE PATH IS OBSCURED, BUT THE TRUTH LIES IN THE SHADOWS. SEEK THE PATTERNS. AMONG THE CHAOS, A BEACON AWAITS: HTTPS://BIT.LY/freakestein0. ONLY THE WORTHY WILL SEE THE UNSEEN. THE JOURNEY HAS JUST BEGUN
```
On clicking the link, i downloaded the image, and again extracting the strings from the image yielded the github link https://github.com/freakada-3301

Upon opening this link, there are 3 files, one contained, what looked like a flag and the other two contained some alien texts, which on translating read to `We were here` & `Somehow forgotten`.
There were 6 commits on the repo, upon looking the previous commits, we came across some poem and a timestamp, which were nothing but line:word:char, from the poem.

Which yielded a string httsdiscorggAHj7R2Qd which translated to https://discord.gg/AHj7R2Qd

Which led us to a discord server where the music `thick of it` was playing, in the members of the server there was a bot called `freakada` , upon messaging the bot 3301, he asked to multiply 3301 with two prime number which were a part of the original image, which turned out to be the dimension of the original image, 449x503 , upon multiplying the number was 745520947, the bot replied with the coordinates of freaky backshots playground  at mit manipal, where we found the qr code containing a link to a audio.

This audio when uploaded to a spectrometer gave the following message, `nite{4_wannabe_` and a morse code beneath that which yielded the key to decode the second half from the github repo, which was `FREEKEY` , we used vigenere decoder to decode the second half with this key and got `1nt3rn3t_my5tery}` and the flag became
`nite{4_wannabe_1nt3rn3t_my5tery}`

# U ARe T Detective
Started with a `signal.sr` file, unzipped it to find some files along with metadata, which hinted towards the pulse view software, on downloading it, found some signals in D1, from the name we guessed we needed to use UART decoder, which was giving frame errors, so i figured out that we need to change the baude rate according to the bit duration, which i found out to be 187.5 ns , so baude rate came out to be 5333333, which removed the frame errors and then i changed the data format to ascii yielding the flag which was
`nite{n0n_std_b4ud_r4t3s_ftw}`