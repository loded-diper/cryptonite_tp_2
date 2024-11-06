# C3

  

**Flag:**  `picoCTF{adlibs}`

How you approached the challenge:

- So basically the encoding is done by finding the index of each character of the flag in `lookup1` string and is encoded as the `(current - previous)%40`th index in `lookup2` string.
- To decode this we have the outputted string which is
```
DLSeGAGDgBNJDQJDCFSFnRBIDjgHoDFCFtHDgJpiHtGDmMAQFnRBJKkBAsTMrsPSDDnEFCFtIbEDtDCIbFCFtHTJDKerFldbFObFCFtLBFkBAAAPFnRBJGEkerFlcPgKkImHnIlATJDKbTbFOkdNnsgbnJRMFnRBNAFkBAAAbrcbTKAkOgFpOgFpOpkBAAAAAAAiClFGIPFnRBaKliCgClFGtIBAAAAAAAOgGEkImHnIl
```  
- We'll take each character if this string and try to find the `cur` variable (which originally made the string) and out decoded message will be simply `lookup1[cur]`.
- This is the code which can decode the `out`
```python
lookup1 = "\n \"#()*+/1:=[]abcdefghijklmnopqrstuvwxyz"
lookup2 = "ABCDEFGHIJKLMNOPQRSTabcdefghijklmnopqrst"
out="DLSeGAGDgBNJDQJDCFSFnRBIDjgHoDFCFtHDgJpiHtGDmMAQFnRBJKkBAsTMrsPSDDnEFCFtIbEDtDCIbFCFtHTJDKerFldbFObFCFtLBFkBAAAPFnRBJGEkerFlcPgKkImHnIlATJDKbTbFOkdNnsgbnJRMFnRBNAFkBAAAbrcbTKAkOgFpOgFpOpkBAAAAAAAiClFGIPFnRBaKliCgClFGtIBAAAAAAAOgGEkImHnIl"
dec = ""
prev =0
for _ in out:
    cur=(prev+lookup2.index(_))%40
    dec += lookup1[cur]
    prev = cur
print(dec)
```
- We first find the cur variable which was used to encode it and the `cur`th index in `lookup1` string is out character of the original string.
- The original string came out to be 
```python
#asciiorder
#fortychars
#selfinput
#pythontwo

chars = ""
from fileinput import input
for line in input():
    chars += line
b = 1 / 1

for i in range(len(chars)):
    if i == b * b * b:
        print chars[i] #prints
        b += 1 / 1
```
- here the comments suggest that the code is in Python 2.0 and we have to give self input to the program to find the flag, after a while i figured out that the self input is this code itself, on running this code with input the code itself on python 2 we got the flag.
![final image](https://github.com/loded-diper/cryptonite_tp_2/blob/main/Images/C3.png)

What you learned through solving this challenge:
1. Cryptography
  
Other incorrect methods you tried:
- Tried to input `lookup1`, `lookup2` and other string as an input to the second step.   
References
- https://www.reddit.com/r/learnpython/comments/gjthg6/print_vs_sysstdoutwrite_in_python_2x_vs_python_3x/
